---
title: Quotes loader
permalink: /quotes_loader/
---

The quotes loader is used to load observable market data quotes into the system.
It is one of a number of [loaders]({{site.baseurl}}/loaders) included in Strata.


## Loader

Quotes can be loaded using the [`QuotesCsvLoader`]({{site.baseurl}}/apidocs/com/opengamma/strata/loader/csv/QuotesCsvLoader.html)

```
ResourceLocator locator = ResourceLocator.ofFile(filename);
Map<QuoteId, Double> quotes = QuotesCsvLoader.load(valuationDate, locator);
```


## Format

The quotes file is a simple CSV-formatted file with the following header row:

```
Valuation Date,Symbology,Ticker,Field Name,Value
```

The columns may be specified in any order, however this is the recommended order.
The meaning of each column is as follows:

| Column name    | Description                                                                          |
|----------------|--------------------------------------------------------------------------------------|
| Valuation Date | The valuation date to which the quote value corresponds, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Symbology      | The symbology of the quote identifier                                                |
| Ticker         | The ticker of the quote, unique within the symbology                                 |
| Field Name     | The field name. The most common are "MarketValue" and "SettlementPrice"              |
| Value          | The numeric quote value                                                              |

The symbology-ticker pair are used to uniquely identify the market data item, such as a security.
The symbology will typically be an industry standard such as ISINs, or one defined by a vendor such as Bloomberg or Reuters.
For example, the entry for Apple equity might have a symbology of "Bloomberg" and a ticker of "AAPL US Equity",
whereas an alternative might be to use ISINs, with a symbology of "ISIN" and a ticker of "US0378331005".
Note that Strata does not mandate any specific names for the symbology or ticker,
although symbologies starting with "OG-" are used in examples.

The field name is used to specify a specific field that is available for the market data item.
Any field name may be used, however two names are most commonly used as they are recognised by Strata:

* `MarketValue` - the standard market quote for the identifier
* `SettlementPrice` - the daily settlement price used in margining

See [`FieldName`]({{site.baseurl}}/apidocs/com/opengamma/strata/data/FieldName.html) for more details.


## Example

This example file specifies three items of market data on two different dates.

```
Valuation Date, Symbology, Ticker,       Field Name,  Value
2015-07-21,     OG-Ticker, USD-IRS3M-2Y, MarketValue, 0.00503
2015-07-21,     OG-Ticker, USD-IRS3M-3Y, MarketValue, 0.0093915
2015-07-21,     OG-Ticker, USD-IRS3M-4Y, MarketValue, 0.013808
2015-07-22,     OG-Ticker, USD-IRS3M-2Y, MarketValue, 0.00509
2015-07-22,     OG-Ticker, USD-IRS3M-3Y, MarketValue, 0.0093921
2015-07-22,     OG-Ticker, USD-IRS3M-4Y, MarketValue, 0.013810
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.
