---
description: This page describes how to use Census with Blackhawk Network.
---

# Blackhawk

Blackhawk Network helps you build connections with customers, clients and employees, through gift cards, rewards, and other incentives. Use Census to send submission data to Blackhawk Network automatically.

## Getting Started

Census makes use of Blackhawk's SFTP mechanism to send data and takes care of the complex data formatting in the process. To connect to Blackhawk, you'll need to provide Census with the information used to connect to Blackhawk's SFTP server.

1. Census will need the following information to connect to Blackhawk's SFTP server:
   * Host
   * Port
   * Username
   * Password
   * Path - Your folder within the Blackhawk SFTP. Note that this should not start with a `/` in Blackhawk's case.

All of these can be obtained from your Blackhawk Network representative.

2. Back in Census, navigate to the Destinations page and click **Add Destination**. Select **Blackhawk Network** from the list of destinations.
3. Provide the information obtained from your Blackhawk Network representative and click **Save**.

You should now be ready to start sending data to Blackhawk Network!

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** |       **Sync Keys**      | **Behaviors** |
| --------------: | :------------: | :----------------------: | :-----------: |
|      Submission |        ✅       | Any Unique Submission ID |      Add      |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

Contact the support team if you want Census to support more Blackhawk objects and/or behaviors.

### Submission Quirks

| **Advanced Configuration** |                    **Description**                    |
| -------------------------: | :---------------------------------------------------: |
|                    Context | The prefix of the file that is created in your folder |

Each individual submission is a relatively complex data structure. Census takes care of the complex data formatting for you, so you can focus on building the data you want to send to Blackhawk.

We currently support two types of fields for submissions

* Demographic fields - These are all built in fields that can be mapped immediately in a Census sync
* Submission attributes - These are custom fields that can be added to a submission. These fields names **must** start with a prefix "SA." in order to be loaded correctly, for example: "SA.Installation Date".

The Blackhawk destination does not currently support sending fields for the Additional Demographic or Product and Product attributes. If you need to send these fields, please contact the support team.

## Need help connecting to Blackhawk Network?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
