---
description: >-
  This page lists and describes the Collections category of endpoints within the
  Template Catalog API. It also includes interactive testing environments for
  each endpoint in this category.
---

# Collections

## Fetch a List of Collections

`/v1/catalog/collections`

**HTTP Method:** `GET`

**Description:** You can pull up a full list of all Collections in the catalog. Collections are groups of templates with similar attributes or purposes. This overview can help you understand the types of template groupings available.

The response will be paginated, with 200 items per page default for easy navigation. However, you can change this default by adjusting the ‘pagesize’ request parameter to suit your viewing preferences.

### Request Parameters

The following table displays request parameters.

| Parameter  | Value | Description                  |
| ---------- | ----- | ---------------------------- |
| `pagesize` | int   | Set the item number per page |

{% openapi src="../../.gitbook/assets/catalog-collections.yaml" path="/v1/catalog/collections" method="get" %}
[catalog-collections.yaml](../../.gitbook/assets/catalog-collections.yaml)
{% endopenapi %}

## Fetch a single Collection

`/v1/catalog/collections/:slug`

**HTTP Method:** `GET`

**Description:** Access a specific Collection using its unique slug found in the URL. This lets you view detailed information about this particular group of templates, including its associated templates and any related details.

{% openapi src="../../.gitbook/assets/catalog-collections-slug.yaml" path="/v1/catalog/collections/:slug" method="get" %}
[catalog-collections-slug.yaml](../../.gitbook/assets/catalog-collections-slug.yaml)
{% endopenapi %}

