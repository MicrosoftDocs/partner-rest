---
title: Referral connectors.
description: How to synchronize referrals.
ms.date: 04/23/2019
ms.localizationpriority: medium
---

# Referral Connectors

This article explains how **referrals connectors** work.

# Prerequisites

- Administrator role on [Microsoft Flow](https://flow.microsoft.com) account.
- Administrator role on Microsoft Dynamics CRM Online instance.
- 
 
### Synchronize referral to lead

A connector does the following to synchronize a referral to a lead from Dynamics CRM:

1. Gets a token to connect to https://api.partner.microsoft.com/v1.0/engagements/referrals.
2. Gets the referral which triggered the connector using https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}.
3. Connects to Microsoft Dynamics CRM.
4. Creates a new lead or updates an existing lead with the latest information on the referral.
5. Updates the referral with the latest updates from the CRM lead.



# Connectors for referrals
You can use connectors for referrals to determine connections between partner referrals and customer relationship management (CRM) leads.


## Prerequisites
* Microsoft Dynamics 365 subscription with sales module enabled
* Administrator access to Microsoft Dynamics 365.
* [Microsoft Flow](https://flow.microsoft.com) subscription
* Administrator access to Microsoft Flow.
* An **application ID** and **secret** to access Partner API. If you don't have these already, see [Partner authentication](api-authentication.md) for setup instructions.
* A [Partner Center Webhook](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhook-events) subscription to [Referral Created](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhook-events#referral-created-event) and [Referral Updated](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhook-events#referral-updated-event) webhook events.

## Configuring Flow Synchronization

You can test that your referral connector flows are synchronized using the flow synchronization packages.

Before you begin, download the two packages to your local machine from the [GitHub repository](#). 
1. [Partner referral to CRM lead flow](#)

After you've downloaded the package, import each package into [Microsoft Flow](https://flow.microsoft.com) using the following steps. 

1. Sign in to [Microsoft Flow](https://flow.microsoft.com) using the appropriate credentials.
3. Choose **My Flows** in the navigation menu.
4. Choose **Import**. 
5. On the **Import package** page, select the flow synchronization package that you downloaded. Then choose **Upload**. 
6. After the package upload is complete, find the package you uploaded in the **Review Package Content** section under **Choose your import options**. 
7. Choose the **Action** button (pencil icon) for your uploaded package. This opens the **Import setup** blade.
8. Choose your **Setup** type.
    * To create a new flow, select **Create as new**, and enter a new **Resource name**.
    * To update an existing flow with the same name, select **Update**.
<!-- Do they need to save their Setup selection manually? Or does it autosave when they close the Import Setup blade? -->
9. On the **Import package** page, find your Dynamics 365 connection in the **Review Package Content** section under **Related Resources**.
10. Choose the **Action** button (pencil icon) for your Dynamics 365 connection. This opens the **Import setup** blade for this related resource. 
11. Choose **Create new** to create a new Dynamics 365 connection, or select an existing connection. 
12. Verify that the **Import package** page now shows your selected flow setup type and Dynamics 365 connection. Then choose **Import**.
13. Confirm a Flow instance is now created. 

### Configure parameters in the flow
1. Select **Flow resource/instance** created.
2. Click on **Edit**
3. Select **AppID** variable, enter value of **application id** of the AAD application.
4. Select **Key** variable, enter value of **secret key** of the AAD application.
5. Select **Tenant** variable, enter value of **tenant id** of AAD application.
6. **Save** changes to the flow. 

### Register flow with Partner Center

1. In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.
2. Choose one of the flows that you just created. 
3. On the flow page, choose **Edit flow**.
4. Copy and save the flow's **HTTP POST URL**. You will need to use this URL in the next step to trigger the flow. 
5. [Register to receive events]("https://api.partnercenter.microsoft.com/webhooks/v1/registration") using the following body format. 

```json
{
    "WebhookUrl": "<<FlowUrl>>",
    "WebhookEvents": [
        "referral-created",
        "referral-updated"
    ],
    "signatureTokenToMsSignatureHeader": true
}
```