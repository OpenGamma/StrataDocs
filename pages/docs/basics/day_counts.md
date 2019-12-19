---
title: Day Counts
permalink: /day_counts/
---

A *day count* is used to convert dates to a numeric representation for financial maths.

A date consists of 12 months of varying lengths and occasional leap days.
As a result of this variation there are many possible ways to convert the amount of time between
two dates into a number. While counting the number of days between two dates is simple, there
are many different ways to convert the amount of time to a fraction of a year.
Each day count specifies a specific set of rules for the conversion.
Different rules are used in different markets and for different products.

The standard approach is based on converting the period between two dates to a *year fraction*.
A year fraction is a floating point number, where one year is represented by 1 and half a year by 0.5.

Most day counts are relatively simple, operating solely on the two dates, returning the year fraction.
Some day counts are more complicated, needing additional information about an associated schedule.

See [Wikipedia](https://en.wikipedia.org/wiki/Day_count_convention) for more background information.


## Day Count

The `strata-basics` project includes a comprehensive implementation of day count conventions.
The key interface is `DayCount` which defines methods to obtain and query a specific day count.

Each day count implementation has a unique name.
This can be used to obtain the day count via the static method `DayCount.of(String)`:

```java
DayCount dayCount = DayCount.of("Act/360");
```

All available day counts can be listed using the static method  `DayCount.extendedEnum()`.

Common day counts can also be obtained using static constants on `DayCounts`:

```java
DayCount dayCount = DayCounts.ACT_360;
```

Once a day count is obtained, two methods are available to obtain the year fraction:

```java
double yf = dayCount.yearFraction(LocalDate, LocalDate);
double yf = dayCount.yearFraction(LocalDate, LocalDate, ScheduleInfo);
```

Both methods convert the period of time between two dates to a floating point number.
The first handles all simple day counts, the second allows additional information about the schedule to be passed in.

> Certain day count implementations cannot give an answer without the schedule information.
> As such, those implementations will throw an exception when called without `ScheduleInfo`.


## Standard Day Counts

The following standard day counts have been implemented.
Each has a string name which acts as a unique key to obtain the day count.
They are also available as constants on the `DayCounts` class.
For more information on each, see the Javadoc of `DayCounts`:

### Actual/360

<table>
<tr>
  <th>Name</th>
  <td>Act/360</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ACT_360</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days by 360</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is a simple division.<br />
The numerator is the actual number of days in the requested period.<br />
The denominator is always 360.</td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'French'</td>
</tr>
<tr>
  <th>Definition</th>
  <td>2006 ISDA definitions 4.16e and ICMA rule 251.1(i) part 1</td>
</tr>
</table>


### Actual/364

<table>
<tr>
  <th>Name</th>
  <td>Act/364</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ACT_364</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days by 364</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is a simple division.<br />
The numerator is the actual number of days in the requested period.<br />
The denominator is always 364.</td>
</tr>
</table>


### Actual/365 Fixed

<table>
<tr>
  <th>Name</th>
  <td>Act/365F</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ACT_365F</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days by 365</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is a simple division.<br />
The numerator is the actual number of days in the requested period.<br />
The denominator is always 365.</td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'English' or `AFI/365`</td>
</tr>
<tr>
  <th>Definition</th>
  <td>2006 ISDA definitions 4.16d</td>
</tr>
</table>


### Actual/365 Actual

<table>
<tr>
  <th>Name</th>
  <td>Act/365 Actual</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ACT_365_ACTUAL</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days by 366 if a leap day is contained, or by 365 if not</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is a simple division.<br />
The numerator is the actual number of days in the requested period.<br />
The denominator is 366 if the period contains February 29th, if not it is 365.<br />
The first day in the period is excluded, the last day is included.</td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'Act/365A'</td>
</tr>
</table>

### Actual/365 Long

<table>
<tr>
  <th>Name</th>
  <td>Act/365L</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ACT_365L</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days by 365 or 366</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is a simple division.<br />
The numerator is the actual number of days in the requested period.<br />
The denominator is determined by examining the frequency and the period end date (the date of the next coupon).<br />
If the frequency is annual then the denominator is 366 if the period contains February 29th, if not it is 365.<br />
The first day in the period is excluded, the last day is included.<br />
If the frequency is not annual, the denominator is 366 if the period end date is in a leap year, if not it is 365.</td>
</tr>
<tr>
  <th>Schedules</th>
  <td>This day count requires <code>ScheduleInfo</code></td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'Act/365 Leap year'</td>
</tr>
<tr>
  <th>Definition</th>
  <td>2006 ISDA definitions 4.16i and ICMA rule 251.1(i) part 2 as later clarified by ICMA and Swiss Exchange</td>
</tr>
</table>

### Actual/365.25

<table>
<tr>
  <th>Name</th>
  <td>Act/365.25</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ACT_365_25</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days by 365.25</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is a simple division.<br />
The numerator is the actual number of days in the requested period.<br />
The denominator is always 365.25.</td>
</tr>
</table>

### NL/365

<table>
<tr>
  <th>Name</th>
  <td>NL/365</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.NL_365</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days omitting leap days by 365</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is a simple division.<br />
The numerator is the actual number of days in the requested period minus the number of occurrences of February 29.<br />
The denominator is always 365.<br />
The first day in the period is excluded, the last day is included.</td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'Act/365 No Leap'</td>
</tr>
</table>

### Actual/Actual ISDA

<table>
<tr>
  <th>Name</th>
  <td>Act/Act ISDA</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ACT_ACT_ISDA</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days in a leap year by 366 and the actual number of days in a standard year by 365</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is calculated in two parts.<br />
The actual number of days in the requested period that fall in a leap year is divided by 366.<br />
The actual number of days in the requested period that fall in a standard year is divided by 365.<br />
The result is the sum of the two.<br />
The first day in the period is included, the last day is excluded.</td>
</tr>
<tr>
  <th>Definition</th>
  <td>2006 ISDA definitions 4.16b</td>
</tr>
</table>

### Actual/Actual ICMA

<table>
<tr>
  <th>Name</th>
  <td>Act/Act ICMA</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ACT_ACT_ICMA</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days by the actual number of days in the coupon period multiplied by the frequency</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is calculated as follows.<br />
First, the underlying schedule period is obtained treating the first date as the start of the schedule period.<br />
Second, if the period is a stub, then nominal regular periods are created matching the
schedule frequency, working forwards or backwards from the known regular schedule date.<br />
An end-of-month flag is used to handle month-ends.<br />
If the period is not a stub then the schedule period is treated as a nominal period below.<br />
Third, the result is calculated as the sum of a calculation for each nominal period.<br />
The actual days between the first and second date are allocated to the matching nominal period.<br />
Each calculation is a division. The numerator is the actual number of days in
the nominal period, which could be zero in the case of a long stub.<br />
The denominator is the length of the nominal period  multiplied by the frequency.<br />
The first day in the period is included, the last day is excluded.</td>
</tr>
<tr>
  <th>Schedules</th>
  <td>This day count requires <code>ScheduleInfo</code></td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'ISMA-99' or 'ICM/ACT'</td>
</tr>
<tr>
  <th>Definition</th>
  <td>2006 ISDA definitions 4.16c and ICMA rule 251.1(iii) and 251.3 as
<a href="https://www.isda.org/a/AIJEE/1998-ISDA-memo-%E2%80%9CEMU-and-Market-Conventions-Recent-Developments%E2%80%9D.pdf">later clarified</a> by ISDA</td>
</tr>
</table>

### Actual/Actual AFB

<table>
<tr>
  <th>Name</th>
  <td>Act/Act AFB</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ACT_ACT_AFB</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days by 366 if a leap day is contained, or by 365 if not,
with additional rules for periods over one year</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is a simple division.<br />
The numerator is the actual number of days in the requested period.<br />
The denominator is determined by examining the period end date (the date of the next coupon).<br />
The denominator is 366 if the schedule period contains February 29th, if not it is 365.<br />
The first day in the schedule period is included, the last day is excluded.<br />
Read the Javadoc for a discussion of the algorithm, the
<a href="http://www.acp.banque-france.fr/fileadmin/user_upload/banque_de_france/archipel/publications/bdf_bof/bdf_bof_1999/bdf_bof_01.pdf">original French text</a>
and confusion with the <a href="https://www.isda.org/a/pIJEE/The-Actual-Actual-Day-Count-Fraction-1999.pdf">ISDA clarification</a>.</td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'Base Exact/Exact' or 'EXA/EXA'</td>
</tr>
<tr>
  <th>Definition</th>
  <td>Association Francaise des Banques in September 1994 as 'Base Exact/Exact' in 'Definitions Communes plusieurs Additifs Techniques'</td>
</tr>
</table>

### Actual/Actual Year

<table>
<tr>
  <th>Name</th>
  <td>Act/Act Year</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ACT_ACT_YEAR</td>
</tr>
<tr>
  <th>Summary</th>
  <td>Divides the actual number of days by the actual number of days in the year from the start date</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is calculated in two parts - a number of whole years and the remaining part.<br />
If the period is over one year, a number of years is added to the start date to reduce
the remaining period to less than a year. If the start date is February 29th, then each
time a year is added the last valid day in February is chosen.<br />
The remaining period is then processed by a simple division.<br />
The numerator is the actual number of days in the remaining period.<br />
The denominator is the actual number of days in the year from the adjusted start date.<br />
The first day in the period is included, the last day is excluded.<br />
The result is the number of whole years plus the result of the division.</td>
</tr>
</table>

### 30/360 ISDA

<table>
<tr>
  <th>Name</th>
  <td>30/360 ISDA</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.THIRTY_360_ISDA</td>
</tr>
<tr>
  <th>Summary</th>
  <td>A 30/360 style algorithm with special rules for the 31st day-of-month</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is calculated as <code>(360 * deltaYear + 30 * deltaMonth + deltaDay) / 360</code>.<br />
The deltaDay is then calculated once day-of-month adjustments have occurred.<br />
If the second day-of-month is 31 and the first day-of-month is 30 or 31, change the second day-of-month to 30.<br />
If the first day-of-month is 31, change the first day-of-month to 30.</td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'30/360 U.S. Municipal' or '30/360 Bond Basis'</td>
</tr>
<tr>
  <th>Definition</th>
  <td>2006 ISDA definitions 4.16f.</td>
</tr>
</table>

### 30U/360

<table>
<tr>
  <th>Name</th>
  <td>30U/360</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.THIRTY_U_360</td>
</tr>
<tr>
  <th>Summary</th>
  <td>A 30/360 style algorithm with special rules for the 31st day-of-month and the end of February</td>
</tr>
<tr>
  <th>Description</th>
  <td>
    The result is calculated as <code>(360 * deltaYear + 30 * deltaMonth + deltaDay) / 360</code>.<br />
The deltaDay is then calculated once day-of-month adjustments have occurred.<br />
If the schedule uses EOM convention and both dates are the last day of February, change the second day-of-month to 30.<br />
If the schedule uses EOM convention and the first date is the last day of February, change the first day-of-month to 30.<br />
If the second day-of-month is 31 and the first day-of-month is 30 or 31, change the second day-of-month to 30.<br />
If the first day-of-month is 31, change the first day-of-month to 30.
<br /><br />
This day count has different rules depending on whether the EOM rule applies or not.<br />
The EOM rule is set in the <code>ScheduleInfo</code> and defaults to true.
<br /><br />
There are two related day counts.<br />
The '30U/360 EOM' rule is identical to this rule when the EOM convention applies.<br />
The '30/360 ISDA' rule is identical to this rule when the EOM convention does not apply.
  </td>
</tr>
<tr>
  <th>Schedules</th>
  <td>This day count assumes EOM convention is true if <code>ScheduleInfo</code> is not specified</td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'30/360 US', '30US/360' or '30/360 SIA'</td>
</tr>
</table>

### 30U/360 EOM

<table>
<tr>
  <th>Name</th>
  <td>30U/360 EOM</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.THIRTY_U_360_EOM</td>
</tr>
<tr>
  <th>Summary</th>
  <td>A 30/360 style algorithm with special rules for the 31st day-of-month and the end of February</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is calculated as <code>(360 * deltaYear + 30 * deltaMonth + deltaDay) / 360</code>.<br />
The deltaDay is then calculated once day-of-month adjustments have occurred.<br />
If both dates are the last day of February, change the second day-of-month to 30.<br />
If the first date is the last day of February, change the first day-of-month to 30.<br />
If the second day-of-month is 31 and the first day-of-month is 30 or 31, change the second day-of-month to 30.<br />
If the first day-of-month is 31, change the first day-of-month to 30.
<br /><br />
This day count is not dependent on the EOM flag in <code>ScheduleInfo</code>.
<br /><br />
This is the same as '30U/360' when the EOM convention applies.<br />
This day count would typically be used to be explicit about the EOM rule applying.<br />
In most cases, '30U/360' should be used in preference to this day count.</td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'30/360 US', '30US/360' or '30/360 SIA'</td>
</tr>
</table>

### 30/360 PSA

<table>
<tr>
  <th>Name</th>
  <td>30/360 PSA</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.THIRTY_360_PSA</td>
</tr>
<tr>
  <th>Summary</th>
  <td>A 30/360 style algorithm with special rules for the 31st day-of-month and the end of February</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is calculated as <code>(360 * deltaYear + 30 * deltaMonth + deltaDay) / 360</code>.<br />
The deltaDay is then calculated once day-of-month adjustments have occurred.<br />
If the first date is the last day of February, change the first day-of-month to 30.<br />
If the second day-of-month is 31 and the first day-of-month is 30 or 31, change the second day-of-month to 30.<br />
If the first day-of-month is 31, change the first day-of-month to 30.</td>
</tr>
<tr>
  <th>Schedules</th>
  <td>This day count assumes EOM convention is true if <code>ScheduleInfo</code> is not specified</td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'30/360 BMA' (PSA is the Public Securites Association, BMA is the Bond Market Association)</td>
</tr>
</table>

### 30E/360 ISDA

<table>
<tr>
  <th>Name</th>
  <td>30E/360 ISDA</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.THIRTY_E_360_ISDA</td>
</tr>
<tr>
  <th>Summary</th>
  <td>A 30/360 style algorithm with special rules for the 31st day-of-month and the end of February</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is calculated as <code>(360 * deltaYear + 30 * deltaMonth + deltaDay) / 360</code>.<br />
The deltaDay is then calculated once day-of-month adjustments have occurred.<br />
If the first day-of-month is 31, change the first day-of-month to 30.<br />
If the second day-of-month is 31, change the second day-of-month to 30.<br />
If the first date is the last day of February, change the first day-of-month to 30.<br />
If the second date is the last day of February and it is not the maturity date, change the second day-of-month to 30.</td>
</tr>
<tr>
  <th>Schedules</th>
  <td>This day count requires <code>ScheduleInfo</code></td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'30E/360 German' or 'German'</td>
</tr>
<tr>
  <th>Definition</th>
  <td>2006 ISDA definitions 4.16h</td>
</tr>
</table>

### 30E/360

<table>
<tr>
  <th>Name</th>
  <td>30E/360</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.THIRTY_E_360</td>
</tr>
<tr>
  <th>Summary</th>
  <td>A 30/360 style algorithm with special rules for the 31st day-of-month</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is calculated as <code>(360 * deltaYear + 30 * deltaMonth + deltaDay) / 360</code>.<br />
The deltaDay is then calculated once day-of-month adjustments have occurred.<br />
If the first day-of-month is 31, it is changed to 30.<br />
If the second day-of-month is 31, it is changed to 30.</td>
</tr>
<tr>
  <th>Also&nbsp;known</th>
  <td>'30/360 ISMA', '30/360 European', '30S/360 Special German', 'EBD/360' or 'Eurobond'</td>
</tr>
<tr>
  <th>Definition</th>
  <td>2006 ISDA definitions 4.16g and ICMA rule 251.1(ii) and 252.2</td>
</tr>
</table>

### 30E+/360

<table>
<tr>
  <th>Name</th>
  <td>30E+/360</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.THIRTY_EPLUS_360</td>
</tr>
<tr>
  <th>Summary</th>
  <td>A 30/360 style algorithm with special rules for the 31st day-of-month</td>
</tr>
<tr>
  <th>Description</th>
  <td>The result is calculated as <code>(360 * deltaYear + 30 * deltaMonth + deltaDay) / 360</code>.<br />
The deltaDay and deltaMonth are calculated once adjustments have occurred.<br />
If the first day-of-month is 31, it is changed to 30.<br />
If the second day-of-month is 31, it is changed to 1 and the second month is incremented.</td>
</tr>
</table>

### 1/1

<table>
<tr>
  <th>Name</th>
  <td>1/1</td>
</tr>
<tr>
  <th>Constant</th>
  <td>DayCounts.ONE_ONE</td>
</tr>
<tr>
  <th>Description</th>
  <td> An artificial day count that always returns one</td>
</tr>
<tr>
  <th>Definition</th>
  <td>Defined by the 2006 ISDA definitions 4.16a</td>
</tr>
</table>

