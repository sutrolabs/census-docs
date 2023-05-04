---
description: >-
  Write, store, and sync Python directly via Census's built-in Python repository
  for Snowflake connections.
---

# Python Models (Snowflake-Only)

Python Models require nothing other than a Snowflake data source connection in [Advanced Sync Engine](../../../sources/overview.md#sync-engines). Once you have Snowflake connected, you can immediately start creating Python models. Using Snowflake's Snowpark developer framework, your python will be executed in your Snowflake data warehouse. The only requirement is that your results are returned as a Snowpark dataframe.

Python Models are a fast way to write and save data transformations that are difficult to perform in SQL. If you have the [necessary permissions](../../security-and-privacy/workspaces-and-access-controls.md), you can write brand new code or copy-and-paste from an existing system. Give it a name and save it, and you can immediately start using your model as a source for any of your syncs.

<figure><img src="../../../.gitbook/assets/screely-1682711256950.png" alt="Pivoting data using the Python package pandas in Census"><figcaption><p>Pivoting data using the Python package pandas in Census</p></figcaption></figure>

## Version History and Rollback

The version history of each Python Model is also tracked in Census. Under the Activity tab, you have observability into the different changes to your Python Models. You can track:

* Which user made a change
* When the change was made
* What the model change was:
  * Name change
  * Description change
  * Python code change

Clicking the **Restore** button will restore the state of your Python immediately prior to the selected change. This enables you to update your models with confidence, knowing you can always revert your changes if they accidentally break something downstream.

{% hint style="warning" %}
Note that restores will only affect the Python code of the model. Approvals, titles, and descriptions will remain as they were before restoring.
{% endhint %}
