---
title: Curve sensitivity loader
permalink: /sensitivity_loader/
---

The sensitivity loader is used to load curve sensitivities.
It is one of a number of [loaders]({{site.baseurl}}/loaders) included in Strata.


## Loader

Sensitivites can be loaded using the
[`SensitivityCsvLoader`]({{site.baseurl}}/apidocs/com/opengamma/strata/loader/csv/SensitivityCsvLoader.html)

```
ResourceLocator locator = ResourceLocator.ofFile(filename);
ValueWithFailures<ListMultimap<String, CurveSensitivities>> trades = 
  SensitivityCsvLoader.standard().load(ImmutableList.of(locator));
```


## Format

The sensitivity file is a CSV-formatted file.
The columns may be specified in any order.
The parser supports three ways to represent sensitivities - standard format, list format and grid format.
All formats can represent the same data, just using different rows and columns.

Curve sensitivities are expressed using three orthoginal concepts:

* Sensitivity type - the meaning of the value, such as "ZeroRateDelta" or "ZeroRateGamma"
* Reference - the purpose of the curve, what it represents, such as "GBP-SONIA"
* Sensitivity tenor - the tenor of a point on the curve, such as "3M"

The reference can be one of four different things:

* a currency, such as "GBP" - a reference to the discount curve in that currency
* a floating rate name, such as "GBP-LIBOR" - a reference to the forward curve for all GBP LIBOR indices
* a floating rate index, such as "GBP-LIBOR-3M" - a reference to the forward curve for a single index
* a curve name, any arbitrary string that cannot be interpreted as one of the above

The tenors can be defined in terms of days, weeks, months and years.
They typically range from 1D (1 day) to 60Y (60 years).
Tenors cannot mix day-based and month/year-based values, thus 1M10D is not valid.

There is no standard set of tenors. We recommend the following as a good starting point for the tenors to provide.
We would advise against providing more tenors than this, and it is usually fine to provide fewer:

`1D, 1W, 2W, 1M, 2M, 3M, 4M, 5M, 6M, 9M, 12M, 15M, 18M, 21M, 2Y, 3Y, 4Y, 5Y, 6Y, 7Y, 8Y, 9Y, 10Y, 12Y, 15Y, 20Y, 25Y, 30Y, 35Y, 40Y, 45Y, 50Y, 55Y, 60Y`


Note that the resulting `CurveSensitivities` instance will treat all references as curve names.
It is up to the code that uses the sensitivities to interpret them according to the table above.


### Standard format

The standard format uses a fixed set of columns.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Id Scheme             | Optional    | The scheme (symbology) within which the sensitivity identifier is unique, default "OG-Sensitivity". |
| Id                    | Optional    | The sensitivity identifier. |
| Reference             | Mandatory   | The reference, as described above. |
| Sensitivity Type      | Mandatory   | The sensitivity type, as described above. |
| Sensitivity Tenor     | Mandatory   | The tenor of the bucketed sensitivity, such as "3M". |
| Sensitivity Date      | Optional    | The date of the bucketed sensitivity, such as "2018-06-01". |
| Currency              | Optional    | The currency of each sensitivity value, such as "GBP". If omitted, the currency will be implied from the reference, which must start with the currency. |
| Value                 | Mandatory   | The sensitivity value. |


#### Example

This example file specifies two types of sensitivity ("ZeroRateDelta" and "ZeroRateGamma") for two references ("GBP" and "GBP-LIBOR").
Thus there are four distinct sets of sensitivities.
The currency of "GBP" is implied from the reference.
The identifier and date columns are not used (and are rarely used in general).

The parsing result will consist of a `ListMultimap<String, CurveSensitivities>` with one entry keyed by the identifier (an empty string).
The single `CurveSensitivities` will have two `CurrencyParameterSensitivities` entries, one for "ZeroRateDelta" and one for "ZeroRateGamma".
Each `CurrencyParameterSensitivities` instance will have two `CurrencyParameterSensitivity` entries, one for "GBP" and one for "GBP-LIBOR".

```
Reference, Sensitivity Type, Sensitivity Tenor, Value
GBP,       ZeroRateDelta,    1M,                2
GBP,       ZeroRateDelta,    3M,                3
GBP,       ZeroRateDelta,    6M,                4
GBP,       ZeroRateDelta,    1Y,                5
GBP,       ZeroRateDelta,    2Y,                3
GBP,       ZeroRateDelta,    5Y,                -2
GBP,       ZeroRateGamma,    1M,                0.2
GBP,       ZeroRateGamma,    3M,                0.3
GBP,       ZeroRateGamma,    6M,                0.4
GBP,       ZeroRateGamma,    1Y,                0.5
GBP,       ZeroRateGamma,    2Y,                0.3
GBP,       ZeroRateGamma,    5Y,                -0.2
GBP-LIBOR, ZeroRateDelta,    1M,                4
GBP-LIBOR, ZeroRateDelta,    3M,                5
GBP-LIBOR, ZeroRateDelta,    6M,                6
GBP-LIBOR, ZeroRateDelta,    1Y,                7
GBP-LIBOR, ZeroRateDelta,    2Y,                4
GBP-LIBOR, ZeroRateDelta,    5Y,                2
GBP-LIBOR, ZeroRateGamma,    1M,                0.4
GBP-LIBOR, ZeroRateGamma,    3M,                0.5
GBP-LIBOR, ZeroRateGamma,    6M,                0.6
GBP-LIBOR, ZeroRateGamma,    1Y,                0.7
GBP-LIBOR, ZeroRateGamma,    2Y,                0.4
GBP-LIBOR, ZeroRateGamma,    5Y,                0.2
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


### List format

The list format uses flexible columns for sensitivity types.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Id Scheme             | Optional    | The scheme (symbology) within which the sensitivity identifier is unique, default "OG-Sensitivity". |
| Id                    | Optional    | The sensitivity identifier. |
| Reference             | Mandatory   | The reference, as described above |
| Sensitivity Tenor     | Mandatory   | The tenor of the bucketed sensitivity, such as "3M". |
| Sensitivity Date      | Optional    | The date of the bucketed sensitivity, such as "2018-06-01". |
| Currency              | Optional    | The currency of each sensitivity value, such as "GBP". If omitted, the currency will be implied from the reference, which must start with the currency. |
| ZeroRateDelta         | Example*    | The sensitivity values where the header is the sensitivity type, as described above. |
| ZeroRateGamma         | Example*    | The sensitivity values where the header is the sensitivity type, as described above. |

* The file format has one to many flexible columns of sensitivity values.
The table above shows columns for "ZeroRateDelta" and "ZeroRateGamma", but these are not required and other sensitivity types may be used instead.

#### Example

This example file specifies two types of sensitivity ("ZeroRateDelta" and "ZeroRateGamma") for two references ("GBP" and "GBP-LIBOR").
Thus there are four distinct sets of sensitivities.
The currency of "GBP" is implied from the reference.
The identifier and date columns are not used (and are rarely used in general).

The parsing result will consist of a `ListMultimap<String, CurveSensitivities>` with one entry keyed by the identifier (an empty string).
The single `CurveSensitivities` will have two `CurrencyParameterSensitivities` entries, one for "ZeroRateDelta" and one for "ZeroRateGamma".
Each `CurrencyParameterSensitivities` instance will have two `CurrencyParameterSensitivity` entries, one for "GBP" and one for "GBP-LIBOR".

```
Reference, Sensitivity Tenor, ZeroRateDelta, ZeroRateGamma
GBP,       1M,                2,             0.2
GBP,       3M,                3,             0.3
GBP,       6M,                4,             0.4
GBP,       1Y,                5,             0.5
GBP,       2Y,                3,             0.3
GBP,       5Y,                -2,            -0.2
GBP-LIBOR, 1M,                4,             0.4
GBP-LIBOR, 3M,                5,             0.5
GBP-LIBOR, 6M,                6,             0.6
GBP-LIBOR, 1Y,                7,             0.7
GBP-LIBOR, 2Y,                4,             0.4
GBP-LIBOR, 5Y,                2,             0.2
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.

Note that the actual data represented by this example file is identical to that in the standard format example above.
The main difference is that the list format has fewer rows.


### Grid format

The grid format uses flexible columns for references.

| Column name           | Mandatory?  | Description |
|-----------------------|-------------|-------------|
| Id Scheme             | Optional    | The scheme (symbology) within which the sensitivity identifier is unique, default "OG-Sensitivity" |
| Id                    | Optional    | The sensitivity identifier |
| Sensitivity Type      | Mandatory   | The sensitivity type, as described above |
| Sensitivity Tenor     | Mandatory   | The tenor of the bucketed sensitivity, such as "1Y" |
| Sensitivity Date      | Optional    | The date of the bucketed sensitivity, such as "2018-06-01" |
| Currency              | Optional    | The currency of each sensitivity value, such as "GBP". If omitted, the currency will be implied from the reference, which must start with the currency. |
| GBP                   | Example*    | The sensitivity values where the header is the reference, as described above. |
| GBP-LIBOR             | Example*    | The sensitivity values where the header is the reference, as described above. |

* The file format has one to many flexible columns of sensitivity values.
The table above shows columns for "GBP" and "GBP-LIBOR", but these are not required and other references may be used instead.

#### Example

This example file specifies two types of sensitivity ("ZeroRateDelta" and "ZeroRateGamma") for two references ("GBP" and "GBP-LIBOR").
Thus there are four distinct sets of sensitivities.
The currency of "GBP" is implied from the reference and the identifier is not used.

The parsing result will consist of a `ListMultimap<String, CurveSensitivities>` with one entry keyed by the identifier (an empty string).
The single `CurveSensitivities` will have two `CurrencyParameterSensitivities` entries, one for "ZeroRateDelta" and one for "ZeroRateGamma".
Each `CurrencyParameterSensitivities` instance will have two `CurrencyParameterSensitivity` entries, one for "GBP" and one for "GBP-LIBOR".

Note that the actual data represented by this example file is identical to that in the list format example above.
The main difference is that the grid format will have fewer rows than the list format if only specifying delta sensitivity.

```
Sensitivity Type, Sensitivity Tenor, GBP,  GBP-LIBOR
ZeroRateDelta,    1M,                2,    4
ZeroRateDelta,    3M,                3,    5
ZeroRateDelta,    6M,                4,    6
ZeroRateDelta,    1Y,                5,    7
ZeroRateDelta,    2Y,                3,    4
ZeroRateDelta,    5Y,                -2,   2
ZeroRateGamma,    1M,                0.2,  0.4
ZeroRateGamma,    3M,                0.3,  0.5
ZeroRateGamma,    6M,                0.4,  0.6
ZeroRateGamma,    1Y,                0.5,  0.7
ZeroRateGamma,    2Y,                0.3,  0.4
ZeroRateGamma,    5Y,                -0.2, 0.2
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.
