---
title: Trade loader for Bullet Payments
permalink: /trade_loader_bullet_payment/
---

This page details the Strata CSV format for loading [Bullet Payments]({{site.baseurl}}/bullet_payment).
See the [overview page]({{site.baseurl}}/trade_loader) for details of other assets classes.


## Trade loader file format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

Bullet Payments can be specified using two different column sets - by convention and by full details.
The two column sets can be mixed in the same file.
In addition, a single file can contain other asset classes, such as Swaps or FX.
Just add the union of the column headers and fill in the necessary data on a row by row basis.


## Example

This example file specifies a Bullet Payment trade by convention.

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Direction, Currency, Notional, Payment Date
BulletPayment,     OG,        123401, 2017-06-01, Pay,       GBP,      1000000,  2017-06-08
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## Bullet Payment by full details

These columns are used when loading a Bullet Payment trade by convention.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Trade Type     | Mandatory   | The type of the trade, "BulletPayment", "Bullet" or "Bullet Payment", case insensitive |
| Direction             | Mandatory   | Whether the payment is "Pay" or "Receive" |
| Currency              | Mandatory   | The currency of the notional |
| Notional              | Mandatory   | The notional amount, currency defined by the convention |
| Payment Date          | Mandatory   | The payment date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Payment Date Convention | Optional    | The payment [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Payment Date Calendar   | Optional    | The payment [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |
