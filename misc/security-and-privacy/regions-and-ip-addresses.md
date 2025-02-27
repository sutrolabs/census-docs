# Network Access Controls

## Secure Communication

All connections from the Census Data Warehouse Service to your database are protected by TLS encryption - Census will refuse to connect to a warehouse that does not support TLS.

## Regions

Census runs data syncs using Amazon Web Services in the **United States (us-east-1)** and **European Union (eu-central-1)** regions. Census never stores your data, but your selected region determines where data is processed during your Census syncs.

{% hint style="info" %}
By default, Census will run services with US-based infrastructure. Contact support to request to use another region by contacting [support@getcensus.com](mailto:support@getcensus.com).
{% endhint %}

#### Supported Regions

| Geography           | AWS Regions              |
| ------------------- | ------------------------ |
| 🇺🇸 United States  | us-east-1 (N. Virginia)  |
| 🇪🇺 European Union | eu-central-1 (Frankfurt) |

#### Setting up

To view your organization's current region, navigate to the [Settings > General page](https://app.getcensus.com/settings/general) in your Census account. You will find your region identified under **"Organization region"**.

If your data source or self-hosted destinations are behind a firewall, you will need to allowlist [Census's IP Addresses](regions-and-ip-addresses.md#ip-addresses) associated with your region.

![This organization's syncs run in the EU.](<../../.gitbook/assets/screely-1660744037815 (1).png>)

Each workspace can have its own region, which defaults to the organization’s region. You can find the workspace region on the [Settings > General page](https://app.getcensus.com/settings/general). Contact support to request to use another region by contacting [support@getcensus.com](mailto:support@getcensus.com).

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption><p>The workspace's syncs run in the US</p></figcaption></figure>

Similarly, each sync source can perform syncs in its own designated region.

#### During Syncs

Census never stores your customer data, but during a sync, data will flow temporarily through Census servers. A Census sync goes through 4 steps to sync data from your source to your destination:

1. Identifying Changes in your Data Source
2. Unloading Changes to Cloud Storage
3. Preparing Data and Loading into your Destination
4. Reporting Skipped Records and Feedback to your Data Source

Census will perform steps 2 and 3 using infrastructure in the region you've specified. For customers in need of finer-grained security, you may also [provide your own blob storage](../../misc/security-and-privacy/bring-your-own-blob-storage/) where Census will unload the changed records (the "diffs") for each sync. The diagram below showcases which steps in the Census sync process occur in the region of your choice.

<figure><img src="../../.gitbook/assets/Screenshot 2022-08-24 at 4.59.03 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
If your organization has strict data residency requirements, we recommend verifying that your source and destination both store and process data in your desired region. Census will interact with the source and destination using region-specific resources but cannot guarantee that your sources and destinations also operate in the same region.
{% endhint %}

## IP Addresses

Census syncs data from your data sources to your destinations using a set of static IP addresses. To ensure that Census can connect successfully to your sources or any self-hosted destinations, you must allowlist the following IP addresses in your firewall.

<table><thead><tr><th width="412">Region</th><th>IP Addresses (CIDR)</th></tr></thead><tbody><tr><td>🇺🇸 N. Virginia (us-east-1)</td><td><p><code>3.220.140.57</code></p><p><code>54.81.195.173</code></p></td></tr><tr><td>🇪🇺 Frankfurt (eu-central-1)</td><td><p><code>3.73.223.175</code></p><p><code>18.195.84.64</code></p><p><code>3.74.27.151</code></p></td></tr></tbody></table>

Note: Some destinations, such as Oracle Eloqua, use IP whitelisting for both their authentication APIs and standard APIs. In that case, if you're in Europe, you'll need to whitelist both EU and US IPs.

## Connecting via SSH tunnel

Census supports connecting to data warehouse source and destinations that are only accessible on private/internal networks via SSH tunneling. To do so, you'll need to provide an SSH host server that is visible on the public internet and can connect to the private warehouse, and you'll also need to be able to perform some basic admin actions on that server.

1. Create a new user account for Census on the SSH host. This account is separate from the database user account and can have a different username.
2.  When configuring a warehouse connection, enter the warehouse connection details, and then check the 'Use SSH Tunnel' option as shown below. Fill in the host and port of the SSH host machine along with the name of the user created in the previous step.\\

    <figure><img src="../../.gitbook/assets/SSH Tunnel.png" alt=""><figcaption></figcaption></figure>
3.  Once the connection is created, Census will generate a key-pair for SSH authentication which is visible on the connect card.\\

    To install the key-pair, copy the public key in Census to your clipboard and add it to the SSH authorized keys file on the SSH host for the user created in the first step. If, for example, this user is named `census`, the file should be located at `/home/census/.ssh/authorized_keys`. You may need to create this file if it doesn't exist.

    Note that the key-pair is unique for each Census Warehouse connection. Even if you're reusing the same credentials, you'll need to add the new public keys.\\

    <figure><img src="../../.gitbook/assets/Connection Card.png" alt=""><figcaption></figcaption></figure>
4. If the SSH host restricts IP ranges that can connect to it, add the above Census IPs to the allowlist.

With these steps complete, you should be able to complete a connection test, indicating that your tunneled connection is ready to be used in syncs.
