---
description: >-
  How to use the profile explorer, which allows you to view a complete 360 view
  of your customer or other dataset.
---

# Profile Explorer

## Before you start

The profile explorer allows you to build and explore your complete customer 360, based on the joining of your key entities.  Typically a member of the data team will need to first set up the entities for your warehouse connection before getting started. Take a look at [Defining Your Data Model](./) for details.

## Using the Profile Explorer

To explore your first dataset, click on **Explorer** in the left-hand navigation of Census and then choose your dataset in the top dropdown.  A sample of the data will be shown in the explorer.&#x20;

This data can then be searched using the search box. The following fields are searchable for each [dataset type](../../datasets/core-concepts/type-and-property-mappings.md#type):

<table><thead><tr><th>Entity Type</th><th>Searchable fields</th><th data-hidden></th></tr></thead><tbody><tr><td><span data-gb-custom-inline data-tag="emoji" data-code="1f464">👤</span> Person</td><td>Unique ID, Email</td><td></td></tr><tr><td><span data-gb-custom-inline data-tag="emoji" data-code="1f3e2">🏢</span> Company</td><td>Unique ID, Name, Domain</td><td></td></tr><tr><td><span data-gb-custom-inline data-tag="emoji" data-code="2753">❓</span>Other</td><td>Unique ID</td><td></td></tr></tbody></table>

Results can be sorted by clicking on the sort button.  By selecting each column header you can also sort or hide each property.  To show a property that has been hidden use the 'show properties' button.&#x20;

Each record can also be explored in more detail by clicking on an individual row,  this will bring up a profile view of that record with all the information known.&#x20;

<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The icon for a person or company will show if the dataset has been given the following mappings, in this order of priority:

* Person: Full name, email address, first name, last name
* Company: Domain, company name
