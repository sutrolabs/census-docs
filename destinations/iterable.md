---
description: This page describes how to use Census with Iterable.
---

# Iterable

{% hint style="info" %}
Please note that for larger syncs, it might take ~10 minutes for you to see the new data in Iterable's UI.
{% endhint %}

## 🏃‍♂️ Getting Started

### 1. Create a new Iterable API key

To connect Census to your Iterable, you'll need to provide Census with an API key so that we can talk to it directly. 

**A. Go to your Integration &gt; API keys page**

In the top right, click on your name, and select Account Settings

![](../.gitbook/assets/iterable_setup1.png)

**B. Create a new key for Census**

Click the Create New API key button in the top left.

![](../.gitbook/assets/iterable_setup2.png)

Select the "Standard" key type from the subsequent dropdown. 

![](../.gitbook/assets/iterable_setup3.png)

Copy the resulting key \(a string of 32 characters\) to add it to Census.

**C. Create a new Iterable connection in Census**

* Visit the Connections tab in Census
* Then select Iterable from the Add Service menu
* Finally, paste in the API Key you just created. You can customize the name of the connection if you plan to connect multiple instances of Iterable.

![](../.gitbook/assets/iterable_setup4.png)

Iterable will now appear as a new destination for Census syncs. 

### 2. Syncing data into Iterable

Once the service is added, you can sync users from your database into your Iterable audience \(and augment existing contacts with new product data\).

When creating a sync in Census, you can use _email_ or _userId_ as an identifier. 

![](../.gitbook/assets/iterable_setup5.png)

You can map data fields into your existing Iterable audience schema \(including into nested schemas\). You can also create new custom fields by clicking "+ Add Custom Field" when editing the mapping.

![](../.gitbook/assets/iterable_setup6.png)

