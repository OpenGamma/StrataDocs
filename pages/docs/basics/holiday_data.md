---
title: Holiday Data
permalink: /holiday_data/
---

Strata provides a comprehensive [holiday calendar]({{site.baseurl}}/holidays) system.
However, such a system also needs the associated data, specifying which days are holidays.
This page details the provided holiday calendars.


## Holiday calendars

Each holiday calendar represents a consistent set of weekends and holidays.
In most cases they refer to a specific location, however some calendars are location independent.

The intention of providing these calendars is to allow the system to be easily evaluated.
When using this library in production, OpenGamma strongly recommends replacing the data provided
with data from an external vendor of holiday information.

The holiday dates are based on original research and typically cover 1950 to 2099.
Future and past dates are an extrapolations of the known holiday dates.

| Name | Holidays                                         | Weekends          | ISDA reference      |
|------|--------------------------------------------------|-------------------|---------------------|
| AUSY | Sydney (Australia) holidays                      | Saturday/Sunday   |                     |
| BRBD | Brazil holidays                                  | Saturday/Sunday   |                     |
| CAMO | Montreal (Canada) holidays                       | Saturday/Sunday   |                     |
| CATO | Toronto (Canada) holidays                        | Saturday/Sunday   |                     |
| CHZU | Zurich (Switzerland) holidays                    | Saturday/Sunday   |                     |
| CZPR | Prague (Czech Republic) holidays                 | Saturday/Sunday   |                     |
| DEFR | Frankfurt (Germany) holidays                     | Saturday/Sunday   |                     |
| DKCO | Copenhagen (Denmark) holidays                    | Saturday/Sunday   |                     |
| EUTA | TARGET interbank payment (Europe) holidays       | Saturday/Sunday   | section 1.8 (2006)  |
| FRPA | Paris (France) holidays                          | Saturday/Sunday   |                     |
| GBLO | London (UK) holidays                             | Saturday/Sunday   |                     |
| HUBU | Budapest (Hungary) holidays                      | Saturday/Sunday   |                     |
| JPTO | Tokyo (Japan) holidays                           | Saturday/Sunday   |                     |
| MXMC | Mexico City (Mexico) holidays                    | Saturday/Sunday   |                     |
| NOOS | Oslo (Norway) holidays                           | Saturday/Sunday   |                     |
| NYFD | Federal Reserve Bank of New York holidays        | Saturday/Sunday   | section 1.9 (2006)  |
| NYSE | New York Stock Exchange holidays                 | Saturday/Sunday   | section 1.10 (2006) |
| PLWA | Warsaw (Poland) holidays                         | Saturday/Sunday   |                     |
| SEST | Stockholm (Sweden) holidays                      | Saturday/Sunday   |                     |
| USGS | United States Government Securities              | Saturday/Sunday   | section 1.11 (2006) |
| USNY | New York (USA) holidays                          | Saturday/Sunday   |                     |
| ZAJO | Johannesburg (South Africa) holidays             | Saturday/Sunday   |                     |
|------------|----------------------|-------------------|----|
| NoHolidays | No holiday dates     | No weekends       |    |
| Sat/Sun    | No holiday dates     | Saturday/Sunday   |    |
| Fri/Sat    | No holiday dates     | Friday/Saturday   |    |
| Thu/Fri    | No holiday dates     | Thursday/Friday   |    |

Holiday calendars have a constant in `HolidayCalendarIds`.
The identifier can also be created dynamically using `HolidayCalendarId.of(name)`.


## Default Holiday Calendar for a currency

Strata defines a default holiday calendar for many currencies.

| Currency | Calendar Name | Holidays                                         |
|----------|---------------| -------------------------------------------------|
| AUD      | AUSY          | Sydney (Australia) holidays                      |
| BRL      | BRBD          | Brazil holidays                                  |
| CAD      | CATO          | Montreal (Canada) holidays                       |
| CHF      | CHZU          | Zurich (Switzerland) holidays                    |
| CZK      | CZPR          | Prague (Czech Republic) holidays                 |
| DKK      | DKCO          | Copenhagen (Denmark) holidays                    |
| EUR      | EUTA          | TARGET interbank payment (Europe) holidays       |
| GBP      | GBLO          | London (UK) holidays                             |
| HUF      | HUBU          | Budapest (Hungary) holidays                      |
| JPY      | JPTO          | Tokyo (Japan) holidays                           |
| MXN      | MXMC          | Mexico City (Mexico) holidays                    |
| NOK      | NOOS          | Oslo (Norway) holidays                           |
| PLN      | PLWA          | Warsaw (Poland) holidays                         |
| SEK      | SEST          | Stockholm (Sweden) holidays                      |
| USD      | USNY          | New York (USA) holidays                          |
| ZAR      | ZAJO          | Johannesburg (South Africa) holidays             |
