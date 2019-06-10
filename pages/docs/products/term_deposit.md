---
title: Term Deposit
permalink: /term_deposit/
---

{% include macros.html %}

A Term Deposit is a financial instrument that provides a fixed rate of interest on an amount for a specific term.
For example, investing GBP 1,000 for 3 months at a 1% interest rate.

The instrument has two payments, one at the start date and one at the end date.
For example, investing  GBP 1,000 for 3 months implies an initial payment to the counterparty
of GBP 1,000 and a final payment from the counterparty of GBP 1,000 plus interest.


## Key classes

A Term Deposit is represented in Strata using the [`TermDeposit`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/deposit/TermDeposit.html) class.
The `TermDeposit` class stores details of the product that was agreed.
The trade details are stored in [`TermDepositTrade`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/deposit/TermDepositTrade.html) class.

A `TermDeposit` can be created using a builder as follows:

```java
TermDeposit td = TermDeposit.builder()
  .buySell(BuySell.BUY)
  .currency(Currency.USD)
  .notional(10_000_000)
  .startDate(LocalDate.of(2014, 9, 12))
  .endDate(LocalDate.of(2014, 12, 12))
  .dayCount(DayCounts.THIRTY_360_ISDA)
  .rate(0.013)
  .build();
```

{{tip}}The strata-loader project provides the ability to load a Term Deposit
from [FpML]({{site.baseurl}}/fpml_loader) and [CSV]({{site.baseurl}}/trade_loader_term_deposit).{{end}}


## Risk measures

The `strata-measure` module provides high-level risk measures for Term Deposits.
The main entry point is
[`TermDepositTradeCalculations`]({{site.baseurl}}/apidocs/com/opengamma/strata/measure/deposit/TermDepositTradeCalculations.html).

The following measures are available:

* present value, and associated sensitivity
* par rate
* par spread
* currency exposure
* current cash

These measures are also available using the calculation API.

The `strata-pricer` module provides lower-level pricing support for Term Deposits:

* `DiscountingTermDepositTradePricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/deposit/DiscountingTermDepositTradePricer.html).
* `DiscountingTermDepositProductPricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/deposit/DiscountingTermDepositProductPricer.html).


## Product model

The following table summarizes the fields on `TermDeposit` that can be used to control the product.
For more detail on the meaning of each field, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/deposit/TermDeposit.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| buySell           | Whether the deposit is buy or sell | Required |
| currency          | The primary currency | Required |
| notional          | The notional amount | Required |
| startDate         | The start date | Required |
| endDate           | The end date | Required |
| businessDayAdjustment | The holiday adjustment to the start/end date | Optional |
| dayCount          | The day count | Required |
| rate              | The fixed rate of interest | Required |

The fixed interest rate must be specified in decimal form.
A 5% rate is specified as 0.05.
