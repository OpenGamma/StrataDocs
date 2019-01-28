---
title: Reference documentation
permalink: /docs/
---

{% include macros.html %}

This is the home page for reference documentation about Strata, the open source market risk library from OpenGamma.

## Concepts

The following documentation introduces the core concepts of the system:

* [Calculation Flow]({{site.baseurl}}/calculation_flow)
* [Market Data]({{site.baseurl}}/market_data)
* [Reference Data]({{site.baseurl}}/reference_data)
* [Product Model]({{site.baseurl}}/product_model)


## Modules

The Strata codebase consists of a number of modules.
Detailed reference documentation on each module will expand over time.

Full documentation of the API is available in the [Javadoc]({{site.baseurl}}/apidocs/).
Note that any package with `impl` in the name is considered to be an implementation detail.


### Collect module

The `strata-collect` module provides a standard library for collections and utilities to support the rest of Strata.
The module builds on [Guava](https://github.com/google/guava), Google's high quality library of Java essentials.

The collect module adds features in a number of areas:

* [Extended enums]({{site.baseurl}}/extended_enum) - provides support for `enum`-like data structures that are loaded at startup
* Functions - additional Java SE 8 functional interfaces
* Ranges - ranges of values
* Result - functional result model
* Time-Series - a series of values over time
* Tuple - pair and triple
* Validate - general utility classes


### Basics module

The `strata-basics` module provides basic concepts used in finance, primarily in the area of
[reference data]({{site.baseurl}}/reference_data).
For more information, see the following guides:

* [Holidays]({{site.baseurl}}/holidays) - to determine if a date is a working day or a holiday
* [Date adjustments]({{site.baseurl}}/date_adjustments) - adjusting dates relative to holidays
* [Schedules]({{site.baseurl}}/schedules) - building periodic schedules
* [Value adjustments]({{site.baseurl}}/value_adjustments) - adjusting values relative to a schedule
* [Day counts]({{site.baseurl}}/day_counts) - converting date-based periods to numeric year fractions


### Product module

The `strata-product` module contains the [main domain model]({{site.baseurl}}/product_model),
defining instruments such as interest rate swaps, FRAs and futures.
For more information, see the following guides:

* [Swap]({{site.baseurl}}/swap) - Swaps (Fixed, Ibor, Overnight, Inflation)
* [FRA]({{site.baseurl}}/fra) - Forward Rate Agreements
* [Swaption]({{site.baseurl}}/swaption) - Options on swaps
* [FX Forward/Spot]({{site.baseurl}}/fx_single) - FX Forward and FX spot
* [FX Swap]({{site.baseurl}}/fx_swap) - FX Swap
* [FX Vanilla Option]({{site.baseurl}}/fx_vanilla_option) - FX Vanilla Option
* [Term Deposit]({{site.baseurl}}/term_deposit) - Fixed rate deposits
* [Bullet Payment]({{site.baseurl}}/bullet_payment) - Unidirectional one-off payments
* See also the [product coverage]({{site.baseurl}}/product_coverage) page


### Data module

The `strata-data` module provides [market data]({{site.baseurl}}/market_data) containers.
Both single-scenario and multi-scenario containers are available.


### Market module

The `strata-market` module includes the representations of the market, including curves and surfaces.


### Loader module

The `strata-loader` module provides the ability to [load]({{site.baseurl}}/loaders)
products and market data from files.
This includes an FpML loader for products.


### Pricer module

The `strata-pricer` module provides standard analytics for pricing and risk calculations on financial instruments.
This depends on the `strata-math` module, which is intended to be an implementation detail.


### Calculation module

The `strata-calc` module provides a [calculation runner]({{site.baseurl}}/calculation_flow)
capable of calculating risk analytics.
Given a list of trades and some configuration parameters, it will determine what market data is needed,
obtain it from a source, perform any necessary calibration, and calculate the desired results.


### Measure module

The `strata-measure` module enables applications to calculate high-level measures, such as PV and PV01.
Access is provided directly and via the Calculation API of `strata-calc`.


### Report module

The `strata-report` module provides a small framework for reporting on the results of calculations.
A tool provides the ability to use a report template to drive the calculations necessary to produce a simple report.
