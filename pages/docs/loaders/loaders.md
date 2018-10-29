---
title: Loaders
permalink: /loaders/
---

Strata provides a number of loaders that can be used to load data into the system.


## CSV loaders

The following loaders are defined using CSV as the basic file format:

* [Trades]({{site.baseurl}}/trade_loader) - trades (FRA, Swap)
* [Positions]({{site.baseurl}}/position_loader) - positions (ETD)
* [Sensitivities]({{site.baseurl}}/sensitivity_loader) - curve sensitivities
* [Quotes]({{site.baseurl}}/quotes_loader) - observable market data
* [FX rates]({{site.baseurl}}/fx_rates_loader) - market data for FX
* [Fixings]({{site.baseurl}}/fixings_loader) - historical time-series
* [Curves]({{site.baseurl}}/curves_loader) - pre-calibrated curves
* [Curve calibration]({{site.baseurl}}/curve_calibration_loader) - defines a curve to be calibrated


## XML loaders

The following loaders are defined using XML as the basic file format:

* [Trades]({{site.baseurl}}/fpml_loader) - FpML format trades
