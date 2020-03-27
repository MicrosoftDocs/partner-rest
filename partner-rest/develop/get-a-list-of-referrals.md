---
title: Get a list of referrals
description: How to get a list of referrals using the Partner API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partner-center-sdk
ms.localizationpriority: medium
---

# Get a list of referrals

Applies to:

- Partner API

This topic explains how to get a list of referrals.

## Prerequisites

- Credentials as described in [Partner API authentication](api-authentication.md). This scenario supports authentication with App+User credentials.

## REST request

### Request syntax

| Method  | Request URI                                                  |
|---------|--------------------------------------------------------------|
| **GET** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### Supported OData operations

| Name     | Description            | Example                                                                    |
|:---------|:-----------------------|:---------------------------------------------------------------------------|
| $filter  | Filters results (rows) |`/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` |
| $orderby | Orders results         |`/referrals?$orderby=createdDateTime desc`                                  |

#### Supported filter parameters

Use the following filter parameters to get a list of referrals

| Name         | Type   | Required | Description                                                                             |
|--------------|--------|----------|-----------------------------------------------------------------------------------------|
| engagementId | string | No       | An engagement ID.                                                                       |
| status       | string | No       | A string that represents a [ReferralStatus](referral-resources.md#referralstatus)       |
| substatus    | string | No       | A string that represents a [ReferralSubstatus](referral-resources.md#referralsubstatus) |
| updatedDateTime     | string | No       | UpdatedDatetime of the referral |
| email     | string | No       | Team contact email of the referal |

#### Supported orderby parameters

Use the following orderby parameters to get a list of referrals

| Name           | Type     | Required | Description                        |
|----------------|----------|----------|------------------------------------|
|createdDateTime | DateTime | Yes      | Created date and time of Referrals |

### Request headers

- See [Partner REST headers](headers.md) for more information.

### Request body

None.

### Request example

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

```

## REST response

If the request is successful, the response body contains a collection of [referral resources](referral-resources.md) in the response body.

### Response success and error codes

Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information. Use a network trace tool to read this code, the error type, and additional parameters.

### Response example

``` http
{
    "@odata.context": "http://api.partner.microsoft.com/v1.0/$metadata#Referrals",
    "@odata.count": 100,
    "value": [
        {
            "id": "c5fbb3b6-be74-4795-9fb5-4324c73fed37",  
            "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
            "organizationName": "Contoso Company",
            "engagementId": "65edc0b5-3485-41b7-a17e-dfa9ef4706e2",
            "externalReferenceId": "",
            "createdDateTime": "2018-10-30T21:03:42.4579542Z",
            "updatedDateTime": "2018-10-30T21:03:42.4579542Z",
            "expirationDateTime": "2018-11-13T00:00:00Z",
            "status": "New",
            "substatus": "Pending",
            "qualification": "Direct",
            "type": "Independent",
            "target": [
                    {
                        "type": "BusinessProfileLocation",
                        "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
                    }
            ],
            "customerProfile": {
                "name": "Fabrikam Customer Inc",
                "address": {
                    "addressLine1": "One Microsoft Way",
                    "addressLine2": "",
                    "city": "Redmond",
                    "state": "WA",
                    "postalCode": "98052",
                    "country": "US"
                },
                "size": "1to9employees",
                "team": [
                    {
                        "contactPreference": {
                            "locale": "en-US",
                            "disableNotifications": false
                        },
                        "firstName": "Sue",
                        "lastName": "Smith",
                        "phoneNumber": "1234567890",
                        "email": "sue.smith@fabrikam.com"
                    }
                ],
                "ids": {}
            },
            "consent": {
                "consentToContact": true
            },
            "details": {
                "notes": "We are interested in deploying Microsoft 365 and are looking for support in training our employees. Can you help?",
                "requirements": {
                    "industries": [
                        {
                            "id": "Education"
                        }
                    ],
                    "products": [
                        {
                            "id": "Microsoft365"
                        }
                    ],
                    "services": [
                        {
                            "id": "LearningAndCertification"
                        }
                    ]
                }
            }
            "links": {
                "relatedReferrals":
                    {
                       "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
                        "method": "GET"
                    },
                "self":
                    {
                       "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/c5fbb3b6-be74-4795-9fb5-4324c73fed37",
                        "method": "GET"
                    }
            },
        },
        {
            "id": "61c65491-2f2c-461a-84b4-3654499bc1d9",
            "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
            "organizationName": "Contoso Company",
            "engagementId": "b1c40bb4-6d36-4eca-baa3-e1460cf2a454",
            "createdDateTime": "2018-10-29T21:24:52.040469Z",
            "updatedDateTime": "2018-10-29T21:24:52.040469Z",
            "expirationDateTime": "2018-11-06T00:00:00Z",
            "status": "New",
            "substatus": "Pending",
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
                            "locale": "en-US",
                            "disableNotifications": false
                        },
                        "firstName": "Sue",
                        "lastName": "Smith",
                        "phoneNumber": "1234567890",
                        "email": "sue.smith@contoso.com"
                    },
                    {
                        "contactPreference": {
                            "locale": "en-US",
                            "disableNotifications": false
                        },
                        "firstName": "Joe",
                        "lastName": "Hansen",
                        "phoneNumber": "4035698759",
                        "email": "joe.hansen@contoso.com"
                    }
                ],
                "ids": {}
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
                        "locale": "en-US",
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
                    "organizationId": "msft",
                    "organizationName": "Microsoft"
                }
            },
            "links": {
                "relatedReferrals":
                    {
                       "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq 'b1c40bb4-6d36-4eca-baa3-e1460cf2a454'",
                        "method": "GET"
                    },
                "self":
                    {
                       "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/61c65491-2f2c-461a-84b4-3654499bc1d9",
                        "method": "GET"
                    }
            }
        }
    ],
  
 "@odata.nextLink": "http://api.partner.microsoft.com/v1.0/referrals?$skiptoken=k181pEdP0ykypkieJfcxXIN4ARsee8%2fFUEbbvZaoTUZRLJ3o7TADYve12iEDrlgVevJO5J0ftNkTY5FZepU1sh1m8fRNuUD4YPGazoaywpAqoRAd43JuVJV8fwmcJFTFAH4Wg2%2fQFWkxT6PWujvkj%2biqLMDsU8CI6x3k0CHZWhLiw4inmd3Ib8wVoA4wygjONBhcEegyySiZa85H59pWHQoNFA%2fYP6tyw3%2f0CgcSwa%2fh%2bDf7Ygm0MaOhBZbYmkhRITbgRT1LWDLBGpNzLJN%2fB%2basQXEojDL7tZRLB%2bGlfPJ%2fojPBTctFqEp13TVZta2jdJmC917IhR5fGt91%2blwuxd83Y5PwCjXpg%2fYn8JKna10%2bVe4Devy21pryas%2bu3oGKmbqaXKMBIUCQU8D7cFy59R90Tzcogte05QSSiN6U1KP%2bY1oPchrKmvqt8S6jNoy%2bTaR3Bc9AtzVNpuaEGGkfO9g3SFlLuBv%2bd4aG50iFjmOKCAPIRr76JVUzYsJ76oyUv0AOZ%2bW5lqgtyQQwN%2b%2baEkF3HDebb6%2byTqdagjI86faTAi4YOOn0oVmmGIWZJnp5MuG38P8VHqK4ZdZ5OpKkpMrigLqYrU%2fFliGbBgnTP4Y7Pp%2fai9JzxYF1%2fajIYsE0OdyojAG2GtzNzlyHj1g9e9Tgz2%2fy5BfHrk4asYRcSvQfN%2bdaO1NVWCraMvhxjsr5Twcg9z%2bAETNVqXZMp5qKBsPGxPFcnWGx6OY296kmIzuTnDd2igIoye8wj57xO4WEBIW3%2bFIHrBlzh3bV0ljNHBb%2f5eDF68GK6AMmwusqjleiW3iHmZRPeTiMU2oPuzx5"
}
```

If there are more than 100 items in a collection, use `@odata.nextLink` to get the next page of results.

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json
```
