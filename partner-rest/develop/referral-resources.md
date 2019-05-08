---
title: Referral resources
description: Resources that represents a sales lead direct from a customer, Microsoft, or another partner.
ms.date: 04/18/2019
ms.localizationpriority: medium
---

# Referral resources

**Applies To**

- Partner Center

Resources that represent a sales lead direct from a customer, Microsoft, or another partner.   


## Referral

Represents the referral.

| Property              | Type                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | string                                            | The ID for this Referral.                                                                                         |
| EngagementId          | string                                            | The EngagementID for this Referral. Multiple referrals can be associated to a single EngagementID                 |
| Name                  | string                                            | The name of the Referral.                 |
| ExternalReferenceId   | string                                            | An external identifier for the referral. Example: Store your own Dynamics 365 lead/opportunity ID                    |
| CreatedDateTime       | string in UTC date time format                    | The date the referral was created.                                                                                |
| UpdatedDateTime       | string in UTC date time format                    | The date the referral was last updated.                                                                           |
| ExpirationDateTime    | string in UTC date time format                    | The date the referral will expire.                                                                                |
| Status                | [ReferralStatus](referral-resources.md#referralstatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status. |
| Substatus          | [ReferralSubstatus](referral-resources.md#referralsubstatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral sub status. |
| StatusReason          | string                                            | A descriptive message about the status. Example: Why was the referral lost? |
| ReferralType          | [ReferralType](referral-resources.md#referraltype)          | Represents the referral type.                                                                                     |
| Qualification         | [ReferralQualification](referral-resources.md#referralqualification)| Represents the quality of the referral.                                                                           |
| CustomerProfile       | [CustomerProfile](referral-resources.md#customerprofile)    | Information about the customer.                                                                                     |
| Consent               | [Consent](referral-resources.md#consent)                    | Consent flags around sharing information with other organizations and allowing them to contact users.         |
| Details               | [ReferralDetails](referral-resources.md#referraldetails)    | Customer details, notes, deal value, currency closing date.                                                                |
| Team                  | [Member](referral-resources.md#member)                      | Represents users in the organizations that are involved.                                |
| InviteContext         | [InviteContext](referral-resources.md#invitecontext)        | Represents additional information a user can provide when inviting another organization into the partner engagement.  |
| ETag                  | string                                            | ETags are used and required for concurrency checking when updating resources. |
| Target         | [ReferralTarget](referral-resources.md#target)        | Represents additional information a user can provide when inviting another organization into the partner engagement.  |


## ReferralStatus

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.

| Value           | Description                                                                                |
|-----------------|---------------------------------------------------------------------------------------------|
| None            |                                                                                             |
| New             | Represents a new referral.                                                                 |
| Active          | Represents an active referral.                                                             |
| Closed          | Represents a closed referral.                                                              |


## ReferralSubstatus

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.

| Value           | Description                                                                                |
|-----------------|--------------------------------------------------------------------------------------------|
| None            |                                                                                            |
| Pending         | Represents a new referral that is pending.                                                 |
| Received        | Represents a new referral that has been received.                   |
| Accepted        | Represents a active referral that has been accepted.                                                    |
| Won             | Represents a closed referral that has been won.                                            |
| Lost            | Represents a closed referral that has been lost.                                           |
| Declined        | Represents a closed referral that has been declined.                                       |
| Expired         | Represents a closed referral that has expired.                                             |

**Status & Substatus transition states**

| Status                | Allowed Status Transition     | Allowed Substatus                |
|-----------------------|-------------------------------|---------------------------------------|
| New                   | New, Active, Closed           | Pending, Received                     |
| Active                | Active, Closed                | Accepted                              |
| Closed                | Closed                        | Won, Lost, Declined, Expired          |


## ReferralType

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral type.

| Property              | Description                                                                     |
|-----------------------|---------------------------------------------------------------------------------|
| Shared                | Represents a referral in which all parties involved will collaborate to close.  |
| Independent           | Represents a referral in which two parties will collaborate to close.           |


## ReferralQualification

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.

| Value                | Description                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------|
| None                 | Represents a referral that has no quality measure associated.                               |
| Direct               | Represents a referral that has been created directly by a customer.                         |
| MarketingQualified   | Represents a referral that has been generated via Microsoft marketing automation systems.   |
| SalesQualified       | Represents a referral from a Microsoft sales agent.                                         |


## CustomerProfile

Contains the customer contact information.

| Property | Type                                                   | Description                                            |
|----------|--------------------------------------------------------|--------------------------------------------------------|
| Id       | string                                                 | The Id for this CustomerProfile.                       |
| Name     | string                                                 | The customer organization name.                        |
| Address  | [Address](referral-resources.md#address)                         | The address of the customer.                           |
| Size     | string                                                 | The number of employees at the customers organization. |
| Team     | [Member](referral-resources.md#member)                           | The contacts for the customer organization.            |
| Ids      | [CustomerProfileType](referral-resources.md#customerprofiletype) | External ID's for the customer.                        |


## CustomerProfileType

Contains the External ID's for the customer. 

| Property | Type   | Description                                                                           |
|----------|--------|---------------------------------------------------------------------------------------|
| Duns     | string | The [Dun & Bradstreet number](https://www.dnb.com/duns-number.html) for the customer. |
| External | string | A customer ID unique to your organization.                                            |


## Address

An address to use for the customer.

| Property     | Type   | Description                                                |
|--------------|--------|------------------------------------------------------------|
| AddressLine1 | string | The first line of the address.                             |
| AddressLine2 | string | The second line of the address. This property is optional. |
| City         | string | The city.                                                  |
| State        | string | The state.                                                 |
| PostalCode   | string | The zip code or postal code                                |
| Country      | string | The country/region in ISO country code format[CountryCodes](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.regioninfo.threeletterisoregionname?view=netframework-4.7.2).             |
| Region       | string | The region.                                                |


## Member

Describes contact information for a specific individual.

| Property    | Type   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | string | The contact's first name.    |
| LastName    | string | The contact's last name.     |
| PhoneNumber | string | The contact's phone number.  |
| Email       | string | The contact's email address. |
| ContactPreference       | [ContactPreference](referral-resources.md#contactpreference) | The contact's preference for receiving email notifications. |

## ContactPreference

Describes contact preferences for receiving email notifications.

| Property    | Type   | Description                  |
|-------------|--------|------------------------------|
| Locale   | string | The locale of the email notification. [AllCultures](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_AllCultures), [NeutralCultures](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_NeutralCultures), and [SpecificCultures](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_SpecificCultures) are supported  |
| DisableNotifications    | bool | Will disable email notifications for the user.     |


## Consent

Consent flags around sharing information with other organizations and allowing them to contact users.

| Property                                         | Type      | Description                                                                                |
|--------------------------------------------------|-----------|--------------------------------------------------------------------------------------------|
| ConsentToToShareInfoWithOthers                   | boolean   | Indicates consent to share personally identifiable information (PII) with others.             |
| ConsentToContact                                 | boolean   | Indicates consent to contact users.  |


## InviteContext

Additional information that can be shared when inviting another organizations. 

| Property              | Type                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Notes                 | string                                                     | Additional notes for the receiving organization.                |
| InvitedBy | [InvitedBy](referral-resources.md#invitedby)                                     | The organization ID that sent the referral.                                   |

## InvitedBy

Additional information that can be shared when inviting another organizations. 

| Property              | Type                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| OrganizationId        | string                                                     | The organization ID that sent the referral.                |
| OrganizationName      | string                                                     | The organization name that sent the referral.                                   |

## ReferralDetails

Represents the referral details.

| Property              | Type                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Notes                 | string                                                     | Additional notes for the receiving organization.                |
| DealValue             | decimal                                                    | Value of the referral.                                    |
| Currency              | string                                                    | The [ISO 4217 currency symbol](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.regioninfo.isocurrencysymbol?view=netframework-4.7.2)                                   |
| ClosingDateTime       | string in UTC date time format                         | Date the customer is looking to close by.                           |
| Requirements          | [ReferralRequirements](referral-resources.md#referralrequirements)   | Industry, products, service type, and solutions the customer is interested in.|


## ReferralRequirements

Contains the customer requirements.

| Property        | Type                                                         | Description                                          |
|-----------------|--------------------------------------------------------------|------------------------------------------------------|
| Industries      | [Tag](referral-resources.md#tag)                                       | The industries the customer is interested in.        |
| Products        | [Tag](referral-resources.md#tag)                                       | The products the customer is interested in.          |
| Services        | [Tag](referral-resources.md#tag)                                       | The services the customer is interested in.          |
| Solutions       | [SolutionTag](referral-resources.md#solutiontag)                       | The solutions the customer is interested in.                             |

## SolutionTag

Contains the solution details.

| Property        | Type                                         | Description                                          |
|-----------------|----------------------------------------------|------------------------------------------------------|
| Id              | string                                       | The ID of the solution.        |
| Name            | string                                       | The name of the solution.          |
| SolutionType    | [SolutionType](referral-resources.md#solutiontype)     | The type of solution.          |

## SolutionType

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the solution type.

| Property        | Description                                                     |
|-----------------|-----------------------------------------------------------------|
| None            |                                                                  |
| Category        |  Leverages pre-defined solution names.                            |
| Name            |  Ability to reference solutions from the Microsoft catalog. |


## Target

Describes the Referral Target.

| Property                  | Type                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | string                                                | The ID of the referral target. 
| Type                      | [ReferralTargetType](referral-resources.md#targettype) | Referral target type


## TargetType

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the solution type.

| Property        | Description                                                     |
|-----------------|-----------------------------------------------------------------|
| None            |                                                                  |
| BusinessProfileLocation         |  Profile location from the partner business profile.                            |
| SolutionProfile            |  Solution profile of the partner. |


## Tag

Describes the tag.

| Property                  | Type                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | string                                                | The ID for this tag.                                          |


### Products

| Value        |
|-----------------|
|Azure|
|EnterpriseMobilityAndSecurity|
|Exchange|
|DeveloperTools|
|Dynamics365Business|
|Dynamics365Enterprise|
|DynamicsAX,GP,NAV,SL|
|Microsoft365|
|Office|
|PowerBI|
|Project|
|SharePoint|
|SkypeForBusiness|
|Surface|
|SurfaceHub|
|SQL|
|Teams|
|Visio|
|Windows|
|Yammer|

### Services

| Value        |
|-----------------|
|ConsultingAndProfessional|
|CustomSolution(ISV)|
|DeploymentOrMigration|
|Hardware|
|Integration|
|IPServices(ISV)|
|LearningAndCertification|
|Licensing|
|ManagedServices|
|ProjectServices|


### Industries

| Value        |
|-----------------|
|Agriculture, Forestry, & Fishing|
|Communications & Media|
|Education|
|Financial Services|
|Government|
|Healthcare|
|Hospitality|
|Manufacturing|
|Power & Utilities|
|Public Safety and National Security|
|Retail & Consumer Goods|
|Services|
|Travel & Transportation|
|Wholesale & Distribution|


### Solutions

| Value        |
|-----------------|
|AdvancedAnalytics|
|ApplicationIntegration|
|ArtificialIntelligence|
|AzureSecurityOperationManagement|
    |AzureStack|
    |BackupDisasterRecovery|
    |BigData|
    |Blockchain|
    |Chatbot|
    |CloudDatabaseMigration|
    |CloudMigration|
    |CloudVoice|
    |CognitiveServices|
    |CompetitiveDatabaseMigration|
    |Containers|
    |DataWarehouse|
    |DatabaseonLinux|
    |DevelopmentandTest|
    |DevOps|
    |DigitalMedia|
    |Dynamics365forCustomerService|
    |Dynamics365forFieldService|
    |Dynamics365forFinanceOperations|
    |Dynamics365forRetail|
    |Dynamics365forSales|
    |Dynamics365forTalent|
    |DynamicsonAzure|
    |EnterpriseBusinessIntelligence|
    |Gaming|
    |HighPerformanceComputing|
    |HybridStorage|
    |IdentityandAccessManagement|
    |InformationManagement|
    |InternetofThings|
    |MachineLearning|
    |Microserviceapplications|
    |MobileApplications|
    |MySQLPostgresMigrationtoAzure|
    |Networking|
    |NoSQLMigration|
    |RedhatonAzure|
    |RegulatoryComplianceGDPR|
    |SAPonAzure|
    |ServerlessComputing|
    |SharepointonAzure|
    |SQLServerUpgrade|
    |ThreatProtection|
    |WebDevelopment|


### Customer Size

| Value        |
|-----------------|
|    1to50employees|
|    51to500employees|
|    Morethan500employees|
|    1to9employees|
|    10to50employees|
|    51to250employees|
|    251to1000employees|
|    1001to5000employees|
|    5001to10000employees|
|    10001to20000employees|
|    Morethan20000employees|
