---
description: This page describes how to use Census with Mailchimp Transactional (Mandrill).
---

# Mailchimp Transactional (Mandrill)

Mailchimp Transactional, formerly known as Mandrill, is a transactional email API for Mailchimp users. It's a powerful, scalable, and secure delivery API for transactional emails from websites and applications.

## Getting Started

To connect Census to Mailchimp Transactional (Mandrill), you'll need an API Key.

1. From the home page of your Mandrill account, click on [**Settings**](https://mandrillapp.com/settings) in the left hand navigation bar.
2. Click the **+ New API Key** button and create a new API key with the necessary permissions. Copy the generated API key.
   * Census requires at least the `Templates > List` and `Messages > Send-Template` permissions.
3. Now return to Census and visit the [**Destinations**](https://app.getcensus.com/workspaces/10341/destinations) page. Click on the **New Destination** button and select **Mailchimp Transactional (Mandrill)** from the menu. Copy and paste the API Key into the dialog and hit save. You should be ready to create a new sync!

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|           **Object Name** | **Supported?** |         **Identifiers**         | **Behaviors** |
| ------------------------: | :------------: | :-----------------------------: | :-----------: |
| Send via Message Template |        ✅       | Unique identifier for each send |      Send     |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

Contact our support team if you want Census to support more Mailchimp objects and/or behaviors

### Send Emails via Message Templates

Census takes advantage of Mandrill's templating system to send emails. When configuring a sync to Mandrill, the first step will be selecting the existing message template you'd like Census to use when sending.

In addition to the template, you can also map a number of other fields to control the email:

* To - The email address of the recipient.
* From - The email address of the sender.
* Attachments - URLs of files to attach to the email. These files must be publicly accessible.

Any additional custom fields provided by the sync configuration will be provided as merge variables to the Mandrill template.

## Need help connecting to Mailchimp Transactional (Mandrill)?

Contact our support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
