---
description: Write, store, and sync SQL directly in Census's built-in SQL repository.
---

# SQL Queries

SQL Queries require nothing other than a data source connection. Once you have a data source connected (except Google Sheets, which sadly doesn't run SQL yet!), you can immediately start creating queries.

SQL Queries are a fast way to write and save SQL so that it can be referenced multiple times and updated in once spot as needed. If you have the [necessary permissions](../../security-and-privacy/workspaces-and-access-controls.md), you can write a brand new query or copy-and-paste one from an existing system. Give it a name and save it, and you can immediately start using your model as a source for any of your syncs.

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Here's what an example User Mart Query SQL Query looks like in Census.</p></figcaption></figure>

## Version History and Rollback

The version history of each SQL query is also tracked in Census. Under the Activity tab, you have observability into the different changes to your SQL Models. You can track:

* Which user made a change
* When the change was made
* What the model change was:
  * Name change
  * Description change
  * Approval status change
  * SQL Query change

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption><p>View of Model Activity Tracking</p></figcaption></figure>

Clicking the **Restore** button will restore the state of your SQL query immediately prior to the selected change. This enables you to update your models with confidence, knowing you can always revert your changes if they accidentally break something downstream.

{% hint style="warning" %}
Note that restores will only affect the SQL code of the model. Approvals, titles, and descriptions will remain as they were before restoring.
{% endhint %}
