---
title: Curve calibration loader
permalink: /curve_calibration_loader/
---

The curve calibration loader is used to define the inputs to curve calibration.
It is one of a number of [loaders]({{site.baseurl}}/loaders) included in Strata.


## Loader

Curves can be loaded using the [`RatesCalibrationCsvLoader`]({{site.baseurl}}/apidocs/com/opengamma/strata/loader/csv/RatesCalibrationCsvLoader.html)

```
ResourceLocator groupsLocator = ResourceLocator.ofFile(groupsFilename);
ResourceLocator settingsLocator = ResourceLocator.ofFile(settingsFilename);
ResourceLocator calibrationLocator = ResourceLocator.ofFile(calibrationFilename);
Map<CurveGroupName, RatesCurveGroupDefinition> defns = RatesCalibrationCsvLoader.load(
    valuationDate, groupsLocator, settingsLocator, calibrationLocator);
```

Curves must be calibrated as part of a group, that specifies a purpose for the curve, such as whether it is
a discount or forward curve. See the [curve groups]({{site.baseurl}}/curve_groups_file) file for more details.

Settings that are shared across all the nodes in a curve are defined in the
[curve settings]({{site.baseurl}}/curve_settings_file) file.


## Format

The curve calibration file is a simple CSV-formatted file with the following header row:

```
Curve Name,Label,Symbology,Ticker,Field Name,Type,Convention,Time,Date,Min Gap,Clash Action,Spread
```

The columns may be specified in any order, however this is the recommended order.
The last four columns - Date, Min Gap, Clash Action and Spread - are all optional.

The meaning of each column is as follows:

| Column name    | Description                                                                          |
|----------------|--------------------------------------------------------------------------------------|
| Curve Name     | The name of the curve                                                                |
| Label          | A description of the node, used to identify it in bucketed sensitivity results       |
| Symbology      | The symbology of the quote identifier                                                |
| Ticker         | The ticker of the quote, unique within the symbology                                 |
| Field Name     | The field name. The most common are "MarketValue" and "SettlementPrice"              |
| Type           | The type of the curve node, such as "FRA" or "IRS"                                   |
| Convention     | The convention to use to create the trade associated with the curve node             |
| Time           | The description of the trade time, used to convert the convention into a trade       |
| Date           | The date of the curve node, in the form `yyyy-MM-dd`, "LastFixing" or "End"          |
| Min Gap        | The minimum gap between this curve node and each adjacent node                       |
| Clash Action   | The action to perform if the minimum gap is violated, "DropThis" or "DropOther       |
| Spread         | The spread to add to the market data value for the node                              |

A single curve will consist of at least two nodes, and typically many more, with one row required for each node.
Each curve must be contained within a single CSV file, but a single file may contain curves.

The "Symbology", "Ticker" and "Field Name" columns uniquely identify the market data quote that is used to create the trade.
See the [quotes loader]({{site.baseurl}}/quotes_loader) for more details.

The "Type", "Convention" and "Time" columns define the trade to be created for the node.
See the next section for more details.

The "Date" column allows the date of the curve node to be overridden.
By default, it will select the "End" date of the trade.
The two other options are to select the last fixing date ("LastFixing"), or to specify the date exactly.

The "Min Gap" and "Clash Action" columns allow the node to be removed if it is invalid.
This is most useful for futures, where the date of the future is fixed,
but the surrounding swaps or FRAs can move freely.
By declaring a minimum gap and clash action, a single curve calibration file can be used over many weeks,
with the futures nodes being deleted if they get too close to other nodes.
If the gap and action are not specified and the dates of two nodes clash, an exception will be thrown.


## Node types

The following node types are supported:

### "DEP" or "TermDeposit"

A term deposit node, only suitable for use on curves that are used for discounting.
The convention column must contain a convention name from
[`TermDepositConventions`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/deposit/type/TermDepositConventions.html).
The time column must contain the tenor as an ISO-8601 style period, such as "P2D".
The "P" may be omitted, thus "P2D" and "2D" are equivalent.

### "FIX" or "IborFixingDeposit"

A special node creating an artificial trade based on the value of the Ibor index.
This is used instead of a term deposit node when calibrating a curve that is not used for discounting.
The convention column must contain the name of an Ibor index.
See the [indices]({{site.baseurl}}/indices) page for Strata's default index names.
The time column is not used.

### "FRA"

A Forward Rate Agreement (FRA) node.
The convention column must contain the name of an Ibor index.
See the [indices]({{site.baseurl}}/indices) page for Strata's default index names.
The time column must contain a description of the FRA.
For example, "3X6" means a FRA that starts in 3 months and ends in 6 months.

The time format consists of three parts - period to start, "X" and period to end.
Each of the periods is am integer, optionally prefixed by "P" and optionally suffixed by "M".
There may be a space either side of the "X".
Thus "3X6", "P3M X P6M" and "3MX6M" are all equivalent.

### "IFU" or "IborFuture"

An Ibor future node (STIR).
The convention column must contain a contract specification from
[`IborFutureContractSpecs`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/index/type/IborFutureContractSpec.html).
The time column must contain a description of the future, either as a relative or absolute month.
For example, "Jun16" defines the future absolutely, whereas, "7D+3" defines the future in relative terms.

The absolute time format is simply the three letter month name in English, followed by the two digit year.

The relative time format consists of four parts - base period, "+", sequence number and an optional suffix.
The base period is an ISO-8601 style period of days, weeks or months, such as "P2D" or "P1W".
The "P" may be omitted, thus "P2D" and "2D" are equivalent.
There may be a space either side of the "+".
The sequence number is a simple integer.
The suffix can be "B" for the base sequence or "F" for the full sequence, if omitted "B" is assumed.
For example, many futures have a base quarterly sequence but with an initial listing of serial months.
The base sequence is quarterly, the full sequence includes the serial months as well.

The selected future is determined by adding the base period to the valuation date,
and then finding the nth matching future according to the convention, where n is the sequence number.

### "ONF" or "OvernightFuture"

An Overnight future node (STIR).
The convention column must contain a contract specification from
[`OvenightFutureContractSpecs`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/index/type/OvernightFutureContractSpec.html).

In other respects this is the configured as per as an "IFU" node, see above.

### "OIS" or "FixedOvernightSwap"

An OIS interest rate swap node.
The convention column must contain a convention name from
[`FixedOvernightSwapConventions`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/type/FixedOvernightSwapConventions.html).
The time column must contain the tenor as an ISO-8601 style period, such as "P1Y".
The "P" may be omitted, thus "P1Y" and "1Y" are equivalent.

### "IRS" or "FixedIborSwap"

A vanilla interest rate swap node.
The convention column must contain a convention name from
[`FixedIborSwapConventions`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/type/FixedIborSwapConventions.html).
The time column must contain the tenor as an ISO-8601 style period, such as "P1Y".
The "P" may be omitted, thus "P1Y" and "1Y" are equivalent.

### "BAS" or "IborIborSwap"

An Ibor-Ibor basis swap node.
The convention column must contain a convention name from
[`IborIborSwapConventions`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/type/IborIborSwapConventions.html).
The time column must contain the tenor as an ISO-8601 style period, such as "P1Y".
The "P" may be omitted, thus "P1Y" and "1Y" are equivalent.

### "ONI" or "OvernightIborBasisSwap"

A Overnight-Ibor basis swap node.
The convention column must contain a convention name from
[`OvernightIborSwapConventions`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/type/OvernightIborSwapConventions.html).
The time column must contain the tenor as an ISO-8601 style period, such as "P1Y".
The "P" may be omitted, thus "P1Y" and "1Y" are equivalent.

### "BS3" or "ThreeLegBasisSwap"

A three-leg basis swap node.
The convention column must contain a convention name from
[`ThreeLegBasisSwapConventions`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/type/ThreeLegBasisSwapConventions.html).
The time column must contain the tenor as an ISO-8601 style period, such as "P1Y".
The "P" may be omitted, thus "P1Y" and "1Y" are equivalent.

### "XCS" or "XCcyIborIborSwap"

A cross currency basis swap node.
The convention column must contain a convention name from
[`XCcyIborIborSwapConventions`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/type/XCcyIborIborSwapConventions.html).
The time column must contain the tenor as an ISO-8601 style period, such as "P1Y".
The "P" may be omitted, thus "P1Y" and "1Y" are equivalent.

### "INF" or "FixedInflationSwap"

An inflation swap node.
The convention column must contain a convention name from
[`FixedInflationSwapConventions`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/type/FixedInflationSwapConventions.html).
The time column must contain the tenor as an ISO-8601 style period, such as "P1Y".
The "P" may be omitted, thus "P1Y" and "1Y" are equivalent.

### "FXS" or "FxSwap"

An FX swap node.
The convention column must contain a convention name from
[`FxSwapConventions`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fx/type/FxSwapConventions.html).
The time column must contain the tenor as an ISO-8601 style period, such as "P1Y".
The "P" may be omitted, thus "P1Y" and "1Y" are equivalent.
The spread column must be omitted or set to zero.


## Example

This example file specifies one curve, consisting of a fixing, 2 FRAs, a swap, three futures and 11 swaps.
The first of the futures will be dropped as it is before the 1-year swap.

The "Date" and "Spread" columns are not shown, as they are optional and were unused.

```
Curve Name, Label, Symbology, Ticker,        Field Name,      Type, Convention,                 Time, Min Gap, Clash Action
USD-3ML,    3M,    OG-Ticker, USD-Fixing-3M, MarketValue,     FIX,  USD-LIBOR-3M
USD-3ML,    6M,    OG-Ticker, USD-FRA-3Mx6M, MarketValue,     FRA,  USD-LIBOR-3M,               3Mx6M
USD-3ML,    9M,    OG-Ticker, USD-FRA-6Mx9M, MarketValue,     FRA,  USD-LIBOR-3M,               6Mx9M
USD-3ML,    1Y,    OG-Ticker, USD-IRS3M-1Y,  MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      1Y
USD-3ML,    9M-F,  OG-Future, USD-L3M-Seq3,  SettlementPrice, IFU,  USD-LIBOR-3M-Quarterly-IMM, 0D+3, 7D,      DropThis,
USD-3ML,    15M-F, OG-Future, USD-L3M-Seq5,  SettlementPrice, IFU,  USD-LIBOR-3M-Quarterly-IMM, 0D+5, 7D,      DropThis,
USD-3ML,    18M-F, OG-Future, USD-L3M-Seq6,  SettlementPrice, IFU,  USD-LIBOR-3M-Quarterly-IMM, 0D+6, 7D,      DropThis,
USD-3ML,    2Y,    OG-Ticker, USD-IRS3M-2Y,  MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      2Y
USD-3ML,    3Y,    OG-Ticker, USD-IRS3M-3Y,  MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      3Y
USD-3ML,    4Y,    OG-Ticker, USD-IRS3M-4Y,  MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      4Y
USD-3ML,    5Y,    OG-Ticker, USD-IRS3M-5Y,  MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      5Y
USD-3ML,    7Y,    OG-Ticker, USD-IRS3M-7Y,  MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      7Y
USD-3ML,    10Y,   OG-Ticker, USD-IRS3M-10Y, MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      10Y
USD-3ML,    12Y,   OG-Ticker, USD-IRS3M-12Y, MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      12Y
USD-3ML,    15Y,   OG-Ticker, USD-IRS3M-15Y, MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      15Y
USD-3ML,    20Y,   OG-Ticker, USD-IRS3M-20Y, MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      20Y
USD-3ML,    25Y,   OG-Ticker, USD-IRS3M-25Y, MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      25Y
USD-3ML,    30Y,   OG-Ticker, USD-IRS3M-30Y, MarketValue,     IRS,  USD-FIXED-6M-LIBOR-3M,      30Y
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.
