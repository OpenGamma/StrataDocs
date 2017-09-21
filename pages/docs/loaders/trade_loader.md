---
title: Trade loader
permalink: /trade_loader/
---

The trade loader is used to load FRA and Swap trades.
It is one of a number of [loaders]({{site.baseurl}}/loaders) included in Strata.


## Loader

Trades can be loaded using the [`TradeCsvLoader`]({{site.baseurl}}/apidocs/com/opengamma/strata/loader/csv/TradeCsvLoader.html)

```
ResourceLocator locator = ResourceLocator.ofFile(filename);
ValueWithFailures<List<Trades>> trades = TradeCsvLoader.load(locator);
```


## Format

The trades file is a CSV-formatted file. Details TODO!


## Example

This example file specifies one FRA and one Swap.

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Convention,            Buy Sell, Period To Start, Tenor, Fixed Rate, Notional
Fra,               OG,        123401, 2017-06-01, GBP-LIBOR-3M,          Buy,      P2M,             ,      0.5,        1000000
Swap,              OG,        123411, 2017-06-01, GBP-FIXED-1Y-LIBOR-3M, Buy,      P1M,             P5Y,   0.4,        2000000
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.
