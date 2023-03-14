# Filter Segments

## GET /sources/\[ID]/filter\_segments

This endpoint lists information all the filter segments for a given source, including information on what columns it includes.

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the sync runs ascending or descending by creation time.
* `page` - `number`. Specifies which page of results to return. Defaults to 1.
* `per_page` - `number`. Specifies number of results per page. Defaults to 25.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources/[ID]/filter_segments' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "success",
    "data": [
        {
            "id": 5,
            "name": "my segment",
            "created_at": "2023-03-10T17:32:37.459Z",
            "updated_at": "2023-03-14T16:50:31.371Z",
            "filter_segment_source_object_id": 10,
            "molecules": [
                [
                    {
                        "attribute": "id",
                        "attribute_type": "column",
                        "operator": "isnotnull",
                        "value": null,
                        "moleculeIndex": 0,
                        "atomIndex": 0
                    }
                ]
            ],
            "parent_source_object_id": 3,
            "parent_source_object_type": "DataWarehouse::BusinessObjectSource",
            "record_count": 1,
            "query": "select * from (\n  SELECT 1 AS id, 'Planet Express'::text AS company_name\n)\n as census_1d19740e93f711b22efaea201fcf3f8f\n where (\"id\" IS NOT NULL )"
        },
        {
            "id": 3,
            "name": "Valid name",
            "created_at": "2023-03-09T21:32:32.190Z",
            "updated_at": "2023-03-10T17:29:34.191Z",
            "filter_segment_source_object_id": 6,
            "molecules": [
                [
                    {
                        "attribute": "id",
                        "attribute_type": "column",
                        "operator": "isnotnull",
                        "value": null,
                        "moleculeIndex": 0,
                        "atomIndex": 0
                    }
                ],
                "AND",
                {
                    "relationship_id": 1,
                    "molecules": [
                        [
                            {
                                "attribute": "user_id",
                                "attribute_type": "column",
                                "operator": "lessthan",
                                "value": "3",
                                "moleculeIndex": 0,
                                "atomIndex": 0
                            },
                            "AND",
                            [
                                {
                                    "attribute": "user_id",
                                    "attribute_type": "column",
                                    "operator": "equals",
                                    "value": null
                                }
                            ]
                        ]
                    ],
                    "moleculeIndex": 2
                }
            ],
            "parent_source_object_id": 3,
            "parent_source_object_type": "DataWarehouse::BusinessObjectSource",
            "record_count": 1,
            "query": "select * from (\n  SELECT 1 AS id, 'Planet Express'::text AS company_name\n)\n as census_1d19740e93f711b22efaea201fcf3f8f\n where (\"id\" IS NOT NULL ) AND exists (select * from (\n  select 1 as user_id\n)\n as census_b547c2bb7be10ee8c44874b33a1a04f4_d1\nwhere census_1d19740e93f711b22efaea201fcf3f8f.id = user_id AND ((\"user_id\" < 3 AND (TRUE))))"
        },
    ],
    "next": "https://app.getcensus.com/api/v1/sources/2/filter_segments?page=2&per_page=25"
}
```
{% endtab %}
{% endtabs %}

| Data Property             | Description                                                                                                                |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| A list of filter segments | A list of your filter segments. The properties of a sync are expanded on below in the GET /filter segments/\[ID] endpoint. |

### GET /sources/\[ID]/filter\_segments/\[ID]

This endpoint lists information for a given filter segments, including information on what columns it includes.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources/[ID]/filter_segments/[ID]' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "success",
    "data": {
        "id": 3,
        "name": "Valid name",
        "created_at": "2023-03-09T21:32:32.190Z",
        "updated_at": "2023-03-10T17:29:34.191Z",
        "filter_segment_source_object_id": 6,
        "molecules": [
            [
                {
                    "attribute": "id",
                    "attribute_type": "column",
                    "operator": "isnotnull",
                    "value": null,
                    "moleculeIndex": 0,
                    "atomIndex": 0
                }
            ],
            "AND",
            {
                "relationship_id": 1,
                "molecules": [
                    [
                        {
                            "attribute": "user_id",
                            "attribute_type": "column",
                            "operator": "lessthan",
                            "value": "3",
                            "moleculeIndex": 0,
                            "atomIndex": 0
                        },
                        "AND",
                        [
                            {
                                "attribute": "user_id",
                                "attribute_type": "column",
                                "operator": "equals",
                                "value": null
                            }
                        ]
                    ]
                ],
                "moleculeIndex": 2
            }
        ],
        "parent_source_object_id": 3,
        "parent_source_object_type": "DataWarehouse::BusinessObjectSource",
        "record_count": 1,
        "query": "select * from (\n  SELECT 1 AS id, 'Planet Express'::text AS company_name\n)\n as census_1d19740e93f711b22efaea201fcf3f8f\n where (\"id\" IS NOT NULL ) AND exists (select * from (\n  select 1 as user_id\n)\n as census_b547c2bb7be10ee8c44874b33a1a04f4_d1\nwhere census_1d19740e93f711b22efaea201fcf3f8f.id = user_id AND ((\"user_id\" < 3 AND (TRUE))))"
    }
}
```
{% endtab %}
{% endtabs %}

| Data Property                       | Description                                                                                                                                                                                                                                                                      |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                                  | The id of this filter segment.                                                                                                                                                                                                                                                   |
| name                                | The name of this filter segment.                                                                                                                                                                                                                                                 |
| filter\_segment\_source\_object\_id | The source object id for this model.                                                                                                                                                                                                                                             |
| model\_id                           | The id of the model that this filter segment is related to (either directly from legacy segments or indirectly via the entity)                                                                                                                                                   |
| query                               | The SQL query associated with this filter segment.                                                                                                                                                                                                                               |
| record\_count                       | The cached size of the segment at that particular moment in time.                                                                                                                                                                                                                |
| created\_at                         | When this filter segment was created.                                                                                                                                                                                                                                            |
| updated\_at                         | When this filter segment was last updated.                                                                                                                                                                                                                                       |
| molecules                           | <p>A JSON array composed of the conditions that describe the segment. The types of elements you can find in this array are as follows:<br>- arrays of conditions on the top level entity<br>- objects to describe conditions on related entities<br>- the enums "AND" / "OR"</p> |

### POST /sources/\[ID]/filter\_segments

This endpoint creates a filter segment with the given data.

{% tabs %}
{% tab title="Request" %}
```
curl --location --request POST 'https://app.getcensus.com/api/sources/6/filter_segments' \
--header 'Authorization: Bearer [API_TOKEN]' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "API Generated Filter Segment",
    "molecules": [[
                    {
                        "attribute": "id",
                        "attribute_type": "column",
                        "operator": "exactly",
                        "value": "2",
                        "moleculeIndex": 0,
                        "atomIndex": 0
                    }
                ]],
    "business_object_id": 2,
 
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "created",
    "data": {
        "id": 79
    },
    "filter_segment_source_url": "https://app.getcensus.com/api/v1/sources/9789/filter_segments/3710/source_status"
}
```
{% endtab %}
{% endtabs %}

| Request Property       | Description                                             |
| ---------------------- | ------------------------------------------------------- |
| name\*                 | `required`. The name of this filter segment.            |
| molecule\*             | The shape of the molecule.                              |
| business\_object\_id\* | The id of the entity on which this segment is based on. |

| Response Property            | Description                                                                                                                                                                                                                                                 |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| status                       | `created` or `error` indicating whether the filter segment was created.                                                                                                                                                                                     |
| data                         | Present if successful. An object containing the `filter_segment_id`                                                                                                                                                                                         |
| filter\_segment\_source\_url | Some subproperties of the filter\_segment are created asynchronously. You can query this url to fetch the status of the creation (true or false). When status is true, it will return all properties returned in GET /sources/\[ID]/filter\_segments/\[ID]. |
| message                      | Present if error. Contains message describing the error.                                                                                                                                                                                                    |

### PATCH /sources/\[ID]/filter\_segments/\[ID]

This endpoint updates a filter segment with the given ID.

{% tabs %}
{% tab title="Request" %}
```
curl --request PATCH 'https://app.getcensus.com/api/v1/sources/filter_segments/98' \
--header 'Authorization: Bearer [API_TOKEN]' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "API Updated Filter Segments",
    "molecules": [],
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "updated",
    "data": {
        "id": 3,
        "name": "API Updated Filter Segments",
        "created_at": "2023-03-09T21:32:32.190Z",
        "updated_at": "2023-03-10T17:29:34.191Z",
        "filter_segment_source_object_id": 6,
        "molecules": [],
        "parent_source_object_id": 3,
        "parent_source_object_type": "DataWarehouse::BusinessObjectSource",
        "record_count": 1,
        "query": "select * from (\n  SELECT 1 AS id, 'Planet Express'::text AS company_name\n)\n as census_1d19740e93f711b22efaea201fcf3f8f\n where (\"id\" IS NOT NULL ))))"
    }
}
```
{% endtab %}
{% endtabs %}

| Request Property | Description                      |
| ---------------- | -------------------------------- |
| name             | The name of this filter segment. |
| molecule         | The shape of the molecule.       |

| Response Property | Description                                                                   |
| ----------------- | ----------------------------------------------------------------------------- |
| status            | `updated` or `error` indicating whether the filter segments was updated.      |
| data              | Present if successful. Returns the same object as `GET /filter_segments/[ID]` |
| message           | Present if error. Contains message describing the error.                      |

### DELETE /sources/\[ID]/filter\_segments/\[ID]

This endpoint deletes a filter segment with the given ID.

{% tabs %}
{% tab title="Request" %}
```
curl --request DELETE 'https://app.getcensus.com/api/v1/sources/6/filter_segments/98' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "deleted"
}
```
{% endtab %}
{% endtabs %}

| Response Property | Description                                                                      |
| ----------------- | -------------------------------------------------------------------------------- |
| status            | `deleted` or `404` indicating whether the filter segments was found and deleted. |

