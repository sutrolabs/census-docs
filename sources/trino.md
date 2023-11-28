---
description: This page describes how to use Trino or Starburst as a source in Census.
---

# Trino

## 🏃‍♀️ Getting Started <a href="#getting-started" id="getting-started"></a>

Census can use Trino (and any supported Trino catalog) as a source. Census has been tested with the open-source Trino as well as Starburst Galaxy and Starburst Enterprise.

* Open Census and navigate to the **Sources** page.
* Click **New Source** and select Trino from the list.
* Configure your Trino connection:
  * Enter your Trino host name
  * Enter your Trino user name
  * Enter your Trino password
  * (Optional) If your Trino instance does not run on port 443, enter the port here. Census requires a TLS connection to Trino.
* You’re all set! Head over to the **Syncs** page to activate your data.

## 💡 Notes <a href="#notes" id="notes"></a>

As of November 2023, Trino only supports our [Basic Sync Engine](overview.md#sync-engines).

## 🚑 Need help connecting to Materialize?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
