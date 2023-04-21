---
description: >-
  Census Enrichment makes it easy to connect third-party data sources to the
  first-party data you already have in your warehouse
---

# Enrichment

## What is data enrichment?

A typical data warehouse is filled with all of the data your business generates: order history, user interaction events, an update snapshot of the data in your app database, all of your ETLed SaaS data, and more. This is often called "first party" data, ie data that only you know about.

But there's a lot of other data out in the world and some of those data sets can be very valuable in building a single source of truth in the warehouse.

Here's a really simple example of a query a user may want to run on your warehouse:

> Give me all my current users that work at companies with more than 100 employees.

That type of query is incredibly simple but the data to answer it is missing from most warehouses, specifically the data point of `number_of_employees`.

But this data exists out there, provided by many [Service Providers](enrichment.md#supported-enrichment-services). These are called third-party data providers and the process of connecting that with your data is called Data Enrichment. Historically, this has involved hitting an API directly or extracting enriched data that haphazardly gets ETLed into the warehouse by virtue of enrichment happening in some other tool such as a CRM.

Census Enrichment makes it drop dead simple to enable data enrichment directly in your warehouse with just a few clicks.

## Enabling enrichments

{% hint style="info" %}
Enrichments is currently supported on Snowflake, Redshift, and Postgres with more warehouses coming soon!
{% endhint %}

Enrichments are configured on [entities.md](entities.md "mention"). Every entity now has a Data Enrichment tab that allows configuring enrichment. The data within the entity will act as the source data that is passed to the enrichment service, and Census will automatically store the results in the warehouse as well as add the data you specify to the entities.

Before you start, you'll need to create a service connection to your enrichment service. You can add these in the [Connections tab](https://app.getcensus.com/connections). You'll see a Data Enrichment tag indicating a service can be used for enrichment and you can see the [full set of services we support](enrichment.md#supported-enrichment-services) below.

With enrichment services enabled, you'll now see the option to turn on enrichment on your entities. Enabling enrichment requires three pieces of configuration:

* Data Category or type to use, if the service provides multiple. For example, do you want to enrich users or people? If your entity is a User or Company type, this will be automatically selected for you.
* The identifier (or identifiers) to pass to the enrichment service. Enrichment services use these identifiers to match against their databases. The type of identifier needed will vary depending on which data category was specified.
* The attributes from the enrichment service to add to the entity. You can choose which attributes to add to your entity, you don't need to add them all so you can skip attributes that would create duplicate columns and confusion.

Once your enrichment is configured, Census will start querying your enrichment service and populating results.

You can immediately start using the new enrichment-powered attributes on your entity within Census Segments and Syncs. Note that you'll see an indication in syncs and segments if the enrichment is still actively running but data will be backfilled in future sync runs if enrichment data is not immediately available at sync time.

## How Census Enrichment works

Once you've defined your enrichments, Census takes care of managing that data, storing it in your warehouse as well as making available within Census.

Underneath the covers, Census is running a special type of Sync. This sync does a couple of things:

1. First it looks at your entity to determine what new records have been added that need to be enriched.
2. Once it's identified the new records, it passes those identifiers to your configured enrichment service.
3. Finally, it writes the results back to your data warehouse.

Because this data is available in your warehouse, you're also free to use it in the rest of your data stack, not just within Census. The data will be available with in the Census schema and will include the name of the enrichment service as well as the data category.

For example, in Snowflake the Census schema is stored within a Census database. So a Clearbit People enrichment table name will be `CENSUS.CENSUS.ENRICHMENT_FROM_CLEARBIT_FOR_PEOPLE`. All of the properties returned from the service are flattened into columns, and Census also includes a timestamp when the data was first captured. Deleting records from this table will cause Census to re-enrich those records.

## Supported Enrichment Services

Here are the list of services Census currently integrations to provide data enrichment and this list is constantly growing. Looking for a particular service, [let us know](mailto:support@getcensus.com)!

### Apollo.io

Fill your warehouse with 65+ firmographic fields for scoring, routing, research, analytics, and more for smarter targeting based on your ideal customer profile.

To connect to Apollo.io, you will need to visit the [Apollo developer portal](https://developer.apollo.io/) and create or reuse an existing API key. Keep in mind:

* Apollo.io API keys can be scoped to limit access to particular API endpoints. To enable enrichment, Census will need access to the `/people/match` and `/organizations/enrich` endpoints. The [Apollo sync destination](../../destinations/apollo.md) uses a different set of permissions so you may need to update the API key configuration first to use it with enrichments.
* Enriching does use Apollo API credits. Please see [Apollo's documentation](https://apolloio.github.io/apollo-api-docs/?shell#bulk-people-enrichment) for details on credit usage.

| Data Category | Identifier(s) | Data Points                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| People        | Email         | first\_name, last\_name, name, linkedin\_url, title, city, email\_status, photo\_url, twitter\_url, github\_url, facebook\_url, extrapolated\_email\_confidence, headline, country": "United States, email, state, excluded\_for\_leadgen, personal\_emails, departments, subdepartments, functions, seniority                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Organization  | Domain        | name, website\_url, blog\_url, angellist\_url, linkedin\_url, twitter\_url, facebook\_url, primary\_phone, languages, alexa\_ranking, phone, linkedin\_uid, founded\_year, publicly\_traded\_symbol, publicly\_traded\_exchange, logo\_url, crunchbase\_url, primary\_domain, persona\_counts, industry, keywords, estimated\_num\_employees, snippets\_loaded, retail\_location\_count, raw\_address, street\_address, city, state, postal\_code, country, owned\_by\_organization\_id, suborganizations, num\_suborganizations, seo\_description, short\_description, annual\_revenue\_printed, annual\_revenue, total\_funding, total\_funding\_printed, latest\_funding\_round\_date, latest\_funding\_stage, funding\_events, technology\_names, current\_technologies, departmental\_head\_count |

## Clearbit

Look up person and company data based on an email or domain. Sync fresh and reliable data across your systems in real time with over 100 attributes on more than 44 million companies and 350 million contacts.

Keep in mind:

* Census uses the Clearbit API **Secret Key**, not the Publishable Key. This should be available in the [Clearbit API](https://dashboard.clearbit.com/api) section.
* Enriching does use API credits. Please see your [Clearbit Dashboard](https://dashboard.clearbit.com/dashboard) to track your usage.

| Data Category | Identifier | Data Points                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Person        | email      | id, name.givenName, name.familyName, name.fullName, location, timeZone, utcOffset, geo.city, geo.state, geo.country, geo.lat, geo.lng, bio, site, avatar, employment.name, employment.title, employment.role, employment.subRole, employment.seniority, employment.domain, facebook.handle, github.handle, github.id, github.avatar, github.company, github.blog, github.followers, github.following, twitter.handle, twitter.id, twitter.followers, twitter.following, twitter.location, twitter.site, twitter.statuses, twitter.favorites, twitter.avatar, linkedin.handle, googleplus.handle, fuzzy, emailProvider, indexedAt                                                                                                                                                                                                                                                                                                                          |
| Company       | domain     | id, name, legalName, domain, domainAliases, site.phoneNumbers, site.emailAddresses, tags, category.sector, category.industryGroup, category.industry, category.subIndustry, category.sicCode, category.naicsCode, description, foundedYear, location, timeZone, utcOffset, geo.streetNumber, geo.streetName, geo.subPremise, geo.city, geo.state, geo.stateCode, geo.postalCode, geo.country, geo.countryCode, geo.lat, geo.lng, identifiers.usEIN, metrics.raised, metrics.alexaUsRank, metrics.alexaGlobalRank, metrics.employees, metrics.employeesRange, metrics.marketCap, metrics.annualRevenue, metrics.estimatedAnnualRevenue, metrics.fiscalYearEnd, facebook.handle, linkedin.handle, twitter.handle, twitter.id, twitter.bio, twitter.followers, twitter.following, twitter.location, twitter.site, twitter.avatar, crunchbase.handle, logo, emailProvider, type, phone, tech, techCategories, parent.domain, ultimateParent.domain, indexedAt |

## Need help with data enrichment?

having issues with one of our data providers? Looking for another service? [Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
