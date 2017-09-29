---
title: Indices
permalink: /indices/
---

Strata provides information about the standard market conventions for various indices.
These represent the correct convention to our best knowledge at the time of coding.

Strata defines an index as "an agreed mechanism for determining certain financial indicators,
such as exchange rates or interest rates". Most common indices are published each working day.


## Overnight Indices:

An Overnight index is used to represent the rate where money is deposited for one night.
Usually this is from today to tomorrow, but it can be from tomorrow to the day after, known as "tom/next".

| Name           | Description              | Day Count    |
|----------------|--------------------------|--------------|
| AUD-AONIA      | AONIA index for AUD      | Act/365F     |
| BRL-CDI        | CDI index for BRL        | Bus/252 BRBD |
| CAD-CORRA      | CORRA index for CAD      | Act/365F     |
| CHF-TOIS       | TOIS index for CHF       | Act/360      |
| CHF-SARON      | SARON index for CHF      | Act/360      |
| DKK-TNR        | TNR index for CHF        | Act/360      |
| EUR-EONIA      | EONIA index for EUR      | Act/360      |
| GBP-SONIA      | SONIA index for GBP      | Act/365F     |
| NOK-NOWA       | NOWA index for NOK       | Act/Act Year |
| PLN-POLONIA    | POLONIA index for PLN    | Act/365F     |
| SEK-SIOR       | SIOR index for SEK       | Act/360      |
| JPY-TONAR      | TONAR index for JPY      | Act/365F     |
| USD-FED-FUND   | Fed-Fund index for USD   | Act/360      |

Overnight indices have a constant in `OvernightIndices`.
The identifier can also be obtained dynamically using `OvernightIndex.of(name)`.


## Ibor Indices:

An Ibor index is used to represent the rate where money is deposited for a period longer than one day.
The deposit period is known as the tenor, and a rate is published for a number of different tenors.

| Name                 | Tenors                   | Description               | Day Count    |
|----------------------|--------------------------|---------------------------|--------------|
| AUD-BBSW-XX          | 1M,2M,3M,4M,5M,6M        | BBSW index for AUD        | Act/365F     |
| CAD-CDOR-XX          | 1M,2M,3M,6M,12M          | CDOR index for CAD        | Act/365F     |
| CHF-LIBOR-XX         | 1W,1M,2M,3M,6M,12M       | LIBOR index for CHF       | Act/360      |
| CZK-PRIBOR-XX        | 1W,2W,1M,2M,3M,6M,12M    | PRIBOR index for CZK      | Act/360      |
| DKK-CIBOR-XX         | 1W,2W,1M,2M,3M,6M,9M,12M | CIBOR index for DKK       | Act/360      |
| EUR-LIBOR-XX         | 1W,1M,2M,3M,6M,12M       | LIBOR index for EUR       | Act/360      |
| EUR-EURIBOR-XX       | 1W,2W,1M,2M,3M,6M,9M,12M | EURIBOR index for EUR     | Act/360      |
| GBP-LIBOR-XX         | 1W,1M,2M,3M,6M,12M       | LIBOR index for GBP       | Act/365F     |
| HUF-BUBOR-XX         | 1W,2W,1M,2M,3M,6M,9M,12M | BUBOR index for HUF       | Act/360      |
| MXN-TIIE-XX          | 4W,13W,26W               | TIIE index for MXN        | Act/360      |
| JPY-LIBOR-XX         | 1W,1M,2M,3M,6M,12M       | LIBOR index for JPY       | Act/360      |
| JPY-TIBOR-JAPAN-XX   | 1W,1M,2M,3M,6M,12M       | TIBOR index for JPY       | Act/365F     |
| JPY-TIBOR-EUROYEN-XX | 1W,1M,2M,3M,6M,12M       | TIBOR index for JPY       | Act/360      |
| NOK-NIBOR-XX         | 1W,1M,2M,3M,6M           | NIBOR index for NOK       | Act/360      |
| PLN-WIBOR-XX         | 1W,1M,3M,6M,12M          | WIBOR index for PLN       | Act/365F     |
| SEK-STIBOR-XX        | 1W,1M,2M,3M,6M           | STIBOR index for SEK      | Act/360      |
| USD-LIBOR-XX         | 1W,1M,2M,3M,6M,12M       | LIBOR index for USD       | Act/360      |
| ZAR-JIBAR-XX         | 1M,3M,6M,9M,12M          | JIBAR index for ZAR       | Act/365F     |

To get the name of the index, replace "XX" with one of the tenors.
For example, "GBP-LIBOR-3M" is a valid index name.

Ibor indices have a constant in `IborIndices`.
The identifier can also be obtained dynamically using `IborIndex.of(name)`.


## Prices Indices (for inflation):

A Price index is used to represent the rate at which prices rise in an economy.
The difference between two values represents inflation.

| Name           | Country | Description      | 
|----------------|---------|------------------|
| GB-HICP        | GB      | Non-revised Harmonised Index of Consumer Prices |
| GB-RPI         | GB      | Non-revised Retail Price Index All Items |
| GB-RPIX        | GB      | Non-revised Retail Price Index Excluding Mortgage Interest Payments |
| CH-CPI         | CH      | Non-revised Consumer Price Index |
| EU-AI-CPI      | EU      | Non-revised Harmonised Index of Consumer Prices All Items |
| EU-EXT-CPI     | EU      | Non-revised Harmonised Index of Consumer Prices Excluding Tobacco |
| JP-CPI-EXF     | EU      | Non-revised Consumer Price Index Nationwide General Excluding Fresh Food |
| US-CPI-U       | EU      | Non-revised index of Consumer Prices for All Urban Consumers before seasonal adjustment |
| FR-EXT-CPI     | EU      | Non-revised Harmonised Index of Consumer Prices Excluding Tobacco |

Price indices have a constant in `PriceIndices`.
The identifier can also be obtained dynamically using `PriceIndex.of(name)`.
