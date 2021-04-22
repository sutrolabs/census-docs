---
description: This page describes how to use Census with Braze.
---

# Braze

## 🏃‍♂️ Getting Started

{% embed url="https://youtu.be/qwa2BEuxEBs" %}

### 1. Connect Census to Braze

Census needs two pieces of information to connect to your Braze account:

* An API Key with the appropriate permissions
* The Braze API Endpoint URL for your account

### 2. Create a Braze API key

Braze lets you create a number of API keys, each with their own set of permissions. You'll almost certainly want to create a new API key for Census rather than reusing an existing one.

1. Within Braze's left navigation bar, scroll down to the very bottom. Under **App Settings** and click **Developer Console**.

   ![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5f5963864cedfd0017633106/file-3SXNZ9JFVp.png)

2. Within the **API Settings** tab, under **Rest API Keys**, click **+ Create New API Key**.

   ![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5f59639ecff47e00168f5386/file-3hKx2IG3vD.png)

3. Provide a name you'll recognize \("Census" is a good choice\) and select the following permissions. Currently, we only need the User Data permissions, except for `users.delete.` This permission set may change as we add support for more Braze objects so you may want to grant more permissions now or plan to update these permissions in the future. Scroll down and click **Save API Key**.

   ![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5f5963b4c9e77c0016037a29/file-PQO7N1yQbN.png)

4. Finally, copy the long code you see under **Identifier**. We'll use that in a minute.

   ![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5f5963f04cedfd0017633108/file-r3U3MNAAhf.png)

### 3. Select your Braze API Endpoint

Braze requires that we use a slightly different URL to access your account depending on where it's been set up. See the [full list of all Braze API Endpoints](https://www.braze.com/docs/api/basics/#endpoints). In general, you just need the number from the URL you see in your browser when you're signed into Braze.  
  
For example, if your Braze URL is https://dashboard- **03**.braze.com/, then your API Endpoint should be https://rest.iad-**03**.braze.com.

### 4. Create the Census Connection

Great! Now let's pull it all together. 

1. In the **Settings** tab, Create a new Braze Service Connection in Census.

   ![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5f596461c9e77c0016037a2e/file-xBkduoFgm4.png)

2. You can provide whatever name you like.
3. Provide the appropriate Braze Endpoint URL.
4. Copy and paste your new Braze API key.  


   ![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5f59647fcff47e00168f538b/file-rVjsrwoX9w.png)

And you're all set and ready to get syncing! 🎉

## 🔄 Supported Sync Behaviors

As of September 2020, Census supports syncing your data to the **User** object in Braze. 

