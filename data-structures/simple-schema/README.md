---
description: Learn more about how to use Beefree SDK's simple schema for AI-driven design.
---

# Simple Schema

{% hint style="info" %}
Simple Schema is available on [Superpowers and Enterprise plans](https://developers.beefree.io/pricing-plans).
{% endhint %}

## Overview

Beefree JSON is the JSON schema we use to structure and validate designs within Beefree SDK. It's a very comprehensive and complex schema and for this reason, it does not provide the best structure for training AI models in workflows that include AI-driven design creation. Beefree SDK's Simple Schema is a lightweight alternative that's more accessible for AI engines (and humans).&#x20;

As a simpler model, Simple Schema is an intuitive language you can use as a baseline for training AI agents and building templates programmatically outside of Beefree SDK's visual builders. These headless templates can then be instantly transformed into Beefree’s native JSON and loaded inside the builder for end users to edit accordingly in a no-code environment.

You can convert the simple schema into native Beefree JSON using the [Content Services API endpoint](../../apis/content-services-api/content-services-api-reference.md#simple-to-full-json) `/v1/conversion/simple-to-full-json`.

Simple Schema also enhances [Custom AddOns development](../../builder-addons/addons/custom-addons/addon-development.md) by:

* Providing a comprehensive set of properties for full flexibility in your design.
* Consolidating the Custom Rows, Single Content AddOn, and Row Mixed schemas into a unified, compatible schema type.
* Enabling global updates—changes in one module apply across all modules.
* Improving how modules load on the stage.

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

## API Endpoint: Convert Simple Schema to Full JSON

You can convert Simple Schema into fully functional Beefree native JSON using the [following endpoint](../../apis/content-services-api/content-services-api-reference.md#simple-to-full-json):

```
POST /v1/conversion/simple-to-full-json
```

This endpoint is essential for building headless template workflows, where templates are generated or assembled programmatically—by AI models, config files, or external systems—and later converted for use inside the builder.

## Use Cases

The following section lists several ways you can leverage Simple Schema to bring additional value to your end users.

#### AI-Powered and Headless Template Creation

Build a chatbot or frontend tool where users describe what they want. An AI model creates a Simple Schema layout, which you convert to Beefree JSON using the API. Load the result into the builder—or send it directly into a campaign—without ever touching the editor during creation.

For example, your dev team can build a frontend that lets users describe their design (email, page, or popup), and submit that description to an AI agent on the frontend. On the backend:

1. The prompt is processed by an AI model trained to produce a template using Simple Schema.
2. You pass the schema to `/v1/conversion/simple-to-full-json`.
3. You receive Beefree native JSON, which is then loaded directly into the Beefree SDK builder.

This approach blends AI-driven design creation and your own custom user interface, which supports your end users in not starting their content creation workflow from scratch, but rather from an AI-generated design.

#### A/B Testing and Variations

Use schema generation logic to produce slightly varied layouts for testing. Combine this with AI or custom logic to automatically create multiple variants of templates.

#### Custom Validation Workflows

Enforce validation rules that check your schema structure or inputs to meet your unique business or design standards.

#### Fully Headless Workflows

Simple Schema lets you build and manage complete email, page, and popup templates without ever opening the visual builder. Use it for content generation, programmatic campaigns, template marketplaces, or internal automation systems.

## Custom AddOns

Simple Schema enhances the development experience for Custom AddOns by integrating new properties that foster an additional layer of customization.

**Developer Notes:**

* All AddOn content types now rely on Simple Schema.
* The `locked` property is only enforced inside Row AddOns to avoid poor UX in single-content modules.
* Use the `text` field consistently for content across all textual modules.
* Default values will be applied if specific properties are omitted in the Simple JSON.

### Content Dialog Handler Behavior

To develop your own [Custom AddOn](../../builder-addons/addons/custom-addons/addon-development.md), you need to utilize Beefree SDK's [Content Dialog](../../other-customizations/advanced-options/content-dialog.md) method. When `contentDialog.addon.handler` is triggered:

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

This structure supports consistent block-level styling globally.

## Custom Rows

Simple Schema provides a comprehensive set of properties for customizing and creating [Custom Rows](./#custom-rows).

## Simple Schema Relationships at a Glance

```plaintext
simple_template
  └── rows[] (simple_row)
         └── columns[] (simple_column)
                └── modules[] (discriminator on "type")
                        ├── simple_button
                        ├── simple_divider
                        ├── simple_image
                        ├── simple_html
                        ├── simple_list
                        ├── simple_menu
                        ├── simple_paragraph
                        ├── simple_title
                        └── [etc.]
```

* **`definitions.schema.json`** is referenced across almost all module and container schemas for styling props.
* **Modules are polymorphic**, distinguished by their `"type"` and validated using the `oneOf` structure in `simple_column`.

### Which Schema Should You Use?

| Scenario                   | Schema(s) to Use                                                                         |
| -------------------------- | ---------------------------------------------------------------------------------------- |
| **Client-side validation** | Any individual module schema (`simple_button`, `simple_list`, etc.)                      |
| **Saving a full template** | `simple_template.schema.json` (including `rows`, `columns`, and `modules`)               |
| **API endpoint schema**    | Request body can directly use `simple_template`                                          |
| **Database modeling**      | Use nested object structure defined in `simple_template`, with shared fields via `$ref`s |

## Schema Validation

The following code snippet provides an example of custom Simple Schema fields for merge tag support, and custom validations.

```ts
urlOrMergeTags: (text: string): boolean => {
  try {
    new URL(text)
    return true
  } catch (e) {
    return /{{.*}}/.test(text)
  }
},

noAnchorTags: (text: string): boolean =>
  !/<a[^>]*>[\s\S]*?<\/a>|<a\s*\/>/i.test(text),
```

These validators ensure generated content is correct and aligns with the data structure defined within the Simple Schema.
