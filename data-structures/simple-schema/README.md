---
description: Learn more about how to use Beefree SDK's simple schema for AI-driven design.
---

# Simple Schema

{% hint style="info" %}
**Simple Schema Features by Plan Type:**

* **Superpowers & Enterprise Plans:** Access to Simple Schema for [Custom AddOns](./#custom-addons) and [Custom Rows](../../rows/reusable-content/create/pre-build/implement-custom-rows.md).
* **All Paid Plans:** Access the [Simple Schema API](../../apis/content-services-api/convert.md#simple-to-full-json) through the [Content Services API](../../apis/content-services-api/) (CSAPI).
{% endhint %}

## Overview

Beefree JSON is the JSON schema used to structure and validate designs within Beefree SDK. It is comprehensive and precise, which makes it powerful inside the visual builder, but that same complexity makes it difficult to work with programmatically, outside of it.

Simple Schema is a lightweight alternative designed for exactly that: assembling templates and content blocks from code, without opening the visual editor. It is easier to validate and maps directly to Beefree-native JSON through the Content Services API.

As a deterministic format, Simple Schema is well-suited for content that follows defined rules: branded components, localized footers, reusable rows, and any structure that needs to be generated consistently at scale. Templates assembled via Simple Schema can be instantly converted to native Beefree JSON and loaded into the builder for end users to edit in a no-code environment.

You can convert the simple schema into native Beefree JSON using the [Content Services API endpoint](../../apis/content-services-api/convert.md) `/v1/conversion/simple-to-full-json`.

Simple Schema also enhances [Custom AddOns development](../../builder-addons/custom-addons/) by:

* Providing a comprehensive set of properties for full flexibility in your design.
* Consolidating the Custom Rows, Single Content AddOn, and Row Mixed schemas into a unified, compatible schema type.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

## Simple Unified Schema

There are two ways you can use the schemas available in the documentation and the GitHub repository to implement Simple Schema.

These approaches are:

* Use the [Simple Unified Schema](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/blob/main/simple_unified.schema.json). This option allows you to use one reference file to structure your templates and validate them prior to sending them to the endpoint. Learn more about the Simple Unified Schema in the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/blob/main/simple_unified.schema.json).&#x20;
* Use the individual, but connected, simple schemas for templates, rows, columns, and modules. This option allows you to use multiple focused schema files to structure your templates and validate them prior to sending them to the endpoint. These schemas are detailed in the [subsequent pages](template-schema.md).&#x20;

## Webinar

The following webinar includes an in-depth exploration of [Simple Schema](https://github.com/BeefreeSDK/beefree-sdk-simple-schema), the `/simple-to-full-json` API endpoint, and covers two example scenarios and applications of Simple Schema.

{% embed url="https://www.youtube.com/watch?v=DEpQERhWV9E" %}

## API Endpoints: convert simple schema to full JSON (or the other way around)

You can convert Simple Schema into fully functional Beefree native JSON using the following endpoint:

```
POST /v1/conversion/simple-to-full-json
```

Or you can use the following endpoint to turn an existing Beefree design (Full JSON) into the Simple Schema:

```
POST /v1/conversion/full-to-simple-json
```

These endpoints are essential for building programmatic template workflows, where templates are generated, assembled, or adjusted from code — via configuration files, data pipelines, or external systems — and then converted for use inside the builder.

Visit the [Content Services API Simple to Full JSON](https://docs.beefree.io/beefree-sdk/apis/content-services-api/convert#post-v1-collection-simple-to-full-json) and Full to Simple documentation to learn more about how to use these endpoints.

{% hint style="warning" %}
**Tip:** Reference an [example valid request body in the GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/blob/main/example_valid_request.json) to experiment with the API endpoint and see it in action.
{% endhint %}

## Use cases

The following section lists several ways you can leverage Simple Schema to bring additional value to your end users.

#### Programmatic content generation

Simple Schema works great for deterministic, rule-based content generation. It can assemble templates and content blocks from code, based on data and logic your application controls, without opening the visual editor.

This is the right approach when the output needs to be consistent and predictable: branded footers, localized headers, reusable row components, or any structure that follows defined rules rather than requiring creative interpretation. Because no AI inference is involved in this workflow, it also scales efficiently, without per-generation token costs.

A practical example: a fitness platform serving multiple gym locations could use Simple Schema to generate email footers automatically, each one pulling the correct address, phone number, and logo variant based on geography. The logic lives in your application; Simple Schema provides the structure that converts directly to Beefree-native JSON.

The general workflow on the backend is:

1. Your application generates a Simple Schema document based on your data and rules.
2. You pass the schema to `/v1/conversion/simple-to-full-json`.
3. You receive Beefree native JSON, ready to load into the Beefree SDK builder.

This lets you build and manage templates entirely outside the visual editor, and surface the result inside Beefree SDK whenever end users need to edit it.

#### A/B testing and variations

Use schema generation logic to produce slightly varied layouts for testing. Apply custom logic to automatically create multiple template variants and validate each one against your defined schema before conversion.

#### Custom validation workflows

Enforce validation rules that check your schema structure or inputs to meet your unique business or design standards.

#### Backend template workflows

Simple Schema lets you build and manage complete email, page, and popup templates from your own application, without the visual editor involved at any stage. Use it for programmatic campaigns, content pipelines, template marketplaces, or internal automation systems where templates are assembled from data and rules rather than designed manually.

## Custom AddOns

Simple Schema enhances the development experience for Custom AddOns by integrating new properties that foster an additional layer of customization.

**Developer notes:**

* All AddOn content types now rely on Simple Schema.
* The `locked` property is only enforced inside Row AddOns to avoid poor UX in single-content modules.
* Use the `text` field consistently for content across all textual modules.
* Default values will be applied if specific properties are omitted in the Simple JSON.

### Content Dialog handler behavior

To develop your own [Custom AddOn](/broken/pages/Bq7XDpt9x3HZnkEXrkRr), you need to utilize Beefree SDK's [Content Dialog](../../other-customizations/advanced-options/content-dialog.md) method. The following code snippet provides and example of how to utilize the Content Dialog for Custom AddOns with Simple Schema.

```json
{
  "contentDialogId": "addOnID",
  "value": {
    "blockStyle": {
      // Padding, hover styles, and other block-level styling
    }
  }
}
```

{% hint style="warning" %}
**Tip:** The structure in the code snippet supports consistent block-level styling globally.
{% endhint %}

## Custom Rows

Simple Schema provides a comprehensive set of properties for customizing and creating [Custom Rows](./#custom-rows).

## Which schema should you use?

| Scenario                   | Schema(s) to Use                                                                         |
| -------------------------- | ---------------------------------------------------------------------------------------- |
| **Client-side validation** | Any individual module schema (`simple_button`, `simple_list`, etc.)                      |
| **Saving a full template** | `simple_template.schema.json` (including `rows`, `columns`, and `modules`)               |
| **API endpoint schema**    | Request body can directly use `simple_template`                                          |
| **Database modeling**      | Use nested object structure defined in `simple_template`, with shared fields via `$ref`s |

## Schema validation

The following code snippet provides an example of custom Simple Schema fields for merge tag support, and custom validations.

```ts
urlOrMergeTagsOrEmpty: (text: string): boolean => {
      try {
        if (text === '') {
          return true
        }
        new URL(text)
        return true
      } catch (e) {
        return /{{.*}}/.test(text)
      }
    },
```

These validators ensure generated content is correct and aligns with the data structure defined within the Simple Schema.
