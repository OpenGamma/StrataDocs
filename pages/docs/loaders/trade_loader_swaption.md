---
title: Trade loader for Swaption
permalink: /trade_loader_swaption/
---

This page details the Strata CSV format for loading [Swaptions]({{site.baseurl}}/swaption).
See the [overview page]({{site.baseurl}}/trade_loader) for details of other assets classes.


## Trade loader file format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

Swaptions can be specified using two different column sets - by convention and by full details.
The two column sets can be mixed in the same file.
In addition, a single file can contain other asset classes, such as Swaps or FRAs.
Just add the union of the column headers and fill in the necessary data on a row by row basis.


## Example

This example file specifies a Swaption trade by convention.

```
Strata Trade Type, Trade Date, Convention,            Buy Sell, Period To Start, Tenor, Notional, Fixed Rate, Long Short, Payoff Settlement Type, Expiry Date, Expiry Time, Expiry Zone,  Premium Direction, Premium Date, Premium Currency, Premium Amount
Swaption,          2017-06-01, GBP-FIXED-1Y-LIBOR-3M, Buy,      P1M,             P5Y,   2000000,  0.4,        Long,       Physical,               2017-06-03,  11:00,       Europe/Paris, Pay,               2017-03-03,   GBP,              1000
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## Swaption by convention

These columns are used when loading a Swaption trade by convention.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name             | Mandatory?  | Underlying | Description |
|-------------------------|-------------|---|----------|
| Strata Trade Type       | Mandatory   |   | The type of the trade, "Swaption", case insensitive |
| Start Date              | Conditional | Y | The unadjusted start date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| End Date                | Conditional | Y | The unadjusted end date, such as "2022-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Period To Start         | Conditional | Y | The period from the trade date to the trade start date, such as "P2M" or "2M" |
| Tenor                   | Conditional | Y | The period from the start date to the end date, such as "P5Y" or "5Y", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Convention              | Mandatory   | Y | The Swap convention, such as "GBP-FIXED-1Y-LIBOR-3M" |
| Buy Sell                | Mandatory   | Y | Whether the Swap is "Buy" or "Sell" |
| Notional                | Mandatory   | Y | The notional amount, currency defined by the convention |
| Fixed Rate              | Mandatory   | Y | The fixed rate, as a percentage, such as "1.2" for 1.2% |
| FX Rate                 | Conditional | Y | The FX rate, mandatory for cross-currency swaps |
| Roll Convention         | Optional    | Y | The roll convention, such as "Day21" or "EOM" |
| Stub Convention         | Optional    | Y | The stub convention, such as "ShortInitial" |
| First Regular Start Date | Optional   | Y | The unadjusted start date of the first regular accrual period, such as "2017-09-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Last Regular End Date   | Optional    | Y | The unadjusted end date of the last regular accrual period, such as "2022-03-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Date Convention         | Optional    | Y | The [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Date Calendar           | Optional    | Y | The [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |
| Long Short              | Mandatory   |   | Whether the option is "Long" or "Short" |
| Payoff Settlement Type  | Mandatory   |   | The type of payoff settlement, "Physical", "CashPrice", "ParYield", "ZeroCouponYield", "CollateralizedCashPrice" |
| Payoff Settlement Date  | Conditional |   | The date of the payoff settlement, mandatory unless type is "Physical" |
| Expiry Date             | Mandatory   |   | The expiry date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Expiry Time             | Mandatory   |   | The expiry time-of-day, such as "11:00", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Expiry Zone             | Mandatory   |   | The expiry zone, such as "Europe/Paris" (IANA time zone names) or "+02:00" |
| Premium Direction       | Mandatory   |   | The premium direction, "Pay" or "Receive" |
| Premium Currency        | Mandatory   |   | The premium currency, such as "GBP" |
| Premium Amount          | Mandatory   |   | The premium amount, in the premium currency, positive with direction defined by Pay/Receive |
| Premium Date            | Mandatory   |   | The premium date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Premium Date Convention | Optional    |   | The premium [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Premium Date Calendar   | Optional    |   | The premium [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |

Valid combinations of conditional fields are as follows (other combinations are not allowed):

* "Start Date" and "End Date"
* "Start Date" and "Tenor"
* "Trade Date", "Period To Start" and "Tenor"

The columns marked with Underlying of "Y" represent the underlying Swap,
and have the same [CSV columns]({{site.baseurl}}/trade_loader_swap).


## Swaption by full details

To represent an Swaption by full details, replace the columns marked Underlying of "Y"
with the full details columns from the [Swap]({{site.baseurl}}/trade_loader_swap) CSV format.
