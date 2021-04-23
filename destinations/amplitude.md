---
description: This page describes how to use Census with Amplitude.
---

# Amplitude

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect your Amplitude project to [Census](https://www.getcensus.com/) and create your first sync.

### **Prerequisites**

* [Create a Free Trial Census Account](https://app.getcensus.com/)
* Have the credential to access your warehouse. See our articles for each data warehouse
  * [Redshift](../source-warehouse/redshift.md)
  * [Snowflake](../source-warehouse/snowflake.md)
  * [Google BigQuery](../source-warehouse/google-bigquery.md)
  * [Databricks](../source-warehouse/databricks.md)
  * [Postgres](../source-warehouse/postgres.md)



### **1. Get API key from Amplitude**

Census needs only one piece of information to connect to your Amplitude project:

* The API Key for an HTTP API data source for your Amplitude project

### **2. Create a HTTP API Data Source in Amplitude, and copy the API key**

Amplitude lets you pull data from a number of different sources, including via HTTP API. If you don't have this data source set up in Amplitude already, you'll need to create one. The same steps below will also allow you to find the API key for a pre-existing HTTP API data source, as Amplitude will only permit one per project.

1. Within Amplitude’s left navigation bar, scroll down to the very bottom. **Click on Sources & Destinations.**  


   ![](https://lh6.googleusercontent.com/IldQDvHh30Q3BQTJI1tAjTdnYaoLgkALhEYU9wpXfMAbmPe0Qu8eUavNYVzRNGT3Chjpr_G-SODK6pRQluXA44WkdKpjUESz8lItwWdkWUVGE60gJfLHJdFrnEd8lJwdiD_nvvph)

2. ‌Once here, navigate to the top-right of the screen and click to **Add Data Source**. ****![](https://lh3.googleusercontent.com/Xt-bGTekukUBgNGE-d805HzLvnODAgkuC7JCO_uiW_3gpE7-oFBID3fgEjkHfRkdlyXtEGG_wubzXWH8EBss8sJ-Ce_i9CGAnD5oy-L9F1rvn9YyQlcsxzY4ms5K8guaGWru4MlL)
3. Select **“HTTP API”** as the type of data source, and click **Next**.![](https://lh6.googleusercontent.com/3oT5uRNYeOJCVX6v9h7I4zwmp0P6z2H0NTocMnaOTwauCi01GFLjVZNYdjoYLK_AxvmMVIxK-Ec8o9xDZGExO9YYlh-T2i055heRbi-VWU5B-0MsR1bDXwfOEaIkAmIr5jIokemj)
4. **Copy the API Key** \(it will be a long string of numbers and characters\), click **Next.** 
5. If you are setting up the HTTP API data source for the first time, Amplitude will require you to POST an event to their API to complete set-up. Amplitude provides instructions to send a sample event and complete set-up at this stage.
6. When the event is received by Amplitude, click **Finish** to finish setting up this source within Amplitude.

### 3. **Create the Census Connection**

Now that we have the API Key from Amplitude, we can now set up Amplitude as a Destination in Census.

1. In the **Settings** tab of Census, create a new Amplitude Service Connection. ****![](https://lh5.googleusercontent.com/TYNs2uji9P65wu4JR-3bU3k_0svIJ7dAdaS9I25gzHHY0U-kxlQ6twBRFPIwrUzsNGOnamNJT-8ygYqnyPsuGW51k2EGWhghMJGpur6Ewde5Rw5xaoevAyr6_CkUSZ_OiY-58b7D)
2. You can provide whatever name you like.
3. Provide the copied API Key from Amplitude.
4. Save.

## 🗄️ Supported Objects

| Object Name | Supported? | Identifiers |
| :--- | :---: | :--- |
| Devices | ✅ | Device ID |
| Users | ✅ | User ID |
| Groups | 🔜 | Group ID |
| Events | 🔜 | User ID |

Both User and Device objects will resolve to a single User Profile in Amplitude, if mappings for the other identifier are also provided in the sync.‌ 

🎒 [Contact us](mailto:support@getcensus.com) if you want Census to support more Objects for this destination

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

| **Behaviors** | **Supported?** | **Objects?** |
| ---: | :---: | :---: |
| **Update or Create** | ✅ | Device, User |
| **Create Only** | 🔜 | Event |

‌ 🔋 [Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for this destination



‌

## 🚑 Need help connecting to Amplitude?

‌ Contact us via [support@getcensus.com](mailto:support@getcensus.com) or start a conversion via the [in-app](https://app.getcensus.com/) chat.

{% hint style="info" %}
This part of our documentation is still under construction! If you have any questions, please don't hesitate to [contact us](mailto:support@getcensus.com).
{% endhint %}

