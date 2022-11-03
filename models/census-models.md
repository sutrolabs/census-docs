---
description: How to use Census's built-in SQL model repository.
---

# Census Models

Census models require nothing other than a data source connection. Once you have a data source connected (except Google Sheets, which sadly doesn't run SQL yet!), you can immediately start creating Census models.&#x20;

You can think of Census models as a fast way to write and reference a SQL query using your Data Source Connection. If you have the [necessary permissions](../basics/security-and-privacy/permissions.md), you can write a brand new query or copy-and-paste one from an existing system. Give it a name and save it, and you can immediately start using your model as a source for any of your syncs.&#x20;

Here is what a Census SQL Model looks like in the UI. For an overview of how models work, please take a look at the [Overview page](overview.md).

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Example User Mart Query</p></figcaption></figure>

## Activity Tab

On Census models, under the Activity tab you have observability into the different changes to your SQL Models. You can track:

* Which user made a change
* When the change was made
* What the model change was:
  * Name change
  * Description change
  * Approval status change
  * SQL Query change

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>View of Model Activity Tracking</p></figcaption></figure>

Clicking the "Restore" button will restore the state of your SQL query immediately prior to the selected change. This enables you to update your models with confidence, knowing you can always revert your changes if they accidentally break something downstream.

{% hint style="warning" %}
Note that the "Restore" button will only affect the SQL code of the model. Approvals, titles, and descriptions will remain as they were before clicking "Restore."&#x20;
{% endhint %}
