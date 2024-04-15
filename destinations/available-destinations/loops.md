---
description: This page describes how to use Census with Loops.
---

{% hint style="info" %}
Loops is a Partner-Built Destination. See our [PBD announcement](https://www.getcensus.com/blog/announcing-partner-built-destinations) and [docs](https://developers.getcensus.com/custom-destinations/partner-connectors) for more info.
{% endhint %}

# Loops

Loops is the email platform for SaaS.

With Loops, you can track changes in contact properties and then use that information to send emails to increase revenue, engagement or just generally improve your user's experience of your app.

## Getting Started

You will need to have a Loops account and API key to use the Loops connector in Census.

You can get started for free today at [Loops](https://app.loops.so/register).

## Supported Objects and Behaviors

With the connector, you can sync your contact data from your data warehouse to Loops.

The connector supports Upsert and Mirror Operations

### Quirks

When using the connector, you will be able to sync contacts using either email or user id as a unique identifier. Please note that in order to store a contact in Loops, an email address is required.

Additionally, when setting up your connection, you will have the option to trigger loops or not. If you choose to trigger loops, then any contact changes will trigger any applicable loops.

If you choose not to trigger loops, then the up-to-date contact data will be stored in Loops, but no loops will be triggered.