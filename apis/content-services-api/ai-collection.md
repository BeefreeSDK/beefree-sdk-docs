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

{% openapi-operation spec="metadata-endpoint" path="/v1/{collection}/metadata" method="post" %}
[OpenAPI metadata-endpoint](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/327db3f634df95f1ea2c4dc1475b0e19ae2ef3b25942401bea437fb1dd5d7079.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=6949830200cf8c4d704b1e4b8bcd1a92%2F20261104%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261104T141607Z&X-Amz-Expires=172800&X-Amz-Signature=a8d991c1f70dcf38d627cecd0489047f1a9a2dacf2f938b2a78588dd33f7b25d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

### SMS <a href="#sms" id="sms"></a>

`v1/ai/sms`

{% openapi-operation spec="sms-endpoint" path="/v1/{collection}/sms" method="post" %}
[OpenAPI sms-endpoint](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/5a0289796ed07080cd3aafa10b5299a2abe70c8a0096b2576a363cfaeef27c2e.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=6949830200cf8c4d704b1e4b8bcd1a92%2F20261104%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261104T141608Z&X-Amz-Expires=172800&X-Amz-Signature=6de18b7f78a1174cb7dce5abd8653cae756baeba78dac4e094da8d696ec34471&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

### Summary

`v1/ai/summary`

{% openapi-operation spec="summary-endpoint" path="/v1/{collection}/summary" method="post" %}
[OpenAPI summary-endpoint](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/44ee493c1cc9d159c976e053f8f0752e3e00d5df71525c0217641aca7e1ad084.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=6949830200cf8c4d704b1e4b8bcd1a92%2F20261104%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20261104T141608Z&X-Amz-Expires=172800&X-Amz-Signature=5d64d2979e823d77af202a431312b42f19c54edc001f4b34e8761b815234c3b6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
