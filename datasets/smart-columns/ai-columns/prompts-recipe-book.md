# AI Prompts Recipe Book

**Why AI Columns?**

AI columns allow you to enrich, enhance, clean and classify data using LLMs. The potential is limitless, but we've shared our favorite prompts in this recipe book. Our team uses AI columns to:

* Enrich records with industry data, persona classifiers, or other personalization drivers.
* Layer sentiment analysis and other LLM capabilities into our Apollo data to drive automations
* Process large amounts of product usage data that just wouldn't be cost-effective in Salesforce or other end platforms
* Get around cumbersome formula fields in Salesforce
* Avoid writing complex regex to clean and format data

Learn more in our interactive demo below:

{% @arcade/embed flowId="dlpvULqMDw8YEz82e2ia" url="https://app.arcade.software/share/dlpvULqMDw8YEz82e2ia?variable.company_name=INSERT_VALUE_HERE&variable.first_name=INSERT_VALUE_HERE" %}

Learn more about AI Columns and how to set them up [here](./).

Not a Census user yet? [Try AI columns for free](https://login.getcensus.com/u/signup/identifier?state=hKFo2SBVaGhKcUwwcktoTGJRdmxlc19ZRE52aW9hNXFNMDJPYaFur3VuaXZlcnNhbC1sb2dpbqN0aWTZIDZaOXp2ck9vc190dktVX0RvbjJfZERFTGxHWmFIWnMzo2NpZNkgajFnb29hYnExSEFDb000V3ZmaDJhSk5yTXlFWGZJM0E&_gl=1*14swtjj*_gcl_aw*R0NMLjE3MjU5MTM1NzIuQ2p3S0NBand1ZnEyQmhBbUVpd0FuWnF3OHFjYmFpWkQ5VGh5SVJjdm5uR0t5LVh1RnFUVkxvRGY1cE1HUDVUVmlMUmhORHp4eThlb19Sb0NuaE1RQXZEX0J3RQ..*_gcl_au*MTQzNDczNzM2LjE3MjIyMjQ2NDg.).

### Classify and Summarize Data

<details>

<summary>Classify outbound responses by sentiment </summary>

{% code overflow="wrap" %}
```
Your role is to determine the sentiment of a response to a request for a demo.

1. Review the emails in {{record['RESPONSE']}}. Based on the text, determine the sentiment of its author.
2. Based on the sentiment of the response, categorize the response as either:
Interested
Not interested
Enthusiastic
Snarky or Annoyed
```
{% endcode %}

Columns Needed: Email responses uploaded from your outbound platform

Best response type: Enum or string

Activation Strategy: Use these to improve prioritization and reporting on the quality of outbounding efforts

</details>

<details>

<summary>Mark a new lead as a B2B or a B2C company</summary>

{% code overflow="wrap" %}
```
For the following company, return company type based on the company name
COMPANY NAME: {{ record['COMPANY_NAME']}}

```
{% endcode %}

Use Enum as the response type and include in potential values such as B2B, B2C, Both.

</details>

<details>

<summary>Analyze product usage trends to provide personalized support</summary>

{% code overflow="wrap" %}
````
Summarize the company's product usage trends over the last 30 days, focusing on key feature activity and highlighting any significant changes compared to the previous 30 days. Use a conversational style with bullet points to highlight key observations for sales talking points. Prioritize the following metrics for analysis:

- Sync Creation Attempts
- Model Creation
- New Sync Configurations
- Deleted or Paused Syncs
- Failed and Invalid Records by service_connection_type
- Records Updated by service_connection_type

Important: Any event in `{{ record['ACTIVITY_SUMMARY_JSON'] }}` that starts with `attempted_` or ends with `_deleted` or `_paused` should not be considered positive. These should be flagged for further investigation by the Customer Success team.

The following JSON includes fields that provide insights into their product usage:

1. `failed_records`: 
    - The number of failed syncs per service_connection_type. An increase in this indicates possible issues with syncs.

2. `invalid_records_sum`: 
    - The total number of invalid records by service_connection_type, signaling potential data issues. An increase in this indicates possible issues with model and dataset creation.

3. `records_updated_sum`: 
    - The number of records updated per service_connection_type, indicating active data syncing. An increase in this could indicate new and growing use cases which are positive. A decrease could indicate that a company is scaling back and something we should flag for the Customer Success team.

4. `activity_summary`: 
    - Provides a breakdown of sync creation attempts, model creation, new sync configurations, and syncs paused or deleted over the last 30 days compared to the previous 30 days.

Use the information from the provided JSON:

Failed, invalid, and successful records by service_connector_type: 
```
{{ record['WEEKLY_RECORDS_ACTIVITES'] }}
```
And the feature usage JSON:
```
{{ record['ACTIVITY_SUMMARY_JSON'] }}
```

---

Structure:

1. Overview of that data:
   - Summarize the company's product activity over the time period provided, focusing on key features such as sync creation, model creation, and new sync configurations.
   - Highlight any significant differences between the current and previous 30 days.
   - Highlight any significant increases or decrease in `records_updated`, `records_failed` or `reocrds_invalid`
   
2. Growth Signals & Potential Issues:
   - Identify areas of growth, such as an increase in model creation or sync configurations.
   - Flag potential concerns like decreases in sync creation, increases in invalid records, or events marked as `attempted_`, `_deleted`, or `_paused` for Customer Success follow-up.

3. Feature Usage Breakdown:
   - For each feature used (e.g., sync creation, model creation), provide details about the activity:
     - Sync Creation Attempts: How many syncs were attempted in the last 30 days? Is there a drop?
     - Model Creation: How many models were created, and does this suggest deeper product exploration?
     - Failed/Invalid Records: Were there increases in failed or invalid records? Flag these for Customer Success follow-up.
     - Records Updated: Were there any notable increases in records updated, signaling active syncing?
   
4. Service Connection Type Concerns:
   - Highlight any service_connection_types showing a growth in invalid or failed records, or events marked as `attempted_`, `_deleted`, or `_paused`. Provide specific details and suggest investigation.

5. Suggested Next Steps:
   - Suggest personalized actions for the Customer Success team, such as offering more resources, providing troubleshooting support for invalid records, or scheduling check-ins to resolve sync issues.
   - Encourage deeper engagement with underutilized features, particularly if certain features haven't been used in the last 15 days.

```

````
{% endcode %}

Columns needed: We use a JSON formatted column to pass the activity details and their meanings to the LLM.&#x20;

Best response type: String

</details>

<details>

<summary>Assign sales territory based on company address</summary>

{% code overflow="wrap" %}
```
Your task is to determine what sales territory a given account falls into based on its location relative to the Mississippi river. 

1. Each of the records in {{record['ADDRESS']}} ends in a state abbreviation and a five-digit ZIP code. Focus only on these parts of the address.

2. For each record, determine whether it is east or west of the Mississippi River. 
If the address is in the United States and east of the Mississippi River, return [US East]
If the address is in the United States and West of the Mississippi River, return [US West]
If the address is in Canada, return [Canada]
```
{% endcode %}

Columns Needed: An address including a state or zip code, shown here as ADDRESS

Best response type: Enum or string

</details>

<details>

<summary>Assign a marketing persona based on a job title</summary>

{% code overflow="wrap" %}
```
Your task is to assign personas to the listed job titles.

1. Review the job title listed in {{record['TITLE']}}. 

2. Assign a matching persona by the following logic:
If the person is a senior leader, return [Executive]. Look for titles including Vice President, VP, Chief, or anything in the C-suite
If the person has a sales or marketing title, return [Go to market]
If the person has a title in growth or ops, return [Ops]
```
{% endcode %}

Update the categories as needed.

Columns Needed: Job Title, shown here as TITLE

Best Response type: Enum or string

Activate to: Your marketing automation platforms to power personalized email nurtures or trigger PLG playbooks.

</details>

<details>

<summary>Summarize reviews to prioritize areas for improvement</summary>

{% code overflow="wrap" %}
```
Your task is to determine the reasons behind our five star reviews. 

1. Read the reviews in {{Record['REVIEW']}}
2. Categorize the core focus of the review into one of the following:
-Food
-Service
-Atmosphere
-Location

If multiple answers are relevant, select the one that appears first. Provide only the summarized reason for the review and no other context. 
```
{% endcode %}

Update the categories as needed.

Columns Needed: the text of a review, shown here as REVIEW

Best Response type: Enum or string

</details>

<details>

<summary>Customer Sentiment Analysis for B2B and B2C Businesses</summary>

{% code overflow="wrap" %}
```
You are a customer support quality analyst reviewing support requests submitted to a B2B SaaS company. Please assign a sentiment category for each customer request based on the following criteria:

Sentiment Categories (select one only from the list below):
	1.	Positive - Upgrade: The customer expresses interest in upgrading their plan or adding features.
	2.	Positive - General Inquiry: The customer has a general question about the service, showing a positive tone.
	3.	Neutral - General Inquiry: The customer has a straightforward question without a positive or negative tone.
	4.	Neutral - Billing: The customer is inquiring about billing or payment details without expressing frustration.
	5.	Negative - Service Issue: The customer indicates a problem with the service or functionality.
	6.	Negative - Access Issue: The customer is having trouble accessing their account or logging in.
	7.	Negative - Billing Concern: The customer expresses a concern or dissatisfaction regarding billing.
	8.	Negative - Delayed Support: The customer mentions a delay in support or response times.
	9.	Complaint - Product Feature: The customer expresses dissatisfaction with a specific product feature.
	10.	Complaint - Other: The customer provides general complaints or dissatisfaction not covered above.

Important: You must select only one category from the list above. Do not create additional categories or variations. For each request, provide the chosen sentiment category first, followed by a brief explanation.

Inputs:
	•	Subject: {{ record['SUBJECT'] }}
	•	Body: {{ record['BODY'] }}

Example Message for Analysis:

Subject: Unable to access my account

Body: "I am trying to log into my account, but I keep getting an error message. Can someone help me resolve this issue as soon as possible?"

Sentiment: Negative - Access Issue

Explanation: The message indicates a problem with accessing the account, suggesting the customer is frustrated due to login issues.

Another Example Message for Analysis:

Subject: Interested in upgrading to a higher plan

Body: "Hello, I'd like to learn more about the premium plan options and see if they'd be a better fit for our team."

Sentiment: Positive - Upgrade

Explanation: The message reflects interest in an upgrade and shows a positive outlook toward exploring premium options.
```
{% endcode %}

Update the categories as needed.

Columns Needed: Email Subject and Body<br>

Best response type: Enum

</details>

<details>

<summary>Account Fit Scoring / Lead Scoring</summary>

{% code overflow="wrap" %}
```
Using {{ record['CUSTOMER_TRAITS'] }}, perform an Ideal Customer Profile (ICP) analysis using regression. List positive and negative traits with their correlation strengths (strong, moderate, weak), noting data gaps without assuming negatives. Identify valuable traits exclusively based on regression analysis, with category weights summing to 100% for LLM scoring.


Success Metrics


Use these metrics to assess success, loyalty, and conversion:
   •   ARR: Annual recurring revenue, indicating customer value.
   •   ever_customer: If the account has been a customer.
   •   is_customer: Current active customer status.
   •   LTV: Expected revenue per customer.
   •   months_as_customer: Duration as an active customer.
   •   weeks_to_convert: Time from first interaction to conversion.


Categories (with weights)


   1.  Technology (30%):  Identify high/medium confidence tech with success correlations.
   2.  Industry (15%): Highlight industries with positive/negative success correlations.
   3.  Annual Revenue Range (10%): List revenue ranges correlating with success.
   4.  Employee Size Range (15%): Specify employee count ranges with success alignment.
   5.  Geographic Fit (10%): Identify country or regional correlations.
   6.  Investors (10%): Highlight investor partnerships with positive or negative impacts.
   7.  Hiring Trends (10%): Analyze relevant job titles and hiring volume; exclude negative indicators.


Final Output: Structure findings with headings, correlation strengths, and category weights. Note data gaps and additional traits from regression analysis for scoring and lead comparison.

```
{% endcode %}

Update the categories as needed.

Columns Needed: Customer Traits<br>

Best response type: Enum or Numbers

</details>

<details>

<summary>Analyze Traits: Identify High Value Customers</summary>

{% code overflow="wrap" %}
````

You are a data analyst. Using the customer data from the highest plan and the lowest plan, create a trait-by-trait analysis showing the likelihood of being a high-value customer.


For each trait in the data:
1. List each possible value within that trait
2. Calculate the ratio of that value appearing in the high-tier vs low-tier plan
3. Sort traits by their predictive strength (strongest correlation to weakest)


Format your output as:


TRAIT: [Name of Trait]
- VALUE: [Specific Value]
 - High Plan: [%]
 - Low Plan: [%]
 - LIKELIHOOD RATIO: [X]x more likely to be high-value
 Only include traits where there is at least a 10% difference between plans.
Sort values within each trait by likelihood ratio (highest to lowest).
```


This should generate output like:


```
TRAIT: Age Range
- VALUE: 18-25
 - High Plan: 40%
 - Low Plan: 28%
 - LIKELIHOOD RATIO: 1.43x more likely to be high-value


TRAIT: Visit Frequency
- VALUE: Daily
 - High Plan: 38%
 - Low Plan: 24%
 - LIKELIHOOD RATIO: 1.58x more likely to be high-value
```

````
{% endcode %}



</details>

<details>

<summary>Customer Upsell Score / Potential</summary>

{% code overflow="wrap" %}
```
Using only the following benchmark data, calculate the customer's upsell score by adding the likelihood ratios of their matching traits found in this analysis:


Using the traits:
AGE: 
AGE_RANGE: 
FITNESS_GOAL: 
GENDER: 
LOCATION: 
LOYALTY_STATUS: 
MEMBERSHIP_PLAN: 
MEMBERSHIP_PRICE: 
PERSONAL_TRAINING_USAGE: 
PREFERRED_WORKOUT_TYPE: 
SIGNUP_DATE: 
USER_ID: 
VISIT_FREQUENCY: 
	1.	Sum the exact likelihood ratios for each matching trait.
	2.	Identify the top matching trait from the list based on the highest likelihood ratio.

Then output only the following:
	•	Upsell Score: one word: High, Medium, or Low
	•	Top Trait: the name of the top matching trait. The complete list is:
	1.	Visit Frequency
	2.	Personal Training Usage
	3.	Loyalty Status
	4.	Gender
	5.	Fitness Goal
	6.	Age Range
	7.	Location

Output format:

Upsell Score: [High/Medium/Low]  
Top Trait: [Top_Trait_Name] 

        

```
{% endcode %}



</details>



### Enrich and Enhance Records

<details>

<summary>Enrich and enhance account recommendations in Salesforce</summary>

{% code overflow="wrap" %}
````
If the {{ record['DOMAIN_PAGE_DETAILS_JSON'] }} equals "Not enough activity to provide a summary," display the following message:  
**Not enough activity to provide a summary.**  

Otherwise, summarize the company's engagement and interest trends based on their web page interactions over the past 90 days.

```html
{{ record['DOMAIN_PAGE_DETAILS_JSON'] }}
```

Summarize the company's engagement using a conversational style with bullet points, focusing on the following prioritized pages and blog posts. If there are visits to non-prioritized pages (e.g., career, about) without visits to key pages, include them; otherwise, ignore. For customers with a `{{ record['SALES_STATUS'] }}` set to “Customer,” remember they are already paying for our product. It's still valuable to engage their team to explore potential future needs or improvements. For those marked as “Aware” or “Unaware,” they are in the early stages of the buying journey. Prospects with a `{{ record['SALES_STATUS'] }}` of “Ready to Engage” or “Engaged” are already in conversation with our sales team and likely evaluating specific solutions.

We also have `{{ record['INDUSTRY'] }}` for context. The higher the `{{ record['HEX_FIT_SCORE'] }}`, the more we want to pursue them, so prioritize accordingly.

Prioritized Pages:
- `/pricing`
- `/integrations`
- `/customers`
- `/dbt`
- `/product`
- `/destinations`
- `/segments`
- `/audiencehub`
- `/embedded`
- `/real-time-live-syncs`
- `/datasets`
- `/solutions`
- `/security`
- `/what-is-reverse-etl`
- `/compare/census-vs-hightouch`

Prioritized Blog Posts:
- `/blog/4-ways-to-export-csv-files-from-databricks`
- `/blog/introducing-the-universal-data-platform`
- `/blog/3-ways-to-export-csv-files-from-snowflake-and-one-better-idea`
- `/blog/4-ways-to-export-csv-files-from-redshift`
- `/blog/how-to-hack-it-extracting-data-from-google-bigquery-with-python-2`
- `/blog/toward-a-universal-data-platform`
- `/blog/3-ways-to-export-csv-files-from-google-bigquery`
- `/blog/data-teams-embrace-the-data-warehouse-turn-it-into-a-composable-cdp`
- `/blog/retail-brands-realtime-data-for-revenue`
- `/blog/implementing-entity-resolution-with-python-record-linkage`
- `/blog/connect-python-with-snowflake`
- `/blog/how-to-move-data-from-snowflake-to-salesforce`
- `/blog/a-complete-guide-to-revenue-cohort-analysis`
- `/blog/how-to-unload-data-from-snowflake`
- `/blog/census-live-syncs-on-snowflake`
- `/blog/what-is-master-data-management-master`
- `/blog/send-data-from-bigquery-to-slack`
- `/blog/computed-columns-last-mile-data-transformation`
- `/blog/your-complete-guide-to-redshift-unload`
- `/blog/realtime-reverse-etl-for-google-bigquery`

The following JSON includes fields that provide further insights into each page view:

1. ai_potential_questions:
    - Lists potential user questions about methods, processes, features, or comparisons after reading the content.

2. customer_journey_stage:
    - Indicates where the customer is in their decision-making journey, such as “Think” or “Consider.”

3. key_insights:
    - Summarizes key takeaways or advantages, such as product benefits like scalability, security, or efficiency.

4. persona_classification:
    - Identifies the target audience (e.g., “Data Persona” or “Both”), reflecting the content's relevance to different user types.

5. reader_intent:
    - Highlights what the reader aims to understand, like learning processes, evaluating pricing, or exploring features.

6. summary_text:
    - Provides a concise article summary, outlining key points, benefits, and how it solves relevant challenges.

Use the information from the provided JSON:

```
{{ record['DOMAIN_PAGE_DETAILS_JSON'] }}
```

---

Structure:

1. Overview of Last 90 Days:
    - Summarize the company's web activity over the last 90 days, focusing on the prioritized pages and blog posts.
    - Highlight key areas of interest such as product features, pricing, integrations, and comparisons.

2. Buying Signals & Potential Questions:
    - Identify buying signals suggesting the company is nearing a purchase decision or still evaluating options.
    - Include potential questions they might be asking based on their engagement with these key pages.

3. Page Engagement:
    - For each prioritized page or blog post visited, provide details about the content and its relevance:
        - Page Purpose: What does the page cover? (e.g., pricing, product features)
        - User's Interest: Why does this page matter to them? (e.g., cost evaluation, competitive comparison)

4. Suggested Next Steps:
    - Suggest personalized actions for the sales team, such as offering more resources, scheduling demos, or providing case studies.
    - Emphasize further engagement on the most visited pages like product features, pricing, or competitive comparisons.

---

Sample Output:

```html
<p><b>Overview of Last 90 Days:</b></p>
<ul>
    <li><b>Recent Activity:</b> The company has shown significant interest in pricing, integrations, and product features over the past 90 days.</li>
    <li>They visited multiple pages related to integrations with their existing tools and reviewed solutions for data syncing and audience segmentation.</li>
</ul>

<p><b>Buying Signals & Potential Questions:</b></p>
<ul>
    <li>🟢 The company appears to be in the "Consider" stage, as they've been reviewing product pages and pricing options multiple times.</li>
    <li>💡 Possible Questions: What integrations are available for their specific tech stack? What are the pricing options for large data syncs?</li>
</ul>

<p><b>Page Engagement:</b></p>
<ul>
    <li>💲 <b>Pricing Page:</b> The user spent time reviewing pricing tiers, likely assessing the cost for scaling their data operations.</li>
    <li>⚙️ <b>Integrations Page:</b> They explored integration capabilities with their existing systems, indicating interest in seamless data syncing solutions.</li>
    <li>💨 <b>Real-Time Sync Page:</b> The user reviewed content on real-time data syncing, signaling a focus on minimizing data latency.</li>
</ul>

<p><b>Suggested Next Steps:</b></p>
<ul>
    <li> 📅 Schedule a tailored demo showcasing how your solution can integrate with their tech stack and meet their real-time syncing needs.</li>
    <li>📧 Share detailed pricing options, emphasizing scalability for data-heavy operations, and provide relevant case studies from similar companies.</li>
</ul>

<p><b>Talking Points:</b></p>
<ul>
    <li>📊 The company has demonstrated a strong interest in scaling their data operations, particularly regarding real-time syncs and secure transformations.</li>
    <li>📰 Focus on discussing how Census has helped industry leaders like the New York Times efficiently handle large-scale data while ensuring security and operational efficiency.</li>
    <li>📈 Highlight Enterprise plan features, such as advanced transformation tools and data governance capabilities, that can meet their growing needs for scalability and agility.</li>
</ul>
```
```

- 30 days since last purchase, $10 LTV -> 30%
- 60 days since last purchase, $10 LTV -> 20%
- 30 days since last purchase, $250 LTV -> 20%
- 60 days since last purchase, $250 LTV -> 10%

Evaluate the formula for this customer:

Customer's Lifetime Value (LTV): {{ record['CUSTOMER_LTV']}}
Days since last purchase: {{ record['DAYS_SINCE_LAST_PURCHASE']}}

````
{% endcode %}

</details>

<details>

<summary>Create personalized discount based on customer's LTV</summary>

We will use customer's life time value as an input column. If you don't have LTV yet in your dataset, you can easily calculate that for each user using [Computed Columns](../computed-columns.md).&#x20;

You can also use [Computed Columns](../computed-columns.md) to calculate days since last purchase.

{% code overflow="wrap" %}
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
{% endcode %}

</details>

<details>

<summary>Create Personalized emails based on account info</summary>

{% code overflow="wrap" %}
```
The data activation company Census links its customer case studies on this page. https://www.getcensus.com/customers

I'd like you to help me prepare a sales email to a prospect with job title {{record['ROLE']}} working at company {{record['COMPANY']}}. Your task is to:

1. Search {{record['COMPANY']}} on the web to identify what kind of company they are and what challenges they are facing. Then, search {{record['ROLE']}} on the web to understand what kinds of challenges that person may care about most.

2. Identify a case study from the Census case study page that best matches the challenges that are relevant to the person's role and company. If you can, use a case study from a person with the same role as the recipient.

3. Write me a brief, concise email that summarizes the selected case study and how it applies to the email recipient. A good email is:

-Concise, can be read in a minute or less
-Includes a link to a the specific case study being referenced
-Opens with a personalized greeting. You can use Marc Benioff, the Salesforce CEO, as an example.
-Focuses on one specific challenge this person may have, rather than summarizing the whole product
-Includes 3 specific numbers and outcomes from the case study

4. Remember to keep your output brief and consider all of the instructions. Provide no explanation beyond the email text.

```
{% endcode %}

</details>

<details>

<summary>Add SIC codes and Industry labels to account records</summary>

{% code overflow="wrap" %}
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
{% endcode %}

Columns Needed: Company name, shown here as COMPANY.  The data could be improved by including a URL to the company website, but this is not necessary.

Best Response type: String

</details>

### Data Cleanup

<details>

<summary>Standardize email field values</summary>

{% code overflow="wrap" %}
```
For the following field, return a single value as an email address. Remove all unwanted text. If the field does not have any email address, return empty string.
Field: {{ record['USER_EMAIL']}}

You will not provide any explanation or description. 
```
{% endcode %}

</details>

<details>

<summary>Clean up leading and trailing spaces</summary>

{% code overflow="wrap" %}
```
For the following field, return the text with leading and trailing spaces removed. Don't remove space in-between words.
Field: {{ record['TEXT_FIELD']}}

You will not provide any explanation or description. 
```
{% endcode %}

</details>

<details>

<summary>Remove Special Characters from a name</summary>

{% code overflow="wrap" %}
```
For the following name field, return the name with special characters and numeric digits removed
Name Field: {{ record['CUSTOMER_NAME']}}
```
{% endcode %}

</details>

<details>

<summary>Translate text</summary>

{% code overflow="wrap" %}
```
Your task is to determine the reasons behind our five star reviews.

1. Translate the text in {{record['REVIEW']}} into English
```
{% endcode %}

</details>

<details>

<summary>Review a Translation for Quality</summary>

{% code overflow="wrap" %}
```
You will be given a review in a non-english language and an AI-generated translation of that review. Your task is to determine the quality of the translation.
1. First, consider the original review in {{record['REVIEW']}}. Consider both the meaning of the individual words and the meanings of the sentences as a whole.
2. Consider the translation in {{record['REVIEWS_ENGLISH']}}. Check the translation for accuracy.
3. Consider the slang or vernacular expressions of the region in which the original language is spoken. Ensure that there are no potential double meanings or slang expressions being misunderstood.
4. Output a confidence score for the translation based on the accuracy of the translation and the presence of potential double meanings or slang expressions. The confidence score should be a numerical value 1-5, with 1 meaning low confidence and 5 indicating high confidence.
5. Return your answer in the format:
[Confidence Score], [Explanation]
```
{% endcode %}

</details>

<details>

<summary>Standardize mailing addresses</summary>

{% code overflow="wrap" %}
```
For the following address field, return the outcome in an standardized US address format. 
Address Field: {{ record['USER_ADDRESS']}}.
```
{% endcode %}

</details>

<details>

<summary>Enforce Enum format to analyze data cleanly</summary>

{% code overflow="wrap" %}
```
Your task is to sort data into categories.
1. Consider the data in {{record['INDUSTRIES_GPT']}}
2. For each record, determine whether each response falls into the category of:
-Physical product
-Digital Product
-Services
-Other

Sort each row into its closest match. Return only one response for each row, and return only categories that exactly match those listed above.
```
{% endcode %}

</details>

