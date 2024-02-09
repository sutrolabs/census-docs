---
description: This page describes how to use Census with Facebook Product Catalog.
---

# Facebook Product Catalog

Facebook Product Catalog allows you to sync your product data to Facebook for use in dynamic ads, Instagram Shopping, and more.

In this guide, we will show you how to connect Facebook Product Catalog to Census and create your first sync.

## 🏃‍♀️ Getting Started

This connector relies on a [Facebook System User](https://www.facebook.com/business/help/327596604689624?id=2190812977867143) token for authenticating requests. A regular system user is recommended over an admin system user. You can use an existing system user or create a new one with the following steps:&#x20;

### Creating a new System User

1.  If you don't have one already the first thing you need to generate a system token is an application

    * Open your Business Manager
    * Navigate to **Business Settings > Accounts > Apps**
    * Click **Add** and then **Create New App ID**
    * For use case select **Other**

    <figure><img src="../.gitbook/assets/FB App UseCase.png" alt="Facebook App UseCase Screen" width="375"><figcaption><p>New app usecase screen</p></figcaption></figure>

    * Then for Type select **Business**

    <figure><img src="../.gitbook/assets/FB New App Type.png" alt="" width="375"><figcaption><p>New app type</p></figcaption></figure>

    * Then fill out the relevant details and press **Create App**

    <figure><img src="../.gitbook/assets/FB New App Details.png" alt="" width="375"><figcaption><p>New app details</p></figcaption></figure>
2.  Now you can generate a system user for the app. Go to your Business Manager and navigate to **Business Settings > Users > System Users**



    <figure><img src="../.gitbook/assets/Screenshot 2023-05-18 at 8.23.16 AM.png" alt="" width="375"><figcaption><p>Business Manager Navigation Panel</p></figcaption></figure>
3. Above your list of system users click **Add** to create a new System User
4. Provide a name and role. Census does **not** need an `Admin` role, `Employee` is sufficient.
5. Once the system user is created click on **Add Assets** and assign the relevant Product Catalogs that you want Census to sync to. Make sure to assign _full control_ of the catalog to the system user.
6. Now generate a token for the System User by pressing **Generate New Token**, select the relevant app you created earlier, select the relevant scopes, and then press **Generate Token**
   * You will need to provide _at least_ the `business_management` and `catalog_management` scopes for Census to sync to your product catalogs
   *   Make sure to select `Never` for token expiration so you do not need to manually reauthorize your Census connection every 60 days.



       <figure><img src="../.gitbook/assets/Screenshot 2023-05-18 at 8.33.35 AM.png" alt="" width="375"><figcaption><p>Token Expiration &#x26; Scopes Page</p></figcaption></figure>
7. Once your token is generated be sure to save it in a safe place. This is the token you must provide to Census as a credential for your connection.

### Using an Existing System User

If you already have a system user you can use it by simply generating a new token with the correct permissions. Census needs the `business_management` and `catalog_management` scopes. Also be sure to assign the catalog asset to your system user so Census can sync to it.

### Setting Up Connection

You are now ready to set up a connection. Head to the Census Destinations page and press **New Destination**. From the list select Facebook Product Catalog.

You will need to provide the System User Token you generated earlier along with your Business Account Id and the Catalog Id you want associated with this specific connection. You can find those in your Business Settings in **Business Info** and **Data Sources > Catalogs** respectively.

<figure><img src="../.gitbook/assets/FB New Connection.png" alt=""><figcaption><p>New Facebook Product Catalog connection page</p></figcaption></figure>

## 🗄 Supported Objects and Behaviors

Each Facebook Product Catalog supports products for a specific vertical. Each vertical is a variant on the base product object within the Facebook system. Currently we support the following variants with more to come. If there's a variant you would like to sync to please [contact us](facebook-ads-1.md#need-help-connecting-to-facebook) about making it happen.

| **Object Name** | **Supported?** | **Identifiers** | **Behaviors**  |
| --------------: | :------------: | ----------- | :------------: |
|    Product Item |        ✅       | Retailer Id | Update or Create, Mirror |
|           Hotel |        ✅       | Hotel Id    | Update or Create, Mirror |
|      Hotel Room |       🔜       |             |             |
|          Flight |       🔜       |             |             |
|     Destination |       🔜       |             |             |
|    Home Listing |       🔜       |             |             |
|         Vehicle |       🔜       |             |             |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Facebook Product Catalog.

## 🚑 Need help connecting to Facebook?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
