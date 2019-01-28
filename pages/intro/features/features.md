---
title: Features
permalink: /features/
---

Strata is a high-quality Java library that provides extensible market risk functionality to applications for many use-cases.
Its key features include:

* **Calculation API** for consistent access to the full [product coverage]({{site.baseurl}}/product_coverage),
regardless of asset class or measure.
* **Reporting API** for running trade and cashflow reports, driven by report templates.
* **Scenarios** as a first-class concept, with the ability to describe scenarios declaratively, and apply
perturbations to a set of base market data.
* Ability to plug in **market data sources** to automatically satisfy market data requirements.
* Carefully-designed **trade models**, guided by FpML.
* **Conventions, index definitions, and holiday calendars** built-in for common markets and exchanges.
* **Analytics library** built-in to provide the product coverage.
* **Extensible** in every area.

## Components and extension points

Strata can be divided into a number of major components, each of which has been designed to be highly extensible.
Its built-in coverage relies on all the same extension points as could be used externally to add custom coverage.
The scope of Strata and its extension points are illustrated below.

<img alt="Components and extension points" src="{{site.baseurl}}/images/components.png" />

## Main APIs

Strata provides three main APIs: pricer-level, measure-level and calculation-level.
The APIs differ primarily in the amount of data they can handle.

The pricer-level API provides the ability to calculate one result (risk measure).
The inputs consist of one trade and one set of market data.
Where possible it is recommended to use the measure-level API in preference to the pricer-level API.

The measure-level API provides the ability to calculate one result (risk measure).
The inputs consist of one trade, with methods to handle either one set of market data or many sets (scenarios).

The calculation-level API provides the ability to calculate many results.
The inputs consist of one or more trades, one or more measures and one or more sets of market data (scenarios).
