---
title: Create a referral
description: How to create a referral
ms.date: 02/07/2019
ms.localizationpriority: medium
---

# Create a referral


**Applies To**

- Partner API

This topic explains how to create a referral.There are 2 types of referrals:  

1. Independent: When a referral is visible to one partner
2. Shared: When a referral is shared across two parties working together for ex: Microsoft and Partner in a co-selling deal


## <span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites

- Credentials as described in [Partner authentication](authentication.md). This scenario supports authentication with App+User credentials.


## <span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request


**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | https://api.partner.microsoft.com/v1.0/engagements/referrals                                   |

 
**Request headers**

- See [Partner API REST headers](headers.md) for more information.

**Request body**

This table describes the [Referral](referral-resources.md) properties in the request body for a brand new referral.

| Property              | Type                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Name                  | string                                            | The name of the Referral.                 |
| ExternalReferenceId   | string                                            | An external identifier for the referral. For example, your own Dynamics 365 lead or opportunity ID                                                                         |
| CreatedDateTime       | string in UTC date time format                    | The date the referral was created.                                                                                |
| UpdatedDateTime       | string in UTC date time format                    | The date the referral was last updated.                                                                           |
| ExpirationDateTime    | string in UTC date time format                    | The date the referral will expire.                                                                                |
| Status                | [ReferralStatus](referral-resources.md#ReferralStatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status. |
| Substatus             | [ReferralSubstatus](referral-resources.md#ReferralSubstatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral sub status. |
| StatusReason          | string                                            | A descriptive message about the status. For example, explain why the referral was lost. |
| ReferralType          | [ReferralType](referral-resources.md#ReferralType)          | Represents the referral type.                                                                                     |
| Qualification         | [ReferralQualification](referral-resources.md#ReferralQualification)| Represents the quality of the referral.                                                                           |
| CustomerProfile       | [CustomerProfile](referral-resources.md#CustomerProfile)    | Customer contact information.                                                                                     |
| Consent               | [Consent](referral-resources.md#Consent)                    | Consent flags around sharing information with other organizations and allowing them to contact users.         |
| Details               | [ReferralDetails](referral-resources.md#ReferralDetails)    | Customer details, notes, deal value, currency closing date.                                                                |
| Team                  | [Member](referral-resources.md#Member)                      | Represents users in the organizations that are involved in the partner engagement.                                |
| InviteContext         | [InviteContext](referral-resources.md#InviteContext)        | Represents additional information a user can provide when inviting another organization into the partner engagement.  |

**Status & Substatus transition states**

| Status                | Allowed Status Transition     | Allowed Substatus                     |
|-----------------------|-------------------------------|---------------------------------------|
| New                   | New, Active, Closed           | Pending, Received                     |
| Active                | Active, Closed                | Accepted                              |
| Closed                | Closed                        | Won, Lost, Declined, Expired          |

**Request example**

```http
POST https://api.partnercenter.microsoft.com/referrals/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json
 
 {
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
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
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
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
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    }
}
```

## <span id="Response"/><span id="response"/><span id="RESPONSE"/>REST Response

If successful, this method returns the populated [Referral](referral-resources.md) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
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
        "ids": []
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
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```
