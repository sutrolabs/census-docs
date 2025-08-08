---
description: >-
  Census can work with all leading AI Foundation Model Providers using your
  credentials giving you controls over how your data is shared.
---

# AI Model Integrations

Census supports several features that leverage Large Language Models to make it easier to define data.&#x20;

* [Dataset SQL Generation](../datasets/overview/mesh-datasets.md) helps users create SQL to shape and transform their data&#x20;
* [AI Columns](../datasets/smart-columns/ai-columns/) make it easy to quickly create new columns on existing datasets by applying a prompt to every row of a dataset automatically.

In both cases, customers can provide an API key from one of several model providers, as well as select the specific model to choose the appropriate cost/intelligence tradeoff.&#x20;

Customers without an API key have access to a small amount of AI credits to try out a new model. Every Census organization has a fixed amount of AI Credits, so once you've used yours, you'll need to add an API Key for the service.

| Service       | API Key Access                                                         | Terms of Service                                                                                                                          |
| ------------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Anthropic     | [console.anthropic.com](https://console.anthropic.com/)                | [Commercial Terms of Service](https://www.anthropic.com/legal/commercial-terms)                                                           |
| Google Gemini | [Google Cloud Platform](https://ai.google.dev/gemini-api/docs/api-key) | [Gemini Terms of Service](https://ai.google.dev/gemini-api/terms)                                                                         |
| OpenAI        | [platform.openai.com](https://platform.openai.com/api-keys)            | [OpenAI Services Agreement](https://openai.com/policies/services-agreement/) [Enterprise Privacy](https://openai.com/enterprise-privacy/) |

## Credits

Credits make it easy to explore exciting new transformation features like [AI Columns](../datasets/smart-columns/ai-columns/). Census offers free trial credits to eligible organizations.&#x20;

While using Credits, you don't need your own API key to connect to OpenAI or other LLM and Enrichment providers. If you run out of credits or would like to use your own account, you can bring your own API key.&#x20;

To monitor your Credits usage, log into Census and navigate to "Organization Home / Credits".

### Rates

Every Census sync that runs using AI or Enrichments will use up a fixed amount of credits based on the action and the number of records processed. To generate values with:

#### OpenAI

| Model             | Cost per record |
| ----------------- | --------------- |
| GPT-5             | 300             |
| GPT-5 Mini        | 60              |
| GPT-5 Nano        | 15              |
| GPT-4o            | 300             |
| GPT-4o mini       | 20              |

#### Anthropic

| Model             | Cost per record |
| ----------------- | --------------- |
| Claude 3.5 Sonnet | 500             |
| Claude 3.5 Haiku  | 150             |
| Claude 3 Opus     | 1,500           |

#### Google Gemini

| Model             | Cost per record |
| ----------------- | --------------- |
| Gemini 2.5 Pro    | 450             |
| Gemini 2.5 Flash  | 75              |
| Gemini 2.5 Flash-Lite | 15          |
| Gemini 2.0 Flash  | 20              |
| Gemini 1.5 Pro    | 150             |
| Gemini 1.5 Flash  | 10              |

Additional credits are not available for purchase; in order to continue using enrichments, you can provide your own API key.

## Use of Data

Census currently supports the following Foundation Model Providers. Each provider sets their own terms of service on how data passed to the provider is used. The specific terms that apply are determined by how your API key was generated. If you use Census's AI Credits, the above terms of service apply to the APIs provided through the AI Credits system.&#x20;

Census does not ever use your data for training and will not send your data to any of the above services unless you explicitly enable one of the associated features. See [Census's Terms and Conditions](https://www.getcensus.com/legal/terms-conditions) for more details.

## Disabling AI Features

If you'd prefer your organization not have access to any AI capabilities at all, [admins](security-and-privacy/role-based-access-controls.md) can disable AI capabilities completely in Organization Settings.

1. Go to [Organization Settings](https://app.getcensus.com/home/organization-settings) and click the **Organization Settings** tab
2. Uncheck the **AI Features** option.

This will disable and hide all AI Features within Census. It can only be re-enabled by another admin.

