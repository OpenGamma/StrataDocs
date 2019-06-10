---
title: FX Swap
permalink: /fx_swap/
---

{% include macros.html %}

An FX Swap is a financial instrument that represents the exchange of an equivalent amount
in two different currencies between counterparties on two different dates.

For example, an FX swap might represent the payment of USD 1,000 and the receipt of EUR 932
on the *near* date, and the payment of EUR 941 and the receipt of USD 1,000 on the *far* date.


## Key classes

An FX Swap is represented in Strata using the [`FxSwap`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fx/FxSwap.html) class.
The `FxSwap` class stores details of the product that was agreed.
The trade details are stored in [`FxSwapTrade`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fx/FxSwapTrade.html) class.

An `FxSwap` can be created as follows:

```java
FxSwap fx = FxSwap.ofForwardPoints(CurrencyAmount.of(Currency.USD, 1000),  // amount
                                   EUR                                     // other currency
                                   0.932,                                  // FX rate at near date
                                   0.009,                                  // forward points
                                   LocalDate.of(2015, 6, 15),              // near date
                                   LocalDate.of(2015, 9, 15));             // far date
```

{{tip}}The strata-loader project provides the ability to load an FX Swap
from [FpML]({{site.baseurl}}/fpml_loader) and [CSV]({{site.baseurl}}/trade_loader_fx_swap).{{end}}


## Risk measures

The `strata-measure` module provides high-level risk measures for FX Swaps.
The main entry point is
[`FxSwapTradeCalculations`]({{site.baseurl}}/apidocs/com/opengamma/strata/measure/fx/FxSwapTradeCalculations.html).

The following measures are available:

* present value, and associated sensitivity
* par spread
* currency exposure
* current cash

These measures are also available using the calculation API.

The `strata-pricer` module provides lower-level pricing support for FX Swaps:

* `DiscountingFxSwapTradePricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/fx/DiscountingFxSwapTradePricer.html).
* `DiscountingFxSwapProductPricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/fx/DiscountingFxSwapProductPricer.html).


## Product model

The following table summarizes the fields on `FxSwap` that can be used to control the product.
For more detail on the meaning of each field, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fx/FxSwap.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| nearLeg           | The [FxSingle]({{site.baseurl}}/fx_single) near leg | Required |
| farLeg            | The [FxSingle]({{site.baseurl}}/fx_single) far leg | Required |
