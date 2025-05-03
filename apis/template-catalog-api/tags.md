---
description: >-
  This page lists and describes the Tags category of endpoints within the
  Template Catalog API. It also includes interactive testing environments for
  each endpoint in this category.
---

# Tags

## Fetch a list of all Tags

`/v1/catalog/tags`

**HTTP Method:** `GET`

**Description:** Retrieve a full list of all the Tags in the catalog. Tags are keywords tied to templates, helping you find and sort templates based on certain themes or attributes.

### Request Parameters

The following table displays request parameters.

| Parameter  | Value | Description                  |
| ---------- | ----- | ---------------------------- |
| `pagesize` | int   | Set the item number per page |

{% openapi src="../../.gitbook/assets/catalog-tags.yaml" path="/v1/catalog/tags" method="get" %}
[catalog-tags.yaml](../../.gitbook/assets/catalog-tags.yaml)
{% endopenapi %}
