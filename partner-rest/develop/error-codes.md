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

Any response with a status code indicating an error (4xx or 5xx)
includes an error message with additional details about the error
condition(s) encountered.

The following table and code sample describes the schema of an error
response.

| Name        | Type   | Description                                                                                    |
|-------------|--------|------------------------------------------------------------------------------------------------|
| code        | string | Always returned. Indicates the kind of error that occurred. Non-null.                          |
| description | string | Always returned. Describes the error in detail, and provides additional debugging information. Non-null, non-empty. Maximum length is 1024 characters. |
| data        | array  | Only returned for some error types. A list of error objects.                                   |
| source      | string | Always returned. The source of the error.                                                      |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
## }
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```

