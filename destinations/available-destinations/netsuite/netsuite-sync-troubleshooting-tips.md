---
description: >-
  This guide explains common NetSuite sync failures, how to diagnose them, and
  best practices for working with NetSuite fields, especially sublist
  (line-level) fields on transaction records.
---

# NetSuite Sync Troubleshooting Tips

### Using NetSuite API Documentation

To confirm valid fields and structure:

1. Open the [NetSuite Schema Browser](https://www.netsuite.com/help/helpcenter/en_US/srbrowser/Browser2022_1/schema/record/account.html)
2. Search for the record type (for example, **Journal Entry**)
3. Review:
   * Header/body fields
   * Sublist fields (such as `lineList`, `itemList`, or `applyList`)
4. Click into the sublist definition to see:
   * Available fields
   * Required vs optional fields

This is the most reliable way to validate field names and structure.

### Sublist Field Formatting

#### What Is a Sublist?

Many NetSuite records contain sublists:

* **Header (body) fields**\
  High-level information such as date, currency, or memo
* **Sublist (line) fields**\
  Line-item details such as account, item, amount, or quantity

**Example: Journal Entry**

* Header: Post date, currency, memo
* Sublist: Debit and credit lines, account, amount

***

#### Sublist Field Structure

Sublist fields are sent as **arrays of objects** in the NetSuite API.

Example:

```json
[
  { "account": { "internalId": 426 }, "credit": 13 },
  { "account": { "internalId": 426 }, "debit": 13 }
]
```

**Important notes:**

* Sublist fields are the most common source of NetSuite sync errors
* Field names are case-sensitive
* Fields must match NetSuite’s API schema exactly

***

#### Apply Fields (Special Sublist Case)

Some transactions can be applied to other transactions, such as:

* Applying a vendor credit to a bill
* Applying a payment to an invoice

These fields behave like sublists and often include:

* `apply`
* `amount`
* `doc`
* `line`

Example:

```json
[
  { "apply": true, "doc": "9247", "total": 12 }
]
```

**Key detail:**\
`doc` should be the **internal ID** of the transaction being applied.

### Common NetSuite Sync Error

#### Error Message: `Passed nil into T.must`

**What This Means**

This error often indicates that a field included in your sync configuration could not be found or resolved by NetSuite.

In many cases, the issue is related to a sublist (line-level) field.

* A sublist field does not exist on the record type being synced
* The field name is not an exact match (NetSuite is case-sensitive)
* A custom field is referenced using its label instead of its ScriptID
* A recently added field is not yet available via the NetSuite API

***

### How to Troubleshoot

#### 1. Review the Fields in Your Sync Configuration

* Identify which fields are being written to NetSuite, especially line-level (sublist) fields
* Double-check spelling and capitalization

#### 2. Confirm the Field Exists on the Correct Sublist

Fields must exist on the **exact sublist** being used (for example, `itemList`, `lineList`, or `applyList`).

A field that exists on one transaction type or sublist may not exist on another.

***

#### 3. Validate Custom Fields

If the field is custom:

* Confirm it was created as a Transaction Line Field (not a body field)
* Ensure you are using the Script ID, not the display label

To find the Script ID in NetSuite:

1. Go to **Customization → Lists, Records, & Fields → Transaction Line Fields**
2. Open the field
3. Use the value shown as **ID** (for example: `custcol_example_field`)

***

### Alternative Approach: HTTP Request Object

For complex scenarios or unsupported objects, you can use the **HTTP Request** object to interact directly with NetSuite’s REST API.

#### Benefits

* Easier debugging
* More flexible field handling

[NetSuite’s REST API documentation](https://system.netsuite.com/help/helpcenter/en_US/APIs/REST_API_Browser/record/v1/2025.2/index.html) often provides clearer examples that can be tested iteratively.
