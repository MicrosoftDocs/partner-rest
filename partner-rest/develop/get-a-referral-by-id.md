---
title: Get a referral by ID
description: How to get a referral by ID
ms.date: 02/07/2019
ms.localizationpriority: medium
---

# Get a referral by ID


**Applies To**

- Partner 


This topic explains how to get a referral by ID.


## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites

- Credentials as described in [Partner authentication](authentication.md). This scenario supports authentication with App+User credentials.


## <span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request

**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **GET** | https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}                                     |

 
**URI parameter**

Use the following ID in the URL

| Name                   | Type     | Required | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | string   | Yes       | A referral ID       |

**Request headers**

- See [Partner REST headers](headers.md) for more information.

**Request body**

This table describes the [Referral](referral-resources.md) properties in the request body.
    
**Request example**

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/0d43414c-fb9f-4ca0-9b8d-29deb70364cf HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

```


## <span id="Response"/><span id="response"/><span id="RESPONSE"/>REST Response

If successful, this method returns the populated [Referral](referral-resources.md) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` http
{
    
    "@odata.context": "https://api.partner.microsoft.com/v1.0/engagments/referrals/$metadata#Referrals/$entity",
    "id": "61c65491-2f2c-461a-84b4-3654499bc1d9",
    "engagementId": "b1c40bb4-6d36-4eca-baa3-e1460cf2a454",
    "createdDateTime": "2018-10-29T21:24:52.040469Z",
    "updatedDateTime": "2018-10-29T21:24:52.040469Z",
    "expirationDateTime": "2018-11-06T00:00:00Z",
    "status": "New",
    "substatus": "Pending",
    "statusReason": null,
    "qualification": "SalesQualified",
    "type": "Independent",
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
            "region": "Washington"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": [
                {
                "profileType": "Duns",
                "id": "795986822"
                }
            ]
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, Can you help this customer? Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq 'b1c40bb4-6d36-4eca-baa3-e1460cf2a454'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/61c65491-2f2c-461a-84b4-3654499bc1d9",
            "method": "GET"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\""
}
```
