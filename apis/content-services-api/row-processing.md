---
description: >-
  This page lists and describes the Row Processing category of endpoints within
  the Content Services API.  It also includes interactive testing environments
  for each endpoint in this category.
---

# Row Processing

{% hint style="info" %}
Row Processing endpoints are part of the [Content Services API](./). The Content Services API is available on [Beefree SDK plans that are Essentials or above](https://developers.beefree.io/pricing-plans).
{% endhint %}

## Overview

The Rows endpoints help you keep templates consistent and avoid redundancy. Use them to list [saved rows](../../rows/reusable-content/create/save/), apply updates across multiple templates, or retrieve [synced rows](row-processing.md#merge-2).

### Available Collection Values for Row Processing Endpoints

The following table lists the collection values available in this category of endpoints, and their corresponding collection options.

Prior to referencing the table, the following example shows how you can replace the **{collection}** placeholder.

#### How to Replace the {collection} Placeholder

The following example URL has a **{collection}** placeholder. This placeholder needs to be filled in with a **Collection Option** prior to making an API call.

`https://api.getbee.io/v1/{collection}/merge-rows`

As an example, if you'd like to merge rows for emails using this endpoint, replace **{collection}** with **message**.

The final URL to make the API call will be:

`https://api.getbee.io/v1/message/merge-rows`

The following table provides a comprehensive reference of all available options.

| Resource       | Collection Options                                                          |
| -------------- | --------------------------------------------------------------------------- |
| `/merge`       | <ul><li><code>/message</code></li><li><code>/page</code></li></ul>          |
| `/merge-rows`  | <ul><li><code>/message</code></li></ul><ul><li><code>/page</code></li></ul> |
| `/synced-rows` | <ul><li><code>/message</code></li></ul><ul><li><code>/page</code></li></ul> |
| `/merge-index` | <ul><li><code>/message</code></li></ul><ul><li><code>/page</code></li></ul> |

## Merge <a href="#merge" id="merge"></a>

The `merge` method allows you to update a row across multiple templates. Specifically, it enables the host application to modify an element within an existing JSON document. This means you can implement a feature that updates templates in the background—without requiring any action from your users. It's ideal for merging shared content ([saved rows](../../rows/reusable-content/create/save/)) into templates that use it—for example, updating the same footer across 30 different email or page templates.

{% hint style="info" %}
**Important:** `collection` is a placeholder within the URL. This placeholder can be replaces with any of the `collection` options available for the Row Processing resource. Reference the [Row Processing Resource and Collection Options table](./#row-processing) for a list of available option.
{% endhint %}

**URL:** `https://api.getbee.io/v1/{collection}/merge`

{% openapi src="../../.gitbook/assets/merge_endpoint.yaml" path="/v1/{collection}/merge" method="post" %}
[merge_endpoint.yaml](../../.gitbook/assets/merge_endpoint.yaml)
{% endopenapi %}

## Merge Rows <a href="#merge" id="merge"></a>

**URL:** `https://api.getbee.io/v1/{collection}/merge-rows`

{% openapi src="../../.gitbook/assets/merge_rows_endpoint.yaml" path="/v1/{collection}/merge-rows" method="post" %}
[merge_rows_endpoint.yaml](../../.gitbook/assets/merge_rows_endpoint.yaml)
{% endopenapi %}



{% hint style="info" %}
When utilizing this feature, it's important to consider adding a handle to the metadata. This handle serves a crucial role in functions such as `onDeleteRow` and `onEditRow`. In our provided example, we use a handle named `guid`. However, users have the flexibility to choose their own handle name according to their preferences and requirements. When selecting a handle name, we recommend you choose something descriptive and meaningful for ease of identification and management within your workflow.
{% endhint %}

## Synced Rows <a href="#merge" id="merge"></a>

**URL:** `https://api.getbee.io/v1/{collection}/synced-rows`

What if a footer is shared by 10 messages and needs to be updated in all of them? The [Synced Rows](../../rows/reusable-content/sync/implement-synced-rows.md) feature was created precisely to address the scenario of content that is shared across multiple emails, pages, or popups, and it is used in conjunction with the Content Services API.

{% openapi src="../../.gitbook/assets/synced_rows_endpoint.yaml" path="/v1/{collection}/synced-rows" method="post" %}
[synced_rows_endpoint.yaml](../../.gitbook/assets/synced_rows_endpoint.yaml)
{% endopenapi %}

## Index <a href="#index" id="index"></a>

The `index` method in the Content Services API lets you retrieve a list of assets that include a specific saved row. This method is essential for determining which assets need to be updated using the `merge` method.

**Typical Use Cases**

* Updating shared headers or footers across multiple templates
* Modifying expiration dates in seasonal campaigns
* Applying price or link changes to reused promotional content
* Making any update to shared blocks without manually editing each message

Use the `index` method first to locate all impacted assets, then apply changes with the `merge` method to ensure content is updated consistently.

{% openapi-operation spec="merge-index" path="/v1/{collection}/merge/index" method="post" %}
[OpenAPI merge-index](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/13a4ff91deb98730e0db8b67e6cac612032b9bc459f7474d1d3eaee5e5d0fa70.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250910%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250910T191642Z&X-Amz-Expires=172800&X-Amz-Signature=f99bf352cb731b4c26528a26df633613a4e63fd17913c7cb12278d9d6edfa0e9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
