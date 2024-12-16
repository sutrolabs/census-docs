---
description: This page describes how to use Census with Antavo.
---

# Antavo

Antavo is an Enterprise Loyalty Cloud, providing best-in-class technology to manage experience-based, paid, and lifestyle loyalty programs.

## Getting Started

1. Communicating with Antavo requires an API key, region, and secret key, all of which are available from the API section within the Antavo Loyalty Platform. For more information on Antavo security, [see their documentation](https://apidocs.antavo.com/api/security.html).
2. In Census, navigate to the Destinations page and click **Add Destination**. Select Antavo from the list of destinations. Provide your API Key, region, and secret key, then click **Save**.

You should now be ready to start syncing data to Antavo!

## Supported Objects and Behaviors

|   **Object Name** | **Supported?** |    **Sync Keys**   | **Behaviors** |
| ----------------: | :------------: | :----------------: | :-----------: |
| Customer Profiles |        ✅       | Antavo Customer ID |  Update Only  |
|         Audiences |        ✅       | Antavo Customer ID |  Update Only  |

## Quirks

* Antavo does not provide the ability to create new Customer Profiles via the API, so only the Update operation is supported.

## Need help connecting to Antavo?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
