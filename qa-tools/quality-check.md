---
description: >-
  Beefree SDK's Quality Check lets your user identify and fix issues with
  accessibility, image weight, links, and more, all without leaving the builder.
---

# Quality Check

{% hint style="info" %}
You can enable Quality Check if you are on a Beefree SDK paid plan (Essentials and above) at no extra cost.

Advanced customization options require a Superpowers or Enterprise plan. See [Customization](quality-check.md#customization) for details.
{% endhint %}

### Overview

Quality Check is a built-in readymade widget that gives your end-users actionable feedback on their email and page designs inside the editor, answering the simple question “is this email or page ready to publish?”

Without leaving the builder, your users can identify and fix crucial issues related to accessibility, image weight, missing links, HTML size, and more.

For integrators, the setup is minimal: once you enable the feature in the SDK Console, the full checker experience becomes available to your end-users. It does not require you to build a custom UI or set up additional infrastructure.

{% hint style="success" %}
If you want to develop your fully custom check solution, you can rely on our [Check CSAPI endpoint](https://docs.beefree.io/beefree-sdk/apis/content-services-api/check).
{% endhint %}

API calls made through Quality Check don't count towards your CSAPI allotment. This means they have no separate billing or usage limits.

### Availability

Quality Check is available for **email** and **page** designs.&#x20;

You can activate Quality Check with the dedicated flag in the SDK Console.

<figure><img src="../.gitbook/assets/SDK console - QA tools.png" alt=""><figcaption></figcaption></figure>

### How it works

#### Running a check

Once Quality Check is enabled, your end users see a shield icon in the editor. By clicking it, they run the check against the current email or page and open the Quality Check sidebar.&#x20;

<figure><img src="../.gitbook/assets/Quality Check Arrow.jpg" alt=""><figcaption></figcaption></figure>

Quality Check evaluates the complete email or page JSON to ensure the final exported output meets quality and accessibility standards. The sole exception are [Content details (Meta tag)](quality-check.md#content-details-meta-tag) checks which are only performed when the Meta tags (Title, Subject, Pre-header) are enabled in the SDK console.

#### Understanding the results

Quality Check organizes results into three groups, displayed in the sidebar as:

1. **Warnings**: critical issues that your users should resolve before exporting or sending.
2. **Suggestions**: non-critical issues worth addressing to improve quality and accessibility.
3. **Passed**: checks that found no issues.

Each group shows a badge count reflecting the number of individual element-level issues found. For example, if three images are missing alt text, the related badge will show `3`.

<figure><img src="../.gitbook/assets/Quality check results.jpg" alt=""><figcaption></figcaption></figure>

#### Navigating to issues

When your users click a check result, the editor will highlight the related element in the stage. A click on the navigation arrow opens the associated editor sidebar, so your users can go straight to editing the element that Quality Check flagged.&#x20;

<figure><img src="../.gitbook/assets/Quality Check.gif" alt=""><figcaption></figcaption></figure>

Global-level checks (such as missing subject line) open the general settings panel instead, while other checks are informational only (e.g. “Add headings to improve structure”).

### Checks reference

The tables below list all checks performed by the Quality Check widget. Columns show which content types each check supports.

#### Accessibility

The content your users create should be accessible to everyone, so Quality Check will highlight if your users’ designs don’t follow key accessibility best practices.

<table data-search="false"><thead><tr><th>Check</th><th>Key</th><th width="95">Email Builder</th><th width="95">Page Builder</th><th width="116">Single Row Mode</th><th>Target</th><th width="114">Type</th></tr></thead><tbody><tr><td>Missing alt text</td><td><code>missingAltText</code></td><td>✓</td><td>✓</td><td>✓</td><td>Images, GIFs, stickers, icons, social</td><td>Warning</td></tr><tr><td>Missing headings</td><td><code>missingHeadings</code></td><td>✓</td><td>✓</td><td></td><td>Headings</td><td>Warning</td></tr><tr><td>Missing main language</td><td><code>missingMainLanguage</code></td><td>✓</td><td>✓</td><td></td><td>Design settings (metadata)</td><td>Warning</td></tr><tr><td>Insufficient color contrast</td><td><code>insufficientColorContrast</code></td><td>✓</td><td>✓</td><td>✓</td><td>Buttons, headings, paragraphs, lists, menus, tables, icons</td><td>Warning</td></tr><tr><td>Missing primary heading (H1)</td><td><code>missingHeadings</code></td><td>✓</td><td>✓</td><td></td><td>Headings</td><td>Suggestion</td></tr><tr><td>Too many H1 headings</td><td><code>overageHeadings</code></td><td>✓</td><td></td><td></td><td>Headings</td><td>Suggestion</td></tr><tr><td>Insufficient font size</td><td><code>insufficientFontSize</code></td><td>✓</td><td>✓</td><td>✓</td><td>Buttons, headings, paragraphs, menus, lists, tables</td><td>Suggestion</td></tr></tbody></table>

#### Link presence

A missing link will negatively impact your users’ campaign performance, so Quality Check will highlight if your users missed adding them.

<table data-search="false"><thead><tr><th>Check</th><th>Key</th><th width="95">Email Builder</th><th width="95">Page Builder</th><th width="116">Single Row Mode</th><th>Target</th><th width="114">Type</th></tr></thead><tbody><tr><td>Missing link on interactive elements</td><td><code>missingCopyLink</code></td><td>✓</td><td>✓</td><td>✓</td><td>Buttons, social icons, menus</td><td>Warning</td></tr><tr><td>Missing link on images</td><td><code>missingImageLink</code></td><td>✓</td><td>✓</td><td>✓</td><td>Images, GIFs, stickers, icons</td><td>Suggestion</td></tr></tbody></table>

#### Image & HTML weight

Overly large images can cause loading issues (in particular on mobile), and large HTML files can cause messages to get clipped in Gmail. Quality Check helps your users prevent these mistakes.

<table data-search="false"><thead><tr><th>Check</th><th>Key</th><th width="95">Email Builder</th><th width="95">Page Builder</th><th width="116">Single Row Mode</th><th>Target</th><th width="114">Type</th></tr></thead><tbody><tr><td>Image exceeds weight limit</td><td><code>overageImageWeight</code></td><td>✓</td><td>✓</td><td>✓</td><td>Images, GIFs, stickers, icons, social</td><td>Warning</td></tr><tr><td>HTML exceeds size limit</td><td><code>overageHtmlWeight</code></td><td>✓</td><td></td><td></td><td>Full email HTML output</td><td>Warning</td></tr></tbody></table>

Here are the default limits that Quality check applies:&#x20;

* Maximum image weight: 500 KB for email, 700 KB for pages
* Maximum HTML size: 80 KB for email HTML

You can override the default thresholds via [BeeConfig](quality-check.md#selecting-checks-and-thresholds) (Superpowers and Enterprise plans only).

#### Content details (Meta tag)

{% hint style="info" %}
These checks only appear when the corresponding Meta tag fields are enabled in the SDK Console.
{% endhint %}

Subject lines and preheaders for emails are often the first things recipients see, so missing them has an impact on deliverability and open rates. In a similar way, titles and descriptions for pages are fundamental for both users and search engines, and the lack thereof can hurt click-through and SEO.

<table data-search="false"><thead><tr><th>Check</th><th>Key</th><th width="95">Email Builder</th><th width="95">Page Builder</th><th width="116">Single Row Mode</th><th>Target</th><th width="114">Type</th></tr></thead><tbody><tr><td>Missing email details (subject / preheader)</td><td><code>missingDetailsEmail</code></td><td>✓</td><td></td><td></td><td>Meta tag: subject, preheader</td><td>Suggestion</td></tr><tr><td>Missing page details (title / description)</td><td><code>missingDetailsPage</code></td><td></td><td>✓</td><td></td><td>Meta tag: title, description</td><td>Suggestion</td></tr></tbody></table>

### Customization

#### Selecting checks and thresholds

If you are on a Superpowers or Enterprise plan, you can customize the Quality Check behavior via `beeConfig`. As you can see in the code example below, the available options are passed inside a dedicated `qualityCheck` section.

You can control which checks are presented to end users. If this option is omitted, all available checks are shown by default.

```javascript
const beeConfig = {
  qualityCheck: {
    email: {
      thresholds: {
        overageImageWeight: 500, // in KB; default: 500
        overageHtmlWeight: 80,   // in KB; default: 80; email only
      },
      checks: [
        "missingAltText",
        "missingCopyLink",
        "missingImageLink",
        "overageImageWeight",
        "insufficientColorContrast",
        "missingDetailsEmail",
        "missingDetailsPage",
        "overageHtmlWeight",
        "missingHeadings",
        "overageHeadings",
        "missingMainLanguage",
        "insufficientFontSize",
      ],
    },
    page: {
      thresholds: {
        overageImageWeight: 700, // in KB; default: 700
      },
      checks: [], // empty array = all available checks
    },
    row: {
      thresholds: {
        overageImageWeight: 500, // in KB; default: 500
      },
      checks: [], // empty array = all available checks
    },
  },
};
```

#### Styling & copy

{% hint style="info" %}
CSS-based styling is available to Superpowers and Enterprise plans.
{% endhint %}

You can use [Custom CSS](https://docs.beefree.io/beefree-sdk/other-customizations/appearance/custom-css) to customize

* The badge counters in the side panel
* Colors and UI. By default, warning badges use a system yellow token; suggestion badges use grey, and both are overridable. Themes are not currently supported.
* Icons, as Quality Check by default inherits the icons configured in the content tab.

{% hint style="warning" %}
If you've customized content-tab icons using Custom CSS, those styles do not automatically carry over to the Quality Check panel. You'll need to apply the same CSS rules separately for the checker context.
{% endhint %}

Copy customization is possible by passing [Translation](https://docs.beefree.io/beefree-sdk/getting-started/readme/installation/configuration-parameters#translations) configuration parameters.\
Here you can find the list of the labels used by Quality Check.

<details>

<summary>Quality Check Labels</summary>

```json
{
  "checker-panel": {
    "color-state-default": "CUSTOM-COLOR-STATE-DEFAULT",
    "color-state-hover": "CUSTOM-COLOR-STATE-HOVER",
    "color-state-link": "CUSTOM-COLOR-STATE-LINK",
    "missing-alt-text-issue-label": "CUSTOM-MISSING-ALT-TEXT-ISSUE-LABEL",
    "missing-alt-text-issue-description": "CUSTOM-MISSING-ALT-TEXT-ISSUE-DESCRIPTION",
    "missing-alt-text-passed-label": "CUSTOM-MISSING-ALT-TEXT-PASSED-LABEL",
    "missing-alt-text-passed-description": "CUSTOM-MISSING-ALT-TEXT-PASSED-DESCRIPTION",
    "missing-copy-link-issue-label": "CUSTOM-MISSING-COPY-LINK-ISSUE-LABEL",
    "missing-copy-link-issue-description": "CUSTOM-MISSING-COPY-LINK-ISSUE-DESCRIPTION",
    "missing-copy-link-passed-label": "CUSTOM-MISSING-COPY-LINK-PASSED-LABEL",
    "missing-copy-link-passed-description": "CUSTOM-MISSING-COPY-LINK-PASSED-DESCRIPTION",
    "insufficient-color-contrast-issue-label": "CUSTOM-INSUFFICIENT-COLOR-CONTRAST-ISSUE-LABEL",
    "insufficient-color-contrast-issue-description": "CUSTOM-INSUFFICIENT-COLOR-CONTRAST-ISSUE-DESCRIPTION",
    "insufficient-color-contrast-passed-label": "CUSTOM-INSUFFICIENT-COLOR-CONTRAST-PASSED-LABEL",
    "insufficient-color-contrast-passed-description": "CUSTOM-INSUFFICIENT-COLOR-CONTRAST-PASSED-DESCRIPTION",
    "missing-headings-issue-label": "CUSTOM-MISSING-HEADINGS-ISSUE-LABEL",
    "missing-headings-issue-description": "CUSTOM-MISSING-HEADINGS-ISSUE-DESCRIPTION",
    "missing-headings-passed-label": "CUSTOM-MISSING-HEADINGS-PASSED-LABEL",
    "missing-headings-passed-description": "CUSTOM-MISSING-HEADINGS-PASSED-DESCRIPTION",
    "missing-main-language-issue-label": "CUSTOM-MISSING-MAIN-LANGUAGE-ISSUE-LABEL",
    "missing-main-language-issue-description": "CUSTOM-MISSING-MAIN-LANGUAGE-ISSUE-DESCRIPTION",
    "missing-main-language-passed-label": "CUSTOM-MISSING-MAIN-LANGUAGE-PASSED-LABEL",
    "missing-main-language-passed-description": "CUSTOM-MISSING-MAIN-LANGUAGE-PASSED-DESCRIPTION",
    "overage-html-weight-issue-label": "CUSTOM-OVERAGE-HTML-WEIGHT-ISSUE-LABEL",
    "overage-html-weight-issue-description": "CUSTOM-OVERAGE-HTML-WEIGHT-ISSUE-DESCRIPTION",
    "overage-html-weight-passed-label": "CUSTOM-OVERAGE-HTML-WEIGHT-PASSED-LABEL",
    "overage-html-weight-passed-description": "CUSTOM-OVERAGE-HTML-WEIGHT-PASSED-DESCRIPTION",
    "missing-image-link-issue-label": "CUSTOM-MISSING-IMAGE-LINK-ISSUE-LABEL",
    "missing-image-link-issue-description": "CUSTOM-MISSING-IMAGE-LINK-ISSUE-DESCRIPTION",
    "missing-image-link-passed-label": "CUSTOM-MISSING-IMAGE-LINK-PASSED-LABEL",
    "missing-image-link-passed-description": "CUSTOM-MISSING-IMAGE-LINK-PASSED-DESCRIPTION",
    "overage-image-weight-issue-label": "CUSTOM-OVERAGE-IMAGE-WEIGHT-ISSUE-LABEL",
    "overage-image-weight-issue-description": "CUSTOM-OVERAGE-IMAGE-WEIGHT-ISSUE-DESCRIPTION",
    "overage-image-weight-passed-label": "CUSTOM-OVERAGE-IMAGE-WEIGHT-PASSED-LABEL",
    "overage-image-weight-passed-description": "CUSTOM-OVERAGE-IMAGE-WEIGHT-PASSED-DESCRIPTION",
    "insufficient-font-size-issue-label": "CUSTOM-INSUFFICIENT-FONT-SIZE-ISSUE-LABEL",
    "insufficient-font-size-issue-description": "CUSTOM-INSUFFICIENT-FONT-SIZE-ISSUE-DESCRIPTION",
    "insufficient-font-size-passed-label": "CUSTOM-INSUFFICIENT-FONT-SIZE-PASSED-LABEL",
    "insufficient-font-size-passed-description": "CUSTOM-INSUFFICIENT-FONT-SIZE-PASSED-DESCRIPTION",
    "overage-headings-issue-label": "CUSTOM-OVERAGE-HEADINGS-ISSUE-LABEL",
    "overage-headings-issue-description": "CUSTOM-OVERAGE-HEADINGS-ISSUE-DESCRIPTION",
    "overage-headings-passed-label": "CUSTOM-OVERAGE-HEADINGS-PASSED-LABEL",
    "overage-headings-passed-description": "CUSTOM-OVERAGE-HEADINGS-PASSED-DESCRIPTION",
    "missing-details-email-issue-label": "CUSTOM-MISSING-DETAILS-EMAIL-ISSUE-LABEL",
    "missing-details-email-issue-description": "CUSTOM-MISSING-DETAILS-EMAIL-ISSUE-DESCRIPTION",
    "missing-details-email-passed-label": "CUSTOM-MISSING-DETAILS-EMAIL-PASSED-LABEL",
    "missing-details-email-passed-description": "CUSTOM-MISSING-DETAILS-EMAIL-PASSED-DESCRIPTION",
    "missing-details-page-issue-label": "CUSTOM-MISSING-DETAILS-PAGE-ISSUE-LABEL",
    "missing-details-page-issue-description": "CUSTOM-MISSING-DETAILS-PAGE-ISSUE-DESCRIPTION",
    "missing-details-page-passed-label": "CUSTOM-MISSING-DETAILS-PAGE-PASSED-LABEL",
    "missing-details-page-passed-description": "CUSTOM-MISSING-DETAILS-PAGE-PASSED-DESCRIPTION",
    "detail-type-add-language": "CUSTOM-DETAIL-TYPE-ADD-LANGUAGE",
    "detail-type-add-subject": "CUSTOM-DETAIL-TYPE-ADD-SUBJECT",
    "detail-type-add-preheader": "CUSTOM-DETAIL-TYPE-ADD-PREHEADER",
    "detail-type-add-title": "CUSTOM-DETAIL-TYPE-ADD-TITLE",
    "detail-type-add-meta-description": "CUSTOM-DETAIL-TYPE-ADD-META-DESCRIPTION",
    "header-title": "CUSTOM-HEADER-TITLE",
    "section-warnings": "CUSTOM-SECTION-WARNINGS",
    "section-suggestions": "CUSTOM-SECTION-SUGGESTIONS",
    "section-passed": "CUSTOM-SECTION-PASSED",
    "loading": "CUSTOM-LOADING",
    "no-checks": "CUSTOM-NO-CHECKS",
    "error-title": "CUSTOM-ERROR-TITLE",
    "error-subtitle": "CUSTOM-ERROR-SUBTITLE",
    "all-clear": "CUSTOM-ALL-CLEAR",
    "multiple-colors-applied": "CUSTOM-MULTIPLE-COLORS-APPLIED",
    "show-less": "CUSTOM-SHOW-LESS",
    "show-more": "CUSTOM-SHOW-MORE",
    "primary-language-only": "CUSTOM-PRIMARY-LANGUAGE-ONLY"
  },
  "a11y-aria-attributes": {
    "checker-navigate-to-module-label": "CUSTOM-CHECKER-NAVIGATE-TO-MODULE-LABEL",
    "checker-navigate-to-module-view-label": "CUSTOM-CHECKER-NAVIGATE-TO-MODULE-VIEW-LABEL",
    "checker-navigate-to-settings-label": "CUSTOM-CHECKER-NAVIGATE-TO-SETTINGS-LABEL",
    "checker-panel-close-label": "CUSTOM-CHECKER-PANEL-CLOSE-LABEL",
    "checker-panel-trigger-toggle-label": "CUSTOM-CHECKER-PANEL-TRIGGER-TOGGLE-LABEL"
  }
}

```

</details>

### &#xD; Permissions

Quality Check respects the permissions assigned to the current end user. This means that for a **user with edit permissions**, clicking a check result navigates to the relevant widget in the sidebar for direct editing.

When a user lacking editing permissions clicks on a check result, the commenting panel opens instead, allowing them to flag the issue for collaborators without making changes themselves. If commenting is not enabled, the click has no action.

### AddOns

Quality Check supports the [Giphy](../builder-addons/partner-addons/partner-addons-directory.md#gifs) and [Stickers](../builder-addons/partner-addons/partner-addons-directory.md#stickers) AddOns, but only when they are configured using the default name. If you've renamed either AddOn during configuration, the widget will not recognize those elements and they will not be checked.

Other Partner and Custom AddOns are not supported.

#### Language support

Quality Check runs against the primary language of the design. Multi-language template alternatives are not currently supported.
