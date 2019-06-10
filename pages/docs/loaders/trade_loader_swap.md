---
title: Trade loader for Swaps
permalink: /trade_loader_swap/
---

This page details the Strata CSV format for loading [Swaps]({{site.baseurl}}/swap).
See the [overview page]({{site.baseurl}}/trade_loader) for details of other assets classes.


## Trade loader file format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

Swaps can be specified using two different column sets - by convention and by full details.
The two column sets can be mixed in the same file.
In addition, a single file can contain other asset classes, such as FRAs or FX.
Just add the union of the column headers and fill in the necessary data on a row by row basis.


## Example

This example file specifies a Swap trade by convention.

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Convention,            Buy Sell, Period To Start, Tenor, Notional, Fixed Rate
Swap,              OG,        123411, 2017-06-01, GBP-FIXED-1Y-LIBOR-3M, Buy,      P1M,             P5Y,   2000000,  0.4
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## Swap by convention

These columns are used when loading a Swap trade by convention.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name           | Mandatory?  | Example/Format                                                             | Description |
|-----------------------|-------------|----------------------------------------------------------------------------|-------------|
| Strata Trade Type     | Mandatory   | `Swap`                                                                     | The type of the trade, case insensitive |
| Start Date            | Conditional | `2017-06-01` ([formats]({{site.baseurl}}/common_formats/#date))            | The unadjusted start date |
| End Date              | Conditional | `2022-06-01` ([formats]({{site.baseurl}}/common_formats/#date))            | The unadjusted end date |
| Period To Start       | Conditional | `2M` ([formats]({{site.baseurl}}/common_formats/#period))                  | The period from the trade date to the trade start date |
| Tenor                 | Conditional | `5Y` ([formats]({{site.baseurl}}/common_formats/#period))                  | The period from the start date to the end date |
| Convention            | Mandatory   | `GBP-FIXED-1Y-LIBOR-3M`                                                    | The Swap convention name |
| Buy Sell              | Mandatory   | `Buy` ([values]({{site.baseurl}}/common_values/#buy-sell))                 | Whether the Swap is buy or sell |
| Notional              | Mandatory   | `1000000`                                                                  | The notional amount, currency defined by the convention |
| Fixed Rate            | Mandatory   | `1.2`                                                                      | The fixed rate, as a percentage, such as 1.2 for 1.2% |
| FX Rate               | Conditional | `1.364`                                                                    | The FX rate, mandatory for cross-currency swaps |
| Roll Convention       | Optional    | `Day1` ([values]({{site.baseurl}}/common_values/#roll-convention))         | The roll convention |
| Stub Convention       | Optional    | `ShortInitial` ([values]({{site.baseurl}}/common_values/#stub-convention)) | The stub convention |
| First&nbsp;Regular&nbsp;Start&nbsp;Date | Optional | `2017-09-01` ([formats]({{site.baseurl}}/common_formats/#date)) | The unadjusted start date of the first regular accrual period |
| Last&nbsp;Regular&nbsp;End&nbsp;Date | Optional | `2022-03-01` ([formats]({{site.baseurl}}/common_formats/#date)) | The unadjusted end date of the last regular accrual period |
| Date Convention       | Optional    | `ModifiedFollowing` ([values]({{site.baseurl}}/common_values/#business-day-convention)) | The [business day convention]({{site.baseurl}}/date_adjustments/) |
| Date Calendar         | Optional    | `GBLO` ([values]({{site.baseurl}}/holiday_data/)) | The [holiday calendar]({{site.baseurl}}/holidays/) to use |

Valid combinations of conditional fields are as follows (other combinations are not allowed):

* `Start Date` and `End Date`
* `Start Date` and `Tenor`
* `Trade Date`, `Period To Start` and `Tenor`


## Swap by full details

These columns are used when loading a Swap trade by full details.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name           | Mandatory?  | Example/Format          | Description |
|-----------------------|-------------|-------------------------|-------------|
| Strata Trade Type     | Mandatory   | `Swap`                  | The type of the trade, case insensitive |

A swap is primarily defined by its legs.
The leg columns are of the form "Leg n xxx" where "n" is the leg number starting at 1 and "xxx" is the leg column name.

| Leg column name                      | Mandatory?  | Example/Format          | Description |
|--------------------------------------|-------------|-------------------------|-------------|
| Leg 1 Direction                      | Mandatory   | `Pay` ([values]({{site.baseurl}}/common_values/#pay-receive))   | The direction of the leg |
| Leg 1 Start Date                     | Fallback    | `2017-06-01` ([formats]({{site.baseurl}}/common_formats/#date)) | The unadjusted start date |
| Leg 1 End Date                       | Fallback    | `2022-06-01` ([formats]({{site.baseurl}}/common_formats/#date)) | The unadjusted end date |
| Leg 1 Frequency                      | Mandatory   | `3M` ([formats]({{site.baseurl}}/common_formats/#period))       | The accrual frequency |
| Leg 1 Date Convention                | Optional    | `ModifiedFollowing` ([values]({{site.baseurl}}/common_values/#business-day-convention)) | The accrual [business day convention]({{site.baseurl}}/date_adjustments/) |
| Leg 1 Date Calendar                  | Optional    | `GBLO` ([values]({{site.baseurl}}/holiday_data/))               | The accrual [holiday calendar]({{site.baseurl}}/holiday_data/) to use |
| Leg 1 Start Date Convention          | Optional    | `ModifiedFollowing` ([values]({{site.baseurl}}/common_values/#business-day-convention)) | The start date business day convention |
| Leg 1 Start Date Calendar            | Optional    | `GBLO` ([values]({{site.baseurl}}/holiday_data/))               | The start date holiday calendar |
| Leg 1 End Date Convention            | Optional    | `ModifiedFollowing` ([values]({{site.baseurl}}/common_values/#business-day-convention)) | The end date business day convention |
| Leg 1 End Date Calendar              | Optional    | `GBLO` ([values]({{site.baseurl}}/holiday_data/))               | The end date holiday calendar |
| Leg 1 Roll Convention                | Optional    | `Day1` ([values]({{site.baseurl}}/common_values/#roll-convention)) | The roll convention |
| Leg 1 Stub Convention                | Optional    | `ShortInitial` ([values]({{site.baseurl}}/common_values/#stub-convention)) | The stub convention, defaults to "SmartInitial" |
| Leg 1 First Regular Start Date       | Optional    | `2017-09-01` ([formats]({{site.baseurl}}/common_formats/#date)) | The unadjusted start date of the first regular accrual period |
| Leg 1 Last Regular End Date          | Optional    | `2022-03-01` ([formats]({{site.baseurl}}/common_formats/#date)) | The unadjusted end date of the last regular accrual period |
| Leg 1 Override Start Date            | Optional    | `2017-03-01` ([formats]({{site.baseurl}}/common_formats/#date)) | The unadjusted start date override |
| Leg 1 Override Start Date Convention | Optional    | `ModifiedFollowing` ([values]({{site.baseurl}}/common_values/#business-day-convention)) | The start date override business day convention |
| Leg 1 Override Start Date Calendar   | Optional    | `GBLO` ([values]({{site.baseurl}}/holiday_data/))               | The start date override holiday calendar |
| Leg 1 Payment Frequency              | Optional    | `3M` ([formats]({{site.baseurl}}/common_formats/#period))       | The payment frequency, defaults to the accrual frequency |
| Leg 1 Payment Relative To            | Optional    | `PeriodEnd`                                                     | The date that payments are relative to, defaults to "PeriodEnd" |
| Leg 1 Compounding Method             | Optional    | `Flat` ([values]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/CompoundingMethod.html)) | The compounding method, defaults to "None" |
| Leg 1 Payment Offset Days            | Optional    | `2`                                                             | The payment offset in days, defaults to no offset |
| Leg 1 Payment Offset Calendar        | Optional    | `GBLO` ([values]({{site.baseurl}}/holiday_data/))               | The payment offset calendar, defaults to "NoHolidays" |
| Leg 1 Payment Offset Adjustment Convention | Optional | `Following` ([values]({{site.baseurl}}/common_values/#business-day-convention)) | The payment offset adjustment business day convention |
| Leg 1 Payment Offset Adjustment Calendar | Optional | `GBLO` ([values]({{site.baseurl}}/holiday_data/))              | The payment offset adjustment holiday calendar |
| Leg 1 Currency                       | Fallback    | `GBP` ([values]({{site.baseurl}}/common_values/#currency))      | The payment currency |
| Leg 1 Notional                       | Fallback    | `1000000`                                                       | The notional amount, in the notional currency |
| Leg 1 Notional Currency              | Optional    | `USD` ([values]({{site.baseurl}}/common_values/#currency))      | The currency of the notional, defaults to the payment currency |
| Leg 1 FX Reset Index                 | Optional    | `GBP/USD-WM` ([values]({{site.baseurl}}/indices/#fx))           | The FX index used if the swap is FX Reset |
| Leg 1 FX Reset Initial Notional      | Optional    | `1200000`                                                       | The first fixed FX reset notional |
| Leg 1 FX Reset Relative To           | Optional    | `PeriodStart`                                                   | The date that the FX reset is relative to, defaults to "PeriodStart" |
| Leg 1 FX Reset Offset Days           | Optional    | `2`                                                             | The FX reset offset in days, defaults to no offset |
| Leg 1 FX Reset Offset Calendar       | Optional    | `GBLO` ([values]({{site.baseurl}}/holiday_data/))               | The FX reset offset calendar, defaults to "NoHolidays" |
| Leg 1 FX Reset Offset Adjustment Convention | Optional | `Following` ([values]({{site.baseurl}}/common_values/#business-day-convention)) | The FX reset offset adjustment business day convention |
| Leg 1 FX Reset Offset Adjustment Calendar | Optional | `GBLO` ([values]({{site.baseurl}}/holiday_data/))             | The FX reset offset adjustment holiday calendar |
| Leg 1 Notional Initial Exchange      | Optional    | `true`                                                          | Whether there is an initial exchange of notionals |
| Leg 1 Notional Intermediate Exchange | Optional    | `true`                                                          | Whether there is an intermediate exchange of notionals |
| Leg 1 Notional Final Exchange        | Optional    | `true`                                                          | Whether there is an final exchange of notionals |

The columns marked as "Fallback" can be set in two ways.
The code will first look for a column named "Leg 1 Start Date", then for a column named "Start Date".
This allows the start date, end date, currency and notional to be set once if they are the same on both legs.

Fixed rate legs:

| Leg column name                      | Mandatory?  | Example/Format          | Description |
|--------------------------------------|-------------|-------------------------|-------------|
| Leg 1 Fixed Rate                     | Mandatory   | `1.2`                                                           | The fixed rate, as a percentage, such as 1.2 for 1.2% |
| Leg 1 Day Count                      | Recommended | `Act/360` ([values]({{site.baseurl}}/common_values/#day-count)) | The day count convention, defaults from floating leg index |
| Leg 1 Future Value Notional          | Optional    | `123456`                                                        | The future value notional as used in BRL swaps |
| Leg 1 Initial Stub Rate              | Optional    | `2.1`                                                           | The fixed rate of the initial stub, such as 2.1 for 2.1% |
| Leg&nbsp;1&nbsp;Initial&nbsp;Stub&nbsp;Amount&nbsp;Currency   | Optional    | `GBP` ([values]({{site.baseurl}}/common_values/#currency))      | The currency of the initial stub |
| Leg 1 Initial Stub Amount            | Optional    | `45000`                                                         | The amount of the initial stub |
| Leg 1 Final Stub Rate                | Optional    | `2.1`                                                           | The fixed rate of the final stub, such as 2.1 for 2.1% |
| Leg 1 Final Stub Amount Currency     | Optional    | `GBP` ([values]({{site.baseurl}}/common_values/#currency))      | The currency of the final stub |
| Leg 1 Final Stub Amount              | Optional    | `45000`                                                         | The amount of the final stub |

Overnight rate legs:

| Leg column name                      | Mandatory?  | Example/Format          | Description |
|--------------------------------------|-------------|-------------------------|-------------|
| Leg 1 Index                          | Mandatory   | `GBP-SONIA` ([values]({{site.baseurl}}/indices/#overnight))     | The Overnight index |
| Leg 1 Day Count                      | Optional    | `Act/360` ([values]({{site.baseurl}}/common_values/#day-count)) | The day count convention, defaults from the index |
| Leg 1 Accrual Method                 | Optional    | `Compounded` ([values]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/OvernightAccrualMethod.html)) | The accrual method, defaults to "Compounded" |
| Leg 1 Rate Cut Off Days              | Optional    | `2`                                                             | The number of days before the end of the period that the rate is locked down |
| Leg&nbsp;1&nbsp;Negative&nbsp;Rate&nbsp;Method | Optional | `AllowNegative` ([values]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/NegativeRateMethod.html)) | The negative rate method, defaults to "AllowNegative" |
| Leg 1 Gearing                        | Optional    | `1.5`                                                           | The gearing multiplier |
| Leg 1 Spread                         | Optional    | `0.1`                                                           | The spread rate, as a percentage, such as 0.1 for 0.1% |

Ibor rate legs:

| Leg column name                      | Mandatory?  | Example/Format          | Description |
|--------------------------------------|-------------|-------------------------|-------------|
| Leg 1 Index                          | Mandatory   | `GBP-LIBOR-3M` ([values]({{site.baseurl}}/indices/#ibor))       | The Ibor index |
| Leg 1 Day Count                      | Optional    | `Act/360` ([values]({{site.baseurl}}/common_values/#day-count)) | The day count convention, defaults from the index |
| Leg 1 Fixing Relative To             | Optional    | `PeriodStart`                                                   | The date that fixings are relative to, defaults to "PeriodStart" |
| Leg 1 Fixing Offset Days             | Optional    | `2`                                                             | The fixing offset in days, defaults to no offset, defaults from the index |
| Leg 1 Fixing Offset Calendar         | Optional    | `GBLO` ([values]({{site.baseurl}}/holiday_data/))               | The fixing offset calendar, defaults to "NoHolidays", defaults from the index |
| Leg 1 Fixing Offset Adjustment Convention | Optional | `Following` ([values]({{site.baseurl}}/common_values/#business-day-convention)) | The payment fixing adjustment business day convention, defaults from the index |
| Leg 1 Fixing Offset Adjustment Calendar | Optional | `GBLO` ([values]({{site.baseurl}}/holiday_data/))               | The payment fixing adjustment holiday calendar, defaults from the index |
| Leg 1 Reset Frequency                | Optional    | `1M` ([formats]({{site.baseurl}}/common_formats/#period))       | The reset frequency, only used if more frequent than the accrual frequency |
| Leg 1 Reset Date Convention          | Optional    | `Following` ([values]({{site.baseurl}}/common_values/#business-day-convention)) | The reset date business day convention |
| Leg 1 Reset Date Calendar            | Optional    | `GBLO` ([values]({{site.baseurl}}/holiday_data/))               | The reset date holiday calendar |
| Leg 1 Reset Method                   | Optional    | `Weighted` ([values]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/IborRateResetMethod.html)) | The reset method, defaults to "Weighted" |
| Leg 1 First Rate                     | Optional    | `1.1`                                                           | The first interest rate, as a percentage, such as 1.1 for 1.1% |
| Leg 1 Negative Rate Method           | Optional    | `AllowNegative` ([values]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/NegativeRateMethod.html)) | The negative rate method, defaults to "AllowNegative" |
| Leg 1 Gearing                        | Optional    | `1.5`                                                           | The gearing multiplier |
| Leg 1 Spread                         | Optional    | `0.1`                                                           | The spread rate, as a percentage, such as 0.1 for 0.1% |
| Leg 1 Initial Stub Rate              | Optional    | `2.1`                                                           | The fixed rate of the initial stub, such as 2.1 for 2.1% |
| Leg 1 Initial Stub Amount Currency   | Optional    | `GBP` ([values]({{site.baseurl}}/common_values/#currency))      | The currency of the initial stub |
| Leg 1 Initial Stub Amount            | Optional    | `45000`                                                         | The amount of the initial stub |
| Leg 1 Initial Stub Index             | Optional    | `GBP-LIBOR-1M` ([values]({{site.baseurl}}/indices/))            | The index to use for the initial stub |
| Leg 1 Initial Stub Interpolated Index | Optional   | `GBP-LIBOR-3M` ([values]({{site.baseurl}}/indices/))            | The index to use for interpolation in the initial stub |
| Leg 1 Final Stub Rate                | Optional    | `2.1`                                                           | The fixed rate of the final stub, such as 2.1 for 2.1% |
| Leg 1 Final Stub Amount Currency     | Optional    | `GBP` ([values]({{site.baseurl}}/common_values/#currency))      | The currency of the final stub |
| Leg 1 Final Stub Amount              | Optional    | `45000`                                                         | The amount of the final stub |
| Leg 1 Final Stub Index               | Optional    | `GBP-LIBOR-1M` ([values]({{site.baseurl}}/indices/))            | The index to use for the final stub |
| Leg 1 Final Stub Interpolated Index  | Optional    | `GBP-LIBOR-3M` ([values]({{site.baseurl}}/indices/))            | The index to use for interpolation in the final stub |


Inflation rate legs:

| Leg column name                      | Mandatory?  | Example/Format          | Description |
|--------------------------------------|-------------|-------------------------|-------------|
| Leg 1 Index                          | Mandatory   | `GB-RPI` ([values]({{site.baseurl}}/indices/#price))            | The Price index |
| Leg 1 Inflation Lag                  | Optional    | `3M` ([formats]({{site.baseurl}}/common_formats/#period))       | The lag used when reading the price index, defaults from the index |
| Leg 1 Inflation Method               | Optional    | `Interpolated` ([values]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/PriceIndexCalculationMethod.html)) | The method to use, defaults from the currency |
| Leg&nbsp;1&nbsp;Inflation&nbsp;First&nbsp;Index&nbsp;Value | Optional | `154.3`                                      | The value of the price index at the start of the swap |
| Leg 1 Gearing                        | Optional    | `1.5`                                                           | The gearing multiplier |


## Variable notional/rate

Both formats of swap (convention and full details) support variable notionals and variable fixed rates.
The information is contained in one or more rows that follow the base swap row.
The additional rows only need to contain the minimal information for the variable element.

| Column name             | Mandatory?    | Example/Format          | Description |
|-------------------------|---------------|-------------------------|-------------|
| Strata&nbsp;Trade&nbsp;Type | Mandatory | `Variable`              | The type of the trade |
| Start Date              | Mandatory     | `2018-06-01` ([formats]({{site.baseurl}}/common_formats/#date)) | The unadjusted date when the variable element changes |
| Notional                | Optional      | `1500000`               | The notional amount that applies from the start date onwards for all legs |
| Leg 1 Notional          | Optional      | `1500000`               | As above, but only for a specific leg |
| Fixed Rate              | Optional      | `1.2`                   | The fixed rate, as a percentage, that applies from the start date onwards for all legs |
| Leg 1 Fixed Rate        | Optional      | `1.2`                   | As above, but only for a specific leg |

It is permitted to define a row with neither notional nor fixed rate specified, but such a row would simply be ignored.
For most swaps there is no need to use the leg-specific column names.

This example file has both variable notional and fixed rate:

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Convention,            Buy Sell, Start Date, Tenor, Fixed Rate, Notional
Swap,              OG,        123411, 2017-06-01, GBP-FIXED-1Y-LIBOR-3M, Buy,      2017-06-01  P5Y,   0.4,        2000000
Variable,          ,          ,       ,           ,                      ,         2018-06-01, ,      ,           1600000
Variable,          ,          ,       ,           ,                      ,         2019-06-01, ,      ,           1200000
Variable,          ,          ,       ,           ,                      ,         2020-06-01, ,      0.6,         800000
Variable,          ,          ,       ,           ,                      ,         2021-06-01, ,      ,            400000
```
