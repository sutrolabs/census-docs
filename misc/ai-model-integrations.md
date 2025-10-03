---
description: >-
  Census can work with all leading AI Foundation Model Providers using your
  credentials giving you controls over how your data is shared.
---

# AI Model Integrations

Census supports several features that leverage Large Language Models to make it easier to define data.

* [Dataset SQL Generation](../datasets/overview/mesh-datasets.md) helps users create SQL to shape and transform their data
* [AI Columns](../datasets/smart-columns/ai-columns/) make it easy to quickly create new columns on existing datasets by applying a prompt to every row of a dataset automatically.

In both cases, customers can provide an API key from one of several model providers, as well as select the specific model to choose the appropriate cost/intelligence tradeoff.

| Service       | API Key Access                                                         | Terms of Service                                                                                                                          |
| ------------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Anthropic     | [console.anthropic.com](https://console.anthropic.com/)                | [Commercial Terms of Service](https://www.anthropic.com/legal/commercial-terms)                                                           |
| Google Gemini | [Google Cloud Platform](https://ai.google.dev/gemini-api/docs/api-key) | [Gemini Terms of Service](https://ai.google.dev/gemini-api/terms)                                                                         |
| OpenAI        | [platform.openai.com](https://platform.openai.com/api-keys)            | [OpenAI Services Agreement](https://openai.com/policies/services-agreement/) [Enterprise Privacy](https://openai.com/enterprise-privacy/) |

## Use of Data

Census currently supports the following Foundation Model Providers. Each provider sets their own terms of service on how data passed to the provider is used. The specific terms that apply are determined by how your API key was generated.

Census does not ever use your data for training and will not send your data to any of the above services unless you explicitly enable one of the associated features. See [Census's Terms and Conditions](https://www.getcensus.com/legal/terms-conditions) for more details.

## Disabling AI Features

If you'd prefer your organization not have access to any AI capabilities at all, [admins](security-and-privacy/role-based-access-controls.md) can disable AI capabilities completely in Organization Settings.

1. Go to [Organization Settings](https://app.getcensus.com/home/organization-settings) and click the **Organization Settings** tab
2. Uncheck the **AI Features** option.

This will disable and hide all AI Features within Census. It can only be re-enabled by another admin.
