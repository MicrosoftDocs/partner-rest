---
title: Connectors for referrals.
description: How to synchronize referrals.
ms.date: 04/12/2019
ms.localizationpriority: medium
---

# Referral Connectors

This article explains how **referrals connectors** work.

# Prerequisites

- Administrator role on your [Microsoft Flow](https://flow.microsoft.com) account.
- Administrator role on your Microsoft Dynamics CRM Online instance.
- An **application ID** and **secret** to access Partner API. If you don't have these already, see [Partner authentication](api-authentication.md) for setup instructions.
- A [Partner Center Webhook](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhook-events) subscription to [Referral Created](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhook-events#referral-created-event) and [Referral Updated](https://docs.microsoft.com/en-us/partner-center/develop/partner-center-webhook-events#referral-updated-event) webhook events.

## Connectors

Connectors provide an easy way to synchronize referrals from Partner Center to a partner's Dynamics CRM Online instance.

There are two referral connectors: 
- Synchronize a referral to a Microsoft Dynamics CRM lead.
- Synchronize a Microsoft Dynamics CRM lead to a referral.
 

### Flow

The following diagram shows the flow of how referrals are synchronized with the partner's Dynamics CRM. 

![Connectors flow](./images/referrals-connectors/connectors-flow.png)

## Triggers

Triggers for the connectors are built into the Microsoft Flow documents.

### Synchronize referral to lead

A connector does the following to synchronize a referral to a lead from Dynamics CRM:

1. Gets a token to connect to https://api.partner.microsoft.com/v1.0/engagements/referrals.
2. Gets the referral which triggered the connector using https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}.
3. Connects to Microsoft Dynamics CRM.
4. Creates a new lead or updates an existing lead with the latest information on the referral.
5. Updates the referral with the latest updates from the CRM lead.

### Synchronize lead to referral

A connector does the following to synchronize a lead from Dynamics CRM to a referral: 

1. Connects to Microsoft Dynamics CRM.
2. Gets the lead from Microsoft Dynamics CRM.
3. Reads the referral ID from the subject field of the lead.
4. Gets a token to connect to https://api.partner.microsoft.com/v1.0/engagements/referrals.
5. Gets the referral referral ID using  https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}.
6. Updates the referral with the latest updates from the CRM lead.