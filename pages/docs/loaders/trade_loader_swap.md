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

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Trade Type     | Mandatory   | The type of the trade, "Swap", case insensitive |
| Start Date            | Conditional | The unadjusted start date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| End Date              | Conditional | The unadjusted end date, such as "2022-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Period To Start       | Conditional | The period from the trade date to the trade start date, such as "P2M" or "2M" |
| Tenor                 | Conditional | The period from the start date to the end date, such as "P5Y" or "5Y", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Convention            | Mandatory   | The Swap convention, such as "GBP-FIXED-1Y-LIBOR-3M" |
| Buy Sell              | Mandatory   | Whether the Swap is "Buy" or "Sell" |
| Notional              | Mandatory   | The notional amount, currency defined by the convention |
| Fixed Rate            | Mandatory   | The fixed rate, as a percentage, such as "1.2" for 1.2% |
| FX Rate               | Conditional | The FX rate, mandatory for cross-currency swaps |
| Roll Convention       | Optional    | The roll convention, such as "Day21" or "EOM" |
| Stub Convention       | Optional    | The stub convention, such as "ShortInitial" |
| First Regular Start Date | Optional | The unadjusted start date of the first regular accrual period, such as "2017-09-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Last Regular End Date | Optional    | The unadjusted end date of the last regular accrual period, such as "2022-03-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Date Convention       | Optional    | The [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Date Calendar         | Optional    | The [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |

Valid combinations of conditional fields are as follows (other combinations are not allowed):

* "Start Date" and "End Date"
* "Start Date" and "Tenor"
* "Trade Date", "Period To Start" and "Tenor"


## Swap by full details

These columns are used when loading a Swap trade by full details.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Trade Type     | Mandatory   | The type of the trade, "Swap", case insensitive |

A swap is primarily defined by its legs.
The leg columns are of the form "Leg n xxx" where "n" is the leg number starting at 1 and "xxx" is the leg column name.

| Leg column name                      | Mandatory?  | Description |
|--------------------------------------|-------------|-------------|
| Leg 1 Direction                      | Mandatory   | The direction of the leg, "Pay" or "Receive" |
| Leg 1 Start Date                     | Fallback    | The unadjusted start date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Leg 1 End Date                       | Fallback    | The unadjusted end date, such as "2022-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Leg 1 Frequency                      | Mandatory   | The accrual frequency, such as "P3M" or "3M" |
| Leg 1 Date Convention                | Optional    | The accrual [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following", defaults to "ModifiedFollowing" |
| Leg 1 Date Calendar                  | Optional    | The accrual [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |
| Leg 1 Start Date Convention          | Optional    | The start date business day convention |
| Leg 1 Start Date Calendar            | Optional    | The start date holiday calendar |
| Leg 1 End Date Convention            | Optional    | The end date business day convention |
| Leg 1 End Date Calendar              | Optional    | The end date holiday calendar |
| Leg 1 Roll Convention                | Optional    | The roll convention, such as "Day21" or "EOM" |
| Leg 1 Stub Convention                | Optional    | The stub convention, such as "ShortFinal", defaults to "SmartInitial" |
| Leg 1 First Regular Start Date       | Optional    | The unadjusted start date of the first regular accrual period, such as "2017-09-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Leg 1 Last Regular End Date          | Optional    | The unadjusted end date of the last regular accrual period, such as "2022-03-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Leg 1 Override Start Date            | Optional    | The unadjusted start date override |
| Leg 1 Override Start Date Convention | Optional    | The start date override business day convention |
| Leg 1 Override Start Date Calendar   | Optional    | The start date override holiday calendar |
| Leg 1 Payment Frequency              | Optional    | The payment frequency, such as "P3M" or "3M", defaults to the accrual frequency |
| Leg 1 Payment Relative To            | Optional    | The date that payments are relative to, defaults to "PeriodEnd" |
| Leg 1 Compounding Method             | Optional    | The compounding method, defaults to "None" |
| Leg 1 Payment Offset Days            | Optional    | The payment offset in days, defaults to no offset |
| Leg 1 Payment Offset Calendar        | Optional    | The payment offset calendar, defaults to "NoHolidays" |
| Leg 1 Payment Offset Adjustment Convention | Optional | The payment offset adjustment business day convention |
| Leg 1 Payment Offset Adjustment Calendar | Optional | The payment offset adjustment holiday calendar |
| Leg 1 Currency                       | Fallback    | The payment currency, such as "GBP" |
| Leg 1 Notional                       | Fallback    | The notional amount, in the notional currency |
| Leg 1 Notional Currency              | Optional    | The currency of the notional, defaults to the payment currency |
| Leg 1 FX Reset Index                 | Optional    | The FX index used if the swap is FX Reset |
| Leg 1 FX Reset Initial Notional      | Optional    | The first fixed FX reset notional |
| Leg 1 FX Reset Relative To           | Optional    | The date that the FX reset is relative to, defaults to "PeriodStart" |
| Leg 1 FX Reset Offset Days           | Optional    | The FX reset offset in days, defaults to no offset |
| Leg 1 FX Reset Offset Calendar       | Optional    | The FX reset offset calendar, defaults to "NoHolidays" |
| Leg 1 FX Reset Offset Adjustment Convention | Optional | The FX reset offset adjustment business day convention |
| Leg 1 FX Reset Offset Adjustment Calendar | Optional | The FX reset offset adjustment holiday calendar |
| Leg 1 Notional Initial Exchange      | Optional    | Whether there is an initial exchange of notionals, such as "True" |
| Leg 1 Notional Intermediate Exchange | Optional    | Whether there is an intermediate exchange of notionals, such as "True" |
| Leg 1 Notional Final Exchange        | Optional    | Whether there is an final exchange of notionals, such as "True" |

The columns marked as "Fallback" can be set in two ways.
The code will first look for a column named "Leg 1 Start Date", then for a column named "Start Date".
This allows the start date, end date, currency and notional to be set once if they are the same on both legs.

Fixed rate legs:

| Leg column name                      | Mandatory?  | Description |
|--------------------------------------|-------------|-------------|
| Leg 1 Fixed Rate                     | Mandatory   | The fixed rate, as a percentage, such as "1.2" for 1.2% |
| Leg 1 Day Count                      | Recommended | The day count convention, such as "Act.360", defaults from floating leg index |
| Leg 1 Future Value Notional          | Optional    | The future value notional as used in BRL swaps |
| Leg 1 Initial Stub Rate              | Optional    | The fixed rate of the initial stub |
| Leg 1 Initial Stub Amount Currency   | Optional    | The currency of the initial stub |
| Leg 1 Initial Stub Amount            | Optional    | The amount of the initial stub |
| Leg 1 Final Stub Rate                | Optional    | The fixed rate of the final stub |
| Leg 1 Final Stub Amount Currency     | Optional    | The currency of the final stub |
| Leg 1 Final Stub Amount              | Optional    | The amount of the final stub |

Overnight rate legs:

| Leg column name                      | Mandatory?  | Description |
|--------------------------------------|-------------|-------------|
| Leg 1 Index                          | Mandatory   | The [Overnight index]({{site.baseurl}}/indices/), such as "GBP-SONIA" |
| Leg 1 Day Count                      | Optional    | The day count convention, such as "Act.360", defaults from the index |
| Leg 1 Accrual Method                 | Optional    | The accrual method, "Compounded" or "Averaged", defaults to "Compounded" and normally set from the index |
| Leg 1 Rate Cut Off Days              | Optional    | The number of days before the end of the period that the rate is locked down |
| Leg 1 Negative Rate Method           | Optional    | The negative rate method, "AllowNegative" or "NotNegative", defaults to "AllowNegative" |
| Leg 1 Gearing                        | Optional    | The gearing multiplier |
| Leg 1 Spread                         | Optional    | The spread rate, as a percentage, such as "0.1" for 0.1% |

Ibor rate legs:

| Leg column name                      | Mandatory?  | Description |
|--------------------------------------|-------------|-------------|
| Leg 1 Index                          | Mandatory   | The [Ibor index]({{site.baseurl}}/indices/), such as "GBP-LIBOR-3M" |
| Leg 1 Day Count                      | Optional    | The day count convention, such as "Act.360", defaults from the index |
| Leg 1 Fixing Relative To             | Optional    | The date that fixings are relative to, defaults to "PeriodStart" |
| Leg 1 Fixing Offset Days             | Optional    | The fixing offset in days, defaults to no offset, defaults from the index |
| Leg 1 Fixing Offset Calendar         | Optional    | The fixing offset calendar, defaults to "NoHolidays", defaults from the index |
| Leg 1 Fixing Offset Adjustment Convention | Optional | The payment fixing adjustment business day convention, defaults from the index |
| Leg 1 Fixing Offset Adjustment Calendar | Optional | The payment fixing adjustment holiday calendar, defaults from the index |
| Leg 1 Reset Frequency                | Optional    | The reset frequency, only used if more frequent than the accrual frequency, see [accepted formats]({{site.baseurl}}/common_formats/) |
| Leg 1 Reset Date Convention          | Optional    | The reset date business day convention |
| Leg 1 Reset Date Calendar            | Optional    | The reset date holiday calendar |
| Leg 1 Reset Method                   | Optional    | The reset method, "Weighted" or "Unweighted", defaults to "Weighted" |
| Leg 1 First Rate                     | Optional    | The first interest rate, as a percentage, such as "1.1" for 1.1% |
| Leg 1 Negative Rate Method           | Optional    | The negative rate method, "AllowNegative" or "NotNegative", defaults to "AllowNegative" |
| Leg 1 Gearing                        | Optional    | The gearing multiplier |
| Leg 1 Spread                         | Optional    | The spread rate, as a percentage, such as "0.1" for 0.1% |
| Leg 1 Initial Stub Rate              | Optional    | The fixed rate of the initial stub |
| Leg 1 Initial Stub Amount Currency   | Optional    | The currency of the initial stub |
| Leg 1 Initial Stub Amount            | Optional    | The amount of the initial stub |
| Leg 1 Initial Stub Index             | Optional    | The index to use for the initial stub |
| Leg 1 Initial Stub Interpolated Index | Optional   | The index to use for interpolation in the initial stub |
| Leg 1 Final Stub Rate                | Optional    | The fixed rate of the final stub |
| Leg 1 Final Stub Amount Currency     | Optional    | The currency of the final stub |
| Leg 1 Final Stub Amount              | Optional    | The amount of the final stub |
| Leg 1 Final Stub Index               | Optional    | The index to use for the final stub |
| Leg 1 Final Stub Interpolated Index  | Optional    | The index to use for interpolation in the final stub |


Inflation rate legs:

| Leg column name                      | Mandatory?  | Description |
|--------------------------------------|-------------|-------------|
| Leg 1 Index                          | Mandatory   | The [Price index]({{site.baseurl}}/indices/), such as "GB-RPI" |
| Leg 1 Inflation Lag                  | Optional    | The lag used when reading the price index, such as "P3M", "3M" or "3", defaults from the index |
| Leg 1 Inflation Method               | Optional    | The method to use, "Monthly", "Interpolated" or "InterpolatedJapan", defaults from the currency |
| Leg 1 Inflation First Index Value    | Optional    | The value of the price index at the start of the swap |
| Leg 1 Gearing                        | Optional    | The gearing multiplier |


## Variable notional/rate

Both formats of swap (convention and full details) support variable notionals and variable fixed rates.
The information is contained in one or more rows that follow the base swap row.
The additional rows only need to contain the minimal information for the variable element.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Trade Type     | Mandatory   | The type of the trade, "Variable" |
| Start Date            | Mandatory   | The unadjusted date when the variable element changes, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Notional              | Optional    | The notional amount that applies from the start date onwards for all legs |
| Leg 1 Notional        | Optional    | As above, but only for a specific leg |
| Fixed Rate            | Optional    | The fixed rate, as a percentage, that applies from the start date onwards for all legs |
| Leg 1 Fixed Rate      | Optional    | As above, but only for a specific leg |

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
