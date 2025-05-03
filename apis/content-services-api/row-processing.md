---
description: >-
  This page lists and describes the Row Processing category of endpoints within
  the Content Services API.  It also includes interactive testing environments
  for each endpoint in this category.
---

# Row Processing

## Merge <a href="#merge" id="merge"></a>

The `merge` method allows you to update a row across multiple templates. Specifically, it enables the host application to modify an element within an existing JSON document. This means you can implement a feature that updates templates in the background—without requiring any action from your users. It's ideal for merging shared content ([saved rows](../../rows/reusable-content/create/save/)) into templates that use it—for example, updating the same footer across 30 different email or page templates.

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
[Broken link](broken-reference)
{% endopenapi-operation %}
