---
description: This page describes how to sync data to your Snowflake data warehouse.
---

# Snowflake

## 🏃‍♀️ Getting Started

1. Click **Add Service**.
2. Select **Snowflake** from the menu.
3. Enter the requested database credentials:
   1. **Account** (should be in the form `iq18923.us-east-1`)
   2. **User**
   3. **Password**
   4. **Warehouse**
   5. **Database**
   6. **Schema Name**: (optional—you'll have the option to select this when creating a sync)
   7. **Number of Client Connections**

<figure><img src="../.gitbook/assets/snowflake-destination.png" alt=""><figcaption><p>Enter your Snowflake credentials to connect with Census.</p></figcaption></figure>

## 🔀 Supported Objects and Behaviors

| **Object Name** | **Supported?** | **Identifiers**                                     | **Behaviors**                         |
| --------------: | :------------: | --------------------------------------------------- | ------------------------------------- |
|           Table |        ✅       | Primary keys or columns with uniqueness constraints | Update or Create, Update Only, Append |

[Contact us](mailto:support@getcensus.com) if you want Census to support more sync behaviors for Snowflake.

## 🚑 Need help connecting to Snowflake?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
