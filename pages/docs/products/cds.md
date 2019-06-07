---
title: CDS and CDS Index
permalink: /cds/
---

{% include macros.html %}

A Credit Default Swap (CDS) is a financial instrument that provides the ability to manage credit risk.
The protection seller agrees to compensate the protection buyer when the specified legal entity suffers a default.
The protection seller is paid a regular premium until the expiry of the CDS contract or until the defaults.
As such, CDS can be viewed as a form of insurance against the default of a specific legal entity.

The Strata CDS instrument follows the ISDA standard.

A CDS Index is a standardized financial derivative that contains a basket single name CDS.


## Key classes

A CDS is represented in Strata using the [`Cds`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/credit/Cds.html) class.
The `Cds` class stores details of the product that was agreed.
The trade details are stored in [`CdsTrade`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/credit/CdsTrade.html) class.

CDS products are relatively standard, so the `CdsConvention` is a good way to create one:

```java
CdsTrade cdsTrade = CdsConventions.USD_STANDARD.toTrade(
    StandardId.of("OG-Entity", "RISKY_CORP"),  // entity that might default
    TradeInfo.of(LocalDate.of(2017, 6, 23)),   // trade date
    LocalDate.of(2017, 6, 21),                 // start date
    LocalDate.of(2019, 6, 12),                 // end date
    BuySell.BUY,                               // whether buying protection, or selling it
    1_000_000,                                 // notional
    0.012);                                    // fixed rate of 1.2%
```

A CDS Index is represented in Strata using the [`CdsIndex`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/credit/CdsIndex.html) class.
Most of the details are the same as a CDS.

> **TIP:** The strata-loader project provides the ability to load a CDS
from [FpML]({{site.baseurl}}/fpml_loader)
and CSV ([CDS]({{site.baseurl}}/trade_loader_cds) and [CDS Index]({{site.baseurl}}/trade_loader_cds_index)).


## Risk measures

The `strata-measure` module provides high-level risk measures for CDS.

The `strata-pricer` module provides lower-level pricing support for CDS:

* `IsdaCdsTradePricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/credit/IsdaCdsTradePricer.html).
* `IsdaCdsProductPricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/credit/IsdaCdsProductPricer.html).

For CDS Index, see:

* `IsdaHomogenousCdsIndexTradePricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/credit/IsdaHomogenousCdsIndexTradePricer.html).
* `IsdaHomogenousCdsIndexProductPricer`, see [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/credit/IsdaHomogenousCdsIndexProductPricer.html).
