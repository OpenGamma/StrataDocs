---
title: Releases
permalink: /releases/
---

Releases of Strata are performed when a set of functionality has stabilized.
To access a release, see the options for [obtaining Strata]({{site.baseurl}}/obtaining_strata).


## Strata v2.11.0

* 7 January 2022

This release contains over 70 [fixed issues](https://github.com/OpenGamma/Strata/milestone/30?closed=1).

* Continue change to support Overnight indices as an alternative to Ibor indices (source and binary incompatible)
 [#2398](https://github.com/OpenGamma/Strata/issues/2398),
 [#2382](https://github.com/OpenGamma/Strata/issues/2382),
 [#2407](https://github.com/OpenGamma/Strata/issues/2407)
* Extend usefulness of Act/Act ICMA day count
 [#2365](https://github.com/OpenGamma/Strata/issues/2365)
* Fix joined holiday calendars like "GBLO~USNY"
 [#2405](https://github.com/OpenGamma/Strata/issues/2405)
* More indices, "GBP-SONIAICETERM", "GBP-SONIAREFINITIVTERM", "JPY-TORF", "USD-SOFRCMETERM", "USD-BSBY", "USD-AMERIBORTERM",
 with mappings updated to cover ISDA 2021 standards
 [#2383](https://github.com/OpenGamma/Strata/issues/2383),
 [#2378](https://github.com/OpenGamma/Strata/issues/2378),
 [#2366](https://github.com/OpenGamma/Strata/issues/2366)
* Enhance swaptions, including Bermudan
 [#2376](https://github.com/OpenGamma/Strata/issues/2376),
 [#2364](https://github.com/OpenGamma/Strata/issues/2364),
 [#2357](https://github.com/OpenGamma/Strata/issues/2357),
 [#2354](https://github.com/OpenGamma/Strata/issues/2354),
 [#2358](https://github.com/OpenGamma/Strata/issues/2358),
 [#2343](https://github.com/OpenGamma/Strata/issues/2343)
* Enhance Ibor Cap/Floor pricing/parsing
 [#2361](https://github.com/OpenGamma/Strata/issues/2361),
 [#2342](https://github.com/OpenGamma/Strata/issues/2342),
 [#2318](https://github.com/OpenGamma/Strata/issues/2318)
* Enhance FX option pricing/parsing
 [#2349](https://github.com/OpenGamma/Strata/issues/2349),
 [#2346](https://github.com/OpenGamma/Strata/issues/2346),
 [#2323](https://github.com/OpenGamma/Strata/issues/2323),
 [#2325](https://github.com/OpenGamma/Strata/issues/2325),
 [#2324](https://github.com/OpenGamma/Strata/issues/2324),
 [#2317](https://github.com/OpenGamma/Strata/issues/2317)
* Enhance schedule building
 [#2350](https://github.com/OpenGamma/Strata/issues/2350),
 [#2352](https://github.com/OpenGamma/Strata/issues/2352),
 [#2353](https://github.com/OpenGamma/Strata/issues/2353)
* Treat gold as the base currency in conventional order
 [#2339](https://github.com/OpenGamma/Strata/issues/2339)
* FX conversion for `ExplainMap`
 [#2345](https://github.com/OpenGamma/Strata/issues/2345)

#### Compatibility

The LIBOR transition has caused us to alter a few parameters and return types in an incompatible way.

* `SwapIndex` and implementations now hold a `FixedFloatSwapTemplate` instead of `FixedIborSwapTemplate`.
* `CmsLeg` now holds a `RateIndex` instead of `IborIndex`.
* `SwaptionVolatilities` and implementations now hold a `FixedFloatSwapConvention` instead of `FixedIborSwapConvention`.
* `Swaption` was changed to be based on `RateIndex` in v2.10.

A spelling mistake was fixed in `FixedInflationSwapConventions` - HCIP instead of HICP.

The `MapStream` class has changed the filter method from `BiFunction<K, V, Boolean>` to `BiPredicate<K, V>`.


## Strata v2.10.0

* 22 April 2021

This release contains over 15 [fixed issues](https://github.com/OpenGamma/Strata/milestone/29?closed=1).

* Change Swaption to support Overnight index (source and binary incompatible)
 [#2305](https://github.com/OpenGamma/Strata/issues/2305)
* Add vega to FX option
 [#2292](https://github.com/OpenGamma/Strata/issues/2292)
* Update Japanese holiday calendar
 [#2293](https://github.com/OpenGamma/Strata/issues/2293)


## Strata v2.9.0

* 2 February 2021

This release contains over 50 [fixed issues](https://github.com/OpenGamma/Strata/milestone/28?closed=1).

* Add new indices for CZK, HUF, IDR, ILS, RUB, SAR, TRY and AMERIBOR
 [#2248](https://github.com/OpenGamma/Strata/issues/2248),
 [#2268](https://github.com/OpenGamma/Strata/issues/2268)
* Add OIS conventions for ESTR
 [#2257](https://github.com/OpenGamma/Strata/issues/2257)
* Make CSV parsing extensible via standard extended enum approach
 [#2284](https://github.com/OpenGamma/Strata/issues/2284),
 [#2285](https://github.com/OpenGamma/Strata/issues/2285),
 [#2286](https://github.com/OpenGamma/Strata/issues/2286)
* Handle CNY repo swaps
 [#2249](https://github.com/OpenGamma/Strata/issues/2249)
* Add constants for standard ID schemes
 [#2240](https://github.com/OpenGamma/Strata/issues/2240),
 [#2287](https://github.com/OpenGamma/Strata/issues/2287),
 [#2261](https://github.com/OpenGamma/Strata/issues/2261)
* Switch code to use main branch instead of master
 [#2267](https://github.com/OpenGamma/Strata/issues/2267)


## Strata v2.8.0

* 11 September 2020

This release contains over 65 [fixed issues](https://github.com/OpenGamma/Strata/milestone/27?closed=1).

* Calibrate curves using Overnight Futures
 [#2216](https://github.com/OpenGamma/Strata/issues/2216),
 [#2208](https://github.com/OpenGamma/Strata/issues/2208)
* Change `IborFutureConvention` to `IborFutureContractSpec` and add `OvernightFutureContractSpec`
 [#2203](https://github.com/OpenGamma/Strata/issues/2203),
 [#2209](https://github.com/OpenGamma/Strata/issues/2209)
* Add `SGD-SORA` index
 [#2215](https://github.com/OpenGamma/Strata/issues/2215)
* Add `MarketTenor` to represent the concept of ON/TN/SN tenors
 [#2184](https://github.com/OpenGamma/Strata/issues/2184)


## Strata v2.7.0

* 25 February 2020

This release contains over 70 [fixed issues](https://github.com/OpenGamma/Strata/milestone/26?closed=1).

* Add `PortfolioItem.withInfo()` method, source compatible but not binary compatible for callers,
also not source compatible for custom implementations of `PortfolioItem`
 [#2133](https://github.com/OpenGamma/Strata/issues/2133)
* Rename `ESTER` index to `ESTR`, old code will be accepted on input for compatibility
 [#2101](https://github.com/OpenGamma/Strata/issues/2101)
* Fix `EtdOptionPosition` and `EtdFuturePosition` `resolveTarget()` methods
 [#2138](https://github.com/OpenGamma/Strata/issues/2138)
* Fix `CurrencyParameterSensitivity.toUnitParameterSensitivity()` method
 [#2127](https://github.com/OpenGamma/Strata/issues/2127)


## Strata v2.6.0

* 30 July 2019

This release contains over 20 [fixed issues](https://github.com/OpenGamma/Strata/milestone/25?closed=1).

* Add SWIFT code formats for day conut and business day convention
 [#2023](https://github.com/OpenGamma/Strata/issues/2023)
* Performance enhancements
 [#2027](https://github.com/OpenGamma/Strata/issues/2027),
 [#2031](https://github.com/OpenGamma/Strata/issues/2031)
* AttributeType now has stronger Java type,
 [#2044](https://github.com/OpenGamma/Strata/issues/2044)

## Strata v2.5.0

* 28 June 2019

This release contains over 10 [fixed issues](https://github.com/OpenGamma/Strata/milestone/24?closed=1).

* Ability to represent the Central Counterparty Clearing House (CCP), see `CcpId`
 [#2013](https://github.com/OpenGamma/Strata/issues/2013),
 [#2014](https://github.com/OpenGamma/Strata/issues/2014)
* Ability to represent groups of Exchange Traded Derivatives (ETDs) for risk, see `EtdContractGroupId`
 [#2015](https://github.com/OpenGamma/Strata/issues/2015)
* Add ability to get the opposite of Buy/Sell, Long/Short and Put/Call
 [#2008](https://github.com/OpenGamma/Strata/issues/2008)
* Remove dependency on TestNG from `TestHelper`
 [#2007](https://github.com/OpenGamma/Strata/issues/2007)


## Strata v2.4.0

* 10 June 2019

This release contains over 35 [fixed issues](https://github.com/OpenGamma/Strata/milestone/23?closed=1).

* Reading/writing CDS Index from/to CSV
 [#1999](https://github.com/OpenGamma/Strata/issues/1999)
* Enhance CSV parsing
 [#1995](https://github.com/OpenGamma/Strata/issues/1995),
 [#1986](https://github.com/OpenGamma/Strata/issues/1986),
 [#1981](https://github.com/OpenGamma/Strata/issues/1981),
 [#1983](https://github.com/OpenGamma/Strata/issues/1983),
 [#1984](https://github.com/OpenGamma/Strata/issues/1984)
* Check if document is FpML
 [#1982](https://github.com/OpenGamma/Strata/issues/1982)
* Add market quote measure for swaps
 [#1972](https://github.com/OpenGamma/Strata/issues/1972),
 [#1976](https://github.com/OpenGamma/Strata/issues/1976)
* Add aliases for various indices
 [#1998](https://github.com/OpenGamma/Strata/issues/1998),
 [#1990](https://github.com/OpenGamma/Strata/issues/1990)
* Fix SONIA index definition
 [#1967](https://github.com/OpenGamma/Strata/issues/1967)
* Update holiday calendars
 [#1961](https://github.com/OpenGamma/Strata/issues/1961),
 [#1969](https://github.com/OpenGamma/Strata/issues/1969)
* Use a singleton XML factory (requires Java 8u20 or later)
 [#1991](https://github.com/OpenGamma/Strata/issues/1991)


## Strata v2.3.0

* 26 April 2019

This release contains over 40 [fixed issues](https://github.com/OpenGamma/Strata/milestone/22?closed=1).

* Writing trades to CSV
 [#1952](https://github.com/OpenGamma/Strata/issues/1952)
* Parsing trades from CSV - support for Swaption, FX Vanilla Option, CDS and Bullet Payment
 [#1945](https://github.com/OpenGamma/Strata/issues/1945),
 [#1954](https://github.com/OpenGamma/Strata/issues/1954),
 [#1956](https://github.com/OpenGamma/Strata/issues/1956),
 [#1927](https://github.com/OpenGamma/Strata/issues/1927)
* Enhance parsing trades from CSV - parse more kinds of Swap and FRA
 [#1951](https://github.com/OpenGamma/Strata/issues/1951),
 [#1947](https://github.com/OpenGamma/Strata/issues/1947)
* Add collateralized cash price settlement for swaptions
 [#1902](https://github.com/OpenGamma/Strata/issues/1902),
 [#1921](https://github.com/OpenGamma/Strata/issues/1921)
* Add TWD-TAIBOR, THB-THBFIX and EUR-ESTER
 [#1931](https://github.com/OpenGamma/Strata/issues/1931),
 [#1930](https://github.com/OpenGamma/Strata/issues/1930),
 [#1923](https://github.com/OpenGamma/Strata/issues/1923),
 [#1893](https://github.com/OpenGamma/Strata/issues/1893)
* Fix HKD-HIBOR,  AUD-BBSW and COP FX
 [#1887](https://github.com/OpenGamma/Strata/issues/1887),
 [#1891](https://github.com/OpenGamma/Strata/issues/1891)
* Fix bond detachment date logic for accrued year fraction
 [#1953](https://github.com/OpenGamma/Strata/issues/1953)
* More lenient schedule generation
 [#1925](https://github.com/OpenGamma/Strata/issues/1925)
* Support working on weekends to handle "Golden Week" in China
 [#1958](https://github.com/OpenGamma/Strata/issues/1958)


## Strata v2.2.0

* 28 January 2019

This release contains over 25 [fixed issues](https://github.com/OpenGamma/Strata/milestone/21?closed=1).

* Brazilian swaps
 [#1828](https://github.com/OpenGamma/Strata/issues/1828),
 [#1878](https://github.com/OpenGamma/Strata/issues/1878)
* Update indices and conventions,
 [#1879](https://github.com/OpenGamma/Strata/issues/1879),
 [#1883](https://github.com/OpenGamma/Strata/issues/1883),
 [#1876](https://github.com/OpenGamma/Strata/issues/1876),
 [#1882](https://github.com/OpenGamma/Strata/issues/1882),
 [#1858](https://github.com/OpenGamma/Strata/issues/1858),
 [#1857](https://github.com/OpenGamma/Strata/issues/1857)
* Enhanced schedule building,
 [#1873](https://github.com/OpenGamma/Strata/issues/1873),
 [#1861](https://github.com/OpenGamma/Strata/issues/1861)
* Fix derived calculation functions
 [#1856](https://github.com/OpenGamma/Strata/issues/1856)


## Strata v2.1.0

* 30 October 2018

This release contains over 45 [fixed issues](https://github.com/OpenGamma/Strata/milestone/20?closed=1).

* Calculation target for sensitivities - `CurveSensitivities`,
 [#1806](https://github.com/OpenGamma/Strata/issues/1806),
 [#1800](https://github.com/OpenGamma/Strata/issues/1800),
 [#1814](https://github.com/OpenGamma/Strata/issues/1814),
 [#1818](https://github.com/OpenGamma/Strata/issues/1818),
 [#1831](https://github.com/OpenGamma/Strata/issues/1831),
 [#1811](https://github.com/OpenGamma/Strata/issues/1811),
 [#1816](https://github.com/OpenGamma/Strata/issues/1816),
 [#1836](https://github.com/OpenGamma/Strata/issues/1836),
 [#1837](https://github.com/OpenGamma/Strata/issues/1837),
 [#1805](https://github.com/OpenGamma/Strata/issues/1805)
* Calculate market quote sensitivities for bonds,
 [#1809](https://github.com/OpenGamma/Strata/issues/1809)
* Trade and stub conventions,
 [#1829](https://github.com/OpenGamma/Strata/issues/1829),
 [#1825](https://github.com/OpenGamma/Strata/issues/1825),
 [#1810](https://github.com/OpenGamma/Strata/issues/1810)
* Extend legal entity support,
 [#1791](https://github.com/OpenGamma/Strata/issues/1791)
* Enhance holiday calendars,
 [#1801](https://github.com/OpenGamma/Strata/issues/1801),
 [#1797](https://github.com/OpenGamma/Strata/issues/1797),
 [#1795](https://github.com/OpenGamma/Strata/issues/1795)
* Add thread-safe `NumberFormatter`,
 [#1793](https://github.com/OpenGamma/Strata/issues/1793),
* Abstract tenor-based parameter metadata instances - `TenoredParameterMetadata`,
 [#1799](https://github.com/OpenGamma/Strata/issues/1799),
 [#1826](https://github.com/OpenGamma/Strata/issues/1826)
* Find curve names in curve definition,
 [#1817](https://github.com/OpenGamma/Strata/issues/1817)
* Additional methods on `MapStream`,
 [#1788](https://github.com/OpenGamma/Strata/issues/1788),
 [#1798](https://github.com/OpenGamma/Strata/issues/1798),
 [#1808](https://github.com/OpenGamma/Strata/issues/1808),
 [#1813](https://github.com/OpenGamma/Strata/issues/1813),
 [#1824](https://github.com/OpenGamma/Strata/issues/1824),
 [#1832](https://github.com/OpenGamma/Strata/issues/1832)
* Enhanced parsing,
 [#1812](https://github.com/OpenGamma/Strata/issues/1812),
 [#1819](https://github.com/OpenGamma/Strata/issues/1819),
 [#1822](https://github.com/OpenGamma/Strata/issues/1822),
 [#1827](https://github.com/OpenGamma/Strata/issues/1827),
 [#1802](https://github.com/OpenGamma/Strata/issues/1802)
* Build reliably on Java 11,
 [#1830](https://github.com/OpenGamma/Strata/issues/1830),
 [#1789](https://github.com/OpenGamma/Strata/issues/1789),
 [#1834](https://github.com/OpenGamma/Strata/issues/1834)


#### Compatibility

The default stub convention has been changed from 'ShortInitial' to 'SmartInitial' (except when loading from FpML).
The new "smart" stub conventions create a long stub when the extra period is less than 7 days.
We believe this better matches market practice.

All existing trade conventions now use a roll convention of 'EOM', which means that a swap
with 1 month frequency starting on the 30th November will now roll at the end of the month
where previously it would have rolled on the 30th of each month.
We believe this better matches market practice.

The interface `LegalEntity` has two new methods.
In the unlikely event that you have implemented the interface you will need to implement the new methods.

The interface `IborFutureTemplate` has one new method.
In the unlikely event that you have implemented the interface you will need to implement the new method.


## Strata v2.0.0

This is a major release with a number of backwards incompatible changes.

There are over 115 [fixed issues](https://github.com/OpenGamma/Strata/milestone/20?closed=1).

* Add Bills and LegalEntityId,
 [#1748](https://github.com/OpenGamma/Strata/issues/1748),
 [#1754](https://github.com/OpenGamma/Strata/issues/1754),
 [#1758](https://github.com/OpenGamma/Strata/issues/1758),
 [#1762](https://github.com/OpenGamma/Strata/issues/1762),
 [#1761](https://github.com/OpenGamma/Strata/issues/1761)
* Add OvernightFutureSecurity,
 [#1763](https://github.com/OpenGamma/Strata/issues/1763)
* Allow FX to have split payment dates,
 [#1729](https://github.com/OpenGamma/Strata/issues/1729),
 [#1732](https://github.com/OpenGamma/Strata/issues/1732)
* Extended support for positions,
 [#1723](https://github.com/OpenGamma/Strata/issues/1723),
 [#1734](https://github.com/OpenGamma/Strata/issues/1734),
 [#1733](https://github.com/OpenGamma/Strata/issues/1733),
 [#1730](https://github.com/OpenGamma/Strata/issues/1730),
 [#1728](https://github.com/OpenGamma/Strata/issues/1728),
 [#1721](https://github.com/OpenGamma/Strata/issues/1721),
 [#1722](https://github.com/OpenGamma/Strata/issues/1722),
 [#1719](https://github.com/OpenGamma/Strata/issues/1719),
 [#1711](https://github.com/OpenGamma/Strata/issues/1711),
 [#1720](https://github.com/OpenGamma/Strata/issues/1720)
* Link trades and positions better,
 [#1712](https://github.com/OpenGamma/Strata/issues/1712),
 [#1713](https://github.com/OpenGamma/Strata/issues/1713),
 [#1724](https://github.com/OpenGamma/Strata/issues/1724),
 [#1712](https://github.com/OpenGamma/Strata/issues/1712),
 [#1731](https://github.com/OpenGamma/Strata/issues/1731)
* Add Product/Security/Trade model,
 [#1697](https://github.com/OpenGamma/Strata/issues/1697),
 [#1695](https://github.com/OpenGamma/Strata/issues/1695),
 [#1691](https://github.com/OpenGamma/Strata/issues/1691),
 [#1696](https://github.com/OpenGamma/Strata/issues/1696),
 [#1689](https://github.com/OpenGamma/Strata/issues/1689),
 [#1674](https://github.com/OpenGamma/Strata/issues/1674),
 [#1667](https://github.com/OpenGamma/Strata/issues/1667)
 [#1666](https://github.com/OpenGamma/Strata/issues/1666)
* Rename rates classes,
 [#1750](https://github.com/OpenGamma/Strata/issues/1750),
 [#1751](https://github.com/OpenGamma/Strata/issues/1751),
 [#1766](https://github.com/OpenGamma/Strata/issues/1766)
* Move configuration to META-INF,
 [#1736](https://github.com/OpenGamma/Strata/issues/1736)
* Gamma calculation with a combined curve,
 [#1680](https://github.com/OpenGamma/Strata/issues/1680),
 [#1677](https://github.com/OpenGamma/Strata/issues/1677),
 [#1699](https://github.com/OpenGamma/Strata/issues/1699),
 [#1625](https://github.com/OpenGamma/Strata/issues/1625),
 [#1624](https://github.com/OpenGamma/Strata/issues/1624)
 * Add USD-SOFR, ZAR-SABOR, CNY-REPO-1W, use CHF-SARON in preference to CHF-TOIS, add more inactive indices,
 [#1765](https://github.com/OpenGamma/Strata/issues/1765),
 [#1775](https://github.com/OpenGamma/Strata/issues/1775),
 [#1681](https://github.com/OpenGamma/Strata/issues/1681),
 [#1693](https://github.com/OpenGamma/Strata/issues/1693)
 [#1694](https://github.com/OpenGamma/Strata/issues/1694)
* Ability to lookup any index by name,
 [#1708](https://github.com/OpenGamma/Strata/issues/1708)
* Remove deprecations,
 [#1716](https://github.com/OpenGamma/Strata/issues/1716),
 [#1718](https://github.com/OpenGamma/Strata/issues/1718),
 [#1743](https://github.com/OpenGamma/Strata/issues/1743),
* Fix NZD and INR FX index definitions,
 [#1726](https://github.com/OpenGamma/Strata/issues/1726),
 [#1772](https://github.com/OpenGamma/Strata/issues/1772)
* Fix Ibor-OIS swap conventions,
 [#1678](https://github.com/OpenGamma/Strata/issues/1678)
* Make Trade/Position/Security easier to modify,
 [#1674](https://github.com/OpenGamma/Strata/issues/1674)
* Make FX and FX trades easier to work with,
 [#1666](https://github.com/OpenGamma/Strata/issues/1666),
 [#1691](https://github.com/OpenGamma/Strata/issues/1691)
* Enhanced CSV loaders,
 [#1745](https://github.com/OpenGamma/Strata/issues/1745),
 [#1735](https://github.com/OpenGamma/Strata/issues/1735),
 [#1670](https://github.com/OpenGamma/Strata/issues/1670),
 [#1709](https://github.com/OpenGamma/Strata/issues/1709),
 [#1702](https://github.com/OpenGamma/Strata/issues/1702),
 [#1705](https://github.com/OpenGamma/Strata/issues/1705)
* Enhanced ETD options to support underlying expiry month,
 [#1668](https://github.com/OpenGamma/Strata/issues/1668),
 [#1669](https://github.com/OpenGamma/Strata/issues/1669)
* Additional interpolator,
 [#1664](https://github.com/OpenGamma/Strata/issues/1664)

#### Compatibility

This is a major release with a number of incompatibilities.

All deprecated classes and methods have been removed.

All configuration files in `com/opengamma/strata/config` have been moved to
`META-INF/com/opengamma/strata/config`. This is necessary to support Java 9.
If you have your own configuration files, they will also need to move.

The rates curve classes have been renamed to be specifically about rates.
If you refer to these classes, you will need to change your code:

* `CurveGroup` becomes `RatesCurveGroup`.
* `CurveGroupId` becomes `RatesCurveGroupId`.
* `CurveGroupInputs` becomes `RatesCurveGroupInputs`.
* `CurveGroupInputsId` becomes `RatesCurveGroupInputsId`.
* `CurveGroupDefinition` becomes `RatesCurveGroupDefinition`.
* `CurveGroupDefinitionBuilder` becomes `RatesCurveGroupDefinitionBuilder`.
* `CurveGroupEntry` becomes `RatesCurveGroupEntry`.
* `CurveCalibrator` becomes `RatesCurveCalibrator`.
* `SyntheticCurveCalibrator` becomes `RatesSyntheticCurveCalibrator`.
* `CurveGroupDefinitionCsvLoader` becomes `RatesCurveGroupDefinitionCsvLoader`.

If you are using bonds, you will likely use classes like `LegalEntityCurveGroup` and
`LegalEntityCurveGroupDefinitionCsvLoader` instead.

The `FxRateLookup` interface has moved package to `com.opengamma.strata.calc.runner`.
If you refer to it, you will need to change your import.

The `FxSingle` class has been altered to support split payment dates.
If you use it, you will need to adapt.
A Joda-Beans mapper will handle deserialization of the old format transparently.

The `LegalEntityDiscountingProvider` implementations and lookup have been altered to
support a new type-safe `LegalEntityId` class. The previous combined security and legal
entity identifier maps have been separated.
If you use bond pricing, you will need to adapt.

The resolved trade classes for security-based products like `ResolvedBondFutureTrade`
have been refactored to allow them to be used as positions.
If you use these classes directly you will need to adapt.

The `ResolvedTrade` interface now exposes `PortfolioItemInfo` instead of `TradeInfo`.
If you use the interface directly you will need to adapt.

The `Trade` and `Position` interfaces have new methods.
If you have implemented your own trades/positions you will need to adapt.

The `SwapLeg` interface has a new method.
If you have implemented your own leg you will need to adapt.

The `Curve` interface has new methods.
If you have implemented your own curves you will need to adapt.

The `RatesProvider` interface has a new method.
If you have implemented your own provider you will need to adapt.

The method `ValueWithFailures.combinedWith` has changed from taking `BinaryOperator` to `BiFunction`.
This is source compatible if using lambdas, but not binary compatible.

The `TradeAttributeType`, `PositionAttributeType` and `SecuirtyAttributeType` classes have been
merged to become `AttributeType`.
A Joda-Convert rename mapper will handle deserialization of the old class names transparently.


## Strata v1.7.1

*6 June 2018*

This minor release contains around 11 fixes. These include:

* Parse zero length periods from CSV format,
 [#1670](https://github.com/OpenGamma/Strata/issues/1670)
* Add ZAR-SABOR, CNY-REPO-1W, use CHF-SARON in preference to CHF-TOIS, add more inactive indices,
 [#1681](https://github.com/OpenGamma/Strata/issues/1681),
 [#1693](https://github.com/OpenGamma/Strata/issues/1693)
 [#1694](https://github.com/OpenGamma/Strata/issues/1694)
* Fix Ibor-OIS swap conventions,
 [#1678](https://github.com/OpenGamma/Strata/issues/1678)
* Summarizer should handle short periods,
 [#1663](https://github.com/OpenGamma/Strata/issues/1663)


## Strata v1.7.0

*19 February 2018*

This release contains over 30 [fixed issues](https://github.com/OpenGamma/Strata/milestone/17?closed=1).

* Provide summaries for trades and positions,
 [#1626](https://github.com/OpenGamma/Strata/issues/1626),
 [#1627](https://github.com/OpenGamma/Strata/issues/1627),
 [#1631](https://github.com/OpenGamma/Strata/issues/1631)
* Additional floating rate index names,
 [#1632](https://github.com/OpenGamma/Strata/issues/1632),
 [#1656](https://github.com/OpenGamma/Strata/issues/1656)
* Better failure messages,
 [#1649](https://github.com/OpenGamma/Strata/issues/1649),
 [#1651](https://github.com/OpenGamma/Strata/issues/1651),
 [#1655](https://github.com/OpenGamma/Strata/issues/1655)
* Add Montreal holiday calendar,
 [#1645](https://github.com/OpenGamma/Strata/issues/1645)
* Add roll conventions,
 [#1647](https://github.com/OpenGamma/Strata/issues/1647)
* Enhance schedule builder,
 [#1652](https://github.com/OpenGamma/Strata/issues/1652),
 [#1646](https://github.com/OpenGamma/Strata/issues/1646)

#### Compatibility

The single method on the interface `FpmlPartySelector` has changed return type.
In the unlikely event that you have implemented the interface you will need to implement the new method.


## Strata v1.6.0

*28 November 2017*

This release contains [31 fixed issues](https://github.com/OpenGamma/Strata/milestone/16?closed=1).
This includes the issues fixed in v1.5.1 and v1.5.2 (see below).

* Add index data for HKD, SGD, KRW, INR and NZD [#1603](https://github.com/OpenGamma/Strata/issues/1603),
 [#1612](https://github.com/OpenGamma/Strata/issues/1612),
 [#1615](https://github.com/OpenGamma/Strata/issues/1615),
 [#1617](https://github.com/OpenGamma/Strata/issues/1617),
 [#1618](https://github.com/OpenGamma/Strata/issues/1618),
 [#1619](https://github.com/OpenGamma/Strata/issues/1619)
* Swap schedules treat single stub period differently from single term period [#1615](https://github.com/OpenGamma/Strata/issues/1615)
* Improve par spread for swaps with only one period [#1608](https://github.com/OpenGamma/Strata/issues/1608)
* Lenient mode for extended enum parsing [#1606](https://github.com/OpenGamma/Strata/issues/1606)
* Conventional currency pair for EUR/GBP swap [#1595](https://github.com/OpenGamma/Strata/issues/1595)
* Add Quote object [#1611](https://github.com/OpenGamma/Strata/issues/1611)
* Validate price index fixings in the loader [#1598](https://github.com/OpenGamma/Strata/issues/1598)
* A repo curve can be looked up without specifying a security [#1621](https://github.com/OpenGamma/Strata/issues/1621)

#### Compatibility

A method was added to the interface `LegalEntityDiscountingProvider`.
In the unlikely event that you have implemented the interface you will need to implement the new method.

The fixed day count associated with various indices has been updated, see [#1592](https://github.com/OpenGamma/Strata/pull/1592).


## Strata v1.5.2

*31 October 2017*

This minor release contains 1 bug fix.

* Return EOM when calculating roll convention from stub [#1590](https://github.com/OpenGamma/Strata/issues/1590)


## Strata v1.5.1

*26 October 2017*

This minor release contains 1 bug fix.

* Fix for CSV outputter when numeric value is prefixed with a sign


## Strata v1.5.0

*26 October 2017*

This release contains [19 fixed issues](https://github.com/OpenGamma/Strata/milestone/15?closed=1).
This includes the issues fixed in v1.4.1 and v1.4.2 (see below).

* Enhance payment schedule stub handling [#1581](https://github.com/OpenGamma/Strata/issues/1581)
* Extended handling of pre-adjusted schedule dates [#1580](https://github.com/OpenGamma/Strata/issues/1580)
* Trade CSV loader extended to support FX forward/spot [#1578](https://github.com/OpenGamma/Strata/issues/1578)
* Trade CSV loader extended to support counterparty [#1583](https://github.com/OpenGamma/Strata/issues/1583)
* Position CSV loader extended to avoid using reference data [#1584](https://github.com/OpenGamma/Strata/issues/1584)
* Extended quoting of CSV [#1586](https://github.com/OpenGamma/Strata/issues/1586)
* Reset dates optional in FpML [#1585](https://github.com/OpenGamma/Strata/issues/1585)
* Plus/minus methods on CurrencyScenarioArray [#1577](https://github.com/OpenGamma/Strata/issues/1577)
* Fix Interpolator-based curve extrapolator [#1588](https://github.com/OpenGamma/Strata/issues/1588)
* Add IntArray.of(IntStream) [#1587](https://github.com/OpenGamma/Strata/issues/1587)
* Upgrade Guava to v23.2-jre [#1589](https://github.com/OpenGamma/Strata/issues/1589)

#### Compatibility

There are no compatibility issues with this release.



## Strata v1.4.2

*5 October 2017*

This minor release contains 3 fixed issues.

* Enhancement - Add DoubleArray.of(DoubleStream) [#1576](https://github.com/OpenGamma/Strata/issues/1576)
* Enhancement - Update to Joda-Beans v2.0.2  [#1575](https://github.com/OpenGamma/Strata/issues/1575)
* Enhancement - Handle single digit hours in loader [#1574](https://github.com/OpenGamma/Strata/issues/1574)


## Strata v1.4.1

*4 October 2017*

This minor release contains 7 fixed issues.

* Enhancement - Parse variable notional/rates [#1572](https://github.com/OpenGamma/Strata/issues/1572)
* Enhancement - New Asian Exchanges [#1571](https://github.com/OpenGamma/Strata/issues/1571)
* Enhancement - CsvInfoResolver [#1570](https://github.com/OpenGamma/Strata/issues/1570)
* Enhancement - Synthetic calibrator: typed market data object [#1568](https://github.com/OpenGamma/Strata/issues/1568)
* Bug fix - Fix CurrencyAmountArray minus() bug [#1569](https://github.com/OpenGamma/Strata/issues/1569)
* Bug fix - Remove duplicate dependency
* Bug fix - Update Joda-Convert dependency [#](https://github.com/OpenGamma/Strata/issues/1539)


## Strata v1.4.0

*21 September 2017*

This release contains [35 fixed issues](https://github.com/OpenGamma/Strata/milestone/14?closed=1).
This includes the issues fixed in v1.3.1, v1.3.2 and v1.3.3 (see below).

* Standard CSV format for trades and positions
[#1540](https://github.com/OpenGamma/Strata/pull/1540),
[#1556](https://github.com/OpenGamma/Strata/pull/1556),
[#1559](https://github.com/OpenGamma/Strata/pull/1559),
[#1551](https://github.com/OpenGamma/Strata/pull/1551)
* Loader for legal entity rates
[#1516](https://github.com/OpenGamma/Strata/pull/1516)
* Add `CHF-SARON` overnight index
[#1557](https://github.com/OpenGamma/Strata/pull/1557)
* Add `DEFR` Frankfurt holidays
[#1560](https://github.com/OpenGamma/Strata/pull/1560)
* Default fixed leg day count from index
[#1553](https://github.com/OpenGamma/Strata/pull/1553)
* Allow `FxIndex` to return fixing and maturity days offset, using it to default on `FxResetCalculation`
[#1536](https://github.com/OpenGamma/Strata/pull/1536)
* Allow notional exchange to be set separately from FX reset
[#1542](https://github.com/OpenGamma/Strata/pull/1542)
* Support fixed initial notional of FX reset swaps
[#1543](https://github.com/OpenGamma/Strata/pull/1543)
* Abstraction over swap conventions
[#1533](https://github.com/OpenGamma/Strata/pull/1533)
* Enhance `FloatingRateName` parsing to better link with the indices
[#1549](https://github.com/OpenGamma/Strata/pull/1549)
* Add `NamedEnum` to mark standard enums and make parsing more lenient
[#1532](https://github.com/OpenGamma/Strata/pull/1532)
* Custom logic when resolving a swap trade
[#1544](https://github.com/OpenGamma/Strata/pull/1544)
* Code from CERN Clot is now included (shaded) to reduce dependencies
[#1529](https://github.com/OpenGamma/Strata/pull/1529),
[#1530](https://github.com/OpenGamma/Strata/pull/1530)
* Update dependencies. The `strata-parent` project can now be used as a BOM.

#### Compatibility

The classes `RepoGroup` and `LegalEntityGroup` moved packages.

The Joda-Beans dependency was updated to v2.0.
This is major version upgrade and any beans you have will need to be regenerated.

In the unlikely event that you have a swap convention implementation, you may need
to change it to extend `SingleCurrencySwapConvention`.

In the unlikely event that you have an `FxIndex` implementation, you will need to
implement the two new methods.

In the unlikely event that you have a `ScenarioPerturbation` implementation, you will
need to implement one additional method.



## Strata v1.3.3

*31 July 2017*

This minor release contains 1 fixed issue.

* Bug fix - Inflation swap conventions:
[#1539](https://github.com/OpenGamma/Strata/issues/1539),
[#1535](https://github.com/OpenGamma/Strata/issues/1535)


## Strata v1.3.2

*28 June 2017*

This minor release contains 2 fixed issues - 1 bug fix and 1 enhancement.

* Bug fix - Schedule generation enhancements:
[#1526](https://github.com/OpenGamma/Strata/issues/1526),
[#1527](https://github.com/OpenGamma/Strata/issues/1527)
* Enhancement - Update Joda-Convert to v1.8.2


## Strata v1.3.1

*26 June 2017*

This minor release contains 2 fixed issues - 1 bug fix and 1 enhancement.

* Bug fix - Floating rate names for MXN were not processed correctly: [#1523](https://github.com/OpenGamma/Strata/issues/1523)
* Enhancement - Add low level ArrayByteSource utility class: [#1524](https://github.com/OpenGamma/Strata/issues/1524)


## Strata v1.3

*5 May 2017*

This release contains [19 fixed issues](https://github.com/OpenGamma/Strata/milestone/13?closed=1).

* Domain model for ETD futures/options
[#1488](https://github.com/OpenGamma/Strata/pull/1488),
[#1496](https://github.com/OpenGamma/Strata/pull/1496),
[#1497](https://github.com/OpenGamma/Strata/pull/1497),
[#1508](https://github.com/OpenGamma/Strata/pull/1508)
* More lenient schedule calculator
[#1515](https://github.com/OpenGamma/Strata/pull/1515)
* Better support for Unicode file formats
[#1511](https://github.com/OpenGamma/Strata/pull/1511),
[#1514](https://github.com/OpenGamma/Strata/pull/1514)

#### Compatibility

The method `DiscountingCapitalIndexedBondProductPricer::zSpreadFromCurvesAndPV` was renamed to
`DiscountingCapitalIndexedBondProductPricer::zSpreadFromCurvesAndPv`, with the old name deprecated.

The Joda-Beans dependency was updated, and some methods are now deprecated.
It is unlikely that these methods were in use, but if they were, consult the Joda-Beans documentation.

The quantile calculation methods have changed return type, but these are in an internal package
and should not have been used directly.



## Strata v1.2

*8 March 2017*

This release contains [61 fixed issues](https://github.com/OpenGamma/Strata/milestone/12?closed=1) -
9 of which are bug fixes.

* Refactor CDS
 [#1466](https://github.com/OpenGamma/Strata/issues/1466),
 [#1474](https://github.com/OpenGamma/Strata/issues/1474)
* Caplet stripping: direct and SABR:
 [#1448](https://github.com/OpenGamma/Strata/issues/1448),
 [#1422](https://github.com/OpenGamma/Strata/issues/1422)
* Enhance CalculationListener:
 [#1454](https://github.com/OpenGamma/Strata/issues/1454),
 [#1455](https://github.com/OpenGamma/Strata/issues/1455),
 [#1458](https://github.com/OpenGamma/Strata/issues/1458)
* Remove Easter Monday from CATO calendar:
 [#1440](https://github.com/OpenGamma/Strata/issues/1440)
* Add inflation seasonality in curves:
 [#1465](https://github.com/OpenGamma/Strata/issues/1465)
* Smith-Wilson method:
 [#1484](https://github.com/OpenGamma/Strata/issues/1484)
* Add holidays and indices for CZK, ZAR, HUF, MXN, BRL and DKK-CIBOR2-DKNA13:
 [#1428](https://github.com/OpenGamma/Strata/issues/1428),
 [#1429](https://github.com/OpenGamma/Strata/issues/1429),
 [#1445](https://github.com/OpenGamma/Strata/issues/1445),
 [#1435](https://github.com/OpenGamma/Strata/issues/1435),
 [#1491](https://github.com/OpenGamma/Strata/issues/1491)
* Enhance indices, FloatingRateName and enum lookup:
 [#1438](https://github.com/OpenGamma/Strata/issues/1438),
 [#1442](https://github.com/OpenGamma/Strata/issues/1442),
 [#1436](https://github.com/OpenGamma/Strata/issues/1436)
* Allow base sensitivity to be split:
 [#1424](https://github.com/OpenGamma/Strata/issues/1424)
* Interpolator calculations supplied on demand:
 [#1463](https://github.com/OpenGamma/Strata/issues/1463),
 [#1464](https://github.com/OpenGamma/Strata/issues/1464)
* Add support for overriding first fixing offset and first rate:
 [#1447](https://github.com/OpenGamma/Strata/issues/1447),
 [#1453](https://github.com/OpenGamma/Strata/issues/1453)


#### Compatibility

The following incompatible changes have been made:

* CDS code has been rewritten from scratch and has an entirely new API (as warned in advance in v1.1)
* A new interface `CurveDefinition` has been added above `NodalCurveDefinition`, with `CurveGroupDefinition` making use of it. Only code that queried `CurveGroupDefinition` will break.
* A number of methods have moved from `IborIndex` and `OvernightIndex` to the parent interface `RateIndex`. Only code that implemented `RateIndex` will break.
* A new method was added to an interface, `FloatingRateName.normalized()`. Only code that implemented `FloatingRateName` will break.
* A new method was added to an interface, `RateIndex.getFloatingRateName()`. Only code that implemented `RateIndex` will break.
* A new method was added to an interface, `PriceIndex.getFloatingRateName()`. Only code that implemented `PriceIndex` will break.
* A new method was added to an interface, `DiscountFactors.discountFactorTimeDerivative()`. Only code that implemented `DiscountFactors` will break.

In general, we try to maintain backwards compatibility.
We break compatibility mainly in areas where a change is likely to have minimal impact yet produce clearer, cleaner code.


## Strata v1.1.2

*3 November 2016*

This minor release contains 5 fixed issues - 1 bug fix and 4 enhancements.

* Bug fix - Example should output to target directory: [#1404](https://github.com/OpenGamma/Strata/issues/1404)
* Enhancement - Inflation seasonality: [#1407](https://github.com/OpenGamma/Strata/issues/1407)
* Enhancement - Enhance schedule generation: [#1403](https://github.com/OpenGamma/Strata/issues/1403)
* Enhancement - Add SCALED shift type: [#1402](https://github.com/OpenGamma/Strata/issues/1402)
* Enhancement - More example: [#1391](https://github.com/OpenGamma/Strata/issues/1391)


## Strata v1.1.1

*20 October 2016*

This minor release contains 8 fixed issues - 3 bug fixes and 5 enhancements.

* Bug fix - No scaling is applied to single-node bucketed gamma in the measures API: [#1383](https://github.com/OpenGamma/Strata/issues/1383)
* Bug fix - ExplainKey.FROM_FIXING_SERIES is only populated if the fixing date equals the valuation date: [#1380](https://github.com/OpenGamma/Strata/issues/1380)
* Bug fix - Measure is not Joda-convertible: [#1386](https://github.com/OpenGamma/Strata/issues/1386)
* Enhancement - Add serializable interface: [#1393](https://github.com/OpenGamma/Strata/issues/1393)
* Enhancement - Added GBP/EUR cross-currency convention: [#1390](https://github.com/OpenGamma/Strata/issues/1390)
* Enhancement - Support single-node bucketed gamma for BulletPaymentTrade: [#1382](https://github.com/OpenGamma/Strata/issues/1382)
* Enhancement - Add ValueWithFailures: [#1396](https://github.com/OpenGamma/Strata/issues/1396)
* Enhancement - Allow Strata to be on the classpath more than once: [#1394](https://github.com/OpenGamma/Strata/issues/1394)


## Strata v1.1

*7 October 2016*

This release contains [62 fixed issues](https://github.com/OpenGamma/Strata/milestone/11?closed=1) -
15 of which are bug fixes.

The key features are:

* Measure-level and Calc-level API support for all asset classes:
[#1263](https://github.com/OpenGamma/Strata/issues/1263), 
[#1344](https://github.com/OpenGamma/Strata/issues/1344), 
[#1331](https://github.com/OpenGamma/Strata/issues/1331)
* Additional holiday calendars and indices for SEK, DKK and PLN:
[#1373](https://github.com/OpenGamma/Strata/issues/1373),
[#1326](https://github.com/OpenGamma/Strata/issues/1326)
* Enhanced performance for swap pricing:
[#1293](https://github.com/OpenGamma/Strata/issues/1293),
[#1329](https://github.com/OpenGamma/Strata/issues/1329)
* More flexible loaders:
[#1267](https://github.com/OpenGamma/Strata/issues/1267),
[#1269](https://github.com/OpenGamma/Strata/issues/1269),
[#1245](https://github.com/OpenGamma/Strata/issues/1245),
[#1249](https://github.com/OpenGamma/Strata/issues/1249),
[#1282](https://github.com/OpenGamma/Strata/issues/1282)
* Support FpML parameterized notional schedule:
[#1242](https://github.com/OpenGamma/Strata/issues/1242)
* Enhanced explain present value:
[#1256](https://github.com/OpenGamma/Strata/issues/1256),
[#1270](https://github.com/OpenGamma/Strata/issues/1270),
[#1362](https://github.com/OpenGamma/Strata/issues/1362)
* Better error messages:
[#1280](https://github.com/OpenGamma/Strata/issues/1280),
[#1275](https://github.com/OpenGamma/Strata/issues/1275),
[#1225](https://github.com/OpenGamma/Strata/issues/1225),
[#1254](https://github.com/OpenGamma/Strata/issues/1254)
* FRA payment dates are now calculated correctly:
[#1301](https://github.com/OpenGamma/Strata/issues/1301)

Feel free to give us feedback or ask a question in the [forums](http://forums.opengamma.com/).

#### Compatibility

This release is backwards compatible except for bond pricing.
A total of 14 methods were marked as deprecated, all with documented replacements.

The backwards incompatibility in bond pricing is unfortunate.
The changes were necessary to enable bond pricing integration into the calculation-level API.
It also allow us to add pricing for Bills in the future.
Migration will mostly consist of simple renames, see this
[pull request](https://github.com/OpenGamma/Strata/pull/1368) for more details.


As an advance warning, the CDS code is likely to change in a backwards incompatible way
in release v1.2. However, it remains our goal to avoid incompatibility as far as reasonably possible.


## Strata v1.0

*15 July 2016*

The first full release of Strata, after two years of development.
Strata is already in use in production and has now reached the point where v1.0 is appropriate.

The key features are:

* Measure-level API - a high level API calculating measures for one trade
* Calc-level API - a high level API calculating measures for a mixed portfolio of trades
* Pricer-level API - a low level API performing calculations for one trade
* Market data structures - representations of curves, surfaces and other kinds of market data
* Product domain model - beans representing different financial instruments
* Conventions, indices, and holiday calendars for common markets

The supported asset classes are:

* Swap - including Vanilla, OIS, Basis, Inflation, Cross Currency and Variable Notional
* Deliverable Swap Future (DSF)
* Constant Maturity Swap (CMS)
* Ibor cap/floor
* Swaptions
* Forward Rate Agreement (FRA)
* FX forward/spot - including Non-Delivered Forward (NDF)
* FX swap
* FX options - vanilla and single barrier
* STIR futures/options
* Bonds - Fixed coupon and Capital indexed
* Bond futures/option
* Term deposit
* Bullet payment
* CDS - currently being reviewed and subject to incompatible change

Feel free to give us feedback or ask a question in the [forums](http://forums.opengamma.com/).
   
  

----

## Strata v0.16

*5 July 2016*

This release prepares the way for v1.0, which will be the next release.
This primarily involved fixing bugs and mistakes in the API.

* Calculation API tightened to clearly separate scenario from non-scenario
* DSF based on standard market price, not decimal/fractional price
* Curve calibration with a Fed-Fund swap
* More control over IborFuture curve nodes
* Add calendar and indices for Norway
* Fixed inflation swap conventions
* Scenario generation API refactored
* New surface interpolators - surface data must now be sorted
* Renamed term deposit conventions
* Renamed scenario return types, eg. CurrencyValuesArray to CurrencyScenarioArray
* Restructured examples
* Removed implementation-specific classes from public API

Feel free to ask a question in the forums if you have difficulty porting code from v0.15 to v0.16.


## Strata v0.15

*17 June 2016*

This release contains a new measures API.
The measures API is intended to be the main access to the functionality of Strata.
Applications currently using the pricer API should consider using the measures API instead.

For example, consider using `SwapTradeCalculations` instead of `DiscountingSwapTradePricer`.

* New measures API
* Extended set of measures access via the calculation API
* Renamed PV01 measures
* Add a calculator to obtain the notional equivalent
* Add currency exposure and current cash to some instruments
* Add support for known amount stubs on swaps (fixed and ibor legs)

Feel free to ask a question in the forums if you have difficulty porting code from v0.14 to v0.15.


## Strata v0.14

*9 June 2016*

This release contains a major simplification of the calculation API.
The "rules" part of the calculation API has been replaced with a "parameter" concept,
for example `RatesMarketDataLookup` that selects from the complete set of market data.
The new design is far simpler, with logic moved out of the framework and into code that applications
can control and extend. The results model now includes column headers.
The calculation runner and market data factory are both affected.

There has also been significant refactoring of packages, module structure and market data.
Separate curve and surface sensitivity objects have been combined.
Scenario market data is now more widely available, with the `MarketDataKey` concept removed.
The `strata-function` project has been renamed to `strata-measure`.
The goal has been to provide a structure that will last Strata in the long term.
v1.0 is approaching and expected at the end of June and will provide backwards compatible API stability.

* Simplified and extensible calculation API
* Curve sensitivity rebucketing
* FX single barrier option trade model and pricer
* FX vanilla option Vanna Volga pricer
* SABR swaption calibrator
* Additional swap conventions
* Abstraction for market data parameters

Feel free to ask a question in the forums if you have difficulty porting code from v0.12 to v0.14.


## Strata v0.12

*11 April 2016*

This release contains a major rework of the security model to introduce positions.
`GenericFuture` and `GenericFutureOption` have gone, with `GenericSecurity` in use instead.
A new `Security` interface is added, with implementations that refer to other securities by identifier.
There is also a new `Position` interface with `SecurityPosition` and `GenericSecurityPosition` implementations.
The next release will be v0.14, not v1.0.

* New security and position domain model
* Replaced generic future/option by generic security
* Inflation swap conventions
* Canadian holidays and indices
* Improved FX rate triangulation
* Enhanced examples

Feel free to ask a question in the forums if you have difficulty porting code from v0.11 to v0.12.


## Strata v0.11

*18 March 2016*

This release contains a major rework of the trade model to introduce reference data.
Holiday calendars are now treated as data, referenced by an identifier.
Securities can also now be referenced by identifier, although only for mark-to-market pricing at present.
While there will no doubt be further trade model tweaks before v1.0, this set of changes should be by far the largest.
The holiday calendar data provided with Strata is now available using `ReferenceData.standard()`.
These changes also caused `StandardId` to change package.
The next release will be v0.12, not v1.0.

* New asset classes - Capital Indexed Bonds
* Refactored trade model treating holidays and securities as reference data
* Added dedicated index observation objects for querying market data
* Type-safe attributes can be attached to trades
* Add Canadian holidays and indices
* Allow holiday calendars to be queried beyond known dates

Feel free to ask a question in the forums if you have difficulty porting code from v0.10 to v0.11.


## Strata v0.10

*29 February 2016*

Additional preparatory work for v1.0. The next release will be v0.11, not v1.0.
The next release will contain a significant refactoring of the trade model to allow holidays
to be managed as reference data.

* New asset classes - CMS, CMS cap/floor and Ibor cap/floor
* Calculation function design simplified, with all functions operating as multi-measure
* Enhance FX conversion of function results
* Enhanced FpML parsing, including inflation swaps
* Control over the date generated for each node in curve calibration
* Synthetic curve calibrator, calibrating on synthetic instruments
* Schedule generation handling all-stub schedules, plus performance tweaks


## Strata v0.9

*14 January 2016*

Additional preparatory work for v1.0.

* Simpler calculation runner concept for calculations with many trades, many measures or many scenarios
* Unified pricing for Swaptions, with present value available via the calculation runner
* Add currency exposure to pricers
* Use data files to define holidays and indices
* Update interpolators and extrapolators
* Efficient data structures for large scenarios


## Strata v0.8

*19 November 2015*

A major update that brings functionality much closer to that needed for v1.0.

* Curve calibration
* New asset classes - FX Forward, FX Swap, FX NDF, Term Deposit, Deliverable Swap Futures, Ibor STIR Futures, Bullet Payment
* Pricing level support for Swaptions, Bonds, FX vanilla options, Bond Futures, Bond Future Options, STIR Future Options (Ibor)
* Loader project, allowing data to be loaded from XML and CSV formats
* Reporting framework promoted from Beta
* Removed dependency on legacy Analytics codebase


## Strata v0.7

*25 June 2015*

The initial release.

* Calculation engine, calculating risk measures, managing market data and scenarios
* Product definitions
* Foundations, including day counts, schedules, holidays and indices
* Asset classes - FRA, Interest Rate Swap, Generic Futures, Generic Future Options, Credit Default Swap
