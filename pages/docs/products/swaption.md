---
title: Swaption
permalink: /swaption/
---

{% include macros.html %}

A swaption is a financial instrument that provides an option based on the future value of an interest rate swap.
The option is European, exercised only on the exercise date.

A *physical delivery swaption* is such that an actual interest rate swap is entered into if the option is exercised.
On the other hand, a *cash settled swaption* settles cash amount computed based on the future value if the option is exercised.


## Key classes

A swaption is represented in Strata using the [`Swaption`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swaption/Swaption.html) class.
The `Swaption` class stores details of the product that was agreed.
The trade details are stored in [`SwaptionTrade`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swaption/SwaptionTrade.html) class.

A `Swaption` can be created using a builder as follows:

```java
Swaption swaption = Swaption.builder()
  .expiryDate(AdjustableDate.of(LocalDate.of(2014, 6, 14), BusinessDayAdjustment.of(FOLLOWING, USNY)))
  .expiryTime(LocalTime.of(10, 0))
  .expiryZone(ZoneId.of("Z"))
  .longShort(LongShort.LONG)
  .swaptionSettlement(PhysicalSettlement.DEFAULT)
  .underlying(SWAP)
  .build();
```

where the expiry date is specified in terms of `AdjustableDate` with a suitable `BusinessDayAdjustment`, and `SWAP` represents the underlying swap product. 

The swaption settlement type is `PhysicalSettlement` or `CashSettlement`, and further detail of cash settled swaptions is defined by `CashSettlementMethod`.
These correspond to the ISDA 2006 definitions.

> **TIP:** The strata-loader project provides the ability to load a Swaption
from [FpML]({{site.baseurl}}/fpml_loader) and [CSV]({{site.baseurl}}/trade_loader_swaption).


## Risk measures

The `strata-measure` module provides high-level risk measures for swaptions.
This is based on the lognormal (Black) model, normal (Bachelier) model and SABR model.
The main entry point is
[`SwaptionTradeCalculations`]({{site.baseurl}}/apidocs/com/opengamma/strata/measure/swaption/SwaptionTradeCalculations.html).

The following measures are available:

* present value, and associated sensitivity
* currency exposure
* current cash
* implied volatility

These measures are also available using the calculation API.

The `strata-pricer` module provides pricing support for swaptions.

* [`BlackSwaptionTradePricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/BlackSwaptionTradePricer.html) class.
* [`NormalSwaptionTradePricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/NormalSwaptionTradePricer.html) class.
* [`SabrSwaptionTradePricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/SabrSwaptionTradePricer.html) class.

For Black and Normal methods, the Greeks can be computed:

* present value delta
* present value gamma
* present value theta
* present value sensitivity to volatility, i.e., present value vega

For the SABR method the pricer supports

* SABR parameter sensitivity


## Product model

The following table summarizes the fields on `Swaption` that can be used to control the product.
For more detail on the meaning of each field, see the [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swaption/Swaption.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| longShort         | Whether the swaption is long or short | Required |
| swaptionSettlement| The settlement method | Required |
| expiryDate        | The expiry date, adjustable | Required |
| expiryTime        | The expiry time | Required |
| expiryZone        | The time-zone of the expiry time | Required |
| underlying        | The underlying swap | Required |



