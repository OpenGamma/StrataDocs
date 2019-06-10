---
title: Bullet Payment
permalink: /bullet_payment/
---

{% include macros.html %}

A Bullet Payment is a simple unidirectional one-off payment.
The reason for the payment is not captured.


## Key classes

A Bullet Payment is represented in Strata using the [`BulletPayment`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/payment/BulletPayment.html) class.
The `BulletPayment` class stores details of the product that was agreed.
The trade details are stored in [`BulletPaymentTrade`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/payment/BulletPaymentTrade.html) class.

A `BulletPayment` can be created using a builder as follows:

```java
BulletPayment bp = BulletPayment.builder()
  .payReceive(PayReceive.PAY)
  .value(CurrencyAmount.of(GBP, 20_000))
  .date(AdjustableDate.of(LocalDate.of(2014, 9, 16), BusinessDayAdjustement.of(FOLLOWING, GBLO)))
  .build();
```

> **TIP:** The strata-loader project provides the ability to load a Bullet Payment
from [FpML]({{site.baseurl}}/fpml_loader) and [CSV]({{site.baseurl}}/trade_loader_bullet_payment).


## Risk measures

The `strata-measure` module provides high-level risk measures for Bullet Payments.
The main entry point is
[`BulletPaymentTradeCalculations`]({{site.baseurl}}/apidocs/com/opengamma/strata/measure/payment/BulletPaymentTradeCalculations.html).

The following measures are available:

* present value, and associated sensitivity
* single-node bucketed gamma
* currency exposure
* current cash

These measures are also available using the calculation API.

The `strata-pricer` module provides lower-level pricing support for Bullet Payments:

* `DiscountingPaymentPricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/DiscountingPaymentPricer.html).


## Product model

The following table summarizes the fields on `BulletPayment` that can be used to control the product.
For more detail on the meaning of each field, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/payment/BulletPayment.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| payReceive        | Whether the amount is paid or received | Required |
| value             | The payment value | Required |
| date              | The payment date, adjustable | Required |
