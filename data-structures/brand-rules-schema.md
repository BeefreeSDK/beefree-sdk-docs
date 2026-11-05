---
description: >-
  Defines the presets, permissions, and limits used to guide AI-generated
  content with MCP and AI Co-Pilot, and to validate designs with Brand Check.
---

# Brand Rules Schema

Brand Rules for AI and Brand Check both read from the same `brandRules` object: one configuration your users define once, and reuse for both AI-assisted creation and pre-send validation. This page is the shared reference for that schema.

Each feature reads only the fields it needs and ignores the rest. Brand Check ignores AI-only fields: content fields (`html`, `text`, `src`, `alt`, `href`, `items`), plus `permissions`, `limits`, and `description`. MCP and AI Co-Pilot ignore `label`. The tables below show which side reads each property.

### Full JSON schema

The complete JSON schema for Brand Rules, including all properties you can define using presets, permissions, and limits, is available here.

{% file src="../.gitbook/assets/brandRules.schema (1).json" %}

{% hint style="info" %}
The brandRulesSchema.json was last updated on November 5, 2026.
{% endhint %}

### Preset structure

A `preset` is the configuration unit for a brand rule: it's a named set of properties that together define one accepted, on-brand style for a block. For example, a specific button style with its own background color, text color, and border radius. A preset can set a single property (like just `backgroundColor`) or a combination of properties (like background and text color together).

Presets are organized by block type first, then by variant. For example, a `button` block can have a `primaryCta` preset and a `secondaryCta` preset. Block types don't need to define the same variants, or the same number of them.

Beyond content blocks, presets also exist for `rows` and email-level `settings`.

Each preset has:

| **Field**     | **Who reads it** | **Notes**                                                                                                                                                                                 |
| ------------- | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key           | Both             | The presets object key (for example, `brandButton`). A unique, code-facing identifier: 1-64 characters, no spaces.                                                                        |
| `label`       | Brand Check only | Display name shown to end users in the Brand Check panel. Optional, we generate a default ("Style 1", "Style 2"...) if you leave it out, but we strongly recommend setting it explicitly. |
| `description` | MCP/Copilot only | Guidance text for the AI on when to use this preset. Not used for Brand Check matching.                                                                                                   |
| `properties`  | Both             | The property/value pairs that define the preset. These are what both features actually match against.                                                                                     |

Applying a preset only touches the fields it defines; it leaves every other field as it was. For example, if a button has a color set from an earlier preset then a second preset is applied that only sets border and fontFamily, the color stays as it is. We strongly recommend defining the same set of fields across every preset for a given block. If one preset sets fewer properties than another, switching between them leaves stale values in place.

### Example: multiple presets for one block

This defines two accepted button styles, a primary and a secondary:

```json
{
  "brandRules": {
    "presets": {
      "blocks": {
        "button": {
          "primaryCta": {
            "label": "Primary button",
            "description": "Use for the main call-to-action, one per email.",
            "properties": {
              "backgroundColor": "#1A73E8",
              "color": "#FFFFFF",
              "borderRadius": "4px",
              "fontWeight": "700"
            }
          },
          "secondaryCta": {
            "label": "Secondary button",
            "description": "Use for secondary actions like 'Learn more'.",
            "properties": {
              "backgroundColor": "#FFFFFF",
              "color": "#1A73E8",
              "borderTop": "1px solid #1A73E8",
              "borderRight": "1px solid #1A73E8",
              "borderBottom": "1px solid #1A73E8",
              "borderLeft": "1px solid #1A73E8",
              "borderRadius": "4px"
            }
          }
        }
      }
    }
  }
}
```

MCP and AI Co-Pilot pick between `primaryCta` and `secondaryCta` using their `description` text as guidance. Brand Check shows both as options on the button's card, using their `label` text, and your end user picks one.

* `permissions` (`noAdd`/`noUpdate`/`noDelete`): AI operation restrictions, not human-editor permissions or co-edit locks
* `limits` (rows, columns, blocks): AI content limits
* `description` on every preset: AI guidance, not a Brand Check matching rule
* `label` on every preset: Brand Check only, ignored by MCP/Copilot

### Validation

Schema validation is all-or-nothing: if even one field doesn't match the schema (i.e. a string where a number is expected), the whole `brandRules` object is treated as invalid. This is checked consistently wherever the schema is validated: the frontend, MCP session creation, and Brand Check's backend.

Mismatched fields across presets of the same block (see Preset structure above) produce a warning, not an error: the preset is still valid and usable. This warning is also returned consistently across the frontend, MCP session creation, and Brand Check's backend, same as the validation above.

`fontFamily` values must exactly match a font available in the editor's configured font catalog (default fonts or `editorFonts.customFonts`), checked at runtime. An unsupported font is treated as an invalid preset wherever it's used.

**What's compared:** Both features compare the property set on the component itself, not what's rendered. For example, a button with a transparent background on a row with a red background fails a `backgroundColor: red` preset, even though it _looks_ red, because its own `backgroundColor` is `transparent`.

For global fields (default font, link color, content area, background color), an `inherit` value resolves to the global value before comparing. `transparent` is never treated as inherited, it's always compared as its own explicit value.

### Content blocks

"Shared" properties are matched by both Brand Check and MCP/AI Co-Pilot. "MCP/Copilot only" properties are ignored by Brand Check (no error, just skipped). For the exact list of shared versus MCP/Copilot-only properties for each block type, see the [schema file itself](brand-rules-schema.md#full-json-schema), it's the one place that detail is guaranteed to stay current as the schema evolves.

A few rules apply across every block type:

* `hideOnMobile` and `hideOnDesktop` are MCP/Copilot only on every block; Brand Check never checks visibility, and applying a preset never changes it.
* A field named `text` appears on title and button (their copy content, MCP/Copilot only). That's unrelated to the `"text"` value type (a plain string), which properties like `color` and `fontFamily` use and which Brand Check fully supports.
* Custom social icons (uploaded images) aren't matched by presets: `social` presets only define a style from the supported icon collections.

### Layout and global settings

| Preset                            | Shared (checked by Brand Check)                                                                                                                                                                                                                 | MCP/Copilot only                                                                                                 |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| rows                              | `rowBackgroundColor, contentAreaBackgroundColor, contentAreaBorderLeft, contentAreaBorderRight, contentAreaBorderTop, contentAreaBorderBottom, contentAreaBorderRadius, contentAreaPadding, columnsSpacing, columnsBorderRadius, verticalAlign` | `rowBackgroundImage` (whole object), `columns` (the row's column structure array), `hideOnMobile, hideOnDesktop` |
| columns (standalone preset group) | none, this entire group only applies to AI-generated content                                                                                                                                                                                    | `columnBackgroundColor, columnPadding, column borders`                                                           |
| settings                          | `contentAreaWidth, contentAreaAlignment, backgroundColor, fontFamily`                                                                                                                                                                           | `contentAreaBackgroundColor, linkColor`                                                                          |

### Ignored fields

* `permissions` (`noAdd`/`noUpdate`/`noDelete`): AI operation restrictions, not human-editor permissions or co-edit locks
* `limits` (rows, columns, blocks): AI content limits
* `description` on every preset: AI guidance, not a Brand Check matching rule
* `label` on every preset: Brand Check only, ignored by MCP/Copilot<br>
