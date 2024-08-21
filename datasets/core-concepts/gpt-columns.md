# GPT Columns

GPT Columns enable you to dynamically generate unique content for each row in your dataset using OpenAI's GPT models. With GPT Columns, you can define a prompt and use [liquid templating](../../basics/core-concept/liquid-templates.md) to reference values from other columns. This setup allows you to send a customized GPT prompt request for each row, with the response automatically written back to your GPT Column.

#### Example Use Cases

1. Automatically generate personalized email content or messages based on customer data.
2. Generate insights or recommendations from transactional data, such as suggesting complementary products based on purchase history.
3. Sentiment analysis of email received by sales team from outbound campaign to help with categorization and reporting
4. Summarize product usage among specific features by “high” or “low” to identify upsell fits and run PLG playbooks
5. Clean up data by removing special characters from a column

#### Pre-requisites

*   Add OpenAI (ChatGPT) as a destination

    * You will need your API key to connect OpenAI (ChatGPT). To create a  new API key, log into OpenAI and navigate to [Dashboard / API keys](https://platform.openai.com/api-keys) and generate a new Project API Key.



    <figure><img src="../../.gitbook/assets/Screenshot 2024-08-20 at 8.45.36 PM.png" alt=""><figcaption></figcaption></figure>

#### How to create a GPT Column

**Step 1:** [Log into](https://app.getcensus.com/) your Census account.

**Step 2:** Navigate to the Datasets tab  by clicking on `Datasets` in the left navigation panel.

**Step 3:** Choose a dataset where you want to add a new AI-based column.

**Step 4:** Select `Computed Columns` on your right and choose `GPT Columns`

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-20 at 8.47.44 PM.png" alt=""><figcaption><p>Census Create GPT Column</p></figcaption></figure>

**Step 5:** Create a GPT prompt and fill the column name.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-20 at 8.50.33 PM.png" alt=""><figcaption><p>Census GPT Column Prompt</p></figcaption></figure>

We recommend you refine your prompt outside Census before saving the prompt for the GPT Columns.

* Model Type - you can select from the provided list of GPT based models or manually enter a valid model. [Here's a full list](https://platform.openai.com/docs/models/gpt-4-turbo-and-gpt-4) of GPT models. We recommend `gpt-4o-mini` model to limit cost associated with the OpenAI tokens.
* The expected output type - there are several optional properties to help you guarantee data quality.
* The prompt to run against each row of your data. Your prompt can leverage [Liquid templating](../../basics/core-concept/liquid-templates.md) to reference column values.&#x20;

**Step 6:** Hit the Create button and that's it. Census will generate a GPT based column into your dataset.&#x20;



The GPT columns refresh every 6 hours and only process new rows. The columns get written back to your data warehouse.&#x20;



{% hint style="info" %}
GPT Columns are currently supported on Snowflake, Redshift, BigQuery, and Postgres with more warehouses coming soon.
{% endhint %}

