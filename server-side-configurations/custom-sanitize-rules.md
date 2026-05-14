---
description: >-
  Customize the tags, attributes, link protocols, and special elements that
  Beefree SDK's HTML Sanitizer is allowed to keep in your end users' content.
---

# Custom Sanitize Rules

{% hint style="info" %}
This feature requires the [Superpowers plan](https://developers.beefree.io/pricing-plans) or above. Available for the Email Builder, Page Builder, and Popup Builder.
{% endhint %}

### Overview

The HTML Sanitizer Service checks and cleans custom HTML, removing unsafe content or tags that might affect deliverability. By default, when the [HTML Sanitizer service](https://docs.beefree.io/beefree-sdk/server-side-configurations/server-side-options/privacy-and-security#html-sanitizer-service) is enabled, Beefree SDK applies a standard whitelist of tags and attributes to two distinct sections of your users’ content:<br>

* the HTML content block inside the editor body, and
* the [Custom Head HTML](https://docs.beefree.io/beefree-sdk/server-side-configurations/custom-head-html) users can add from the Settings tab.

The `sanitizeRules` configuration parameter lets you replace those defaults with your own whitelist, independently for the body and the head. This is useful when:

* your sending or rendering infrastructure supports a wider (or stricter) set of tags and attributes than the SDK defaults;
* you want to lock down your end users to a smaller, more conservative surface than the defaults;
* you want different behavior for the body and the head — for example, allowing `<style>` in the head but not in the body.

{% hint style="warning" %}
**Important:** `sanitizeRules` does not turn the HTML Sanitizer on or off. It only redefines what the sanitizer considers "allowed" once it is running.
{% endhint %}

* To disable sanitization for the HTML content block, use the "Disable the HTML sanitizer service" toggle in the [Privacy and Security](http://./server-side-options/privacy-and-security#html-sanitizer-service) section of the Developer Console.
* To force-enable sanitization on a per-user basis from client-side, use `forceSanitizeHTML`.
* `sanitizeRules` only applies when the sanitizer is active.

### How to configure

`sanitizeRules` is a client-side parameter that you pass inside `beeConfig` when initializing the SDK. It accepts an object with two top-level keys:

| **Key** | **Applies to**                               | **When it takes effect**                                                                      |
| ------- | -------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `body`  | The HTML content block in the editor canvas  | The HTML Sanitizer is enabled (default behavior)                                              |
| `head`  | Custom Head HTML added from the Settings tab | The [Custom Head HTML](http://./custom-head-html) feature is enabled in the Developer Console |

Both body and head accept the same shape of sub-options:

| **Property**            | **Type**  | **Default**                                                                                    | **Description**                                                                                                                                                                                       |
| ----------------------- | --------- | ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `allowedTags`           | string\[] | SDK default whitelist                                                                          | The HTML tags the sanitizer is allowed to keep. Anything not listed here is removed.                                                                                                                  |
| `allowedAttributes`     | object    | SDK default whitelist                                                                          | An object whose keys are tag names and whose values are arrays of allowed attribute names for that tag. The special key "\*" defines attributes allowed on every tag. Anything not listed is removed. |
| `allowedSchemes`        | string\[] | \["https", "http", "ftp", "mailto", "tel", "sms"] for body; \["https", "http", "ftp"] for head | The link protocols allowed on URL-bearing attributes (for example, href and src).                                                                                                                     |
| `allowedComments`       | boolean   | false                                                                                          | When true, HTML comments (\<!-- ... -->) are preserved in the output.                                                                                                                                 |
| `allowedDataAttributes` | boolean   | true                                                                                           | When true, custom data-\* attributes (for example, data-name, data-id) are preserved on every tag.                                                                                                    |
| `allowedARIAAttributes` | boolean   | true                                                                                           | When true, ARIA accessibility attributes (aria-\*, role) are preserved on every tag.                                                                                                                  |

### Full configuration reference

The example below shows every supported key with the SDK's default values. You can copy this snippet as a starting point and adjust the lists to match your application's needs.

```
...
sanitizeRules: {
  body: {
    allowedTags: [
      "a",
      "abbr",
      "acronym",
      "address",
      "area",
      "article",
      "aside",
      "b",
      "base",
      "basefont",
      "bdo",
      "big",
      "blockquote",
      "br",
      "button",
      "caption",
      "center",
      "cite",
      "code",
      "col",
      "colgroup",
      "dd",
      "del",
      "details",
      "dfn",
      "dialog",
      "dir",
      "div",
      "dl",
      "dt",
      "em",
      "embed",
      "fieldset",
      "figcaption",
      "figure",
      "footer",
      "font",
      "form",
      "head",
      "header",
      "h1",
      "h2",
      "h3",
      "h4",
      "h5",
      "h6",
      "hgroup",
      "hr",
      "html",
      "i",
      "img",
      "input",
      "ins",
      "kbd",
      "keygen",
      "label",
      "legend",
      "li",
      "link",
      "main",
      "map",
      "mark",
      "menu",
      "meta",
      "nav",
      "object",
      "ol",
      "optgroup",
      "option",
      "p",
      "param",
      "picture",
      "pre",
      "progress",
      "q",
      "s",
      "samp",
      "section",
      "select",
      "small",
      "source",
      "span",
      "strike",
      "strong",
      "style",
      "sub",
      "summary",
      "sup",
      "table",
      "tbody",
      "td",
      "template",
      "textarea",
      "tfoot",
      "th",
      "thead",
      "time",
      "title",
      "tr",
      "track",
      "tt",
      "u",
      "ul",
      "var",
      "video",
    ],
    allowedAttributes: {
      "*":    ["class", "id", "style", "title", "role" ],
      "base": ["target"],
      "div":  ["itemscope", "itemtype"],
      "meta": ["itemprop", "content"],
      "a":    ["href", "name", "target"],
      "img":  ["align", "alt", "border", "height", "hspace", "src", "vspace", "width", "usemap"],
      "table": ["align", "bgcolor", "border", "cellpadding", "cellspacing", "width"],
      "tbody":  ["align", "valign"],
      "td":     ["align", "bgcolor", "colspan", "height", "rowspan", "valign", "width"],
      "tr":     ["align", "bgcolor", "valign"],
      "tfoot":  ["align", "valign"],
      "th":     ["align", "bgcolor", "colspan", "height", "rowspan", "valign", "width"],
      "thead":  ["align", "valign"],
      "li":     ["type"],
      "video":  ["autoplay", "controls", "height", "loop", "muted", "poster", "preload", "src", "width"],
      "source": ["media", "src", "type"],
      "map":    ["name"],
      "area":   ["alt", "coords", "href", "shape", "target"],
      "ol":     ["start"],
      "input":  ["alt", "type", "checked", "disabled", "multiple", "readonly", "required", "value", "name"],
      "button": ["disabled", "type", "value", "name"],
      "select": ["disabled", "multiple", "required", "name"],
      "option": ["disabled", "selected", "value"],
      "form":   ["action", "method", "enctype", "target"],
      "label":  ["for"],
      "textarea": ["disabled", "readonly", "required", "name", "rows", "cols", "placeholder"],
},
    allowedSchemes: ["https", "http", "ftp", "mailto", "tel", "sms"],
    allowedComments: true,
    allowedDataAttributes: true,
    allowedARIAAttributes: true,
  },
  head: {
    allowedTags: [
      "base",
      "link",
      "meta",
      "style",
      "title",
    ],
    allowedAttributes: {
      "base":  ["href", "target"],
      "link":  ["href", "rel", "type", "media", "sizes"],
      "meta":  ["name", "content", "charset", "property"],
      "style": ["type", "media"],
      "title": [],
    },
    allowedSchemes: ["https", "http", "ftp"],
    allowedComments: true,
    allowedDataAttributes: true,
    allowedARIAAttributes: true,
  },
},
...

```

### How the rules interact with existing settings

sanitizeRules works alongside — not instead of — the existing sanitizer settings. The matrix below shows what happens for each combination:

| **Developer Console setting**                      | **`sanitizeRules` provided in `beeConfig`** | **Result**                                                                                                                           |
| -------------------------------------------------- | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| HTML sanitizer enabled (default)                   | Yes                                         | Sanitizer runs and uses your rules.                                                                                                  |
| HTML sanitizer enabled (default)                   | No                                          | Sanitizer runs and uses the default rules.                                                                                           |
| HTML sanitizer disabled for the HTML content block | Either                                      | The body sanitizer does not run; `sanitizeRules.body` is ignored. `sanitizeRules.head` still applies if Custom Head HTML is enabled. |
| Custom Head HTML disabled in the Developer Console | Either                                      | End users cannot add custom head HTML, so `sanitizeRules.head` has nothing to apply to.                                              |
| `forceSanitizeHTML: true` set per user             | Yes                                         | Sanitizer is force-enabled for this user and uses your rules.                                                                        |

<br>
