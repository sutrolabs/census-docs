---
description: This page describes how to use Census with Oracle Responsys.
---

# Oracle Responsys

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Oracle Responsys** from the menu.
3. Enter your **Authentication Endpoint** (see [this page](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/Authentication/auth-endpoints-rest.htm)), **Username**, and **Password**. Please ensure your Responsys username has API access.

<figure><img src="../.gitbook/assets/oracle-responsys.png" alt=""><figcaption><p>Enter your Responsys credentials to connect with Census.</p></figcaption></figure>

## Supported Objects and Behaviors

| **Object Name** | **Supported?** | **Sync Keys**  | **Behaviors** |
| --------------: | :------------: | ---------------- | --------------|
| Profile List (Recipients) | ✅ | Customer ID, Responsys ID, Email Address, Email MD5 Hash, Email SHA256 Hash, Mobile Number | Update or Create |
| Profile Extension Table | ✅ | Customer ID, Responsys ID, Email Address, Email MD5 Hash, Email SHA256 Hash, Mobile Number | Update or Create |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Responsys objects and/or behaviors.

## Need help connecting to Responsys?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
