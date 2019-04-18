---
title: Partner API authentication
description: Configure your authentication settings to use the Partner API, which uses Azure AD for authentication.
ms.date: 04/12/2019
ms.localizationpriority: medium
---

# Partner API authentication

The Partner API utilizes Azure Active Directory (Azure AD) for authentication. When you interact with the Partner API, you must correctly configure an Azure AD application and then request an access token. You can use access tokens obtained using app + user authentication with the Partner API. 

## Setting up an application

> [!TIP]
> This method is recommended because there is no need to update your username or password in order to keep getting leads. When you use the Azure AD option, you provide the app ID, application key, and directory ID from your Azure AD application.

To configure Azure AD for Microsoft Dynamics CRM:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Select the Azure AD service.
2. Select **App registrations**, then select **New application registration**.
3. Create your new application. For **Application type**, select **Native**. Provide a name and URL, then select **Create**.
4. After creating your application, select **Settings**.
5. Access **Required permissions** through the API. Select **Add**, then select **Select an API** 
6. Search for the *Microsoft Partner* application API. Set the **Delegated Permissions** to **Partner Center**. 
8. For the application you registered, select **Properties** and then select **copy the Application Id**.
9. Select **Settings** and then **Keys**. Create a new key with the **Duration** set to **Never expires**, then select **Save**. 
10. On the **Keys** menu, select **Copy the key value**. Save a copy of this value. 

> [!WARNING]
> Be sure to save a copy of the key value for the key you created. You will need to use this key value later to obtain a token.

## Partner Consent

In the Azure management portal, select **Enterprise applications**. Search for the application you created in the previous section, and select that application. Select **Permissions** , then select **Grant Admin Consent for Partner Account**.