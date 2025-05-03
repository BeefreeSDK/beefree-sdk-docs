---
description: >-
  This page lists and describes the Designers category of endpoints within the
  Template Catalog API. It also includes interactive testing environments for
  each endpoint in this category.
---

# Designers

## Fetch a list of all Designers

`/v1/catalog/designers`

**HTTP Method:** `GET`

**Description:** Access a complete list of all Designers in the catalog.

The response is paginated, with a standard display of 200 items per page. You can manipulate the ‘pagesize’ request parameter to control the number of items shown per page.

### Request Parameters

The following table displays request parameters.

| Parameter  | Value | Description                  |
| ---------- | ----- | ---------------------------- |
| `pagesize` | int   | Set the item number per page |

{% openapi src="../../.gitbook/assets/catalog-designers.yaml" path="/v1/catalog/designers" method="get" %}
[catalog-designers.yaml](../../.gitbook/assets/catalog-designers.yaml)
{% endopenapi %}

## Fetch a single Designer

`/v1/catalog/designers/:slug`

**HTTP Method:** `GET`

**Description:** Retrieve detailed information for a specific Designer, identified by the unique slug present in the URL. This enables the procurement of comprehensive data pertaining to the particular designer, including their portfolio of templates and any associated metadata within the catalog.

{% openapi src="../../.gitbook/assets/catalog-designers-slug.yaml" path="/v1/designers/:slug" method="get" %}
[catalog-designers-slug.yaml](../../.gitbook/assets/catalog-designers-slug.yaml)
{% endopenapi %}
