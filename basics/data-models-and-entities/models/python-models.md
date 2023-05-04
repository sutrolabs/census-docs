---
description: >-
  Write, store, and sync Python directly via Census's built-in Python repository
  for Snowflake connections.
---

# Python Models (Snowflake-Only)

Python Models require nothing other than a Snowflake data source connection in [Advanced Sync Engine](../../../sources/overview.md#sync-engines). Once you have Snowflake connected, you can immediately start creating Python models. Using Snowflake's Snowpark developer framework, your python will be executed in your Snowflake data warehouse. The only requirement is that your results are returned as a Snowpark dataframe.

Python Models are a fast way to write and save data transformations that are difficult to perform in SQL. If you have the [necessary permissions](../../security-and-privacy/workspaces-and-access-controls.md), you can write brand new code or copy-and-paste from an existing system. Give it a name and save it, and you can immediately start using your model as a source for any of your syncs.

<figure><img src="../../../.gitbook/assets/screely-1682711256950.png" alt="Pivoting data using the Python package pandas in Census"><figcaption><p>Pivoting data using the Python package pandas in Census</p></figcaption></figure>
