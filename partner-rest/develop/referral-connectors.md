---
title: Referral connectors.
description: Synchronize partner referrals with Dynamics 365 CRM leads using Microsoft Flow.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
---

# Referral connectors

You can use referral connectors to synchronize partner referrals with customer relationship management (CRM) leads. You can create a referral connector using [Microsoft Flow](https://flow.microsoft.com) as the HTTPS endpoint to receive partner referrals. You can then write the referral received by the flow to a CRM system as a lead.

## Prerequisites

* Microsoft Flow subscription
  * Account with administrator access to this subscription
* Azure Active Directory (Azure AD) application ID, user id, password and tenant ID (used to access the Partner API). For setup instructions, see [Partner authentication](api-authentication.md).
* [Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) subscription.
* [Partner Center webhook event](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) subscription to [Referral Created](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) and [Referral Updated](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) events.
* [Microsoft Dynamics 365](https://dynamics.microsoft.com) subscription
  * Sales module enabled
  * Account with administrator access to this subscription

## Flow overview

Referrals are imported into the CRM using the following flow:

1. Partner sets up a webhook to receive referral notifications.
2. Partner registers the webhook with Partner Center. The partner also subscribes to webhook events for when referrals are created or updated.
3. Referral client creates or updates a referral.
4. Partner Center webhook system checks for the partner's registration and sends a notification to the webhook.
5. Webhook receives the notification.
6. Flow document in Microsoft flow uses a token to make a call to the Partner Center referral API.
7. Flow endpoint gets the referral.
8. Flow endpoint creates the CRM lead.

![Flow chart showing the steps in this section for importing partner referrals into the CRM.](../images/referralwebhook.png)

## Flow document process

The flow document for a referral connector synchronizes a partner referral with a CRM lead from Dynamics 365.

1. Connector gets a token to connect to `https://api.partner.microsoft.com/v1.0/engagements/referrals`.
2. Connector obtains referral that triggered the connector using `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}`.
3. Connector connects to Dynamics 365.
4. Connector creates a new lead or updates an existing lead with the latest information on the referral.
5. Connector updates referral with the latest updates from the CRM lead.

![Flow chart showing the steps in this section for the flow document process.](../images/ReferralFlowSteps.png)

## Sample referral connector

The following *sample referral connector* shows how to synchronize Partner Center referrals to CRM leads in Dynamics 365.

> [!IMPORTANT]
> You can write to different CRMs by replacing the [flow connectors](https://flow.microsoft.com/en-us/connectors/) in the sample code.

### Import flow synchronization package

Download and import the *sample code package* into Microsoft Flow and connect to Dynamics 365:

1. Download the [flow synchronization package](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) from the [GitHub repo](https://github.com/microsoft/Partner-Center-Referrals).
2. Sign in to [Microsoft Flow](https://flow.microsoft.com) using the appropriate credentials.
3. Choose **My Flows** in the navigation menu. Then choose **Import**.
4. On the **Import package** page, select the flow synchronization package that you downloaded. Then choose **Upload**.

    ![Import package screen for package files](../images/importPackage.png)

5. After the package upload is complete, find the package you uploaded in the **Review Package Content** .

    ![Details of import package screen](../images/importPackageDetails.png)

6. Choose the **Action** button (pencil icon) for your uploaded package. This opens the **Import setup** blade.
7. Choose your **Setup** type.

    * To create a new flow, select **Create as new**, and enter a new **Resource name**.
    * To update an existing flow with the same name, select **Update**.

    ![Create or update new pacakge screen](../images/CreateNewConnection.png)

8. On the **Import package** page, find your Dynamics 365 connection in the **Review Package Content** section under **Related Resources**.
9. Choose the **Action** button (pencil icon) for your Dynamics 365 connection. This opens the **Import setup** blade for this related resource.
10. Choose **Create new** to create a new Dynamics 365 connection, or select an existing connection.
11. Verify that the **Import package** page now shows your selected flow setup type and Dynamics 365 connection. Then choose **Import**.

    ![Import package status screen](../images/importStatus.png)

12. Verify that your flow resource is now created or updated.

### Configure flow parameters

Configure the parameters of your flow resource:

1. In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.
2. Choose the flow resource you created or updated in the previous section.
3. On the flow page, choose **Edit flow**.
4. Choose the **AAD-Application (client) ID** variable and enter the ID of your Azure AD application.
5. Choose the **UserId** variable and enter your user ID.
6. Choose the **UserPassword** variable and enter your user password.
7. Select the **AAD-Directory (tenant) ID** variable. Enter the tenant ID of your Azure AD application.
8. Choose **Save** to save your flow.

    ![Flow variables settings screen](../images/SetFlowVariables.png)

### Authenticate the callback

Authenticate the callback event from the Partner Center:

> [!TIP]
> For an example, see the [sample function app code](#sample-function-app-code) in the following section.

1. [Create an Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) that [authenticates the callback event from the Partner Center](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).

    1. Verify that the required headers are present (**Authorization**, **x-ms-certificate-url**, and **x-ms-signature-algorithm**).
    2. Download the certificate used to sign the content (**x-ms-certificate-url**).
    3. Verify the certificate chain.
    4. Verify the **Organization** of the certificate.
    5. Read the content with UTF-8 encoding into a buffer.
    6. Create an RSA Crypto Provider.
    7. [Verify that the signature matches](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) what was signed with the specified hash algorithm (for example, SHA256).
    8. If the verification succeeds, an **OK** message is returned.

2. Note the generated callback URI for your function app's HTTP endpoint. This URI is displayed when you create your function app. You can also find this URI on your function app's Azure resource page.
3. In [Microsoft Flow](https://flow.microsoft.com), edit the flow "Partner Referral to Microsoft Dynamics CRM Lead" that you imported in the section *[Import flow synchronization package](#import-flow-synchronization-package)*.

    1. Add the value of the function app's URI to the "web hook certificate validation" step.
    2. Copy and paste your function app's callback URI into the flow document.
    3. Save your flow document.

#### Sample function app code

```csharp
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;
using System;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Security.Cryptography.X509Certificates;
using System.Text;
using System.Threading.Tasks;

public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
    string requestBody = null;
    if (!string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-certificate-url")) && !string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-signature-algorithm")))
    {
        var certificateUrl = req?.Headers["x-ms-certificate-url"].First();
        try
        {
            string resultContent = null;
            using (var client = new HttpClient())
            {
                var result = await client.GetAsync(req.Headers["x-ms-certificate-url"].First());
                resultContent = await result.Content.ReadAsStringAsync();
                log.LogInformation(resultContent);
            }
            if (!string.IsNullOrEmpty(resultContent))
            {
                var certificate = new X509Certificate2(Encoding.UTF8.GetBytes(resultContent));
                var validationResult = certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
                if (validationResult)
                {
                    return new OkResult();
                }
                else
                {
                    return new BadRequestResult();
                }
            }
        }
        catch (Exception)
        {
            new BadRequestObjectResult("Certificate could not be retrieved, invalid caller to flow");
        }

        requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
    }
    else
    {
        new BadRequestObjectResult("Missing headers");
    }

    return new BadRequestObjectResult("Certificate validation failed");
}

private static string GetFirstValueFromHeader(HttpRequest request, string headerName)
{
    StringValues matchingHeaderValues;
    request.Headers.TryGetValue(headerName, out matchingHeaderValues);
    return matchingHeaderValues.Count != 0 ? matchingHeaderValues.First() : string.Empty;
}
```

### Register flow with Partner Center

Register your flow resource with the Partner Center to trigger the flow and receive webhook events:

1. In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.
2. Choose the flow you created or updated.
3. On the flow page, choose **Edit flow**.
4. Copy and save the flow's **HTTP POST URL**. You will need to use this URL to trigger the flow.
5. [Register to receive webhook events](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) when referrals are created or updated. Use the following body format:

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
