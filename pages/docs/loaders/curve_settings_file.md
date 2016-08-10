---
title: Curve settings file
permalink: /curve_settings_file/
---

The curve settings CSV file is used to control curve-wide settings when loading curves into the system.
It is used by the [curve loader]({{site.baseurl}}/curves_loader) and 
[curve calibration loader]({{site.baseurl}}/curve_calibration_loader).


## Format

The curve settings file is a simple CSV-formatted file with the following header row:

```
Curve Name,Value Type,Day Count,Interpolator,Left Extrapolator,Right Extrapolator
```

The columns may be specified in any order, however this is the recommended order.
The meaning of each column is as follows:

| Field              | Description                                                                                   |
|--------------------|-----------------------------------------------------------------------------------------------|
| Curve Name         | The name of the curve.                                                                        |
| Value Type         | The type of value in the curve, "Zero" for zero rates or "DF" for discount factors            |
| Day Count          | The day count to use for dates in the curve.                                                  |
| Interpolator       | The name of the interpolator, used when querying a value between two nodes on the curve.      |
| Left Extrapolator  | The name of the left extrapolator, used when querying before the earliest point on the curve. |
| Right Extrapolator | The name of the right extrapolator, used when querying after the latest point on the curve.   |

See [DayCounts]({{site.baseurl}}/day_counts) for valid day count names.
See [CurveInterpolators]({{site.baseurl}}/apidocs/com/opengamma/strata/market/curve/interpolator/CurveInterpolators.html) for valid interpolator names.
See [CurveExtrapolators]({{site.baseurl}}/apidocs/com/opengamma/strata/market/curve/interpolator/CurveExtrapolators.html) for valid extrapolator names.

These settings are used when loading individual curve nodes via the ({{site.baseurl}}/curves_loader) or [curve calibration loader]({{site.baseurl}}/curve_calibration_loader).


## Example

This example file specifies the settings for two curves.

```
Curve Name, Value Type, Day Count, Interpolator, Left Extrapolator, Right Extrapolator
USD-Disc,   Zero,       Act/365F,  Linear,       Flat,              Flat
USD-3ML,    Zero,       Act/365F,  Linear,       Flat,              Flat
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.
