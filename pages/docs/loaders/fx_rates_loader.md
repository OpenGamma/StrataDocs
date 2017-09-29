---
title: FX rates loader
permalink: /fx_rates_loader/
---

The FX rates loader is used to load FX rates into the system.
It is one of a number of [loaders]({{site.baseurl}}/loaders) included in Strata.


## Loader

FX rates can be loaded using the [`FxRatesCsvLoader`]({{site.baseurl}}/apidocs/com/opengamma/strata/loader/csv/FxRatesCsvLoader.html)

```
ResourceLocator locator = ResourceLocator.ofFile(filename);
Map<FxRateId, FxRate> fxRates = FxRatesCsvLoader.load(valuationDate, locator);
```


## Format

The FX rates file is a simple CSV-formatted file with the following header row:

```
Valuation Date,Currency Pair,Value
```

The columns may be specified in any order, however this is the recommended order.
The meaning of each column is as follows:

| Column name    | Description                                                                          |
|----------------|--------------------------------------------------------------------------------------|
| Valuation Date | The valuation date to which the rate corresponds, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Currency Pair  | The currency pair, in the format "EUR/USD"                                           |
| Value          | The numeric FX rate                                                                  |


## Example

This example file specifies two FX rates on two different dates.

```
Valuation Date, Currency Pair, Value
2016-01-22,     EUR/USD,       1.11
2016-01-22,     GBP/USD,       1.31
2016-01-23,     EUR/USD,       1.12
2016-01-23,     GBP/USD,       1.32
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.
