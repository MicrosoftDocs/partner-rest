---
title: Get foreign exchange rates
description: Obtain foreign exchange rates for a given month.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
---

# Get foreign exchange rates

Applies to:

- Partner API

This topic explains how to get foreign exchange rates for a given month.

## Prerequisites

- Credentials as described in [Partner API authentication](api-authentication.md). This scenario only supports application user authentication. Application-only is not yet supported.


## Details

- Currently used with [get price sheet API](get-a-price-sheet.md) to calculate expected charges for Azure plan CSP local currencies.
- Foreign exchange rates hold true for the entire month they are posted.
- More information about Azure plan [pricing](pricing.md) can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).

## REST request

### Request syntax

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='{month}')/$value                                  |

### URI required parameters

Use the following path parameters to request the month of foreign exchange rates you want.

| Name                   | Type     | Required | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Month                      | string   | Yes       | Must be in YYYMM format. If omitted defaults to current month.       |

### Request headers

- See [Partner REST headers](headers.md) for more information.

### Request example

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer 
Host: api.partner.microsoft.com

```

## REST response

If successful, this method returns foreign exchange rates as a file stream.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 18548
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=fxrates
Request-ID: 65fb6e59-051b-42f7-8771-c8c139b3c901
Date: Wed, 02 Oct 2019 03:42:54 GMT

"CurrencyCode","USDPerUnit","Month"
"AED","0.27224589249009701","2019”
======= Truncated ==============

```
