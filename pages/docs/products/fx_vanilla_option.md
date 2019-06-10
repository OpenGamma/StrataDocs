---
title: FX Vanilla Option
permalink: /fx_vanilla_option/
---

{% include macros.html %}

An FX option is a financial instrument that provides an option based on the future value of a foreign exchange.
The option is European, exercised only on the exercise date.

For example, a call on a 'EUR 1.00 / USD -1.41' exchange is the option to
perform a foreign exchange on the expiry date, where USD 1.41 is paid to receive EUR 1.00.


## Key classes

An FX Vanilla Option is represented in Strata using the [`FxVanillaOption`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fxopt/FxVanillaOption.html) class.
The `FxVanillaOption` class stores details of the product that was agreed.
The trade details are stored in [`FxVanillaOptionTrade`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fxopt/FxVanillaOptionTrade.html) class.

The underlying FX transaction that will occur if the option is in the money is represented by an
[`FxSingle`]({{site.baseurl}}/fx_single).

An `FxVanillaOption` can be created as follows:

```java
FxSingle fx = FxSingle.of(CurrencyAmount.of(Currency.USD, 1000),
                          FxRate.of(EUR, USD, 1.115),
                          LocalDate.of(2016, 10, 5));
FxVanillaOption fxOpt = FxVanillaOption.builder()
                                       .longShort(SHORT)
                                       .expiryDate(LocalDate.of(2016, 10, 7))
                                       .expiryTime(LocalTime.of(13, 00))
                                       .expiryZone(ZoneId.of("Europe/Paris"))
                                       .underlying(fx)
                                       .build();
```

> **TIP:** The strata-loader project provides the ability to load an FX Vanilla Option
from [CSV]({{site.baseurl}}/trade_loader_fx_vanilla_option).


## Risk measures

The `strata-measure` module provides high-level risk measures for FX Vanilla Options.
The main entry point is
[`FxVanillaOptionTradeCalculations`]({{site.baseurl}}/apidocs/com/opengamma/strata/measure/fxopt/FxVanillaOptionTradeCalculations.html).

Two methods of calculation are supported:

* Black
* Vanna Volga

The following measures are available:

* present value, and associated sensitivity
* currency exposure
* current cash

These measures are also available using the calculation API.

The `strata-pricer` module provides lower-level pricing support for FX Singles:

* `BlackFxVanillaOptionTradePricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/fxopt/BlackFxVanillaOptionTradePricer.html).
* `BlackFxVanillaOptionProductPricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/fxopt/BlackFxVanillaOptionProductPricer.html).
* `VannaVolgaFxVanillaOptionTradePricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/fxopt/VannaVolgaFxVanillaOptionTradePricer.html).
* `VannaVolgaFxVanillaOptionProductPricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/fxopt/VannaVolgaFxVanillaOptionProductPricer.html).

## Product model

The following table summarizes the fields on `FxVanillaOption` that can be used to control the product.
For more detail on the meaning of each field, see the
[Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fxopt/FxVanillaOption.html);

| Property name     | Description | Required/Optional |
|-------------------|-------------|-------------------|
| longShort         | Whether the option is long or short | Required |
| expiryDate        | The date that the option expires | Required |
| expiryTime        | The time-of-day when the option expires | Required |
| expiryZone        | The time-zone of the expiry time | Required |
| underlying        | The [FxSingle]({{site.baseurl}}/fx_single) that the option is based on | Required |

