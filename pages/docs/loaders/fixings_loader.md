---
title: Fixings loader
permalink: /fixings_loader/
---

The fixings loader is used to load historic fixings into the system.
It is one of a number of [loaders]({{site.baseurl}}/loaders) included in Strata.


## Loader

Fixings can be loaded using the [`FixingSeriesCsvLoader`]({{site.baseurl}}/apidocs/com/opengamma/strata/loader/csv/FixingSeriesCsvLoader.html)

```
ResourceLocator locator = ResourceLocator.ofFile(filename);
Map<ObservableId, LocalDateDoubleTimeSeries> fixings = FixingSeriesCsvLoader.load(locator);
```


## Format

The fixings file is a simple CSV-formatted file with the following header row:

```
Reference,Date,Value
```

The columns may be specified in any order, however this is the recommended order.
The meaning of each column is as follows:

| Column name    | Description                                                                          |
|----------------|--------------------------------------------------------------------------------------|
| Reference      | The name of the index that the data is for, such as "USD-LIBOR-3M", see [floating indices]({{site.baseurl}}/indices/) |
| Date           | The date of the fixing, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Value          | The numeric value of the fixing                                                      |

To load a full time-series will require many rows in the file, one for each historic fixing date.
Each fixing series must be contained within a single CSV file, but a single file may contain multiple series.

See the [indices]({{site.baseurl}}/indices) page for Strata's default index names.


## Example

This example file specifies fixings for a single index on five dates.

```
Reference,    Date,       Value
USD-LIBOR-3M, 2015-07-20, 0.00503
USD-LIBOR-3M, 2015-07-21, 0.00504
USD-LIBOR-3M, 2015-07-22, 0.00502
USD-LIBOR-3M, 2015-07-23, 0.00503
USD-LIBOR-3M, 2015-07-24, 0.00506
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.
