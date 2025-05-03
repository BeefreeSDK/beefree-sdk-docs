---
description: Learn more about the Content Services API offering in Beefree SDK.
---

# Content Services API

{% hint style="info" %}
The Content Services API is available on Beefree SDK [paid plans](https://dam.beefree.io/pluginpricing) only.
{% endhint %}

## Beefree SDK API Offering <a href="#in-a-nutshell" id="in-a-nutshell"></a>

Beefree SDK includes a comprehensive API offering designed to expand upon the builder's capabilities. By leveraging Beefree SDK's APIs, you can extend the builder's functionality into other aspects of your application.

Beefree SDK's API offering includes three APIs. They are the following:&#x20;

* [Content Services API](./)
* [Template Catalog API](../template-catalog-api/)
* [HTML Importer API](../html-importer-api/)

This section of the documentation discusses the [Content Services API](./#overview-of-content-services-api), which includes resources for exporting, converting, processing, and styling templates within Beefree SDK. This collection of resources extends the functionality of the builder to offer your end users a complete content creation solution.

<figure><img src="../../.gitbook/assets/mermaid-diagram-BeefreeSDK-API-offering.png" alt="" width="375"><figcaption><p>Diagram Displaying Beefree SDK's API Offering</p></figcaption></figure>

## Overview of Content Services API

The Content Services API is a [REST](https://restfulapi.net/)-based API that enables Beefree SDK integrators to programmatically manipulate template JSON. It is built to follow predictable resource url patterns, and to utilize standard HTTP response codes and methods.    &#x20;

Beefree SDK requires that you [authenticate](authentication.md) prior to accessing the Content Services API's resources. You can generate API keys for both production and [development applications](../../getting-started/readme/development-applications.md). API keys associated with development applications are intended for pre-production environments and endpoint testing. They should not be used in production environments.

There are five categories of resources within the Content Services API. Each of these categories includes a group of endpoints with resources to support various workflows.&#x20;

These categories are the following:

* **Export**: Services that allow users to extract content into various formats (such as HTML, PDF, or image files), making it easy to repurpose or distribute designs across different platforms.
* **Convert**: Tools that transform content from one format to another (for example, converting template JSON to HTML ). This enables compatibility with different systems and workflows.
* **AI Collection**: AI-powered capabilities for text generation, such as creating metadata for emails, summarizing content, or creating SMS messages.
* **Row Processing**: Services that operate at the structural level, such as analyzing, modifying, or extracting specific rows or sections within a design for granular control over the content layout.
* **Brand Style**: Resources focused on enforcing or applying brand guidelines, including applying consistent colors, typography, and spacing rules to ensure brand integrity across all generated content.

The following diagram displays each of the five categories within the Content Services API, and their corresponding resources. &#x20;

<figure><img src="../../.gitbook/assets/mermaid-diagram-CSAPI (1).png" alt=""><figcaption><p>Content Services API Resource Categories and Functionality</p></figcaption></figure>

### Use Cases and Capabilities

This section provides a high level overview of the Content Services API's capabilities, and lists a few scenarios in which this API is particularly helpful.

#### **Export Different Formats**

One of the most common use cases for the Content Services API is exporting different format types. Once your end users complete their designs within the no-code builder, they'll want to export their designs and distribute them. That is where the [Export category](export.md) stands out. By using this category of endpoints, you can provide your end users with the option to export their no-code designs in HTML, plain text, PDF, or image formats.&#x20;

Your end users may want to export their templates into various formats in the following scenarios:

* **HTML:** For sending email campaigns, publishing landing pages, or embedding popups.
* **Plain Text:** For accessibility, compatibility with text-only email clients, improved deliverability, and compliance with communication regulations.
* **PDF:** For attaching designs to emails, SMS, WhatsApp, printing hard copies, or creating flyers, while preserving the design's layout.
* **Image:** For creating visual galleries, dashboards, social media posts, internal presentations, or campaign planning visuals.

#### **Convert Content**

Another common use case of the Content Services API is converting one format to another. The formats in the Convert category differ from those in the Export category, and serve a separate purpose. This category of endpoints is for creating designs and loading them within the builder.  &#x20;

These endpoints allow you to:

* **Page to Email**: Convert existing page templates into email templates. This saves your end users time by allowing them to use their favorite designs across multiple content channels.
* **Email to Page:** Convert existing email templates into page templates. This saves your end users time by allowing them to use their favorite designs across multiple content channels.
* **Simple to Full JSON**: Convert an [AI-generated Simple Schema](../../visual-builders/ai-driven-design-creation.md) into full Beefree JSON that can be loaded within the builder for your end users to edit.&#x20;

#### **AI Collection**

This category of endpoints requires that you configure an AI Provider within the [Beefree SDK Developer Console](../../builder-addons/addons/partner-addons/ai-writing-assistant/available-providers/). Through the integration with your AI Provider, these endpoints generate the following supporting details for your end users templates:

* **SMS**: Generates concise text versions (e.g., promotional SMS).
* **Metadata**: Generates subject lines and preheaders based on a template's content.
* **Summary**: Generate summaries based on a template's content.

#### **Row Processing**

These endpoints manage rows within templates to maintain consistency and reduce redundancy:

* **Index**: List saved rows available.
* **Merge**: Merge row updates across multiple templates. Particularly useful when applying global updates.
* **Synced Rows**: Retrieve a list of synced rows available.

#### **Brand Style Management**

Brand consistency can be enforced or retroactively applied across templates:

* **/templates and /rows** endpoints allow updating visual properties (colors, fonts, spacings, etc.) across multiple templates or rows based on defined brand styles.

## Base URL

All API access is over HTTPS, and accessed from the following URL:

```http
https://api.getbee.io/v1/{collection}/{resource}
```

You can reference each resource and its corresponding collection options in the following section.

### Collections by Category

The following tables list the available collection options for resources within the category.

#### Export

The following table lists the resources available in this category of endpoints and their corresponding collection options.

| Resource      | Collection Options                                                                                                       |
| ------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `/html`       | <ul><li><code>/message</code></li><li><code>/page</code></li><li><code>/popup</code></li><li><code>/amp</code></li></ul> |
| `/plain-text` | <ul><li><code>/message</code></li></ul>                                                                                  |
| `/pdf`        | <ul><li><code>/message</code></li></ul><ul><li><code>/page</code></li></ul>                                              |
| `/image`      | <ul><li><code>/message</code></li></ul><ul><li><code>/page</code></li></ul>                                              |

#### Convert

The following table lists the resources available in this category of endpoints and their corresponding collection options.

| Resource               | Collection Options                         |
| ---------------------- | ------------------------------------------ |
| `/page-to-email`       | <ul><li><code>/conversion</code></li></ul> |
| `/email-to-page`       | <ul><li><code>/conversion</code></li></ul> |
| `/simple-to-full-json` | <ul><li><code>/conversion</code></li></ul> |

#### AI Collection

The following table lists the resources available in this category of endpoints and their corresponding collection options.

| Resource    | Collection Options                 |
| ----------- | ---------------------------------- |
| `/sms`      | <ul><li><code>/ai</code></li></ul> |
| `/metadata` | <ul><li><code>/ai</code></li></ul> |
| `/summary`  | <ul><li><code>/ai</code></li></ul> |

#### Row Processing

The following table lists the resources available in this category of endpoints and their corresponding collection options.

| Resource       | Collection Options                                                          |
| -------------- | --------------------------------------------------------------------------- |
| `/merge`       | <ul><li><code>/message</code></li><li><code>/page</code></li></ul>          |
| `/merge-rows`  | <ul><li><code>/message</code></li></ul><ul><li><code>/page</code></li></ul> |
| `/synced-rows` | <ul><li><code>/message</code></li></ul><ul><li><code>/page</code></li></ul> |
| `/merge-index` | <ul><li><code>/message</code></li></ul><ul><li><code>/page</code></li></ul> |

#### Brand Style

The following table lists the resources available in this category of endpoints and their corresponding collection options.

| Resource | Collection Options                                                 |
| -------- | ------------------------------------------------------------------ |
| `/brand` | <ul><li><code>/template</code></li><li><code>/row</code></li></ul> |

#### Example URLs

The following table provides a few examples of URLs you can reference as an example for making specific types of requests.

<table><thead><tr><th width="160">Type</th><th>Action</th><th>Example URL</th></tr></thead><tbody><tr><td>Email</td><td>Request HTML for email</td><td><code>https://api.getbee.io/v1/message/html</code></td></tr><tr><td>Landing Page</td><td>Request HTML for a landing page</td><td><code>https://api.getbee.io/v1/page/html</code></td></tr><tr><td>Popup</td><td>Request HTML for a popup</td><td><code>https://api.getbee.io/v1/popup/html</code></td></tr><tr><td>AMP</td><td>Request HTML for AMP</td><td><code>https://api.getbee.io/v1/amp/html</code></td></tr></tbody></table>

## Rate Limits

API requests rate limits exist independently of API key’s monthly usage allowance.

By default, the API has the following rate limits:

* **Per minute:** 500 requests
* **Per second:**  100 requests
* **X-Rate-Limit:** An integer representing the total number of requests available per cycle. Exceeding the limit per cycle results in a 429 error.  (e.g. 500)
* **X-Rate-Limit-Remaining:** An integer representing the number of remaining requests before the next cycle begins, and the count resets. (e.g. 100)
* **X-Rate-Limit-Reset:** A Unix timestamp representing the time the next cycle will begin, and the count will reset.
* **Retry-After:** A Unix timestamp representing the time the application may resume submitting requests.

## FAQs <a href="#api-billing-why-we-are-charging-for-this-api" id="api-billing-why-we-are-charging-for-this-api"></a>

Reference the answers to the most frequently asked questions in this section.

### What is the pricing by plan type?&#x20;

The Content Services API allows you to carry out a number of useful tasks, like converting an email or a page into a thumbnail image or a PDF document, or updating a footer into all the emails that use it (for example, a [_saved row_](../../rows/reusable-content/create/save/implement-self-hosted-saved-rows/)).

These tasks consume resources in our Amazon Web Services environment, so we have to account for that. We did extensive research to define pricing that is consistent with other APIs.

Here is a quick summary:

| Plan        | Included API calls | Cost per extra API call |
| ----------- | ------------------ | ----------------------- |
| Essentials  | 15,000             | $0.01                   |
| Core        | 50,000             | $0.01                   |
| Superpowers | 250,000            | $0.003                  |
| Enterprise  | Custom             | Custom                  |

{% hint style="info" %}
**Note:** Overages to the allotted amounts for each Beefree SDK plan type are charged at the end of the billing period. For this reason, the first invoice after cancellation may include usage charges for the Content Services API. Reference the [Usage-based fees article](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) for more information.
{% endhint %}

### How will charges appear on my bill? <a href="#how-will-charges-appear-on-my-bill" id="how-will-charges-appear-on-my-bill"></a>

An additional charge, CSAPI, will be added to your current subscription plan invoice. When you activate the Content Services API, your billing statement will change, and you'll notice a new line item on your Beefree SDK invoice for the service.

### Can I use different payment methods for each app? <a href="#can-i-use-different-payment-methods-for-each-app" id="can-i-use-different-payment-methods-for-each-app"></a>

The Content Services API is provided as a component for your current subscription and the charges will be applied to the subscription payment method. Currently, there is no option to use an alternative payment method specific to these charges.

### How do you calculate request limits? <a href="#how-do-you-calculate-request-limits" id="how-do-you-calculate-request-limits"></a>

API requests rate limits exist independently of any API key’s monthly usage allowance.

The API has the following rate limits:

* **Per minute:** 500 requests
* **Per second:**  100 requests
