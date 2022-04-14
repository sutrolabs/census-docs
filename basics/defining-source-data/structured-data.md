---
description: >-
  This page will cover how to build define semi-structured data in your
  datasource
---

# Structured Data

Some services such at NetSuite, Airtable, and others require certain values to be passed as structured objects rather than single values. The specific fields that require this behavior are specified in the documentation on each connection and will cover the exact format those fields need to be. But how do you get them into the necessary format in the first place? We're here to help!

Most modern warehouses now support syntax for defining semi-structured data and this page goes over how to do that. But in the worst case, you can always pass in JSON-formatted text strings for these fields and Census will parse these values as well.

## Creating structured data

Your traditional database column has a specific type such as `VARCHAR` or `INT` and will only ever contain that type of value. Modern data warehouses have increasingly added support for columns that contain structured data, almost always in the form of [JSON](https://www.json.org/json-en.html). Census takes advantage of these new capabilities to allow sending "nested" data structures where appropriate for each destination.&#x20;

For most data warehouses, you can create the appropriate data structure to match the destination through a combination of one or more of the follow functions:

* Creating an array of values by either providing a list of values or aggregating a list of values through a `GROUP BY`.
* Creating an object made of key-value pairs by providing sets of values, or aggregating a pair of columns through a `GROUP BY`.&#x20;
* Parsing a JSON formatted string.

Note: If you need to get really expressive, you can also combine these creating an array of objects, or an object with arrays as well.&#x20;

Each warehouse does this with its own set of functions. We'll go over each of them here:

### Snowflake

Of all the warehouses, Snowflake provides the richest set of functions to build and manipulate semi-structured data.&#x20;

To create an array, Snowflake provides a number of functions. These two are the most common:

* `ARRAY_CONSTRUCT(value1, value2, ...)` - Creates an array out of the provided values ([Snowflake docs](https://docs.snowflake.com/en/sql-reference/functions/array\_construct.html))
* `ARRAY_AGG(column)` - Creates an array out of the `GROUP BY` or window function values for that aggregation ([Snowflake docs](https://docs.snowflake.com/en/sql-reference/functions/array\_agg.html))

For objects, Snowflake provides several more functions, including the matching set:

* `OBJECT_CONSTRUCT(key1, value1, key2, value2, ...)` - Creates an object out of the provided key and value pairs ([Snowflake docs](https://docs.snowflake.com/en/sql-reference/functions/object\_construct.html))
* `OBJECT_AGG(key_column, value_column)` - Creates an object out of the `GROUP BY` or window function keys and values for that aggregation ([Snowflake docs](https://docs.snowflake.com/en/sql-reference/functions/object\_agg.html))

Finally, to parse JSON, `PARSE_JSON(json_string)` ([Snowflake docs](https://docs.snowflake.com/en/sql-reference/functions/parse\_json.html)) will take care of that for you.&#x20;

In all of these cases, Snowflake will return a `VARIANT` type which is their data type for semi-structured data.&#x20;

### Redshift

Redshift is late to the game on adding support for storing semi-structured data. They've just recently added the `SUPER` datatype and you can take advantage that with the `JSON_PARSE(json_string)` function ([Redshift docs](https://docs.aws.amazon.com/redshift/latest/dg/JSON\_PARSE.html)). Unfortunately, that's the only native option for Redshift at this point so to perform the same object/array aggregations from Snowflake, take a look at the string-based `LISTAGG()` function ([Redshift docs](https://docs.aws.amazon.com/redshift/latest/dg/r\_LISTAGG.html)).

