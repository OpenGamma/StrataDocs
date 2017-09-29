---
title: Curve groups file
permalink: /curve_groups_file/
---

The curve groups CSV file is used to define a curve group when loading curves into the system.
It is used by the [curve loader]({{site.baseurl}}/curves_loader).

A curve group is used to assign a purpose to a coherent set of curves.
For example, a group might contain three curves, one for USD discounting, one for the USD Fed Fund index
and one for the USD LIBOR 3 month index.
Alternatively, the group might contain one curve used for all three purposes.


## Format

The curve groups file is a simple CSV-formatted file with the following header row:

```
Group Name,Curve Type,Reference,Curve Name
```

The columns may be specified in any order, however this is the recommended order.
The meaning of each column is as follows:

| Column name | Description                                                                                    |
|-------------|------------------------------------------------------------------------------------------------|
| Group Name  | The name of the curve group                                                                    |
| Curve Type  | The type of curve, "Discount" for a discounting curve, or "Forward" for a forward curve        |
| Reference   | The reference for which the curve is used, such as the currency or index                       |
| Curve Name  | The name of the curve                                                                          |

A discount curve must have a 3 letter ISO currency code as the reference, such as "USD".
A forward curve must have an index as the reference, such as "USD-LIBOR-3M".
See the [indices]({{site.baseurl}}/indices) page for Strata's default index names.

The groups file refers to curve names that are defined in the [curve settings]({{site.baseurl}}/curve_settings_file) file.


## Example

This example file specifies a single group, "USD-DSCON-LIBOR3M", with two curves, "USD-Disc" and "USD-3ML".
The "USD-Disc" curve is used as both a USD discounting curve and as a Fed Fund forward curve.
The "USD-3ML" curve is only used as a forward curve for 3-month USD LIBOR.

```
Group Name,        Curve Type, Reference,    Curve Name
USD-DSCON-LIBOR3M, Discount,   USD,          USD-Disc
USD-DSCON-LIBOR3M, Forward,    USD-FED-FUND, USD-Disc
USD-DSCON-LIBOR3M, Forward,    USD-LIBOR-3M, USD-3ML
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.
