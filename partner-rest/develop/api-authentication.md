---
title: Partner API authentication
description: Configure your authentication settings to use the Partner API, which uses Azure AD for authentication.
ms.date: 04/26/2019
ms.localizationpriority: medium
---

# Partner API authentication

The Partner API utilizes Azure Active Directory (Azure AD) for authentication. When you interact with the Partner API, you must correctly configure an Azure AD application and obtain an access token. You can obtain access tokens for [application and user access](#application-and-user-access) or [application-only access](#application-only-access).

## Application and user access

This method is recommended to set up **application and user access** to the API. 

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Select the **Azure Active Directory** service.
3. Select **App registrations**, then select **New application registration**.
4. Create your new application. For **Application type**, select **Native**. Provide a name and URL, then select **Create**.
5. After creating your application, select **Settings**.
6. Access **Required permissions** through the API. Select **Add**, then select **Select an API**
7. Search for the *Microsoft Partner* application API. Set the **Delegated Permissions** to **Partner Center**.

## Application-only access

This method is recommended for **application-only access** setup to the APIs.

> [!IMPORTANT]
> You must provide the application ID, application key, and directory ID from your Azure AD application.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Select the **Azure Active Directory** service.
3. Choose **App registrations**, then select **New application registration**.
4. Create your new application. For **Application type**, choose **Web app/API**. Enter a an application **name** and **URL**. Then choose **Create**.
5. After your application is created, choose **Settings**.
6. Access **Required permissions** through the API. Choose **Add**, then select **Select an API**
7. Search for the *Microsoft Partner* (*Microsoft Dev Center*) API. Set the **Delegated Permissions** to **Partner Center**.
8. For the application you registered, select **Properties** and then select **copy the Application ID**.
9. Choose **Settings**, then choose **Keys**. Create a new key with the **Duration** set to **Never expires**, then select **Save**.
10. On the **Keys** menu, choose **Copy the key value**. Save a copy of this value.

> [!WARNING]
> Be sure to save a copy of the key value for the key you created. You will need to use this key value later to obtain a token.

## Partner consent

In the Azure management portal, select **Enterprise applications**. Search for the application you created in the previous section, and select that application. Select **Permissions** , then select **Grant Admin Consent for Partner Account**.