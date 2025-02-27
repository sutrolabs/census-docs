---
description: This page describes how to use Materialize as a source in Census.
---

# Materialize

## Getting Started <a href="#getting-started" id="getting-started"></a>

* Sign in to the Materialize console and navigate to the Connect page.
* Open Census and navigate to the **Sources** page.
* Click **New Source** and select Materialize from the list.
* Configure your Materialize connection:
  * Enter your Materialize host name, which you can find under External Tools in the Materialize console Connect page.
  * Enter your Materialize user name, which is your email address.
  * Create a new App Password in the Materialize console, and copy it into Census in the Password field.
  * (Optional) Specify a database in your Materialize instance to use as a default database for SQL models. The `materialize` database is selected by default.
* You’re all set! Head over to the **Syncs** page to activate your data.

## Notes

As of June 2023, Materialize only supports our [Basic Sync Engine](../overview.md#sync-engines).

## Need help connecting to Materialize?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
