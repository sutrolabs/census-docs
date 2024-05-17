---
description: How to build define semi-structured data in your data source.
---

# Arrays and Nested Objects

Some services such at NetSuite, Airtable, and others require certain values to be passed as structured objects rather than single values. The specific fields that require this behavior are specified in the documentation on each connection and will cover the exact format those fields need to be. But how do you get them into the necessary format in the first place? We're here to help!

Most modern warehouses now support syntax for defining semi-structured data and this page goes over how to do that. But in the worst case, you can always pass in JSON-formatted text strings for these fields and Census will parse these values as well.

## Creating structured data

Your traditional database column has a specific type such as `VARCHAR` or `INT` and will only ever contain that type of value. Modern data warehouses have increasingly added support for columns that contain structured data, almost always in the form of [JSON](https://www.json.org/json-en.html). Census takes advantage of these new capabilities to allow sending "nested" data structures where appropriate for each destination.

For most data warehouses, you can create the appropriate data structure to match the destination through a combination of one or more of the follow functions:

* Creating an array of values by either providing a list of values or aggregating a list of values through a `GROUP BY`.
* Creating an object made of key-value pairs by providing sets of values, or aggregating a pair of columns through a `GROUP BY`.
* Parsing a JSON formatted string.

Note: If you need to get really expressive, you can also combine these creating an array of objects, or an object with arrays as well.

Each warehouse does this with its own set of functions. We'll go over each of them here:

### Snowflake

Of all the warehouses, Snowflake provides the richest set of functions to build and manipulate semi-structured data.

To create an array, Snowflake provides a number of functions. These two are the most common:

* `ARRAY_CONSTRUCT(value1, value2, ...)` - Creates an array out of the provided values ([Snowflake docs](https://docs.snowflake.com/en/sql-reference/functions/array\_construct.html))
* `ARRAY_AGG(column)` - Creates an array out of the `GROUP BY` or window function values for that aggregation ([Snowflake docs](https://docs.snowflake.com/en/sql-reference/functions/array\_agg.html))

For objects, Snowflake provides several more functions, including the matching set:

* `OBJECT_CONSTRUCT(key1, value1, key2, value2, ...)` - Creates an object out of the provided key and value pairs ([Snowflake docs](https://docs.snowflake.com/en/sql-reference/functions/object\_construct.html))
* `OBJECT_AGG(key_column, value_column)` - Creates an object out of the `GROUP BY` or window function keys and values for that aggregation ([Snowflake docs](https://docs.snowflake.com/en/sql-reference/functions/object\_agg.html))

Finally, to parse JSON, `PARSE_JSON(json_string)` ([Snowflake docs](https://docs.snowflake.com/en/sql-reference/functions/parse\_json.html)) will take care of that for you.

In all of these cases, Snowflake will return a `VARIANT` type which is their data type for semi-structured data.

### BigQuery

BigQuery has some interesting quirks regarding their structured object support.

To create an array, BigQuery has one option, as specified in their docs [here](https://cloud.google.com/bigquery/docs/reference/standard-sql/array\_functions#array):

* `ARRAY(SELECT tag FROM tags WHERE user_id = user_id)`
* `ARRAY(SELECT '1' UNION ALL SELECT '2' UNION ALL SELECT '3')`

{% hint style="info" %}
The approach above only works with a subquery that returns one column, as per BigQuery's documentation.
{% endhint %}

For Objects, BigQuery does not support diffing across their `struct` object, so we recommend that you convert it to string via `to_json_string()`. With that caveat, there might still be times when you want to pass JSON of a `struct` for different properties during your use of Census. There are a number of ways to create a struct in BigQuery.

For example, you may wish to pass the JSON `{'id': '110'}` to a destination that supports nested objects as fields. Although you might've constructed the JSON as `struct('110' as id)`, you will need to convert it to a string as follows:

`to_json_string(struct('110' as id))`

### Redshift

Redshift is late to the game on adding support for storing semi-structured data. They've just recently added the `SUPER` datatype and you can take advantage that with the `JSON_PARSE(json_string)` function ([Redshift docs](https://docs.aws.amazon.com/redshift/latest/dg/JSON\_PARSE.html)). Unfortunately, that's the only native option for Redshift at this point so to perform the same object/array aggregations from Snowflake, take a look at the string-based `LISTAGG()` function ([Redshift docs](https://docs.aws.amazon.com/redshift/latest/dg/r\_LISTAGG.html)).
