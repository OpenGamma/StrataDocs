---
title: Indices
permalink: /indices/
---

Strata provides information about the standard market conventions for various indices.
These represent the correct convention to our best knowledge at the time of coding.

Strata defines an index as "an agreed mechanism for determining certain financial indicators,
such as exchange rates or interest rates". Most common indices are published each working day.


## <a name="overnight"></a>Overnight Indices:

An Overnight index is used to represent the rate where money is deposited for one night.
Usually this is from today to tomorrow, but it can be from tomorrow to the day after, known as "tom/next".

| Name           | Description              | Day Count    |
|----------------|--------------------------|--------------|
| AUD-AONIA      | AONIA index for AUD      | Act/365F     |
| BRL-CDI        | CDI index for BRL        | Bus/252 BRBD |
| CAD-CORRA      | CORRA index for CAD      | Act/365F     |
| CHF-SARON      | SARON index for CHF      | Act/360      |
| CLP-TNA *      | TNA index for CLP        | Act/360      |
| COP-OIBR *     | IBR index for COP        | Act/360      |
| CZK-CZEONIA *  | CZEONIA index for CZK    | Act/360      |
| DKK-TNR        | TNR index for DKK        | Act/360      |
| EUR-EONIA      | EONIA index for EUR      | Act/360      |
| EUR-ESTR       | ESTR index for EUR       | Act/360      |
| GBP-SONIA      | SONIA index for GBP      | Act/365F     |
| HKD-HONIA *    | HONIA index for HKD      | Act/365F     |
| HUF-HUFONIA *  | HUFONIA index for HUF    | Act/365F     |
| IDR-INDONIA *  | INDONIA index for IDR    | Act/365F     |
| ILS-OTELBOR *  | OTELBOR index for ILS    | Act/365F     |
| INR-OMIBOR *   | OMIBOR index for INR     | Act/365F     |
| JPY-TONAR      | TONAR index for JPY      | Act/365F     |
| NOK-NOWA       | NOWA index for NOK       | Act/Act Year |
| NZD-NZIONA     | NZIONA index for AUD     | Act/365F     |
| PLN-POLONIA    | POLONIA index for PLN    | Act/365F     |
| RUB-RUONIA *   | RUONIA index for RUB     | Act/365F     |
| SAR-OSAIBOR *  | OSAIBOR index for SAR    | Act/365F     |
| SEK-SIOR       | SIOR index for SEK       | Act/360      |
| SGD-SONAR *    | SONAR index for SGD      | Act/365F     |
| SGD-SORA *     | SORA index for SGD       | Act/365F     |
| TRY-TLREF *    | TLREF index for TRY      | Act/365F     |
| USD-AMERIBOR   | AMERIBOR index for USD   | Act/360      |
| USD-FED-FUND   | Fed-Fund index for USD   | Act/360      |
| USD-SOFR       | SOFR index for USD       | Act/360      |
| ZAR-SABOR      | SABOR index for ZAR      | Act/360      |

Overnight indices have a constant in `OvernightIndices`.
The identifier can also be obtained dynamically using `OvernightIndex.of(name)`.

\* Indices marked with a star do not have a constant in `OvernightIndices`,
and they generally do not have holiday calendar data available.


## <a name="ibor"></a>Ibor Indices:

An Ibor index is used to represent the rate where money is deposited for a period longer than one day.
The deposit period is known as the tenor, and a rate is published for a number of different tenors.

| Name                 | Tenors                   | Description               | Day Count    |
|----------------------|--------------------------|---------------------------|--------------|
| AUD-BBSW-XX          | 1M,2M,3M,4M,5M,6M        | BBSW index for AUD        | Act/365F     |
| CAD-CDOR-XX          | 1M,2M,3M,6M,12M          | CDOR index for CAD        | Act/365F     |
| CHF-LIBOR-XX         | 1W,1M,2M,3M,6M,12M       | LIBOR index for CHF       | Act/360      |
| CNY-REPO-XX *        | 1W                       | REPO index for CNY        | Act/365F     |
| CZK-PRIBOR-XX        | 1W,2W,1M,2M,3M,6M,12M    | PRIBOR index for CZK      | Act/360      |
| DKK-CIBOR-XX         | 1W,2W,1M,2M,3M,6M,9M,12M | CIBOR index for DKK       | Act/360      |
| EUR-LIBOR-XX         | 1W,1M,2M,3M,6M,12M       | LIBOR index for EUR       | Act/360      |
| EUR-EURIBOR-XX       | 1W,2W,1M,2M,3M,6M,9M,12M | EURIBOR index for EUR     | Act/360      |
| GBP-LIBOR-XX         | 1W,1M,2M,3M,6M,12M       | LIBOR index for GBP       | Act/365F     |
| HKD-HIBOR-XX *       | 1W,2W,1M,2M,3M,6M,12M    | HIBOR index for HKD       | Act/365F     |
| HUF-BUBOR-XX         | 1W,2W,1M,2M,3M,6M,9M,12M | BUBOR index for HUF       | Act/360      |
| ILS-TELBOR-XX *      | 1M,3M,6M,12M             | TELBOR index for ILS      | Act/365F     |
| JPY-LIBOR-XX         | 1W,1M,2M,3M,6M,12M       | LIBOR index for JPY       | Act/360      |
| JPY-TIBOR-JAPAN-XX   | 1W,1M,2M,3M,6M,12M       | TIBOR index for JPY       | Act/365F     |
| JPY-TIBOR-EUROYEN-XX | 1W,1M,2M,3M,6M,12M       | TIBOR index for JPY       | Act/360      |
| KRW-CD-XX *          | 13W                      | CD index for KRW          | Act/365F     |
| MXN-TIIE-XX          | 4W,13W,26W               | TIIE index for MXN        | Act/360      |
| NOK-NIBOR-XX         | 1W,1M,2M,3M,6M           | NIBOR index for NOK       | Act/360      |
| NZD-BKBM-XX          | 1M,2M,3M,4M,5M,6M        | BKBM index for NZD        | Act/365F     |
| PLN-WIBOR-XX         | 1W,1M,3M,6M,12M          | WIBOR index for PLN       | Act/365F     |
| SAR-SAIBOR-XX *      | 1W,1M,3M,6M,12M          | SAIBOR index for SAR      | Act/360      |
| SEK-STIBOR-XX        | 1W,1M,2M,3M,6M           | STIBOR index for SEK      | Act/360      |
| SGD-SIBOR-XX *       | 1M,3M,6M,12M             | SIBOR index for SGD       | Act/365F     |
| SGD-SOR-XX *         | 1M,3M,6M                 | SOR index for SGD         | Act/365F     |
| THB-THBFIX-XX *      | 1W,1M,3M,6M,12M          | THBFIX index for THB      | Act/365F     |
| TWD-TAIBOR-XX *      | 1W,1M,2M,3M,6M,9M,12M    | TAIBOR index for TWD      | Act/365F     |
| USD-LIBOR-XX         | 1W,1M,2M,3M,6M,12M       | LIBOR index for USD       | Act/360      |
| ZAR-JIBAR-XX         | 1M,3M,6M,9M,12M          | JIBAR index for ZAR       | Act/365F     |

To get the name of the index, replace "XX" with one of the tenors.
For example, "GBP-LIBOR-3M" is a valid index name.

Ibor indices have a constant in `IborIndices`.
The identifier can also be obtained dynamically using `IborIndex.of(name)`.

\* Indices marked with a star do not have a constant in `IborIndices`,
nor do they have holiday calendar data available.


## <a name="price"></a>Prices Indices (for inflation):

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


## <a name="fx"></a>FX Indices:

An FX index provides a daily snap of the FX rate between two currencies.

| Name                      | Currency pair | Description      | 
|---------------------------|---------------|------------------|
| EUR/CHF-ECB               | EUR/CHF       | Daily fixing from the European Central Bank |
| EUR/GBP-ECB               | EUR/GBP       | Daily fixing from the European Central Bank |
| EUR/JPY-ECB               | EUR/JPYB      | Daily fixing from the European Central Bank |
| EUR/USD-ECB               | EUR/USD       | Daily fixing from the European Central Bank |
| USD/CHF-WM                | USD/CHF       | Daily fixing from the WM company |
| GBP/USD-WM                | GBP/USD       | Daily fixing from the WM company |
| EUR/USD-WM                | EUR/USD       | Daily fixing from the WM company |
| USD/JPY-WM                | USD/JPY       | Daily fixing from the WM company |
| USD/CLP-DOLAR-OBS-CLP10 * | USD/CLP       | Daily fixing as per industry standards |
| USD/CNY-SAEC-CNY01 *      | USD/CNY       | Daily fixing as per industry standards |
| USD/COP-TRM-COP02 *       | USD/COP       | Daily fixing as per industry standards |
| USD/INR-FBIL-INR01 *      | USD/INR       | Daily fixing as per industry standards |
| USD/KRW-KFTC18-KRW02 *    | USD/KRW       | Daily fixing as per industry standards |
| USD/SGD-VWAP-SGD3 *       | USD/SGD       | Daily fixing as per industry standards |
| USD/THB-VWAP-THB01 *      | USD/THB       | Daily fixing as per industry standards |
| USD/TWD-TAIFX1-TWD03 *    | USD/TWD       | Daily fixing as per industry standards |

FX indices have a constant in `FxIndices`.
The identifier can also be obtained dynamically using `FxIndex.of(name)`.

\* Indices marked with a star do not have a constant in `FxIndices`,


