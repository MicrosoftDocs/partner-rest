---
title: Partner API authentication
description: Partner API uses Azure AD for authentication, and to use the Partner APIs you must configure your authentication settings correctly.
ms.date: 02/21/2019
ms.localizationpriority: medium
---

# Partner API authentication

Partner API utilizes Azure Active Directory for authentication. When interacting with the Partner API you must correctly configure an Azure AD application and then request an access token. Access tokens obtained using app + user authentication can be used with the Partner API. However, there are two important items that need to be considered

## Initial setup

1. Sign in to Azure AD from the Azure management portal. In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.

2. In the Azure management portal, **Add application**. Search for "Microsoft Partner", which is the Microsoft Partner application. Set the **Delegated Permissions** to **Access Partner Center**. 

## App + User Authentication
### Partner Consent

In the Azure management portal, **Enterprise applications**. Search for "Application created in the step above". Select the "Application created above". Click on **Permisisons** , then click on **Grant Admin Conset for Partner Account**.