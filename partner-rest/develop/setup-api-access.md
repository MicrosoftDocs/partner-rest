---
title: Set up Partner API access
description: This topic describes the accounts you need to develop against the Partner REST API, how to create an integration sandbox account, and how to test in the integration sandbox.
ms.date: 02/21/2019
ms.localizationpriority: medium
---

# Set up Partner API access

This topic describes the accounts you need to develop against the Partner REST API.

## <span id="supportedAccountTypes"/><span id="supportedaccounttypes"/><span id="SUPPORTEDACCOUNTTYPES"/>Account definitions

To help you integrate and test your API integration, Partner Center supports two kinds of accounts:

<table>
  <tr>
    <td><strong>Primary Partner account</strong></td>
    <td>This account is where you create real orders for real customers. If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers. They will be reflected in your invoice, and your company is responsible for paying for them.</td>
  </tr>
  <tr>
    <td><strong>Integration sandbox account</strong></td>
    <td><p>This account is for testing your code and its integration with the Partner APIs before you deploy it broadly. Changes and transactions you make when you are signed into the integration sandbox account will not appear in your invoice.</p>
      <ul>
        <li>The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</li>
        <li>The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, seats, etc.</li>
        <li>By policy, integration sandbox accounts are for integration testing purposes only.</li>
        <li>By default, there is no integration sandbox account. You must create one yourself if you plan to use the Partner Center SDK.</li>
      </ul>
    </td>
  </tr>
</table>
 
 
## <span id="Set__up_your_accounts"/><span id="set__up_your_accounts"/><span id="SET__UP_YOUR_ACCOUNTS"/>Set up your accounts

<span id="createIntegrationSandbox"/><span id="createintegrationsandbox"/><span id="CREATEINTEGRATIONSANDBOX"/>
**Create an integration sandbox**

1.  Sign in into Partner Dashboard with a global admin account. (This is your primary Partner account.)
2.  From the **Settings icon** (gear) menu, select **Partner settings**.
3.  On the **Account settings** page, select **Integration sandbox**.

    >[!NOTE]
    >If you don't see an Integration sandbox option, you might not have a global admin account, or the integration sandbox has already been set up and you're using an integration sandbox account.

4.  Fill in the contact information for the integration sandbox admin account, and then click **Create account**. You might need to wait a few minutes for the account to be created.

5.  After you see the confirmation message, sign out of Partner Dashboard, then sign back in with your new integration sandbox admin account, in the form *username*@*domain* and with the password you just specified.

6.  After you sign back in with your new integration sandbox admin account, above **Current Tasks**, click **Set Up Account** to complete the sandbox account setup.

<span id="enableAPIAccess"/><span id="enableapiaccess"/><span id="ENABLEAPIACCESS"/>

After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox. You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.

**Enable API access**

1.  Sign into Partner Dashboard using a global admin account.

2.  From the **Settings icon** menu, select **Partner settings**.

3.  On the **Account settings** page, select **App management**.

4. If you do not already have an existing app, add a new web app. If you have an existing web app, click the **Add key** button.

5.  Copy the app registration information, especially the **Key** if you're creating a Web App, and store it in a safe place.

6.  Sign out of Partner Dashboard, then sign back in with your integration sandbox account. Repeat steps 2-5 to enable API access in the integration sandbox.


## <span id="writeTestCode"/><span id="writetestcode"/><span id="WRITETESTCODE"/>Write and test code in the integration sandbox

To write code and test code in Partner Center, you'll need to set up authentication with Azure AD, as described in [Partner API authentication](api-authentication.md). You'll need the following pieces of information:

<table>
  <tr>
    <td><strong>Item name</strong></td>
    <td><strong>Where to find it</strong></td>
  </tr>
  <tr>
    <td>App ID / Client ID</td>
    <td>From the <strong>Settings icon</strong> menu, select <strong>Partner settings</strong>. On the <strong>Account settings</strong> page, select <strong>App Management</strong> The App ID/Client ID is listed as the Registered application <strong>App ID</strong>.</td>
  </tr>
  <tr>
    <td>Key</td>
    <td>If you created a web app, this is the key that you saved in Step 5 of &quot;Enable API access&quot;.</td>
  </tr>
  <tr>
    <td>Domain</td>
    <td>This is the domain for the integration sandbox.</td>
  </tr>
</table>


## <span id="runTestedCode"/><span id="runtestedcode"/><span id="RUNTESTEDCODE"/>Use your solution for real customer data

**Change credentials from integration sandbox to primary account**

1.  When you are ready to use your tested code in your primary Partner account, you must get an Azure AD security token based on your Partner Center app/key/domain instead of the integration sandbox app/key/domain.

    Repeat the same steps for [Partner API authentication](api-authentication.md) that you used to get an Azure AD security token in the integration sandbox, but use your primary Partner Center credentials instead.

2.  After you replace the integration security token with the one for your primary Partner account, the rest of your code should work correctly.
  