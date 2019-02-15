---
title: Partner API REST error codes
description: Partner REST APIs return a JSON object that contains a status code that indicates whether your request was successful or why it failed.
ms.date: 02/11/2019
ms.localizationpriority: medium
---

# Partner API REST error codes

**Applies To**

- Partner API

Partner REST APIs return a JSON object that contains a status
code that indicates whether your request was successful or why it
failed.

- Success responses: A 2xx status code indicates that the client's
    request was successfully received, understood, and accepted.
- [Error responses](#pc_error_payload)
- Error codes
    - 400: Bad request
    - 401: Unauthorized
    - 403: Forbidden
    - 404: Not found
    - 405: Method not allowed
    - 406: Not acceptable
    - 409: Conflict, error code
    - 412: Precondition failed
    - 429: Too many requests
    - 500: Internal server error
    - 501: Not implemented
    - 502: Bad gateway
    - 503: Service unavailable
    - 504: Gateway timeout

## <span id="pc_error_payload"/><span id="PC_ERROR_PAYLOAD"/>Error responses

The error response is a single JSON object that contains a single property
named **error**. This object includes all the details of the error. You can use the information returned here instead of or in addition to the HTTP status code. The following is an example of a full JSON error body.

The following table and code sample describes the schema of an error
response.

| Name        | Type   | Description                                                                                    |
|-------------|--------|------------------------------------------------------------------------------------------------|
| code        | string | Always returned. Indicates the kind of error that occurred. Non-null.                          |
| message | string | Always returned. Describes the error in detail, and provides additional debugging information. Non-null, non-empty. Maximum length is 1024 characters. |
| innerError        | object  | Inner error contains additional information about the error from the paticular API.                                   |
| target      | string | The target where the error originated.                                                      |



```json
{
  "error": {
    "code": "unAuthorized",
    "message": "Caller is not authorized to access the resource.",
    "target": "referral",
    "innerError": {
      "code": "innerErrorCode",
      "message": "Unauthorized referral access"
    }
  }
}

