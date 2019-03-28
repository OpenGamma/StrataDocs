---
title: Trade loader for FX Single
permalink: /trade_loader_fx_single/
---

This page details the Strata CSV format for loading [FX Singles]({{site.baseurl}}/fx_single).
See the [overview page]({{site.baseurl}}/trade_loader) for details of other assets classes.


## Trade loader file format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

FX Singles can be specified using two different column sets - by convention and by full details.
The two column sets can be mixed in the same file.
In addition, a single file can contain other asset classes, such as Swaps or FRAs.
Just add the union of the column headers and fill in the necessary data on a row by row basis.


## Example

This example file specifies a FX Single trade by convention.

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Convention, Buy Sell, Currency, Notional, FX Rate, Payment Date
FxSingle,          OG,        123401, 2017-06-01, USD/CAD,    Buy,      USD,      1000000,  1.31,    2017-06-03
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## FX Single by convention

These columns are used when loading a FX Single trade by convention.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name             | Mandatory?  | Description |
|-------------------------|-------------|-------------|
| Strata Trade Type       | Mandatory   | The type of the trade, "FxSingle", "FX" or "FX Single", case insensitive |
| Convention              | Mandatory   | The convention, which is the currency pair, such as "GBP/USD" |
| Buy Sell                | Mandatory   | Whether the FX is "Buy" or "Sell" |
| Curency                 | Mandatory   | The currency of the notional amount |
| Notional                | Mandatory   | The notional amount, positive with direction defined by Buy/Sell |
| FX Rate                 | Mandatory   | The FX rate, which must be for the specified currency pair |
| Payment Date            | Mandatory   | The payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Payment Date Convention | Optional    | The payment [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Payment Date Calendar   | Optional    | The payment [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |


## FX Single by full details

These columns are used when loading a FX Single trade by full details.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name             | Mandatory?  | Description |
|-------------------------|-------------|-------------|
| Strata Trade Type       | Mandatory   | The type of the trade, "FxSingle", "FX" or "FX Single", case insensitive |
| Payment Date            | Conditional | The payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Payment Date Convention | Optional    | The payment [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Payment Date Calendar   | Optional    | The payment [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |
| Leg 1 Direction         | Mandatory   | The direction of the leg, "Pay" or "Receive" |
| Leg 1 Currency          | Mandatory   | The payment currency, such as "GBP" |
| Leg 1 Notional          | Mandatory   | The notional amount, in the currency of the leg |
| Leg 1 Payment Date      | Conditional | The payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Leg 2 Direction         | Mandatory   | The direction of the leg, "Pay" or "Receive" |
| Leg 2 Currency          | Mandatory   | The payment currency, such as "GBP" |
| Leg 2 Notional          | Mandatory   | The notional amount, in the currency of the leg |
| Leg 2 Payment Date      | Conditional | The payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |

One leg must be "Pay" and the other "Receive".
Either the leg specific payment dates or the shared payment date should be specified.
