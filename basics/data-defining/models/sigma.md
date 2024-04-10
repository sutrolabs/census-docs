---
description: Connect Sigma to Census and sync data directly from Sigma Workbooks
---

# Sigma

You can connect Census directly to [Sigma](https://sigmacomputing.com/) which allows you to build Workbooks with their powerful visual builder and then sync the data to any of your business apps Census refreshes data from Sigma whenever a sync is run so your data is always up to date.

## Set up

To connect Sigma to Census, you'll need two things:

* An existing Census data warehouse connection that matches the data warehouse used by Sigma. See the below section on about permissions.
* Sigma API credentials for the user that has access to the Workbooks you plan to use in Census.

To generate API keys for Census, visit **Administration** under the profile menu in the top right and then choose **APIs & Embed Secrets** at the bottom of the left navigation, and click **Create New**. Select **API Token** as the type and then provide a memorable name and description.

This will generate a Client ID and Client Secret. You will need to provide both to Census. Please copy both to a safe place as you will not be able to access them within Sigma again.

#### Connecting Census to Sigma

Now back in Census, select **Models** from the left navigation bar and, if you have multiple warehouse connections, make sure the one that matches your Sigma instance is currently selected in the top left. Once it is, click the **Sigma** tab just below it. You'll see a **Connect Sigma** button to start the process. From here, simply provide your credentials.

<figure><img src="../../../.gitbook/assets/Sigma Configma.png" alt=""><figcaption></figcaption></figure>

Once saved, Census will scan your Sigma environment looking for Workbooks. Each indiviudal Element within a Sigma Workbook will be accessible as an individual model in Census. If you don't see a workbook or element you were expecting, make sure the user that generated the API token has access to that workbook, otherwise Census will not be able to see it.

## Required data warehouse permissions

Census and Sigma both maintain their own data warehouse credentials and connections which means each can have different permissions. However, Census requires the same permissions your Workbooks use within Sigma. If Census is missing some permissions that Sigma has, you may see a permissions error in Census when attempting to preview the model or use it in a sync.
