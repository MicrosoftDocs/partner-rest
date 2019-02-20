---
title: Partner API REST headers
description: The following HTTP request and response headers are supported by the Partner REST API.
ms.date: 02/11/2019
ms.localizationpriority: medium
---

# Partner REST API headers

The following HTTP request and response headers are supported by the Partner REST API. Not all API calls accept all headers.

## <span id="Request_headers"/><span id="request_headers"/><span id="REQUEST_HEADERS"/>Request headers

The following HTTP request headers are supported by the Partner 
REST API.

| Header                       | Value Type | Description                                                                            |
|------------------------------|------------|----------------------------------------------------------------------------------------|
| Authorization:               | string     | Required. The authorization token in the form Bearer &lt;token&gt;.                    |
| Accept:                      | string     | Specifies the request and response type, "application/json".                           |
| MS-RequestId:                | GUID       | A unique identifier for the call, used to ensure id-potency. In the case of a timeout, the retry call should include the same value. Upon receiving a response (success or business failure), the value should be reset for the next call. |
| MS-CorrelationId:            | GUID       | A unique identifier for the call, useful in logs and network traces for troubleshooting errors. The value should be reset for every call. All operations should include this header. |
| MS-Contract-Version:         | string     | Required. Specifies the version of the API requested; generally api-version: v1 unless otherwise specified in the [Scenarios](scenarios.md) section. |
| If-Match:                    | string     | Used for concurrency control. Some API calls require passing the ETag via the If-Match header. The ETag is usually on the resource and therefore, requires GET-ting the latest. |
| MS-PartnerCenter-Application | string     | Optional. Specifies the name of the application that is using the Partner REST API.    |
| X-Locale:                    | string     | Optional. Specifies the language in which the rates are returned. Default is "en-US".  |

## <span id="Response_headers"/><span id="response_headers"/><span id="RESPONSE_HEADERS"/>Response headers

The following HTTP response headers may be returned by the Partner REST API.

| Header            | Value Type | Description                                                                                      |
|-------------------|------------|--------------------------------------------------------------------------------------------------|
| Accept:           | string     | Specifies the request and response type, "application/json".                                     |
| MS-RequestId:     | GUID       | A unique identifier for the call, used to ensure id-potency. In the case of a timeout, the retry call should include the same value. Upon receiving a response (success or business failure), the value should be reset for the next call. |
| MS-CorrelationId: | GUID       | A unique identifier for the call, useful the logs and network traces for troubleshooting errors. The value should be reset for every call. All operations should include this header.                                                |
