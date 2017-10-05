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


## <a name="Format">Format</a>

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify positions in various ways.


### Example

This example file specifies three positions, a simple security, an ETD future and an ETD option.

```
Strata Position Type, Id Scheme, Id,     Security Id, Quantity, Exchange, Contract Code, Expiry,  Put Call, Exercise Price
SEC,                  OG,        123431, AAPL,        12
FUT,                  OG,        123421, ,            2,        ECAG,     FGBL,          2017-06
OPT,                  OG,        123431, ,            15,       ECAG,     OGBL,          2017-06, P,        5.12
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


### Standard securities

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Position Type  | Mandatory   | The type of the position, "SEC"/"Security" |
| Security Id Scheme    | Optional    | The scheme (symbology) within which the security identifier is unique, default "OG-Security" |
| Security Id           | Mandatory   | The security identifier |
| Quantity              | Conditional | The quantity purchased (positive) or sold (negative) |
| Long Quantity         | Conditional | The long quantity (positive) |
| Short Quantity        | Conditional | The short quantity (positive) |

Valid combinations of conditional fields are as follows (other combinations are not allowed):

* "Quantity"
* "Long Quantity"
* "Short Quantity"
* "Long Quantity" and "Short Quantity"


### ETD futures

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Position Type  | Mandatory   | The type of the position, "FUT"/"Future" |
| Exchange              | Mandatory   | The exchange code, which should be a MIC code |
| Contract Code         | Mandatory   | The contract code, which should be the code defined by the exchange |
| Expiry                | Mandatory   | The year-month of the expiry, such as '2017-09', see [accepted formats]({{site.baseurl}}/common_formats/) |
| Expiry Week           | Optional    | The week number for weekly-expiring futures |
| Expiry Day            | Optional    | The day-of-month for daily-expiring or flex futures |
| Settlement Type       | Optional    | The settlement type for flex futures, see [`EtdSettlementType`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/etd/EtdSettlementType.html) |
| Quantity              | Conditional | The quantity purchased (positive) or sold (negative) |
| Long Quantity         | Conditional | The long quantity (positive) |
| Short Quantity        | Conditional | The short quantity (positive) |

Valid combinations of conditional quantity fields are as follows (other combinations are not allowed):

* "Quantity"
* "Long Quantity"
* "Short Quantity"
* "Long Quantity" and "Short Quantity"


### ETD options

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Strata Position Type  | Mandatory   | The type of the position, "OPT"/"Option" |
| Exchange              | Mandatory   | The exchange code, which should be a MIC code |
| Contract Code         | Mandatory   | The contract code, which should be the code defined by the exchange |
| Expiry                | Mandatory   | The year-month of the expiry, such as '2017-09', see [accepted formats]({{site.baseurl}}/common_formats/) |
| Expiry Week           | Optional    | The week number for weekly-expiring futures |
| Expiry Day            | Optional    | The day-of-month for daily-expiring or flex futures |
| Settlement Type       | Optional    | The settlement type for flex futures, see [`EtdSettlementType`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/etd/EtdSettlementType.html) |
| Exercise Style        | Optional    | The exercise style for flex options, see [`EtdOptionType`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/etd/EtdOptionType.html) |
| Version               | Optional    | The version of the option, defaults to zero |
| Put Call              | Mandatory   | The Put/Call flag, which must be "Put", "P", "Call" or "C", case insensitive |
| Exercise Price        | Mandatory   | The exercise price |
| Quantity              | Conditional | The quantity purchased (positive) or sold (negative) |
| Long Quantity         | Conditional | The long quantity (positive) |
| Short Quantity        | Conditional | The short quantity (positive) |

Valid combinations of conditional fields are as follows (other combinations are not allowed):

* "Quantity"
* "Long Quantity"
* "Short Quantity"
* "Long Quantity" and "Short Quantity"


### Determining the type dynamically

In the formats above, "Strata Position Type" is defined as being mandatory.
In fact, it is possible to omit the column and let the parser determine it automatically.
To do this, it examines the presence or absence of the "Expiry" and "Put Call" columns.
