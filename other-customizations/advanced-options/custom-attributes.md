# Custom Attributes

{% hint style="info" %}
This feature is available on Beefree SDK **Core plan** and above. You can upgrade a **development application** at no extra charge to explore higher-tier features. **Note:** Usage on development applications still counts toward usage-based fees and limits.
{% endhint %}

## Overview

Custom Attributes allow your end users to append additional metadata to specific HTML elements—primarily links (`<a>`) and image tags (`<img>`), depending on the content block. This metadata can support a range of workflows including personalization, analytics, segmentation, conditional logic, styling hooks, and accessibility attributes.

Custom Attributes are configured by the host application and surfaced directly inside the Beefree SDK editor UI. Once added, attributes are included in the exported HTML exactly as the user specified them.

### Supported targets

Custom Attributes can be applied to the following elements, depending on the block:

* **Links inside text blocks** (Title, Paragraph, List, Table via TinyMCE link dialog)
* **Button links**
* **Image tags**, including **video block thumbnails**
* **Links contained in Social, Menu, and Icon items** (attributes are applied to the item’s underlying `<a>` tag)

Depending on the block type, users will configure attributes through the sidebar or through the link dialog.

### Use cases

Custom Attributes support a wide variety of integration-specific or workflow-specific needs. For example:

* **Tracking control**\
  `data-untracked="true"`, `clicktracking="off"`
* **Segmentation and internal reporting**\
  `data-reportingname="October_promo" data-reportingtags="promo,iphone"`
* **Content-processing hints for your application**\
  `data-l10n-skip="rtl"`, `data-variant="A"`, `data-test-id="hero-title"`
* **Styling hooks**\
  `class="is-primary"`
* **Accessibility metadata**\
  `aria-label="Follow on LinkedIn"`, `role="navigation"`

How these attributes behave ultimately depends on your application’s processing and post-render logic.

### How Custom Attributes appear in the editor

The UI surfaces attributes differently depending on the content block:

* **Buttons and Images**\
  Attributes appear in the **sidebar**, under **Attributes**.
* **Links inside text blocks**\
  Attributes are available in the **Insert/Edit Link** dialog (TinyMCE-powered).
* **Links inside Social, Menu, and Icon items**\
  Attributes appear in the sidebar and apply directly to the item’s underlying `<a>` tag. You can also add custom attributes from the “Global” section at the bottom of the sidebar, which use simple name–value fields and apply only to the container.&#x20;

When users apply attributes, the editor emits them as part of the exported HTML.\
**Example:**

```html
<a href="https://beefree.io/" data-segment="emaildesign" aria-label="Visit Beefree">Visit Beefree</a>
```

### Configuring Custom Attributes

Custom Attributes are enabled and configured through the `customAttributes` object passed into the Beefree SDK initialization. You may combine any of the configuration approaches below.

#### 1. Basic: Selectively enabling attribute UI per block

Enable free-form name/value pairs.

```js
customAttributes: {
  enableOpenFields: true
}
```

This allows end users to manually specify both the attribute name and its value. Use this option when you want to give full flexibility with minimal guardrails. This flag also enables custom attributes specifically for videos, images, buttons, and the text toolbar, adding a tag/link selector alongside the standard name–value fields.

#### 2. Standard: Predefined attributes and values

Provide a curated list of attributes, each with optional predefined values and a target element.

```javascript
const beeConfig = {
  container: "beefree-sdk-container",
  customAttributes: {
    attributes: [
      {
        key: "deeplink",
        value: [
          "myapp://product/12345",
          "myapp://checkout/start?campaign=spring_sale"
        ],
        target: "link"
      },
      {
        key: "utm_campaign",
        value: ["spring_sale", "newsletter_weekly", "vip_offer"],
        target: "link"
      },
      {
        key: "utm_medium",
        value: ["email"],
        target: "link"
      },
      {
        key: "utm_source",
        value: ["crm", "automation_flow", "retention_series"],
        target: "link"
      },
      {
        key: "customer_id",
        value: ["{{customer.id}}", "{{profile.subscriber_id}}"],
        target: "link"
      },
      {
        key: "segment",
        value: ["vip", "first_time_buyer", "re-engagement"],
        target: "link"
      },
      {
        key: "class",
        value: ["primary-cta", "secondary-cta", "hero-link"],
        target: "tag"
      }
    ]
  }
};

```

**How this appears in the UI**

* **Deeplink:** Shows a dropdown with two deep link options for mobile app navigation.
  * myapp://product/12345&#x20;
  * myapp://checkout/start?campaign=spring\_sale

**Text Toolbar**

The following GIF displays how to use the toolbar to add a deeplink Custom Attribute.

<figure><img src="../../.gitbook/assets/CleanShot 2025-12-01 at 22.08.09.gif" alt=""><figcaption></figcaption></figure>

**Sidebar**

The following GIF displays how to use the sidebar to add a deeplink Custom Attribute.

<figure><img src="../../.gitbook/assets/CleanShot 2025-12-01 at 22.09.14.gif" alt=""><figcaption></figcaption></figure>

* **utm\_campaign:** Shows a dropdown with three campaign tracking options.
  * spring\_sale&#x20;
  * newsletter\_weekly&#x20;
  * vip\_offer

The following image shows how the utm\_campaign configuration above looks in the user interface.

<figure><img src="../../.gitbook/assets/CleanShot 2025-12-01 at 22.11.53@2x.png" alt="" width="360"><figcaption></figcaption></figure>

* **utm\_medium:** Shows a dropdown with one medium option.
  * email&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2025-12-01 at 22.14.11@2x.png" alt="" width="354"><figcaption></figcaption></figure>

* **utm\_source:** Shows a dropdown with three source tracking options.
  * crm&#x20;
  * automation\_flow&#x20;
  * retention\_series

<figure><img src="../../.gitbook/assets/CleanShot 2025-12-01 at 22.14.38@2x.png" alt="" width="368"><figcaption></figcaption></figure>

* **customer\_id:** Shows a dropdown with two customer ID placeholder options for personalization.
  * \{{customer.id\}}&#x20;
  * \{{profile.subscriber\_id\}}&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2025-12-01 at 22.15.20@2x.png" alt="" width="364"><figcaption></figcaption></figure>

* **segment:** Shows a dropdown with three audience segment options.
  * vip&#x20;
  * first\_time\_buyer&#x20;
  * re-engagement&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2025-12-01 at 22.15.47@2x.png" alt="" width="366"><figcaption></figcaption></figure>

* **class:** Shows a dropdown with three CSS class options for styling elements (applied to tag instead of link).
  * primary-cta&#x20;
  * secondary-cta&#x20;
  * hero-link

<figure><img src="../../.gitbook/assets/CleanShot 2025-12-01 at 22.16.20@2x.png" alt="" width="356"><figcaption></figcaption></figure>

#### 3. Selectively enabling attribute UI per block

Use `enableBlocks` to explicitly enable the **Attributes** UI for specific block types.

```js
customAttributes: {
  attributes: [
    { key: "data-segment", value: ["travel", "luxury"], target: "link" }
  ],
  enableOpenFields: true,
  enableBlocks: [
    "social",
    "icons",
    "menu",
    "video",
    "image",
    "button",
    "textToolbar"
  ]
}
```

**Default behavior:**\
If `enableBlocks` is omitted, attributes remain enabled where previously supported. Newly supported blocks (Social, Icon, Menu) remain disabled unless explicitly added.

#### 4. Configure Advanced Permissions

Use `advancedPermissions` to control if end users can see and edit attributes by block.

```js
advancedPermissions: {
  content: {
    social:  { properties: { customAttributes: { show: true,  locked: false } } },
    icons:   { properties: { customAttributes: { show: true,  locked: false } } },
    menu:    { properties: { customAttributes: { show: true,  locked: false } } },
    image:   { properties: { customAttributes: { show: true,  locked: false } } },
    button:  { properties: { customAttributes: { show: true,  locked: false } } },
    video:   { properties: { customAttributes: { show: true,  locked: false } } }
  }
}
```

Use `locked: true` to prevent users from editing attributes in the editor. Use `show: false` to prevent users from seeing the custom attribute in the Beefree SDK editor.

## Understanding Tags vs. Links

Different block types handle tags and links in different ways. The points below give more context on how each one works and how attributes are applied.

* **Buttons:** Buttons have a clear separation between structure and behavior.
  * **Tag:** `<button>` — this defines the visual button element.
  * **Link:** `<a>` — this is used when the button needs to navigate to a URL.
* **Icons, menus, and social items:** These block types treat the entire widget as the tag, which is why they appear in the bottom section of the sidebar.
  * Each sub-item inside the block (an individual icon or menu label) has its own tag–link relationship, which can differ depending on how the block is implemented.
* **Sub-item behavior:** Sub-items use different underlying HTML structures, so their tags and links aren’t always obvious at first glance.
  * **Icons and social items:**
    * **Tag:** `<td>` — the container cell that holds the visual element.
    * **Link:** `<a>` — wraps the icon when a URL is provided.
  * **Menu items:**
    * **Tag and link:** `<a>` — a single element functions as both the clickable item and its structural tag.
* **Missing URLs:** Some widgets generate link elements only when needed.
  * If a sub-item has no URL, the `<a>` tag may not be rendered at all in the final HTML.

### Feature limitations

To ensure correct implementation, note the following limitations:

* **Block-level attributes for textual blocks** (e.g., wrapping `<p>`, `<h1>`, `<table>`) are **not supported**.\
  Only _links inside_ those blocks accept attributes.
* **Attributes for Social/Menu/Icon blocks** apply **only to their underlying `<a>` tags**, not to surrounding wrapper tags. These widgets can also set custom attributes in the “Global” section at the bottom of the sidebar, where no tag/link selector is provided and the attributes apply to the container instead.
* **`target: "tag"`** only applies to elements that the block exposes (e.g., `<img>` or `<a>`). It cannot apply attributes to arbitrary nested elements.
* **Open fields** (`enableOpenFields: true`) do not validate attribute names or values—your application is responsible for processing invalid or unexpected entries.
* **Attribute visibility** depends on block availability and permission settings. Hidden or locked attributes cannot be modified in the editor UI.
