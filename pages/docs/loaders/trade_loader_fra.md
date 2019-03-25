---
title: Trade loader for FRAs
permalink: /trade_loader_fra/
---

This page details the Strata CSV format for loading [FRAs]({{site.baseurl}}/fra).
See the [overview page]({{site.baseurl}}/trade_loader) for details of other assets classes.


## Trade loader file format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

FRAs can be specified using two different column sets - by convention and by full details.
The two column sets can be mixed in the same file.
In addition, a single file can contain other asset classes, such as Swaps or FX.
Just add the union of the column headers and fill in the necessary data on a row by row basis.


## Example

This example file specifies a FRA trade by convention.

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Convention,            Buy Sell, Period To Start, Notional, Fixed Rate
Fra,               OG,        123401, 2017-06-01, GBP-LIBOR-3M,          Buy,      P2M,             1000000,  0.5,
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## FRA by convention

These columns are used when loading a FRA trade by convention.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Trade Type     | Mandatory   | The type of the trade, "Fra", case insensitive |
| Start Date            | Conditional | The unadjusted start date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| End Date              | Conditional | The unadjusted end date, such as "2017-09-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Period To Start       | Conditional | The period from the trade date to the trade start date, such as "P2M" or "2M" |
| Convention            | Mandatory   | The FRA convention, which must be an [Ibor index]({{site.baseurl}}/indices/), such as "GBP-LIBOR-3M" |
| Buy Sell              | Mandatory   | Whether the FRA is "Buy" or "Sell" |
| Notional              | Mandatory   | The notional amount, currency defined by the convention |
| Fixed Rate            | Mandatory   | The fixed rate, as a percentage, such as "1.2" for 1.2% |
| Date Convention       | Optional    | The [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Date Calendar         | Optional    | The [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |

Valid combinations of conditional fields are as follows (other combinations are not allowed):

* "Start Date" and "End Date"
* "Trade Date" and "Period To Start"


## FRA by full details

These columns are used when loading a FRA trade by full details.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Trade Type     | Mandatory   | The type of the trade, "Fra", case insensitive |
| Start Date            | Mandatory   | The unadjusted start date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| End Date              | Mandatory   | The unadjusted end date, such as "2017-09-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Index                 | Mandatory   | The [floating index]({{site.baseurl}}/indices/), such as "GBP-LIBOR-3M" |
| Interpolated Index    | Optional    | The [floating index]({{site.baseurl}}/indices/) to interpolate with, such as "GBP-LIBOR-6M" |
| Buy Sell              | Mandatory   | Whether the FRA is "Buy" or "Sell" |
| Notional              | Mandatory   | The notional amount, currency defined by the index |
| Fixed Rate            | Mandatory   | The fixed rate, as a percentage, such as "1.2" for 1.2% |
| Day Count             | Optional    | The [day count convention]({{site.baseurl}}/day_counts/), such as "Act/360" |
| Date Convention       | Optional    | The [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Date Calendar         | Optional    | The [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |
