---
title: Trade loader
permalink: /trade_loader/
---

The trade loader is used to load different kinds of trade, such as FRAs, Swaps, Securities and Term Deposits.
It is one of a number of [loaders]({{site.baseurl}}/loaders) included in Strata.


## Loader

Trades can be loaded using the [`TradeCsvLoader`]({{site.baseurl}}/apidocs/com/opengamma/strata/loader/csv/TradeCsvLoader.html)

```
ResourceLocator locator = ResourceLocator.ofFile(filename);
ValueWithFailures<List<Trades>> trades = TradeCsvLoader.load(locator);
```


## Format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

Each asset class has a different set of columns, see the links below.
A single file can contain a mixture of asset classes, just add the union of the column headers and
fill in the necessary data on a row by row basis.

The follow asset classes are supported:

* [FRAs]({{site.baseurl}}/trade_loader_fra)
* [Swaps]({{site.baseurl}}/trade_loader_swap)
* [Swaptions]({{site.baseurl}}/trade_loader_swaption)
* [Bullet Payments]({{site.baseurl}}/trade_loader_bullet_payment)
* [Term Deposits]({{site.baseurl}}/trade_loader_term_deposit)
* [FX Singles]({{site.baseurl}}/trade_loader_fx_single)
* [FX Swaps]({{site.baseurl}}/trade_loader_fx_swap)
* [FX Vanilla Options]({{site.baseurl}}/trade_loader_fx_vanilla_option)
* [CDS]({{site.baseurl}}/trade_loader_cds)
* [Securities]({{site.baseurl}}/trade_loader_security)


### Columns common to all formats

These columns are common to all formats.
They are documented here rather than being repeated on each page:

| Column name           | Mandatory? | Description |
|-----------------------|------------|-------------|
| Id Scheme             | Optional   | The scheme (symbology) within which the trade identifier is unique, default "OG-Trade" |
| Id                    | Optional   | The trade identifier |
| Trade Date            | Optional   | The trade date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Trade Time            | Optional   | The trade time-of-day, such as "11:00", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Trade Zone            | Optional   | The trade zone, such as "Europe/Paris" (IANA time zone names) or "+02:00" |
| Counterparty Scheme   | Optional   | The scheme (symbology) within which the counterparty is unique, default "OG-Counterparty" |
| Counterparty          | Optional   | The counterparty |
| Settlement Date       | Optional   | The date the trade settles, such as "2017-06-03", see [accepted formats]({{site.baseurl}}/common_formats/) |

Note that the columns above are supported by all asset classes.


### Example

This example file specifies one FRA, one Swap and one Term Deposit.

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Convention,            Buy Sell, Period To Start, Tenor, Notional, Fixed Rate
Fra,               OG,        123401, 2017-06-01, GBP-LIBOR-3M,          Buy,      P2M,             ,      1000000,  0.5
Swap,              OG,        123411, 2017-06-01, GBP-FIXED-1Y-LIBOR-3M, Buy,      P1M,             P5Y,   2000000,  0.4
TermDeposit,       OG,        123401, 2017-06-01, GBP-Deposit-T0,        Buy,      P7D,             ,      1000000,  0.5
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## Writer

Trades can be written to CSV using [`TradeCsvWriter`]({{site.baseurl}}/apidocs/com/opengamma/strata/loader/csv/TradeCsvWriter.html)

```
StribfBuilder buf = new StringBuilder();
TradeCsvWriter.write(trades, buf);
```

