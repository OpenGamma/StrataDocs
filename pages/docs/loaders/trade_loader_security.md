---
title: Trade loader for Securities
permalink: /trade_loader_security/
---

This page details the Strata CSV format for loading securities.
See the [overview page]({{site.baseurl}}/trade_loader) for details of other assets classes.

{{note}}Note that there is a separate CSV format for [positions]({{site.baseurl}}/position_loader/).{{end}}


## Trade loader file format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

Securities can be specified using one column set.
In addition, a single file can contain other asset classes, such as Swaps or FX.
Just add the union of the column headers and fill in the necessary data on a row by row basis.


## Example

This example file specifies a Security trade.

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Settlement Date, Buy Sell, Security Id, Quantity, Price
Security,          OG,        123401, 2017-06-01, 2017-06-03,      Buy,      AAPL,        12,       14.5
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## Security trade

These columns are used when loading a Security trade by convention.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Trade Type     | Mandatory   | The type of the trade, "Security", case insensitive |
| Security Id Scheme    | Optional    | The scheme (symbology) within which the security identifier is unique, default "OG-Security" |
| Buy Sell              | Optional    | Whether the trade is "Buy" or "Sell" |
| Security Id           | Mandatory   | The security identifier |
| Quantity              | Mandatory   | The quantity purchased |
| Price                 | Mandatory   | The price paid for each security |

Either use "Buy Sell" and a positive "Quantity", or a signed "Quantity" (positive if bought, negative if sold)
