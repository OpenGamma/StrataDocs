---
title: FX Forward and FX Spot
permalink: /fx_single/
---

{% include macros.html %}

An FX Forward is a financial instrument that represents the exchange of an equivalent amount
in two different currencies between counterparties on a specific date in the future.
An FX spot is a similar instrument where the payment date is the spot date.
These two instruments are referred to as *FX Single* by Strata.

For example, an FX Single might represent the payment of USD 1,000 and the receipt of EUR 932
on a specific date.


## Key classes

An FX Single is represented in Strata using the [`FxSingle`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fx/FxSingle.html) class.
The `FxSingle` class stores details of the product that was agreed.
The trade details are stored in [`FxSingleTrade`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fx/FxSingleTrade.html) class.

An `FxSingle` can be created as follows:

```java
FxSingle fx = FxSingle.of(CurrencyAmount.of(Currency.USD, 1000),
                          FxRate.of(EUR, USD, 1.115),
                          LocalDate.of(2015, 6, 15));
```

> **TIP:** The strata-loader project provides the ability to load an FX Single
from [FpML]({{site.baseurl}}/fpml_loader) and [CSV]({{site.baseurl}}/trade_loader_fx_single).


## Risk measures

The `strata-measure` module provides high-level risk measures for FX Singles.
The main entry point is
[`FxSingleTradeCalculations`]({{site.baseurl}}/apidocs/com/opengamma/strata/measure/fx/FxSingleTradeCalculations.html).

The following measures are available:

* present value, and associated sensitivity
* par spread
* currency exposure
* current cash
* forward FX rate, and associated point/spot sensitivity

These measures are also available using the calculation API.

The `strata-pricer` module provides lower-level pricing support for FX Singles:

* `DiscountingFxSingleTradePricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/fx/DiscountingFxSingleTradePricer.html).
* `DiscountingFxSingleProductPricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/fx/DiscountingFxSingleProductPricer.html).

## Product model

The following table summarizes the fields on `FxSingle` that can be used to control the product.
For more detail on the meaning of each field, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fx/FxSingle.html);

| Property name         | Description | Required/Optional |
|-----------------------|-------------|-------------------|
| baseCurrencyAmount    | The amount in the base currency | Required |
| counterCurrencyAmount | The amount in the counter currency | Required |
| paymentDate           | The payment date | Required |
