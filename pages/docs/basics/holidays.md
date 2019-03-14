---
title: Holidays
permalink: /holidays/
---

A key problem when working with dates is the impact of holidays and weekends.
To manage this complexity, a *holiday calendar* is used.

A holiday calendar implementation keeps track of which dates are holidays and which are weekends.
Different countries have different holiday dates and thus different calendars.
It is not unusual for individual exchanges or other financial entities to have their own calendar.


## Holiday Calendar

The `strata-basics` module includes a holiday calendar interface and some common implementations.
The key interface is `HolidayCalendar` which defines methods to query the calendar.
The calendar is accessed via an identifier `HolidayCalendarId`.

Each holiday calendar has a unique identifier.
To obtain the identifier from a string, use `HolidayCalendarId.of(String)`

The actual holiday calendar can then be obtained from [`ReferenceData`]({{site.baseurl}}/reference_data):

```java
HolidayCalendarId holCalId = HolidayCalendarId.of("GBLO");
HolidayCalendar holCal = holCalId.resolve(ReferenceData.standard());
```

A holiday calendar can also be obtained using a currency:

```java
HolidayCalendarId holCalId = HolidayCalendarId.defaultByCurrency(Currency.USD);
```

The `ReferenceData` provided separation between the identifier and the holiday calendar.
This allows users of Strata to supply their own holiday calendar data.
To aid evaluation, Strata provides some [standard holiday calendars]({{site.baseurl}}/holiday_data) 
and a mapping from [currencies to holiday calendars]({{site.baseurl}}/holiday_data).

All available holiday calendars can be listed using the static method  `HolidayCalendarId.extendedEnum()`.

Common holiday calendars can also be obtained using static constants on `HolidayCalendarIds`:

```java
HolidayCalendarId holCalId = HolidayCalendarIds.GBLO;
```

Once a holiday calendar is obtained, various methods are available to query the calendar.
Some key methods are shown here, see the Javadoc for more information:

```java
// is the date a holiday/weekend or a business day
boolean holiday = holCal.isHoliday(LocalDate);
boolean busday  = holCal.isBusinessDay(LocalDate);
    
// next/previous business day
LocalDate nextDay = holCal.next(LocalDate);
LocalDate nextDay = holCal.nextOrSame(LocalDate);
LocalDate prevDay = holCal.previous(LocalDate);
LocalDate prevDay = holCal.previousOrSame(LocalDate);
    
// last business day of month
boolean lastBusDay   = holCal.isLastBusinessDayOfMonth(LocalDate);
LocalDate lastBusDay = holCal.lastBusinessDayOfMonth(LocalDate);
    
// number of business days
int days = holCal.daysBetween(LocalDate, LocalDate)
```

Note that when querying dates, there is no difference between a holiday and a weekend.


## Standard Holiday Calendars

Strata provides a set of [standard holiday calendars]({{site.baseurl}}/holiday_data).

## Default Currency Holiday Calendars

Strata provides a set of [default holiday calendars]({{site.baseurl}}/holiday_data) for each currency.
