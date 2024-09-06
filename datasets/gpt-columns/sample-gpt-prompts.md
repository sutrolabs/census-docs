# Sample GPT Prompts

GPT Columns enable you to dynamically generate unique content for each row in your dataset using OpenAI's GPT models. With GPT Columns, you can define a prompt and use [Liquid templating](../../basics/core-concept/liquid-templates.md) to reference values from other columns. This setup allows you to send a customized GPT prompt request for each row, with the response automatically written back to your GPT Column.

Learn more about GPT Columns and how to set them up [here](./).



You can do some pretty amazing stuff using the GPT columns including things like lead scoring, industry assignments, assign personalized promo codes and data clean up. GPT can cover use cases across all industries and verticals.&#x20;



We will use this page to post some sample GPT prompts you can use as inspiration to create your own GPT columns.&#x20;



### Classify and Summarize Data

<details>

<summary>Classify outbound responses by sentiment </summary>

```
Your role is to determine the sentiment of a response to a request for a demo.

1. Review the emails in {{record['RESPONSE']}}. Based on the text, determine the sentiment of its author.
2. Based on the sentiment of the response, categorize the response as either:
Interested
Not interested
Enthusiastic
Snarky or Annoyed
```

Columns Needed: Email responses uploaded from your outbound platform

Best response type: Enum or string

Activation Strategy: Use these to improve prioritization and reporting on the quality of outbounding efforts

</details>

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
Your task is to determine what sales territory a given account falls into based on its location relative to the Mississippi river. 

1. Each of the records in {{record['ADDRESS']}} ends in a state abbreviation and a five-digit ZIP code. Focus only on these parts of the address.

2. For each record, determine whether it is east or west of the Mississippi River. 
If the address is in the United States and east of the Mississippi River, return [US East]
If the address is in the United States and West of the Mississippi River, return [US West]
If the address is in Canada, return [Canada]
```

Columns Needed: An address including a state or zip code, shown here as ADDRESS

Best response type: Enum or string

</details>

<details>

<summary>Assign a marketing persona based on a job title</summary>

```
Your task is to assign personas to the listed job titles.

1. Review the job title listed in {{record['TITLE']}}. 

2. Assign a matching persona by the following logic:
If the person is a senior leader, return [Executive]. Look for titles including Vice President, VP, Chief, or anything in the C-suite
If the person has a sales or marketing title, return [Go to market]
If the person has a title in growth or ops, return [Ops]
```

Update the categories as needed.

Columns Needed: Job Title, shown here as TITLE

Best Response type: Enum or string

Activate to: Your marketing automation platforms to power personalized email nurtures or trigger PLG playbooks.

</details>

###

### Enrich and Enhance Records

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

<details>

<summary>Assign a marketing persona based on a job title</summary>

```
You are tasked with determining the industry classification for a given company based on publicly available information. The industry classification should match the Securities and Exchange Commission's (SEC) list of official standard industrial classifications (SIC).
You will be given a company name: {{record['COMPANY']}}

Your task is to:
1. Research the company using publicly available information. This may include the company's official website, SEC filings, financial reports, and reputable business news sources.
2. Based on the information you find, determine the most appropriate industry classification for the company according to the SEC's standard industrial classification (SIC) system. The SIC is a four-digit code that categorizes companies based on their primary business activities.
3. Provide your answer in the following format:
[Insert the corresponding industry name here]([Insert the following SIC code here]
Remember to be as accurate as possible in your classification. If you're unsure about the exact classification, choose the closest match based on the available information.
If you cannot find enough information to make a determination, or if the company name is too vague or ambiguous, or if the confidence level is less than 80%, respond with:
Unable to determine. Insufficient information available.
</industry_classification>
Begin your research and classification now. Provide no explanation.
Before answering, think carefully about the instructions.
```

Columns Needed: Company name, shown here as COMPANY.  The data could be improved by including a URL to the company website, but this is not necessary.

Best Response type: String

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

