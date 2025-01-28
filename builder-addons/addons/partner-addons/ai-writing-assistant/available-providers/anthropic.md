---
description: >-
  Learn how to configure Anthropic as a provider for the AI Writing Assistant
  AddOn.
---

# Anthropic

{% hint style="info" %}
The AI Writing Assistant AddOn is only available for [Superpowers](https://developers.beefree.io/pricing-plans) and [Enterprise](https://developers.beefree.io/pricing-plans) plans. The AI Writing Assistant and Anthropic provider are available for Email, Page, and Popup builders.
{% endhint %}

{% hint style="danger" %}
**Important:** The AI collection is currently experiencing compatibility issues with the Manage Providers feature. We are aware of the issue and actively working to resolve it. In the meantime, the endpoints in the AI collection may not work as expected. &#x20;
{% endhint %}

## Overview

This page discusses how to configure Anthropic as a provider for the [AI Writing Assistant AddOn](../) within the Beefree SDK Developer Console. If the AI Writing Assistant AddOn is already enabled for your application, and you'd like to switch providers, take the steps outlined in the [Switch Providers](../#switch-providers) section of the [AI Writing Assistant page](../#switch-providers) to enable Anthropic as your new provider.&#x20;

### Prerequisites

Prior to getting started, ensure you have the following:

* A [Superpowers or Enterprise Beefree SDK plan](https://developers.beefree.io/pricing-plans)
* The AI Writing Assistant AddOn enabled in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
* An API Key for [Anthropic](https://www.anthropic.com/)&#x20;
  * **Note:** Refer to [Anthropic’s documentation](https://www.anthropic.com/) for instructions on creating an account and generating your API key.

### Configuration Steps

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

\*Reference the [Required Provider Information](../#required-provider-information) section of the [AI Writing Assistant AddOn page](../) to reference what information is required to configure Anthropic as a provider.

### Shared Logic Considerations

Consider the following shared logic when integrating the AI Writing Assistant AddOn and Anthropic as a provider:

* **Methods:** The methods used for the Anthropic provider are inherited from the [AI Writing Assistant AddOn](../). These include functionality for generating content for supported block types (Title, Paragraph, List, Button) and for handling metadata.
* **Events:** The integration supports all events from the [AI Writing Assistant](../), such as tracking user actions and processing content generation requests.
* **Callbacks:**  All callbacks associated with the Anthropic provider are inherited from the [AI Writing Assistant](../). They manage notifications for successful or failed content generation attempts.

### Additional Considerations

* **Billing**: Refer to Anthropic’s [pricing documentation](https://www.anthropic.com/pricing) for more information.
