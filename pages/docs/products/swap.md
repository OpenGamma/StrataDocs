---
title: Swap
permalink: /swap/
---

{% include macros.html %}

A rate swap is a financial instrument that represents the exchange of streams of payments.
The swap is formed of legs, where each leg typically represents the obligations
of the seller or buyer of the swap. In the simplest vanilla interest rate swap,
there are two legs, one with a fixed rate and the other a floating rate.
Many other more complex swaps can also be represented.

For example, a swap might involve an agreement to exchange the difference between
the fixed rate of 1% and the GBP LIBOR rate every 3 months for 2 years.

The Strata swap instrument covers four types of legs - Fixed, Ibor rate, Overnight rate and Inflation rate.
Other types of swap have their own instruments.


## Key classes

A rate swap is represented in Strata using the [`Swap`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/Swap.html) class.
The `Swap` class stores details of the product that was agreed.
The trade details are stored in [`SwapTrade`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/SwapTrade.html) class.

A `Swap` can be created using a builder as follows:

```java
SwapLeg payLeg = RateCalculationSwapLeg.builder()
  .payReceive(PayReceive.PAY)
  .accrualSchedule(PeriodicSchedule.builder()
    .startDate(LocalDate.of(2014, 9, 12))
    .endDate(LocalDate.of(2021, 9, 12))
    .frequency(Frequency.P6M)
    .businessDayAdjustment(BusinessDayAdjustment.of(MODIFIED_FOLLOWING, HolidayCalendarIds.USNY))
    .build())
  .paymentSchedule(PaymentSchedule.builder()
    .paymentFrequency(Frequency.P6M)
    .paymentDateOffset(DaysAdjustment.NONE)
    .build())
  .notionalSchedule(NotionalSchedule.of(Currency.USD, 100_000_000))
  .calculation(FixedRateCalculation.of(0.015, DayCounts.THIRTY_U_360))
  .build();

SwapLeg receiveLeg = RateCalculationSwapLeg.builder()
  .payReceive(PayReceive.RECEIVE)
  .accrualSchedule(PeriodicSchedule.builder()
    .startDate(LocalDate.of(2014, 9, 12))
    .endDate(LocalDate.of(2021, 9, 12))
    .frequency(Frequency.P3M)
    .businessDayAdjustment(BusinessDayAdjustment.of(MODIFIED_FOLLOWING, HolidayCalendarIds.USNY))
    .build())
  .paymentSchedule(PaymentSchedule.builder()
    .paymentFrequency(Frequency.P3M)
    .paymentDateOffset(DaysAdjustment.NONE)
    .build())
  .notionalSchedule(NotionalSchedule.of(Currency.USD, 100_000_000))
  .calculation(IborRateCalculation.of(IborIndices.USD_LIBOR_3M))
  .build();

Swap swap = Swap.of(payLeg, receiveLeg);
```

> **TIP:** The strata-loader project provides the ability to load a Swap
from [FpML]({{site.baseurl}}/fpml_loader) and [CSV]({{site.baseurl}}/trade_loader_swap).


## Risk measures

The `strata-measure` module provides high-level risk measures for rate swaps.
The main entry point is
[`SwapTradeCalculations`]({{site.baseurl}}/apidocs/com/opengamma/strata/measure/swap/SwapTradeCalculations.html).

The following measures are available:

* present value, detailed breakdown, and associated sensitivity
* single-node bucketed gamma
* par rate
* par spread
* cash flows
* accrued interest
* leg initial notional
* leg present value
* currency exposure
* current cash

These measures are also available using the calculation API.

The `strata-pricer` module provides lower-level pricing support for rate swaps:

* `DiscountingSwapTradePricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swap/DiscountingSwapTradePricer.html).
* `DiscountingSwapProductPricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swap/DiscountingSwapProductPricer.html).


## Product model

The following table summarizes the fields on `Swap` that can be used to control the product.
Only the most important fields are shown below.
For more detail on the meaning of each field, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/Swap.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| legs              | The list of swap legs | Required |

There are a number of kinds of swap leg. The most common is `RateCalculationSwapLeg`, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/RateCalculationSwapLeg.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| payReceive        | Whether the leg is pay or receive | Required |
| accrualSchedule   | The accrual schedule, see [schedules]({{site.baseurl}}/schedules) | Required |
| paymentSchedule   | The payment schedule | Required |
| notionalSchedule  | The notional schedule | Required |
| calculation       | The calculation details | Required |

A payment schedule is specified by `PaymentSchedule`, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/PaymentSchedule.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| paymentFrequency  | The periodic frequency of payments | Required |
| paymentRelativeTo | The base date that each payment is relative to | Defaults to period end |
| paymentDateOffset | The offset to the payment date | Required |
| compoundingMethod | Whether and how compounding occurs | Required |

A notional schedule is specified by `NotionalSchedule`, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/NotionalSchedule.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| currency          | The currency of the leg | Required |
| fxReset           | Definition of FX resets | Required |
| amount            | Amount of the notional and how it varies over time | Required |
| initialExchange   | Whether to exchange the initial notional | Defaults to false |
| intermediateExchange | Whether to exchange the intermediate notionals | Defaults to false |
| finalExchange     | Whether to exchange the final notional | Defaults to false |

A fixed rate is specified by `FixedRateCalculation`, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/FixedRateCalculation.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| dayCount          | The day count | Required |
| rate              | The fixed rate of interest | Required |

The fixed interest rate must be specified in decimal form.
A 5% rate is specified as 0.05.

A floating Ibor rate is specified by `IborRateCalculation`, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/IborRateCalculation.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| dayCount          | The day count | Defaults to the day count of the index |
| index             | The Ibor index to observe | Required |
| resetPeriods      | The reset periods, used for rate averaging | Optional |
| fixingRelativeTo  | The base date that each fixing is relative to | Defaults to period start |
| fixingDateOffset  | The offset to the fixing date | Defaults to the offset of the index |
| negativeRateMethod | Whether to allow negative rates | Defaults to allow negative rates |
| firstRegularRate  | The first regular rate, used to lock the first fixing | Optional |
| initialStub       | Details of the initial stub | Optional |
| finalStub         | Details of the final stub | Optional |
| gearing           | How gearing varies over time | Optional |
| spread            | How spread varies over time | Optional |

A floating Overnight rate is specified by `OvernightRateCalculation`, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/OvernightRateCalculation.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| dayCount          | The day count | Defaults to the day count of the index |
| index             | The Overnight index to observe | Required |
| accrualMethod     | Whether to compound or average | Defaults to compounded |
| negativeRateMethod | Whether to allow negative rates | Defaults to allow negative rates |
| rateCutOffDays    | The days before the end to stop observing | Defaults to zero |
| gearing           | How gearing varies over time | Optional |
| spread            | How spread varies over time | Optional |

A floating inflation rate is specified by `InflationRateCalculation`, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swap/InflationRateCalculation.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| index             | The Price index to observe | Required |
| lag               | The period between the index and the accrual date | Required |
| interpolated      | Whether the rate is interpolated | Defaults to false |
| gearing           | How gearing varies over time | Optional |
