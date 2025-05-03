---
description: >-
  This page lists and describes the AI Collection category of endpoints within
  the Content Services API. It also includes interactive testing environments
  for each endpoint in this category.
---

# AI Collection

## AI Collection

The resources in the AI collection accept your template JSON and use generative AI to return text within a JSON object to you.

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

Prior to getting started with the resources in this collection, ensure you have the following:

* **Superpowers** subscription or higher.
* An [AI Provider](../../builder-addons/addons/partner-addons/ai-writing-assistant/available-providers/) configured within the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
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
