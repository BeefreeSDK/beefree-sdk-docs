---
description: Ensure that the content your users create with AI adheres to brand guidelines.
---

# Brand Rules for AI

{% hint style="info" %}
Brand Rules for AI are currently in Beta, and we'd love to hear any and all feedback you might have. Just email us at [beta-feedback@beefree.io](mailto:beta-feedback@beefree.io). If you need a helping hand getting started or have any questions about translating your users' brand guidelines into Brand Rules for AI, we're here to help!\
\
For the duration of the Beta, all SDK customers on Essentials, Core, Superpowers, and Enterprise plans have access to Brand Rules.&#x20;
{% endhint %}

When you're adding agentic design functionality to your product, you don't just want to help your users create content faster. You'll also want to make sure that the content generated with AI is _actually_ on-brand. Brand Rules help you do just that.&#x20;

### Use Brand Rules to help AI create on-brand designs

With Brand Rules, a host application can attach a `brandRules` object to an AI editing session. Brand Rules act as guardrails that the AI must work within so that the output it generates matches your (or your end users') brand. At their core, Brand Rules give guidance on three key questions: <br>

1. **What should certain design elements look like?** You define the styles using `presets` .
2. **What is the AI allowed to touch?** With `permissions` you can control what the AI can (and cannot) edit.
3. **How much content fits?** Use `limits` to define caps on certain content elements.&#x20;

Brand Rules can apply to any AI editing session, whether you're creating with the [MCP](getting-started/) or using the [AI Co-Pilot](ai-co-pilot-closed-beta/).&#x20;

#### The different types of brand rules: Presets, Permissions, and Limits

| **Type**      | **What it does**                                                                                                                                                                                                                                               | **Example**                                                        |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| `presets`     | Named, pre-approved styles for blocks, rows, columns, and settings. Once presets are defined, the AI **must** pick one — preset values override the AI's own styling choices. [Learn more](brand-rules-for-ai.md#key-behaviors-to-carry-into-the-public-docs). | `"brandCta"` → blue background, white bold label, 4px corners      |
| `permissions` | Per-block-type "no" lists: `noAdd`, `noUpdate`, `noDelete`. Refused operations return a clear message to the AI. [Learn more](brand-rules-for-ai.md#permissions).                                                                                              | `noUpdate: ["menu"]` → the AI can never change the navigation menu |
| `limits`      | Content caps: `rows.max/min`, `columns.maxPerRow`, `blocks.max`, `blocks.maxPerType`. [Learn more](brand-rules-for-ai.md#limits).                                                                                                                              | `blocks.maxPerType.menu: 1` → at most one menu in the email        |

Setting Brand Rules is optional. You can choose which Brand Rule type you'd like to define and how detailed you want to be in defining the rules for each of your Brand Rule types. If you don't define a `brandRules` object, it simply means that the AI isn't restricted by any brand guardrails.&#x20;

### Presets <a href="#key-behaviors-to-carry-into-the-public-docs" id="key-behaviors-to-carry-into-the-public-docs"></a>

`presets` are at the core of your Brand Rules because they define styles — colors, typography, and more — the AI _must_ follow when creating content. They allow you to define how content blocks like buttons, paragraphs, or titles should look when they're created by AI. \
\
You can use `presets` in your Brand rules to set one preset per content block or create more sophisticated design systems.&#x20;

#### Basic presets: Define one preset per element

You define a single `preset` per block type that applies to every single content block the AI adds to your design. \
\
Let's say your user's brand guidelines call for all buttons to be bright blue, with slightly rounded corners and white text. You can define your button `presets` like this:

```
{
  "brandRules": {
    "presets": {
      "blocks": {
        "button": {
          "brandButton": {
            "description": "The only approved button style.",
            "properties": {
              "backgroundColor": "#1A73E8",
              "color": "#FFFFFF",
              "borderRadius": "4px",
              "fontWeight": "700"
            }
          }
        }
      }
    }
  }
}
```

Every single time the AI adds a button to the design, it will use the  `brandButton`  styles you defined — and every button will look exactly the same, in compliance with the styles you defined in your `presets`.&#x20;

This basic preset is simple to set up and leaves zero ambiguity for the AI.&#x20;

#### Advanced design systems: Define multiple presets per element

If your users are working with advanced design systems, a single preset per design element might not be enough.&#x20;

For example, while a primary CTA might be blue with white copy, your user's style guide might also allow for secondary CTAs of a different style, and you'll want the AI to work with those instructions as well. &#x20;

`presets` allow you to codify even more complex design systems because you can define multiple `presets` per block type (e.g. `primaryCta`, `secondaryCta`), each with a written `description` that provides guidance on exactly how each preset should be applied. The AI reads the descriptions and picks the right styles for the context. This gives you a richer design system that allows for more design variety while still keeping every choice on-brand.

```
{
  "brandRules": {
    "presets": {
      "blocks": {
        "button": {
          "primaryCta": {
            "description": "Use for the main call-to-action — one per email.",
            "properties": {
              "backgroundColor": "#1A73E8",
              "color": "#FFFFFF",
              "borderRadius": "4px"
            }
          },
          "secondaryCta": {
            "description": "Use for secondary actions like 'Learn more'.",
            "properties": {
              "backgroundColor": "#FFFFFF",
              "color": "#1A73E8",
              "borderTop": "1px solid #1A73E8",
              "borderBottom": "1px solid #1A73E8",
              "borderLeft": "1px solid #1A73E8",
              "borderRight": "1px solid #1A73E8",
              "borderRadius": "4px"
            }
          }
        }
      }
    }
  }
}
```

Every button the AI adds to a design will still be on-brand, but now it can choose between two `presets` — your blue primary button and the white secondary one.&#x20;

#### Important considerations when working with presets

Whether you're working with simple or more sophisticated `presets`, here are some important considerations you must be aware of:&#x20;

* Presets can be applied to content blocks, rows, columns, and the email's overall settings. For a **complete overview of the presets you can define with Brand Rules**, see the [full Brand Rules JSON schema.](brand-rules-for-ai.md#brand-rules-full-json-schema)
* **Presets are mandatory once defined.** For example, if a button preset exists, every button the AI adds or updates must use the preset you defined.
* **Preset values take precedence.** If the AI asks for a red button and the preset says blue, the button in the generated design will be blue—and the AI is told which values were overridden.
* **Presets define only the styles they list — all other styles remain free for the AI to choose.** For example, if a button preset only defines `backgroundColor` and `fontFamily` , it only sets the fixed rules for those two values. The AI retains full freedom over every other property (for example, text, size, padding, borders, etc). For stricter brand control, define all relevant properties.&#x20;

### Permissions

`permissions` are restrictions that prevent the AI from completing certain operations. When the AI attempts an operation that is restricted via `permissions`, the operation is refused, and we'll return a clear message.&#x20;

There are three different types of `permissions` you can set:

| Permission type | Description                                               | Sample response                                         |
| --------------- | --------------------------------------------------------- | ------------------------------------------------------- |
| `noAdd`         | The AI may not **add** these block types to the email.    | `Adding video blocks is not allowed in this session.`   |
| `noUpdate`      | The AI may not **change** existing blocks of these types. | `Updating menu blocks is not allowed in this session.`  |
| `noDelete`      | The AI may not **remove** blocks of these types.          | `Deleting image blocks is not allowed in this session.` |

You can set `permissions` for one or more of the following content blocks: `paragraph`, `title`, `list`, `image`, `button`, `social`, `icon`, `spacer`, `divider`, `table`, `menu`, and `video`.

Here is an example of permissions that define that the AI can never add videos, never touch the menu, and never delete an image:

```
{
  "permissions": {     
    "blocks": {
      "noAdd": ["video"],
      "noUpdate": ["menu"],
      "noDelete": ["image"]
    }
  }
}
```

### Limits

With `limits`, you can define how much content the email can hold and force the AI to work within those limits.&#x20;

| Limit type                 | Allowed value                     | What it means                                                                                     |
| -------------------------- | --------------------------------- | ------------------------------------------------------------------------------------------------- |
| `limits.rows.max`          | whole number (≥ 0)                | The email can hold at most this many rows.                                                        |
| `limits.rows.min`          | whole number (≥ 0)                | The AI cannot delete rows below this count.                                                       |
| `limits.columns.maxPerRow` | whole number (1–12)               | A row can hold at most this many columns.                                                         |
| `limits.blocks.max`        | whole number (≥ 0)                | An email can hold a maximum of this many content blocks (across all block types)                  |
| `limits.blocks.maxPerType` | whole number (≥ 0) per block type | An email can hold a maximum of this many blocks per block type. E.g. `{ "menu": 1, "video": 2 }`. |

Here's an example that uses `limits` to define that an email design stays between 2 and 12 rows, has no more than 4 columns per row, and has no more than 60 content blocks in total:

```
{
  "limits": {
    "rows": { "max": 12, "min": 2 },
    "columns": { "maxPerRow": 4 },
    "blocks": { "max": 60 }
  }
}
```

### Using Brand Rules with the Beefree SDK MCP Server or the AI Co-Pilot

Whether you're using Brand Rules when working directly with our MCP Server or are planning to use it to set guardrails for our built-in AI-Copilot, the underlying schema is exactly the same.&#x20;

How you pass Brand Rules into the AI workflow is a little different depending on the product you're working with. Please review the instructions for each pathway here:&#x20;

* How to use Brand Rules when working with the MCP: [editor-managed session](getting-started/mcp-server-installation-and-setup.md#editor-managed-session) or [API-managed session](getting-started/mcp-server-installation-and-setup.md#api-managed-session)
* How to use Brand Rules when working with the [AI Co-Pilot](ai-co-pilot-closed-beta/#using-brand-rules-with-the-ai-co-pilot)

### Brand Rules - Full JSON schema

The complete JSON schema for Brand Rules, including all properties you can define using presets, permissions, and limits, is available here.&#x20;

{% file src="../.gitbook/assets/brandRulesSchema.json" %}

{% hint style="info" %}
The brandRulesSchema.json was last updated on September 10, 2026
{% endhint %}

### Testing and validating your Brand Rules&#x20;

Whenever  you pass a `brandRules` object to the MCP Server or to the AI Co-Pilot, we validate it automatically at that point. If the payload is invalid, we reject it with a full list of issues.&#x20;

In addition to that, the following validation endpoint helps you test and validate your `brandRules` payload _before_ you start an agent or an MCP session. This can come in handy while you're still developing and testing your Brand Rules implementation, or can be used as a checkpoint in case you're building ways for your end users to create their own Brand Rules. &#x20;

**Endpoint**

`POST https://api.getbee.io/v2/sdk/mcp/template`

**Request body**

| **Field**    | **Type** | **Description**                                 |
| ------------ | -------- | ----------------------------------------------- |
| `brandRules` | object   | the `brandRules` object, passed to be validated |

**Response**

Returns the list of errors found when validating the brandRules object.

### Frequently asked questions

#### What's the difference between Content Defaults and Brand Rules?

[Content Defaults](../other-customizations/appearance/content-defaults.md) let you set default styles that are applied whenever a human drops a new content block onto the stage.&#x20;

Brand Rules, on the other hand, are made to support the agentic design workflow. While the core schema of `presets` within Brand Rules closely mirrors those the schema you might already be familiar with when using Content Defaults, Brand Rules help you go far beyond just setting a single default style. You can use Brand Rules to codify even the most complex design systems, give the AI instructions for when to use which predefined styles, set restrictions on what the AI can and cannot edit, and more.&#x20;
