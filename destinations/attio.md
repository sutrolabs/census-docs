---
description: This page describes how to use Census with Attio.
---

# Attio

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Attio** from the menu.
3.  Open the Attio app in another browser tab. Navigate to **Workspace Settings**

    <figure><img src="../.gitbook/assets/attio-workspace-settings.png" alt=""><figcaption></figcaption></figure>

    1.  Select **Developers** from the left hand menu and click the `Create a new integration` button.

        <figure><img src="../.gitbook/assets/attio-developers.png" alt=""><figcaption></figcaption></figure>
    2.  Once the integration is created, a new access token will be available within your new integration. Copy this value.

        <figure><img src="../.gitbook/assets/attio-access-token.png" alt=""><figcaption></figcaption></figure>
    3.  Ensure your access token has `Read/Write` access for `Record` as well as `Read` access for `Object Configuration` and `Read` access for `User Management` under the `Scopes` section.

        <figure><img src="../.gitbook/assets/attio-scopes.png" alt=""><figcaption></figcaption></figure>
4. Return to Census and paste the access token under **API Token**.

## Supported Objects and Behaviors

| **Object Name** | **Supported?** | **Sync Keys**        | **Behaviors**    |
| --------------: | :------------: | -------------------- | ---------------- |
|         Company |        ✅       | Any unique attribute | Update or Create |
|          People |        ✅       | Any unique attribute | Update or Create |
|  Custom Objects |        ✅       | Any unique attribute | Update or Create |

Attio supports [Don't Sync Nulls](broken-reference). Syncs created prior to August 20, 2024 will need to be updated to sync nulls.

Contact our support team if you want Census to support more Attio objects and/or behaviors.

## Record References

Fields of type `Record Reference` are taken in as an array of objects. Below is an example of the expected format:

```
[
    {
        "target_object": "companies",
        "target_record_id": "<company uuid>"
    },
                    {
        "target_object": "people",
        "target_record_id": "<person uuid>"
    }
],
```

## Attio Name Attribute

Attio supports two syntaxes for [writing name values](https://developers.attio.com/docs/attribute-types-personal-name#writing-values): string and object (recommended). Census supports both via [Liquid templating](https://docs.getcensus.com/basics/defining-source-data/liquid-templates):

1.  String

    * The format must match `last name, first name`.&#x20;
    * Liquid example:

    ```liquid
    "name": "{{ record ['last_name'] }}, {{ record['first_name'] }}"
    ```
2.  Object

    * There are three properties that all must be set: `first name`, `last name`, and `full name`
    * Liquid example:

    ```liquid
    {
        "first_name": "{{ record['first_name'] }}",
        "last_name": "{{ record ['last_name'] }}",
        "full_name": "{{ record['first_name'] }} {{ record['last_name'] }}"
    }
    ```

Census will recognize an object is being sent by the opening `{` in the second example.

## Need help connecting to Attio?

Contact our support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
