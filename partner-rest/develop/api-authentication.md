---
title: Partner API authentication
description: Partner API uses Azure AD for authentication, and to use the Partner APIs you must configure your authentication settings correctly.
ms.date: 02/21/2019
ms.localizationpriority: medium
---

# Partner API authentication

Partner API utilizes Azure Active Directory for authentication. When interacting with the Partner API you must correctly configure an Azure AD application and then request an access token. Access tokens obtained using app + user authentication can be used with the Partner API. Following are the steps for configuring an application

[Setting up an application]
2. Partner Consent

## Setting up an applicaiton
   We recommend this option because you get the added benefit of never needing to update your username/password in order to keep getting leads. To use the Azure Active Directory option you provide the App Id, Application Key, and Directory Id from your Active Directory application.

Use the following steps to configure Azure Active Directory for Dynamics CRM.

1. Sign in to [Azure portal](https://portal.azure.com/) and then select the Azure Active Directory service.
2. Select **App registrations**, and then select **New application registration**.
3. For *Application type*, select **Native**, provide a name and an URL, select **Create**.
4. Once the application is created, select **settings**.
5. API access **Required permissions** then select **Add** then **Select an API** 
6. Search for "Microsoft Partner", which is the Microsoft Partner application. Set the **Delegated Permissions** to **Partner Center**. 

    ![Import flow](./images/partner-newgateway-app.png)

8. Now that your application is registered, select **Properties** and then select **copy the Application Id**.
9. Select **settings**, **Keys** and create a new key with the Duration set to *Never expires*. Select **Save** to create the key. 
10. On the Keys menu, select **Copy the key value.** Save a copy of this value because you'll need it for getting a token. 

## Partner Consent

In the Azure management portal, **Enterprise applications**. Search for "Application created in the step above". Select the "Application created above". Click on **Permisisons** , then click on **Grant Admin Conset for Partner Account**.
