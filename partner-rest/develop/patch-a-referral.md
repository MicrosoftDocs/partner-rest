---
title: Update a lead or opportunity
description: Allows you to update the lead or opportunity details.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
---

# Update a lead or opportunity

Applies to:

- Partner API

This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.

## Prerequisites

- Credentials as described in [Partner API authentication](api-authentication.md). This scenario supports authentication with App+User credentials.
- This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.

## REST Request

### Request syntax

| Method  | Request URI                                                       |
|---------|-------------------------------------------------------------------|
| **PATCH** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### URI parameter


| Name                   | Type     | Required | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | string   | Yes       | The unique identifier for a lead or co-sell opportunity       |

### Request headers

See [Partner REST headers](headers.md) for more information.

### Request body

The request body follows the [Json Patch](https://tools.ietf.org/html/rfc6902) format. A JSON Patch document has an array of operations. Each operation identifies a particular type of change. Examples of such changes include adding an array element or replacing a property value.

> [!Important]
> The API currently only supports the `replace` and `add` operations.

### Request example

```http
PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
Authorization: Bearer <token>
Content-Type: application/json
Prefer: return=representation

[
    {
        "op": "replace",
        "path": "/details/dealValue",
        "value": "10000"
    },
    {
        "op": "add",
        "path": "/team/-",
        "value": {
            "email": "jane.doe@contoso.com",
            "firstName": "Jane",
            "lastName": "Doe",
            "phoneNumber": "0000000001"
        }
    }
]
```

> [!Note]
> If the **If-Match** header is passed, it will be used for concurrency control.

## REST Response

If successful, the response body contains the updated [lead or opportunity](referral-resources.md).


### Response success and error codes

Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information. Use a network trace tool to read this code, the error type, and additional parameters.

### Response example

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> The response body depends on the **Prefer** header. If the header value is omitted in the request, the response body is empty with a HTTP Status code 204. Add `Prefer: return=representation` to the header to get the updated lead or opportunity.

## Sample requests

1. Updates the deal value for the opportunity to 10000 and updates the notes. There are no concurrency checks because of the absense of the `If-Match` header.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. Updates the status of a lead or opportunity to Won.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace", "path":"/status", "value":"Closed"},
        {"op":"replace", "path":"/substatus", "value":"Won"}
    ]
    ```

    > [!Important]
    > The `status` and `substatus` fields should conform to the allowed set of transition values as described [here](referral-resources.md).

3. Adds a new member from your organization to the lead or opportunity team. The response will contain the updated lead or opportunity because of the presence of the `Prefer: return=representation` header.

    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    Prefer: return=representation
    
    [
        {
            "op": "add",
            "path": "/team/-",
            "value": {
                "email": "jane.doe@contoso.com",
                "firstName": "Jane",
                "lastName": "Doe",
                "phoneNumber": "0000000001"
            }
        }
    ]
    ```
