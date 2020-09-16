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
| **PUT** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### Request headers

- For more information, see [Partner API REST headers](headers.md).

> [!IMPORTANT]
> Be sure to set the **If-Match** header.

### Request body

This table describes the [Referral](referral-resources.md) properties in the request body.

| Property            | Type                                                                 | Description                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Id                  | string                                                               | The ID for this Referral.                                                                                            |
| EngagementId        | string                                                               | The EngagementID for this Referral. Multiple referrals can be associated to a single EngagementID                    |
| Name                | string                                                               | The name of the Referral.                                                                                            |
| ExternalReferenceId | string                                                               | An external identifier for the referral. Example: Store your own Dynamics 365 lead/opportunity ID                    |
| CreatedDateTime     | string in UTC date time format                                       | The date the referral was created.                                                                                   |
| UpdatedDateTime     | string in UTC date time format                                       | The date the referral was last updated.                                                                              |
| ExpirationDateTime  | string in UTC date time format                                       | The date the referral will expire.                                                                                   |
| Status              | [ReferralStatus](referral-resources.md#referralstatus)               | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.          |
| Substatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral sub status.      |
| StatusReason        | string                                                               | A descriptive message about the status. For example, explain why the referral was lost.                              |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Represents the referral type.                                                                                        |
| Qualification       | [ReferralQualification](referral-resources.md#referralqualification) | Represents the quality of the referral.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Customer contact information.                                                                                        |
| Consent             | [Consent](referral-resources.md#consent)                             | Consent flags around sharing information with other organizations and allowing them to contact users.                |
| Details             | [ReferralDetails](referral-resources.md#referraldetails)             | Customer details, notes, deal value, currency closing date.                                                          |
| Team                | [Member](referral-resources.md#member)                               | Represents users in the organizations that are involved in the partner engagement.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | Represents additional information a user can provide when inviting another organization into the partner engagement. |
| Target         | [ReferralTarget](referral-resources.md#target)        | Represents additional information a user can provide when inviting another organization into the partner engagement.  |

### Status and substatus transition states

| Status | Allowed Status Transition | Allowed Substatus            |
|--------|---------------------------|------------------------------|
| New    | New, Active, Closed       | Pending, Received            |
| Active | Active, Closed            | Accepted                     |
| Closed | Closed                    | Won, Lost, Declined, Expired |

### Request example

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
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
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> Remove the `"links": { }` object from the PUT resource.

## REST Response

If successful, this method returns the populated [referral](referral-resources.md) resource in the response body.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
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