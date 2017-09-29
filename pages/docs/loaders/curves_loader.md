---
title: Curves loader
permalink: /curves_loader/
---

The curves loader is used to load pre-calibrated curves into the system.
It is one of a number of [loaders]({{site.baseurl}}/loaders) included in Strata.


## Loader

Curves can be loaded using the [`RatesCurvesCsvLoader`]({{site.baseurl}}/apidocs/com/opengamma/strata/loader/csv/RatesCurvesCsvLoader.html)

```
ResourceLocator groupsLocator = ResourceLocator.ofFile(groupsFilename);
ResourceLocator settingsLocator = ResourceLocator.ofFile(settingsFilename);
ResourceLocator curvesLocator = ResourceLocator.ofFile(curvesFilename);
List<CurveGroup> curves = RatesCurvesCsvLoader.load(
    valuationDate, groupsLocator, settingsLocator, ImmutableList.of(curvesLocator));
```

Curves must be loaded as part of a group, that specifies a purpose for the curve, such as whether it is
a discount or forward curve. See the [curve groups]({{site.baseurl}}/curve_groups_file) file for more details.

Settings that are shared across all the nodes in a curve are defined in the
[curve settings]({{site.baseurl}}/curve_settings_file) file.


## Format

The curves file is a simple CSV-formatted file with the following header row:

```
Valuation Date,Curve Name,Date,Value,Label
```

The columns may be specified in any order, however this is the recommended order.
The meaning of each column is as follows:

| Column name    | Description                                                                          |
|----------------|--------------------------------------------------------------------------------------|
| Valuation Date | The valuation date that the curve was calibrated for, see [accepted formats]({{site.baseurl}}/common_formats/) |
| Curve Name     | The name of the curve                                                                |
| Date           | The date of the curve node, see [accepted formats]({{site.baseurl}}/common_formats/) |
| Value          | The value associated with the curve node                                             |
| Label          | A description of the node, used to identify it in bucketed sensitivity results       |

A single curve will consist of at least two nodes, and typically many more, with one row required for each node.
Each curve must be contained within a single CSV file, but a single file may contain multiple curves.


## Example

This example file specifies one curve.

```
Valuation Date, Curve Name, Date,       Value,       Label
2014-01-22,     USD-Disc,   2014-01-23, 0.001571524, 0D
2014-01-22,     USD-Disc,   2014-02-24, 0.000934099, 1M
2014-01-22,     USD-Disc,   2014-03-24, 0.000948444, 2M
2014-01-22,     USD-Disc,   2014-04-24, 0.000935866, 3M
2014-01-22,     USD-Disc,   2014-07-24, 0.001027672, 6M
2014-01-22,     USD-Disc,   2014-10-24, 0.001280398, 9M
2014-01-22,     USD-Disc,   2015-01-26, 0.001841773, 1Y
2014-01-22,     USD-Disc,   2016-01-25, 0.005475661, 2Y
2014-01-22,     USD-Disc,   2017-01-24, 0.009655095, 3Y
2014-01-22,     USD-Disc,   2018-01-24, 0.013191876, 4Y
2014-01-22,     USD-Disc,   2019-01-24, 0.015783922, 5Y
2014-01-22,     USD-Disc,   2020-01-24, 0.017845475, 6Y
2014-01-22,     USD-Disc,   2021-01-25, 0.019539006, 7Y
2014-01-22,     USD-Disc,   2022-01-24, 0.02095814,  8Y
2014-01-22,     USD-Disc,   2023-01-24, 0.02217629,  9Y
2014-01-22,     USD-Disc,   2024-01-24, 0.023239034, 10Y
2014-01-22,     USD-Disc,   2026-01-26, 0.02501226,  12Y
2014-01-22,     USD-Disc,   2029-01-24, 0.026896017, 15Y
2014-01-22,     USD-Disc,   2034-01-24, 0.028543824, 20Y
2014-01-22,     USD-Disc,   2039-01-24, 0.029327868, 25Y
2014-01-22,     USD-Disc,   2044-01-25, 0.029693673, 30Y
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.
