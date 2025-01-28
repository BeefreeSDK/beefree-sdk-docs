---
description: >-
  Learn how to configure Azure OpenAI as a provider for the AI Writing Assistant
  AddOn.
---

# Azure OpenAI

{% hint style="info" %}
The AI Writing Assistant AddOn is only available for [Superpowers](https://developers.beefree.io/pricing-plans) and [Enterprise](https://developers.beefree.io/pricing-plans) plans. The AI Writing Assistant and Azure OpenAI provider are available for Email, Page, and Popup builders.
{% endhint %}

{% hint style="warning" %}
**Important:** The [AI collection](../../../../../apis/content-services-api/content-services-api-reference.md#ai-collection) is only compatible with OpenAI AddOns that were configured before August 1, 2024. We are actively working on making it compatible with AI AddOns and Providers configured after that date, too.&#x20;
{% endhint %}

## **Overview**

This page discusses how to configure Azure OpenAI as a provider for the [AI Writing Assistant AddOn](../) within the Beefree SDK Developer Console. If the AI Writing Assistant AddOn is already enabled for your application, and you'd like to switch providers, take the steps outlined in the [Switch Providers](../#switch-providers) section of the [AI Writing Assistant page](../#switch-providers) to enable Azure OpenAI as your new provider.&#x20;

## **Prerequisites**

Prior to getting started, ensure you have the following:

* Beefree SDK [Superpowers or Enterprise plan](https://app.gitbook.com/s/svPtAq2FGbWqZBP0UXk1/).
* An Azure OpenAI account, API Key, URL Provider, and Deployment ID.
* The AI Writing Assistant AddOn enabled in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).

## **Configuration Steps**

Take the following steps to configure this provider:

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application with the AI Writing Assistant enabled.
   1. Click **Details**.
3. Navigate to the **AddOns** under **Application configuration** section.
   1. Click **View more**.
4. Click the **Manage Providers** tab.
5. Click **Add provider**.
6. Complete the required information.\*
7. Click **Save** to save your provider configuration.

\*Reference the [Required Provider Information](../#required-provider-information) section of the [AI Writing Assistant AddOn page](../) to reference what information is required to configure Azure OpenAI as a provider.

### Shared Logic Considerations

Consider the following shared logic when integrating the AI Writing Assistant AddOn and Azure OpenAI as a provider:

* **Methods:** The methods used for the Azure OpenAI provider are inherited from the [AI Writing Assistant AddOn](../). These include functionality for generating content for supported block types (Title, Paragraph, List, Button) and for handling metadata.
* **Events:** The integration supports all events from the [AI Writing Assistant](../), such as tracking user actions and processing content generation requests.
* **Callbacks:**  All callbacks associated with the Azure OpenAI provider are inherited from the [AI Writing Assistant](../). They manage notifications for successful or failed content generation attempts.

### Additional Considerations

* **Billing**: Refer to [Azure OpenAI's pricing documentation](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/openai-service/) for more information.
