# Sample GPT Prompts

GPT Columns enable you to dynamically generate unique content for each row in your dataset using OpenAI's GPT models. With GPT Columns, you can define a prompt and use [Liquid templating](../../../basics/core-concept/liquid-templates.md) to reference values from other columns. This setup allows you to send a customized GPT prompt request for each row, with the response automatically written back to your GPT Column.

Learn more about GPT Columns and how to set them up [here](./).



You can do some pretty amazing stuff using the GPT columns including things like lead scoring, industry assignments, assign personalized promo codes and data clean up. GPT can cover use cases across all industries and verticals.&#x20;



We will use this page to post some sample GPT prompts you can use as inspiration to create your own GPT columns.&#x20;



### B2B Use Cases

<details>

<summary>Mark a new lead as a B2B or a B2C company</summary>

```
For the following company, return company type based on the company name
COMPANY NAME: {{ record['COMPANY_NAME']}}

```

Use Enum as the response type and include in potential values such as B2B, B2C, Both.

</details>

<details>

<summary>Assign sales territory based on company address</summary>

```
Respond with just the sales territory for the following 
company location: {{ record['CITY'] }}, {{ record['STATE_REGION'] }}, {{ record['COUNTRY'] }}

Note: East / West is determined by Mississippi river.
```

Use Enum as the response type and include in potential values such as NA East, NA West, APAC, EMEA.

</details>

### B2C Use Cases

<details>

<summary>Create personalized discount based on customer's LTV</summary>

We will use customer's life time value as an input column. If you don't have LTV yet in your dataset, you can easily calculate that for each user using [Computed Columns](../core-concepts-3.md).&#x20;

You can also use [Computed Columns](../core-concepts-3.md) to calculate days since last purchase.

```
Build a customer promo formula (from 10% to 30%) based on these examples:

- 30 days since last purchase, $10 LTV -> 30%
- 60 days since last purchase, $10 LTV -> 20%
- 30 days since last purchase, $250 LTV -> 20%
- 60 days since last purchase, $250 LTV -> 10%

Evaluate the formula for this customer:

Customer's Lifetime Value (LTV): {{ record['CUSTOMER_LTV']}}
Days since last purchase: {{ record['DAYS_SINCE_LAST_PURCHASE']}}

```

</details>



### Data Cleanup

<details>

<summary>Standardize email field values</summary>

```
For the following field, return a single value as an email address. Remove all unwanted text. If the field does not have any email address, return empty string.
Field: {{ record['USER_EMAIL']}}

You will not provide any explanation or description. 
```

</details>

<details>

<summary>Clean up leading and trailing spaces</summary>

```
For the following field, return the text with leading and trailing spaces removed. Don't remove space in-between words.
Field: {{ record['TEXT_FIELD']}}

You will not provide any explanation or description. 
```

</details>

<details>

<summary>Remove Special Characters from a name</summary>

```
For the following name field, return the name with special characters and numeric digits removed
Name Field: {{ record['CUSTOMER_NAME']}}
```

</details>

<details>

<summary>Standardize mailing addresses</summary>

```
For the following address field, return the outcome in an standardized US address format. 
Address Field: {{ record['USER_ADDRESS']}}.
```

</details>

