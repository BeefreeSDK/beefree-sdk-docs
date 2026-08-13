---
description: >-
  This page lists and describes the AI Collection category of endpoints within
  the Content Services API. It also includes interactive testing environments
  for each endpoint in this category.
---

# AI Collection

{% hint style="info" %}
AI Collection endpoints are part of the [Content Services API](./). The Content Services API is available on [Beefree SDK plans that are Essentials or above](https://developers.beefree.io/pricing-plans).
{% endhint %}

## Overview

The resources in the AI collection accept your template JSON and use generative AI to return text within a JSON object to you.

{% hint style="info" %}
**Important:** `collection` is a placeholder within the URL. This placeholder can be replaces with any of the `collection` options available for the AI Collection resource. Reference the [AI Collection Resource and Collection Options table ](./#ai-collection)for a list of available option.
{% endhint %}

### Available Collection Value for AI Endpoints

The following table lists the collection values available in this category of endpoints, and their corresponding collection options.

{% hint style="info" %}
**Note:** The only collection value available for this category of endpoints is **ai**. Therefore, all **{collection}** placeholders in the URL in this category should be replaced with **ai**.
{% endhint %}

Prior to referencing the table, the following example shows how you can replace the **{collection}** placeholder with **ai**.

#### How to Replace the {collection} Placeholder

The following example URL has a **{collection}** placeholder. This placeholder needs to be filled in with a **Collection Option** prior to making an API call.

`https://api.getbee.io/v1/{collection}/sms`

As an example, if you'd like to generate SMS text using this endpoint, replace **{collection}** with **ai**.

The final URL to make the API call will be:

`https://api.getbee.io/v1/ai/sms`

The following table provides a comprehensive reference of all available options based on what you'd like to generate.

| Resource    | Collection Options                 |
| ----------- | ---------------------------------- |
| `/sms`      | <ul><li><code>/ai</code></li></ul> |
| `/metadata` | <ul><li><code>/ai</code></li></ul> |
| `/summary`  | <ul><li><code>/ai</code></li></ul> |

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

Prior to getting started with the resources in this collection, ensure you have the following:

* **Superpowers** subscription or higher.
* An [AI Provider](../../ai-and-mcp/ai-addons/ai-writing-assistant/available-providers/) configured within the [Beefree SDK Developer Console](https://developers.beefree.io/login?from=website_menu).
* Content Services **API key.**

{% hint style="info" %}
**Note:** Charges from your AI Provider are separate from those from Beefree SDK.
{% endhint %}

### Metadata (Preheader and Subject) <a href="#metadata" id="metadata"></a>

`v1/ai/metadata`

{% openapi src="../../.gitbook/assets/metadata_endpoint.yaml" path="/v1/{collection}/metadata" method="post" %}
[metadata_endpoint.yaml](../../.gitbook/assets/metadata_endpoint.yaml)
{% endopenapi %}

### SMS <a href="#sms" id="sms"></a>

`v1/ai/sms`

{% openapi src="../../.gitbook/assets/sms_endpoint.yaml" path="/v1/{collection}/sms" method="post" %}
[sms_endpoint.yaml](../../.gitbook/assets/sms_endpoint.yaml)
{% endopenapi %}

### Summary

`v1/ai/summary`

{% openapi src="../../.gitbook/assets/summary_endpoint.yaml" path="/v1/{collection}/summary" method="post" %}
[summary_endpoint.yaml](../../.gitbook/assets/summary_endpoint.yaml)
{% endopenapi %}
