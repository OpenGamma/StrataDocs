---
title: Trade loader for CDS
permalink: /trade_loader_cds/
---

This page details the Strata CSV format for loading [CDS]({{site.baseurl}}/cds).
See the [overview page]({{site.baseurl}}/trade_loader) for details of other assets classes.


## Trade loader file format

The trades file is a CSV-formatted file.
The columns may be specified in any order.
The CSV format is flexible, and the input can specify trades in various ways.

CDS trades can be specified using two different column sets - by convention and by full details.
The two column sets can be mixed in the same file.
In addition, a single file can contain other asset classes, such as FRAs or FX.
Just add the union of the column headers and fill in the necessary data on a row by row basis.


## Example

This example file specifies a CDS trade by convention.

```
Strata Trade Type, Id Scheme, Id,     Trade Date, Convention,   Buy Sell, Tenor, Notional, Fixed Rate, Legal Entity Id
CDS,               OG,        123411, 2017-06-01, GBP-STANDARD, Buy,      P5Y,   2000000,  0.4,        RISKY-CORP
```

Note that Microsoft Excel prefers the CSV file to have no spaces after the comma.


## CDS by convention

These columns are used when loading a CDS trade by convention.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name            | Mandatory?  | Description |
|------------------------|-------------|-------------|
| Strata Trade Type      | Mandatory   | The type of the trade, "CDS", case insensitive |
| Start Date             | Conditional | The unadjusted start date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| End Date               | Conditional | The unadjusted end date, such as "2022-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Tenor                  | Conditional | The period from the start date to the end date, such as "P5Y" or "5Y", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Convention             | Mandatory   | The CDS convention, such as "GBP-STANDARD" |
| Buy Sell               | Mandatory   | Whether the CDS is "Buy" or "Sell" |
| Notional               | Mandatory   | The notional amount, currency defined by the convention |
| Fixed Rate             | Mandatory   | The fixed rate, as a percentage, such as "1.2" for 1.2% |
| Legal Entity Id Scheme | Optional    | The scheme (symbology) within which the legal entity identifier is unique, default "OG-Entity" |
| Legal Entity Id        | Mandatory   | The legal entity identifier |

Valid combinations of conditional fields are as follows (other combinations are not allowed):

* "Start Date" and "End Date"
* "Trade Date" and "Tenor"


## CDS by full details

These columns are used when loading a CDS trade by full details.
See also the [overview page]({{site.baseurl}}/trade_loader) for additional optional columns that can be used
to specify the identifier and counterparty.

| Column name              | Mandatory?  | Description |
|--------------------------|-------------|-------------|
| Strata Trade Type        | Mandatory   | The type of the trade, "CDS", case insensitive |
| Buy Sell                 | Mandatory   | Whether the CDS is "Buy" or "Sell" |
| Currency                 | Mandatory   | The currency of the notional amount |
| Notional                 | Mandatory   | The notional amount |
| Fixed Rate               | Mandatory   | The fixed rate, as a percentage, such as "1.2" for 1.2% |
| Legal Entity Id Scheme   | Optional    | The scheme (symbology) within which the legal entity identifier is unique, default "OG-Entity" |
| Legal Entity Id          | Mandatory   | The legal entity identifier |
| Premium Direction        | Optional    | The premium direction, "Pay" or "Receive" |
| Premium Currency         | Optional    | The premium currency, such as "GBP" |
| Premium Amount           | Optional    | The premium amount, in the premium currency, positive with direction defined by Pay/Receive |
| Premium Date             | Optional    | The premium date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Premium Date Convention  | Optional    | The premium [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following" or "ModifiedFollowing" |
| Premium Date Calendar    | Optional    | The premium [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |
| Day Count                | Optional    | The [day count convention]({{site.baseurl}}/day_counts/), defaults to "Act/360" |
| Payment On Default       | Optional    | Whether the accrued premium is paid in the event of a default, "AccruedPremium" or "None", defaults to "AccruedPremium" |
| Protection Start         | Optional    | When the protection starts on the start date, "Beginning" or "None", defaults to "Beginning" |
| Step In Date Offset Days                  | Optional | The step in date offset in days, defaults to no offset |
| Step In Date Offset Calendar              | Optional | The step in date offset calendar, defaults to "NoHolidays" |
| Step In Date Offset Adjustment Convention | Optional | The step in date offset adjustment business day convention |
| Step In Date Offset Adjustment Calendar   | Optional | The step in date offset adjustment holiday calendar |
| Settlement Date Offset Days                  | Optional | The settlement date offset in days, defaults to no offset |
| Settlement Date Offset Calendar              | Optional | The settlement date offset calendar, defaults to "NoHolidays" |
| Settlement Date Offset Adjustment Convention | Optional | The settlement date offset adjustment business day convention |
| Settlement Date Offset Adjustment Calendar   | Optional | The settlement date offset adjustment holiday calendar |
| Start Date               | Mandatory   | The unadjusted start date, such as "2017-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| End Date                 | Mandatory   | The unadjusted end date, such as "2022-06-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Frequency                | Mandatory   | The payment frequency, such as "P3M" or "3M" |
| Date Convention          | Optional    | The payment date [business day convention]({{site.baseurl}}/date_adjustments/), such as "Following", defaults to "ModifiedFollowing" |
| Date Calendar            | Optional    | The payment date [holiday calendar]({{site.baseurl}}/holiday_data/) to use, such as "GBLO" |
| Start Date Convention    | Optional    | The start date business day convention |
| Start Date Calendar      | Optional    | The start date holiday calendar |
| End Date Convention      | Optional    | The end date business day convention |
| End Date Calendar        | Optional    | The end date holiday calendar |
| Roll Convention          | Optional    | The roll convention, such as "Day21" or "EOM" |
| Stub Convention          | Optional    | The stub convention, such as "ShortFinal", defaults to "SmartInitial" |
| First Regular Start Date | Optional    | The unadjusted start date of the first regular accrual period, such as "2017-09-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
| Last Regular End Date    | Optional    | The unadjusted end date of the last regular accrual period, such as "2022-03-01", see [accepted formats]({{site.baseurl}}/common_formats/) |
