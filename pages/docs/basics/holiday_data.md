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

The default column indicates if that calendar is the default for the currency.

| Name | Holidays                                         | Default | Weekends          | ISDA reference      |
|------|--------------------------------------------------|---------|-------------------|---------------------|
| AUSY | Sydney (Australia) holidays                      | AUD     | Saturday/Sunday   |                     |
| BRBD | Brazil holidays                                  | BRL     | Saturday/Sunday   |                     |
| CAMO | Montreal (Canada) holidays                       |         | Saturday/Sunday   |                     |
| CATO | Toronto (Canada) holidays                        | CAD     | Saturday/Sunday   |                     |
| CHZU | Zurich (Switzerland) holidays                    | CHF     | Saturday/Sunday   |                     |
| CZPR | Prague (Czech Republic) holidays                 | CZK     | Saturday/Sunday   |                     |
| DEFR | Frankfurt (Germany) holidays                     |         | Saturday/Sunday   |                     |
| DKCO | Copenhagen (Denmark) holidays                    |         | Saturday/Sunday   |                     |
| EUTA | TARGET interbank payment (Europe) holidays       | EUR     | Saturday/Sunday   | section 1.8 (2006)  |
| FRPA | Paris (France) holidays                          |         | Saturday/Sunday   |                     |
| GBLO | London (UK) holidays                             | GBP     | Saturday/Sunday   |                     |
| HUBU | Budapest (Hungary) holidays                      | HUF     | Saturday/Sunday   |                     |
| JPTO | Tokyo (Japan) holidays                           | JPY     | Saturday/Sunday   |                     |
| MXMC | Mexico City (Mexico) holidays                    | MXN     | Saturday/Sunday   |                     |
| NOOS | Oslo (Norway) holidays                           | NOK     | Saturday/Sunday   |                     |
| NYFD | Federal Reserve Bank of New York holidays        |         | Saturday/Sunday   | section 1.9 (2006)  |
| NYSE | New York Stock Exchange holidays                 |         | Saturday/Sunday   | section 1.10 (2006) |
| NZAU | Auckland (New Zealand) holidays                  | NZD     | Saturday/Sunday   |                     |
| NZWE | Wellington (New Zealand) holidays                |         | Saturday/Sunday   |                     |
| NZBD | New Zealand holidays                             |         | Saturday/Sunday   |                     |
| PLWA | Warsaw (Poland) holidays                         | PLN     | Saturday/Sunday   |                     |
| SEST | Stockholm (Sweden) holidays                      | SEK     | Saturday/Sunday   |                     |
| USGS | United States Government Securities              |         | Saturday/Sunday   | section 1.11 (2006) |
| USNY | New York (USA) holidays                          | USD     | Saturday/Sunday   |                     |
| ZAJO | Johannesburg (South Africa) holidays             | ZAR     | Saturday/Sunday   |                     |
|------------|----------------------|-|-------------------|----|
| NoHolidays | No holiday dates     | | No weekends       |    |
| Sat/Sun    | No holiday dates     | | Saturday/Sunday   |    |
| Fri/Sat    | No holiday dates     | | Friday/Saturday   |    |
| Thu/Fri    | No holiday dates     | | Thursday/Friday   |    |

Holiday calendars have a constant in `HolidayCalendarIds`.
The identifier can also be created dynamically using `HolidayCalendarId.of(name)`.


### Additional Holiday calendars

Some [indices]({{site.baseurl}}/indices) refer to calendars where example holiday data is not provided.
These do no have a constant in `HolidayCalendarIds` and cannot be resolved without externally provided holiday data.
These are listed below for completeness.

| Name | Holidays                                         | Default |
|------|--------------------------------------------------|---------|
| CLSA | Santiago (Chile) holidays                        | CLP     |
| CNBE | Beijing (China) holidays                         | CNY     |
| COBO | Bogota (Colombia) holidays                       | COP     |
| HKHK | Hong Kong holidays                               | HKD     |
| IDJA | Jakarta holidays                                 | IDR     |
| ILTA | Tel Aviv (Israel) holidays                       | ILS     |
| INMU | Mumbai (India) holidays                          | INR     |
| KRSE | Seoul (Republic of Korea) holidays               | KRW     |
| RUMO | Moscow (Russia) holidays                         | RUB     |
| SARI | Riyadh (Saudi Arabia) holidays                   | SAR     |
| SGSI | Singapore holidays                               | SGD     |
| THBA | Bangkok (Thailand) holidays                      | THB     |
| TRIS | Istanbul (Turkey) holidays                       | TRY     |
| TWTA | Taipei (Taiwan) holidays                         | TWD     |
