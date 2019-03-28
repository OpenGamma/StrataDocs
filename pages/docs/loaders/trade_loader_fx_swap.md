---
title: Trade loader for FX Swap
permalink: /trade_loader_fx_swap/
---

This page details the Strata CSV format for loading [FX Swaps]({{site.baseurl}}/fx_swap).
See the [overview page]({{site.baseurl}}/trade_loader) for details of other assets classes.


## Trade loader file format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

FX Swaps can be specified using two different column sets - by convention and by full details.
The two column sets can be mixed in the same file.
In addition, a single file can contain other asset classes, such as Swaps or FRAs.
Just add the union of the column headers and fill in the necessary data on a row by row basis.


## Example

This example file specifies a FX Swap trade by convention.

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Convention, Buy Sell, Currency, Notional, FX Rate, Payment Date, Far FX Rate, Far Payment Date
FxSwap,            OG,        123401, 2017-06-01, USD/CAD,    Buy,      USD,      1000000,  1.31,    2017-06-03,   1.34,        2017-09-03
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## FX Swap by convention

These columns are used when loading a FX Swap trade by convention.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name             | Mandatory?  | Description |
|-------------------------|-------------|-------------|
| Strata Trade Type       | Mandatory   | The type of the trade, "FxSwap" or "FX Swap", case insensitive |
| Convention              | Mandatory   | The convention, which is the currency pair, such as "GBP/USD" |
| Buy Sell                | Mandatory   | Whether the FX is "Buy" or "Sell" |
| Curency                 | Mandatory   | The currency of the notional amount |
| Notional                | Mandatory   | The notional amount, positive with direction defined by Buy/Sell |
| FX Rate                 | Mandatory   | The near FX rate, which must be for the specified currency pair |
| Payment Date            | Mandatory   | The near payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Far FX Rate             | Mandatory   | The far FX rate, which must be for the specified currency pair |
| Far Payment Date        | Mandatory   | The far payment date, such as "2017-09-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Payment Date Convention | Optional    | The payment [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Payment Date Calendar   | Optional    | The payment [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |


## FX Swap by full details

These columns are used when loading a FX Swap trade by full details.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name             | Mandatory?  | Description |
|-------------------------|-------------|-------------|
| Strata Trade Type       | Mandatory   | The type of the trade, "FxSwap" or "FX Swap", case insensitive |
| Payment Date            | Conditional | The near payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Payment Date Convention | Optional    | The payment [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Payment Date Calendar   | Optional    | The payment [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |
| Leg 1 Direction         | Mandatory   | The near direction of the leg, "Pay" or "Receive" |
| Leg 1 Currency          | Mandatory   | The near payment currency, such as "GBP" |
| Leg 1 Notional          | Mandatory   | The near notional amount, in the currency of the leg |
| Leg 1 Payment Date      | Conditional | The near payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Leg 2 Direction         | Mandatory   | The near direction of the leg, "Pay" or "Receive" |
| Leg 2 Currency          | Mandatory   | The near payment currency, such as "GBP" |
| Leg 2 Notional          | Mandatory   | The near notional amount, in the currency of the leg |
| Leg 2 Payment Date      | Conditional | The near payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Far Payment Date        | Conditional | The far payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Far Leg 1 Direction     | Mandatory   | The far direction of the leg, "Pay" or "Receive" |
| Far Leg 1 Currency      | Mandatory   | The far payment currency, such as "GBP" |
| Far Leg 1 Notional      | Mandatory   | The far notional amount, in the currency of the leg |
| Far Leg 1 Payment Date  | Conditional | The far payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Far Leg 2 Direction     | Mandatory   | The far direction of the leg, "Pay" or "Receive" |
| Far Leg 2 Currency      | Mandatory   | The far payment currency, such as "GBP" |
| Far Leg 2 Notional      | Mandatory   | The far notional amount, in the currency of the leg |
| Far Leg 2 Payment Date  | Conditional | The far payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |

Within the near and far groups, one leg must be "Pay" and the other "Receive".
Within the near and far groups, either the leg specific payment dates or the shared payment date should be specified.
