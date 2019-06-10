---
title: Common values
permalink: /common_values/
---

The CSV loaders have some common values, detailed below:

### Currency

Currencies are specified using the standard three letter ISO-4217 code.
The following currencies have been fully defined in Strata:

AED, ARS, AUD, BGN, BHD, BRL, CAD, CHF, CLP, CNY, COP, CZK, DKK, EGP, EUR, GBP, HKD, HRK, HUF, IDR, ILS, INR, ISK, JPY, KRW, MXN, MYR, NOK, NZD, PEN, PHP, PKR, PLN, RON, RUB, SAR, SEK, SGD, THB, TRY, TWD, UAH, USD, ZAR, XXX, XAG, XAU, XPD, XPT, 

In addition, these historic EUR currencies are defined:

ATS, BEF, CYP, DEM, EEK, ESP, FIM, FRF, GRD, IEP, ITL, LTL, LUF, LVL, MTL, NLG, PTE, SIT, SKK

Other currencies can be used, but may not have the correct number of fractional digits.


### Day Count

See the [day counts]({{site.baseurl}}/day_counts/) page.


### Business Day Convention

The loaders support the following values:

| Standard value               | Valid alternatives         | Notes |
|------------------------------|----------------------------|-------|
| `NoAdjust`                   | `None`                     | Case insensitive |
| `Following`                  | `F`, `Follow`              | Case insensitive |
| `ModifiedFollowing`          | `M`, `MF`, `Modified`, `ModFollowing`| Can replace `Following` with `Follow`. Case insensitive |
| `Preceding`                  | `P`                        | Case insensitive |
| `ModifiedPreceding`          | `MP`, `ModPreceding`       | Case insensitive |
| `Nearest`                    |                            | Case insensitive |
| `ModifiedFollowingBiMonthly` | `ModFollowingBiMonthly`    | Can replace `Following` with `Follow`. Case insensitive |

A space or an underscore can also be used between any two words.
For example, `Modified Following` and `MODIFIED_PRECEDING` are also valid.

See also the [date adjustments]({{site.baseurl}}/date_adjustments/) page.


### Stub Convention

The loaders support the following values:

| Standard value  | Valid alternatives         | Notes |
|-----------------|----------------------------|-------|
| `SmartInitial`  | `SMART_INITIAL`            | Case insensitive |
| `ShortInitial`  | `SHORT_INITIAL`            | Case insensitive |
| `LongInitial`   | `LONG_INITIAL`             | Case insensitive |
| `SmartFinal`    | `SMART_FINAL`              | Case insensitive |
| `ShortFinal`    | `SHORT_FINAL`              | Case insensitive |
| `LongFinal`     | `LONG_FINAL`               | Case insensitive |
| `None`          | `NONE`                     | Case insensitive |
| `Both`          | `BOTH`                     | Case insensitive |

See also the [schedules]({{site.baseurl}}/schedules/) page.


### Roll Convention

The loaders support the following values:

| Standard value  | Valid alternatives         | Notes |
|-----------------|----------------------------|-------|
| `None`          |                            | Case insensitive |
| `Day1`          | `Day_1`, `1`               | Case insensitive |
| `Day2` to `Day27`| `Day_2`, `Day_3` etc, `2`, `3`, etc | Case insensitive |
| `Day28`         | `Day_28`, `28`             | Case insensitive |
| `Day29`         | `Day_29`, `29`             | Case insensitive |
| `Day30`         | `Day_30`, `30`             | Case insensitive |
| `EOM`           | `Day31`, `Day_31`, `31`    | Case insensitive |
| `IMM`           |                            | Case insensitive |
| `IMMCAD`        |                            | Case insensitive |
| `IMMAUD`        |                            | Case insensitive |
| `IMMNZD`        |                            | Case insensitive |
| `SFE`           |                            | Case insensitive |
| `TBILL`         |                            | Case insensitive |
| `DayMon`        | `Day_Mon`, `Mon`           | Case insensitive |
| `DayTue`        | `Day_Tue`, `Tue`           | Case insensitive |
| `DayWed`        | `Day_Wed`, `Wed`           | Case insensitive |
| `DayThu`        | `Day_Thu`, `Thu`           | Case insensitive |
| `DayFri`        | `Day_Fri`, `Fri`           | Case insensitive |
| `DaySat`        | `Day_Sat`, `Sat`           | Case insensitive |
| `DaySun`        | `Day_Sun`, `Sun`           | Case insensitive |

See also the [schedules]({{site.baseurl}}/schedules/) page.


### Buy/Sell

The loaders support the following values:

| Standard value  | Valid alternatives         | Notes |
|-----------------|----------------------------|-------|
| `Buy`           | `B`                        | Case insensitive |
| `Sell`          | `S`                        | Case insensitive |


### Pay/Receive

| Standard value  | Valid alternatives         | Notes |
|-----------------|----------------------------|-------|
| `Pay`           | `P`                        | Case insensitive |
| `Receive`       | `Rec`, `R`                 | Case insensitive |


### Put/Call

| Standard value  | Valid alternatives         | Notes |
|-----------------|----------------------------|-------|
| `Put`           | `P`                        | Case insensitive |
| `Call`          | `C`                        | Case insensitive |


### Long/Short

| Standard value  | Valid alternatives         | Notes |
|-----------------|----------------------------|-------|
| `Long`          | `L`                        | Case insensitive |
| `Short`         | `S`                        | Case insensitive |
