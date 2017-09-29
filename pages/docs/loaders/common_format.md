---
title: Common formats
permalink: /common_formats/
---

The CSV loaders have some common formats for values, detailed below:

### Dates

The loaders support the following date formats:

| Format       | Example    | Description   | Notes |
|--------------|------------|---------------|-------|
| `yyyy-MM-dd` | 2017-06-01 | 1st June 2017 | ISO-8601, Recommended format |
| `yyyyMMdd`   | 20170601   | 1st June 2017 | ISO-8601 basic format |
| `yyyy/MM/dd` | 2017/06/01 | 1st June 2017 | |
| `d-MMM-yyyy` | 1-Jun-2017 | 1st June 2017 | Month abbreviation in English |
| `d-MMM-yy`   | 1-Jun-17   | 1st June 2017 | Month abbreviation in English |
| `dMMMyyyy`   | 1Jun2017   | 1st June 2017 | Month abbreviation in English |
| `dMMMyy`     | 1Jun17     | 1st June 2017 | Month abbreviation in English |
| `d/M/yyyy`   | 1/6/2017   | 1st June 2017 | Excel format |
| `d/M/yy`     | 1/6/17     | 1st June 2017 | |


### Year/Month

The loaders support the following year/month formats:

| Format       | Example    | Description   | Notes |
|--------------|------------|---------------|-------|
| `yyyy-MM`    | 2017-06    | June 2017     | ISO-8601, Recommended format |
| `yyyyMM`     | 201706     | June 2017     | ISO-8601 basic format |
| `yyyy/MM`    | 2017/06    | June 2017     | |
| `MMM-yyyy`   | Jun-2017   | June 2017     | Month abbreviation in English |
| `MMM-yy`     | Jun-17     | June 2017     | Month abbreviation in English |
| `MMMyyyy`    | Jun2017    | June 2017     | Month abbreviation in English |
| `MMMyy`      | Jun17      | June 2017     | Month abbreviation in English |
| `d/M/yyyy`   | 1/6/2017   | June 2017     | Excel format, day must be 1 |


### Times

The loaders support the following time formats:

| Format        | Example        | Description  |
|---------------|----------------|--------------|
| `H`           | `2`            | 02:00 (2 AM) |
| `H:mm`        | `15:30`        | 15:30        |
| `H:mm:ss`     | `11:20:40`     | 11:20:40     |
| `H:mm:ss.SSS` | `12:30:40.123` | 12:30:40.123 |


### Frequency/Tenor

The loaders support the following frequency/tenor formats:

| Format      | Example  | Description | Notes |
|-------------|----------|-------------|-------|
| `PnY`       | `P3Y`    | 3 years     | ISO-8601 |
| `nY`        | `3Y`     | 3 years     | |
| `PnM`       | `P4M`    | 4 months    | ISO-8601 |
| `nM`        | `4M`     | 4 months    | |
| `PnW`       | `P5W`    | 5 weeks     | ISO-8601 |
| `nW`        | `5W`     | 5 weeks     | |
| `PnD`       | `P6D`    | 6 days      | ISO-8601 |
| `nD`        | `6D`     | 6 days      | |
| `Term`      | `Term`   | Frequency = Tenor | Only valid for frequency, indicates that the swap has one accrual period |
