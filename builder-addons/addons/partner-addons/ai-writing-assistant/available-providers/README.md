---
description: Learn more about available providers for the AI Writing Assistant AddOn.
---

# Available Providers

{% hint style="warning" %}
**Important:** The [AI collection](../../../../../apis/content-services-api/content-services-api-reference.md#ai-collection) is only compatible with OpenAI AddOns that were configured before August 1, 2024. We are actively working on making it compatible with AI AddOns and Providers configured after that date, too. &#x20;
{% endhint %}

## Overview

The [AI Writing Assistant AddOn](../) provides your application's end users with access to the the **Write with AI button** for text-based content blocks within the builder. When your end users click this button, a modal appears prompting them to submit a prompt to the AI Assistant. This is the portion of their journey that interacts with the provider that you configured within the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu). Beefree SDK offers a variety of providers as options for enabling the AI Writing Assistant AddOn for your application's end users. These providers each include their own set of benefits, and ultimately, the one you select for your configuration should be the provider with the set of benefits that most closely aligns with the goals you have for your application.

This page outlines and discusses each of the available provider options, and their corresponding set of benefits.

## Available Providers

This section discusses each of the available providers.

### OpenAI

[OpenAI](https://platform.openai.com/docs/concepts) is a versatile and widely recognized provider in the AI space. By integrating OpenAI into your application through the [AI Writing Assistant AddOn](../), your end users gain access to advanced generative text capabilities powered by GPT models. These models are known for their ability to create natural-sounding, coherent text across various use cases, such as marketing copy, email drafts, and creative writing. OpenAI's API also supports a high level of customization, allowing you to fine-tune the model's behavior to align with your application's goals.

#### **Benefits of using OpenAI:**

* Access to industry-leading GPT models for advanced text generation.
* Broad support for a variety of languages and writing styles.
* Extensive documentation and community resources to support implementation.
* Highly scalable infrastructure capable of handling large user bases.

### Azure OpenAI

[Azure OpenAI ](https://learn.microsoft.com/en-us/azure/ai-services/openai/)combines the power of OpenAI’s GPT models with Microsoft’s Azure cloud platform. This integration provides robust enterprise-level security, compliance, and availability while delivering powerful AI capabilities to your application's end users. With Azure OpenAI, you also benefit from seamless integration with other Microsoft services, making it ideal for organizations already using the Azure ecosystem.

#### **Benefits of using Azure OpenAI:**

* Enterprise-grade security and compliance standards, including regional data hosting options.
* Integration with other Azure tools and services for enhanced functionality.
* Flexible scaling to accommodate varying levels of user demand.
* Support for high-availability setups, ensuring consistent performance.

### Anthrophic

[Anthropic](https://docs.anthropic.com/en/docs/welcome) offers a unique approach to generative AI through its focus on safety and alignment in AI systems. Its Claude models prioritize creating helpful and ethical responses, making it an excellent option for applications where responsible AI use is a priority. Anthropic’s models are designed to work well with conversational and creative writing tasks, ensuring that your end users receive thoughtful and high-quality suggestions.

#### **Benefits of using Anthropic:**

* A strong emphasis on safety, ethical considerations, and AI alignment.
* Excellent for conversational use cases and creative writing needs.
* Simplified integration process with clear documentation and support.
* Scalable solutions that maintain consistency and reliability.

## Additional Considerations

If the list of providers detailed on this page do not need the requirements you have for your application, Beefree SDK also offers a [Custom AI Writing Assistant AddOn](../../custom-ai-writing-assistant.md) that allows you to connect your own custom LLM to the **Write with AI** button on your application's frontend. It also provides you with a mechanism to build a customized modal on the frontend of your application that your end users can interact with to submit their AI prompts to your custom LLM.&#x20;

## Other Resources

* Learn more about available settings to customize the [AI Writing Assistant AddOn](../).
* Learn more about how to enable the [AI Writing Assistant within the Developer Console](../#how-to-activate-the-ai-writing-assistant).
* Learn more about [AI Providers and Data Security](../data-security.md).
* Learn more about [Token Upselling](../token-upselling.md) and implementing a system for your end users to purchase more tokens to keep leveraging AI benefits within your application. &#x20;
