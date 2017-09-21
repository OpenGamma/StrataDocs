---
title: Position loader
permalink: /position_loader/
---

The position loader is used to load positions.
It is one of a number of [loaders]({{site.baseurl}}/loaders) included in Strata.


## Loader

Trades can be loaded using the [`PositionCsvLoader`]({{site.baseurl}}/apidocs/com/opengamma/strata/loader/csv/PositionCsvLoader.html)

```
ResourceLocator locator = ResourceLocator.ofFile(filename);
ValueWithFailures<List<Position>> trades = PositionCsvLoader.load(locator);
```


## Format

The positions file is a CSV-formatted file. Details TODO!


## Example

This example file specifies three positions, a simple security, an ETD future and an ETD option.

```
Strata Position Type, Id Scheme, Id,     Security Id, Quantity, Exchange, Contract Code, Expiry,  Put Call, Exercise Price
SEC,                  OG,        123431, AAPL,        12
FUT,                  OG,        123421, ,            2,        ECAG,     FGBL,          2017-06
OPT,                  OG,        123431, ,            15,       ECAG,     OGBL,          2017-06, P,        5.1
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.
