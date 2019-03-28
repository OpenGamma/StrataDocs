---
title: Trade loader for FX Vanilla Option
permalink: /trade_loader_fx_vanilla_option/
---

This page details the Strata CSV format for loading [FX singles]({{site.baseurl}}/fx_vanilla_option).
See the [overview page]({{site.baseurl}}/trade_loader) for details of other assets classes.


## Trade loader file format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

FX Vanilla Options can be specified using two different column sets - by convention and by full details.
The two column sets can be mixed in the same file.
In addition, a single file can contain other asset classes, such as Swaps or FRAs.
Just add the union of the column headers and fill in the necessary data on a row by row basis.


## Example

This example file specifies a FX Vanilla Option trade by convention.

```
Strata Trade Type, Convention, Buy Sell, Currency, Notional, FX Rate, Payment Date, Long Short, Premium Direction, Premium Date, Premium Currency, Premium Amount
FxSingle,          USD/CAD,    Buy,      USD,      1000000,  1.31,    2017-06-03,   Long,       Pay,               2017-03-03,   GBP,              1000
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## FX Vanilla Option by convention

These columns are used when loading a FX Vanilla Option trade by convention.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name             | Mandatory?  | Underlying | Description |
|-------------------------|-------------|---|----------|
| Strata Trade Type       | Mandatory   |   | The type of the trade, "FxVanillaOption" or "FX Vanilla Option", case insensitive |
| Convention              | Mandatory   | Y | The convention, which is the currency pair, such as "GBP/USD" |
| Buy Sell                | Mandatory   | Y | Whether the underlying FX is "Buy" or "Sell" |
| Curency                 | Mandatory   | Y | The currency of the notional amount |
| Notional                | Mandatory   | Y | The notional amount, positive with direction defined by Buy/Sell |
| FX Rate                 | Mandatory   | Y | The FX rate, which must be for the specified currency pair |
| Payment Date            | Mandatory   | Y | The payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Payment Date Convention | Optional    | Y | The payment [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Payment Date Calendar   | Optional    | Y | The payment [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |
| Long Short              | Mandatory   |   | Whether the option is "Long" or "Short" |
| Expiry Date             | Mandatory   |   | The expiry date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Expiry Time             | Mandatory   |   | The expiry time-of-day, such as "11:00", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Expiry Zone             | Mandatory   |   | The expiry zone, such as "Europe/Paris" (IANA time zone names) or "+02:00" |
| Premium Direction       | Mandatory   |   | The premium direction, "Pay" or "Receive" |
| Premium Currency        | Mandatory   |   | The premium currency, such as "GBP" |
| Premium Amount          | Mandatory   |   | The premium amount, in the premium currency, positive with direction defined by Pay/Receive |
| Premium Date            | Mandatory   |   | The premium date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Premium Date Convention | Optional    |   | The premium [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Premium Date Calendar   | Optional    |   | The premium [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |

The columns marked with Underlying of "Y" represent the underlying FX Single,
and have the same [CSV columns]({{site.baseurl}}/trade_loader_fx_single).


## FX Vanilla Option by full details

To represent an FX Vanilla Option by full details, replace the columns marked Underlying of "Y"
with the full details columns from the [FX Single]({{site.baseurl}}/trade_loader_fx_single) CSV format.
