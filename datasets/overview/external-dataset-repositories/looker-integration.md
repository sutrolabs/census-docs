---
description: Connect Looker to Census and sync data directly from Looker Looks.
---

# Looker Integration

Census supports connecting to an existing Looker environment, which allows you to build Looker Looks with Looker's powerful visual builder and then sync the data to any of your business apps.

Census compiles your models on the fly whenever a sync is scheduled so your data and your models are always up to date. Here's a quick video of the instructions that we've covered in the write-up below.

{% embed url="https://youtu.be/sX2oB1Y24G4" %}

## Set up

To connect Looker to your Census instance, you'll need two things:

* An existing Census data source connection that matches the data source used by Looker. See the below section on about permissions.
* Looker API3 credentials for the user that has access to the Looks you plan to use in Census.

To create new API3 credentials, you'll need to visit the **Admin** > **Users** page, select the desired user and click the **Edit** button and then the **Edit Keys** button on the user's profile page. You'll need to note both the **Client ID** and **Client Secret** values to provide to Census. The [Looker documentation](https://docs.looker.com/admin-options/settings/users#edit\_api3\_keys) provides more details on how to find and create keys.\
\
You'll also need the URL of your Looker instance. You should be able to simply pull that directly from your browser URL bar. For example, if the URL is `https://censususer.looker.com/` then the subdomain is `censususer`.&#x20;

If you're using a self-hosted instance of Looker, provide the full URL as well as the port number of your API, for example `https://yourlooker.yourcompany.com:443`. The port number may be 443 or 19999 depending on when your Looker instance was created, or it may be another value if you've overridden the default. See [Looker documentation](https://cloud.google.com/looker/docs/admin-panel-platform-api) for more details.

#### Connecting Census to Looker

Now back in Census, select **Sources** from the left navigation bar and, if you have multiple warehouse connections, click on the **Projects** button of the one that matches your Looker instance. Once you've clicked on **Projects**, pick the **Looker** tab. You'll see a **Connect Looker** button to start the process. From here, simply provide your subdomain, the client id and client secret.



<figure><img src="../../../.gitbook/assets/Screenshot 2024-07-31 at 2.32.13 PM.png" alt=""><figcaption><p>Click on the Projects Button</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2024-07-31 at 2.52.17 PM.png" alt=""><figcaption><p>Enter your Looker credentials</p></figcaption></figure>

Once saved, you should see all of your Looker Looks!

{% hint style="info" %}
Note: Looks that are in development mode are not shared in the Looker API so only Looks that have been published will appear in Census.
{% endhint %}

## Required data warehouse permissions

Census and Looker both maintain their own data warehouse credentials and connections which means each can have different permissions. However, Census requires the same permissions your Looker Looks use within Looker. If Census is missing some permissions that Looker has, you may see a permissions error in Census when attempting to preview the model or use it in a sync.

## Unsupported features

#### Totals & Row Totals

![](../../../.gitbook/assets/looker\_totals\_and\_row\_totals.png)

Looker will autogenerate additional SQL queries when `Totals` or `Row Totals` are selected. These features are not supported for syncs from Census, and therefore the related SQL will not be imported to Census.

We will add the following as the last line of your SQL when this occurs.

```
-- sql for creating the total and/or determining pivot columns was removed by Census
```
