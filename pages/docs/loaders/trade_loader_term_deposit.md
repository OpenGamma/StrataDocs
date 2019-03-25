---
title: Trade loader for Term Deposits
permalink: /trade_loader_term_deposit/
---

This page details the Strata CSV format for loading [Term Deposits]({{site.baseurl}}/term_deposit).
See the [overview page]({{site.baseurl}}/trade_loader) for details of other assets classes.


## Trade loader file format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

Term Deposits can be specified using two different column sets - by convention and by full details.
The two column sets can be mixed in the same file.
In addition, a single file can contain other asset classes, such as Swaps or FX.
Just add the union of the column headers and fill in the necessary data on a row by row basis.


## Example

This example file specifies a Term Deposit trade by convention.

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Convention,     Buy Sell, Tenor, Notional, Fixed Rate
TermDeposit,       OG,        123401, 2017-06-01, GBP-Deposit-T0, Buy,      P7D,   1000000,  0.5
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## Term Deposit by convention

These columns are used when loading a Term Deposit trade by convention.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Trade Type     | Mandatory   | The type of the trade, "TermDeposit" or "Term Deposit", case insensitive |
| Start Date            | Conditional | The unadjusted start date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| End Date              | Conditional | The unadjusted end date, such as "2017-09-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Tenor                 | Conditional | The tenor of the instrument, such as "P2M" or "2M", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Convention            | Mandatory   | The convention, such as "GBP-Deposit-T0" |
| Buy Sell              | Mandatory   | Whether the deposit is "Buy" or "Sell" |
| Notional              | Mandatory   | The notional amount, currency defined by the convention |
| Fixed Rate            | Mandatory   | The fixed rate, as a percentage, such as "1.2" for 1.2% |
| Date Convention       | Optional    | The [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Date Calendar         | Optional    | The [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |

Valid combinations of conditional fields are as follows (other combinations are not allowed):

* "Start Date" and "End Date"
* "Trade Date" and "Tenor"


## Term Deposit by full details

These columns are used when loading a Term Deposit trade by full details.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Trade Type     | Mandatory   | The type of the trade, "TermDeposit" or "Term Deposit", case insensitive |
| Start Date            | Mandatory   | The unadjusted start date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| End Date              | Mandatory   | The unadjusted end date, such as "2017-09-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Buy Sell              | Mandatory   | Whether the trade is "Buy" or "Sell" |
| Currency              | Mandatory   | The deposit currency, such as "GBP" |
| Notional              | Mandatory   | The notional amount, currency defined by the index |
| Fixed Rate            | Mandatory   | The fixed rate, as a percentage, such as "1.2" for 1.2% |
| Day Count             | Mandatory   | The [day count convention]({{site.baseurl}}/day_counts/), such as "Act/360" |
| Date Convention       | Optional    | The [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Date Calendar         | Optional    | The [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |
