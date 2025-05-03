---
description: >-
  This page lists and describes the Categories category of endpoints within the
  Template Catalog API. It also includes interactive testing environments for
  each endpoint in this category.
---

# Categories

## Fetch a list of all Categories

`/v1/catalog/categories`

**HTTP Method:** `GET`

**Description:** Retrieve a list of all the Templates within the catalog, applying filters based on request parameters.

You can extract a list of all the Categories present within the catalog. This comprehensive list includes all categories under which templates are classified.

The response that you receive is paginated for ease of reading and navigation. It displays 200 items per page by default, providing a comprehensive view of the catalog content.

However, if you wish to adjust the number of items shown on each page, you can use the ‘pagesize’ request parameter.

### Request Parameters

The following table displays request parameters.

| Parameter  | Value | Description                  |
| ---------- | ----- | ---------------------------- |
| `pagesize` | int   | Set the item number per page |

{% openapi src="../../.gitbook/assets/catalog-categories.yaml" path="/v1/catalog/categories" method="get" %}
[catalog-categories.yaml](../../.gitbook/assets/catalog-categories.yaml)
{% endopenapi %}

## Fetch a single Category

`/v1/catalog/categories/:slug`

**HTTP Method:** `GET`

**Description:** Retrieve a list of all the Templates within the catalog, applying filters based on request parameters.

Retrieve detailed information about a specific Category using its unique identifier, or slug, which can be found in the URL. This method allows you to access in-depth data related to that particular category, such as its associated templates and related metadata.

{% openapi src="../../.gitbook/assets/catalog-categories-slug.yaml" path="/v1/catalog/categories/:slug" method="get" %}
[catalog-categories-slug.yaml](../../.gitbook/assets/catalog-categories-slug.yaml)
{% endopenapi %}
