---
description: This page describes how to use ClickHouse as a source in Census.
---

# ClickHouse

## Getting Started <a href="#getting-started" id="getting-started"></a>

* Open Census and navigate to the **Sources** page.
* Click **New Source** and select ClickHouse from the list.
* Configure your ClickHouse connection:
  * Enter your ClickHouse host name and port.
  * Enter the name of a ClickHouse database that will be the default database used when authoring SQL models.
  * Enter the user name and password of the database user Census will use to sync data from ClickHouse
  * Click **Connect**
* You’re all set! Head over to the **Syncs** page to activate your data.

## Allowed IP Addresses

You can add Census's IP addresses in your firewall to only allow traffic originating from Census to access your ClickHouse warehouse.

You can find Census's set of IP address for your region in [Regions & IP Addresses](../basics/security-and-privacy/regions-and-ip-addresses.md#ip-addresses).

## Connecting via SSH tunnel

Census optionally allows connecting to ClickHouse warehouses that are only accessible on private/internal networks via SSH tunneling. To do so, you'll need to provide an SSH host server that is visible on the public internet and can connect to the private warehouse, and you'll also need to be able to perform some basic admin actions on that server.

1. Create a new user account for Census on the SSH host. (This account is separate from the database user account and can have a different username.)
2. On the Census Sources page, create a new connection to a ClickHouse warehouse, enter the warehouse connection details, and then check the 'Use SSH Tunnel' option as shown below. Fill in the host and port of the SSH host machine along with the name of the user created in the previous step.

![](../.gitbook/assets/redshift\_pg\_1.png)

3\. Once the connection is created, Census will generate a keypair for SSH authentication which can be accessed from the Sources page.

To install the keypair, copy the public key in Census to your clipboard and add it to the SSH authorized keys file on the SSH host for the user created in the first step. If, for example, this user is named `census`, the file should be located at`/home/census/.ssh/authorized_keys`. You may need to create this file if it doesn't exist.

Note that the keypair is unique for each Census Warehouse connection. Even if you're reusing the same credentials, you'll need to add the new public keys.

![](../.gitbook/assets/redshift\_pg\_2.png)

4\. If the SSH host restricts IP ranges that can connect to it, add the Census IPs to the allowlist.

With these steps complete, you should be able to complete a connection test, indicating that your tunneled connection is ready to be used in syncs.

## Notes <a href="#notes" id="notes"></a>

As of November 2023, ClickHouse only supports our [Basic Sync Engine](overview.md#sync-engines).

## Need help connecting to ClickHouse?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
