---
description: Learn more about how to use the Check endpoints.
---

# Check

{% hint style="info" %}
Check endpoints are part of the [Content Services API](./). The Content Services API is available on [Beefree SDK plans that are Essentials or above](https://developers.beefree.io/pricing-plans).
{% endhint %}

## Overview

The Check group consists of three endpoints that scan a template's JSON or a row's JSON, to identify and report critical design elements that are missing. With these endpoints, you can bring design QA functionality into your application. They automatically check a design for common mistakes (including missing links, missing alt text, overly large images, or HTML file sizes that might cause your users' emails to get clipped in Gmail). This is possible through a `POST` request where you define the `language`, types of `checks` to perform, and the `template` or `row` JSON to check. The response will report any instances within the JSON where an item is missing, a limit is exceeded, and so on. It’ll also include the location (called `target` in the response body) of the item that needs attention within the JSON. For example, the `uuid` of an image module that is missing alt text. &#x20;

When coupled with [Frontend Commands](../../other-customizations/frontend-commands.md), these endpoints act as a core pillar of an interactive feedback experience for your end users. Frontend Commands work by displaying visual cues within the user interface. These cues navigate end users to the part of the design and builder that requires their attention. From there, they can easily apply the changes, perform an additional check if they’d like, and export their designs.&#x20;

Overall, the Check endpoints identify critical design elements, while [Frontend Commands](../../other-customizations/frontend-commands.md) help your end users navigate to the elements that need fixing. Together, they create a tool kit that helps your end users create error-free designs, and support them in ensuring their content is complete and ready for their audiences to consume and enjoy.

For a comprehensive list of all the available checks, reference the [Available Checks section](check.md#available-checks) of this page.&#x20;

### Available Collection Values for Check Endpoints

The following table lists the collection values available in this category of endpoints, and their corresponding collection options.

Prior to referencing the table, the following example shows how you can replace the **{collection}** placeholder based on the type of content you'd like to export.

#### How to Replace the {collection} Placeholder

The following example URL has a **{collection}** placeholder. This placeholder needs to be filled in with a **Collection Option** prior to making an API call.

`https://api.getbee.io/v1/{collection}/check`

As an example, if you'd like to check an email's HTML using this endpoint, replace **{collection}** with **message**.

The final URL to make the API call will be:

`https://api.getbee.io/v1/message/check`

The following table provides a comprehensive reference of all available options based on what you'd like to check.

<table data-full-width="true"><thead><tr><th>Resource</th><th>Collection Options</th></tr></thead><tbody><tr><td><code>/check</code></td><td><ul><li><code>/message</code></li><li><code>/page</code></li><li><code>/row</code></li></ul></td></tr></tbody></table>

## How the Endpoints Work&#x20;

The Check endpoints accept three parameters in the request body: `languages`, `checks`, and `template` or `row`. Reference the descriptions for each parameter below:

* `languages`: Define the language of the template.
* `checks`: Define the checks you want to perform on the template or row JSON. Do this by adding the category, the check, and the details for the check if applicable.
* `template` or `row`: Include the JSON for either an email template, a page template, or a row. This is the JSON that will be checked in ways defined in the checks section of the `POST` request.

{% hint style="info" %}
**IMPORTANT:** This section includes a list of checks you can perform for the following designs:

* [Email designs](check.md#email)
* [Page designs](check.md#page)
* [Rows within designs](broken-reference)

The [Check Endpoints section](check.md#check-endpoints) provides both an interactive testing environment for testing the checks and endpoints, and example request bodies you can use to get started with each of the three Check endpoints.
{% endhint %}

### Authentication

To use these endpoints, [authenticate by creating a Content Services API key](authentication.md) in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu). For steps on how to obtain a Content Services API key, visit the [Content Services API Authentication page](authentication.md).

## Available Checks

Reference the available checks you can perform using the Check endpoints in this section. You can perform checks on:

* **Email template JSON:** Use the `v1/message/check` endpoint to perform a check on email template JSON.
* **Page template JSON:** Use the `v1/page/check` endpoint to perform a check on page template JSON.
* **Row JSON within a template:** Use the `v1/row/check` endpoint to perform a check on row JSON within a template.

This section covers the available checks you can perform using these endpoints. Each check listed in this section will include which endpoints it applies to, how it looks in an example API request, and how it looks in an example response. It also explains each field and includes its corresponding data type and description.&#x20;

Comprehensively, across all endpoints, the available checks are listed in the [Available Checks by Endpoint section](check.md#available-checks-by-endpoint).

### Available Checks by Endpoint

This section lists the each of the available check options by endpoint. The endpoints are `/message/check`, `/page/check`, and `/row/check`.

#### Common Checks Across All Endpoints

The following checks apply to **email (`/message/check`)**, **page (`/page/check`)**, and **row (`/row/check`)** endpoints:

<table data-full-width="true"><thead><tr><th>Check Name</th><th>Key</th><th>Description</th></tr></thead><tbody><tr><td><a href="check.md#missing-alt-text">Missing alt text</a></td><td><code>missingAltText</code></td><td>Checks for images missing the <code>alt</code> attribute.</td></tr><tr><td><a href="check.md#missing-link-on-copy">Missing link on copy</a></td><td><code>missingCopyLink</code></td><td>Ensures CTAs and copy elements have valid links.</td></tr><tr><td><a href="check.md#missing-link-on-images">Missing link on images</a></td><td><code>missingImageLink</code></td><td>Ensures images marked as clickable have links.</td></tr><tr><td><a href="check.md#image-overage-weight">Image overage weight</a></td><td><code>overageImageWeight</code></td><td>Flags images that exceed size thresholds (500 KB for email and row, 700 KB for page).</td></tr><tr><td><a href="check.md#insufficient-color-contrast-wip-not-released-yet">Insufficient color contrast</a></td><td><code>insufficientColorContrast</code></td><td>Detects widgets failing WCAG 2.0 AA contrast ratios.</td></tr><tr><td><a href="check.md#highlight-unreachable-web-link">Unreachable web link</a></td><td><code>unreachableWebLink</code></td><td>Highlights broken or unreachable URLs.</td></tr></tbody></table>

#### `/message/check` (Email)

The following code snippet displays an example of how checks can be added to the body of the `POST` request. Test the endpoint in the [Email section](check.md#email). &#x20;

{% code fullWidth="true" %}
```json
{
  "checks": [
    { "category": "missingAltText" },
    { "category": "missingImageLink" },
    { "category": "missingCopyLink" },
    { "category": "overageImageWeight", "limit": 500 },
    { "category": "missingDetailsEmail" },
    { "category": "overageHtmlWeight", "limit": 80, "beautified": true },
    { "category": "missingHeadings" },
    { "category": "overageHeadings" },
    { "category": "missingMainLanguage" },
    { "category": "unreachableWebLink" },
    { "category": "insufficientColorContrast" }
  ]
}
```
{% endcode %}

**Email-specific checks:**

<table data-full-width="true"><thead><tr><th>Check Name</th><th>Key</th><th>Description</th></tr></thead><tbody><tr><td><a href="check.md#missing-email-details">Missing email details</a></td><td><code>missingDetailsEmail</code></td><td>Ensures required metadata (subject, preheader, footer info) is present.</td></tr><tr><td><a href="check.md#html-overage-size">HTML overage size</a></td><td><code>overageHtmlWeight</code></td><td>Flags overly large HTML payloads (limit 80 KB, beautified).</td></tr><tr><td><a href="check.md#missing-headings">Missing headings</a></td><td><code>missingHeadings</code></td><td>Ensures headings exist for accessibility/navigation.</td></tr><tr><td><a href="check.md#overage-headings">Overage headings</a></td><td><code>overageHeadings</code></td><td>Ensures exactly one <code>&#x3C;h1></code> exists (not missing or duplicated).</td></tr><tr><td><a href="check.md#missing-main-language">Missing main language</a></td><td><code>missingMainLanguage</code></td><td>Verifies that a language is set in template metadata.</td></tr></tbody></table>

#### `/page/check` (Page)

The following code snippet displays an example of how checks can be added to the body of the `POST` request. Test the endpoint in the [Page section](check.md#page).

{% code fullWidth="true" %}
```json
{
  "checks": [
    { "category": "missingAltText" },
    { "category": "missingImageLink" },
    { "category": "missingCopyLink" },
    { "category": "overageImageWeight", "limit": 700 },
    { "category": "missingDetailsPage" },
    { "category": "missingHeadings" },
    { "category": "overageHeadings" },
    { "category": "missingMainLanguage" },
    { "category": "unreachableWebLink" },
    { "category": "insufficientColorContrast" }
  ]
}
```
{% endcode %}

**Page-specific checks:**

<table data-full-width="true"><thead><tr><th>Check Name</th><th>Key</th><th>Description</th></tr></thead><tbody><tr><td><a href="check.md#missing-page-details">Missing page details</a></td><td><code>missingDetailsPage</code></td><td>Ensures required metadata (title, description) is present.</td></tr><tr><td><a href="check.md#missing-headings">Missing headings</a></td><td><code>missingHeadings</code></td><td>Ensures headings exist for accessibility/navigation.</td></tr><tr><td><a href="check.md#overage-headings">Overage headings</a></td><td><code>overageHeadings</code></td><td>Ensures exactly one <code>&#x3C;h1></code> exists (not missing or duplicated).</td></tr><tr><td><a href="check.md#missing-main-language">Missing main language</a></td><td><code>missingMainLanguage</code></td><td>Verifies that a language is set in template metadata.</td></tr></tbody></table>

#### `/row/check` (Row)

The following code snippet displays an example of how checks can be added to the body of the `POST` request. Test the endpoint in the [Row section](check.md#row).

{% code fullWidth="true" %}
```json
{
  "checks": [
    { "category": "missingAltText" },
    { "category": "missingImageLink" },
    { "category": "missingCopyLink" },
    { "category": "overageImageWeight", "limit": 500 },
    { "category": "unreachableWebLink" },
    { "category": "insufficientColorContrast" }
  ]
}
```
{% endcode %}

**Row-specific checks:**\
All supported checks are listed in the [Common Checks Across All Endpoints section](check.md#common-checks-across-all-endpoints).

### Missing Alt Text

This section covers the Missing Alt Text check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Warning</td></tr><tr><td><strong>Available for</strong></td><td>Email and page messages, email and page templates, rows</td></tr><tr><td><strong>Applicable widgets</strong></td><td>Image, gif, sticker, icon, social</td></tr></tbody></table>

Perform this check by adding `{"category":"missingAltText"}` to your API call's request body.

#### Example response for a check that passed

The following JSON response shows an example of a missing alt text check that passed. This means that within the email, page, or row JSON, an instance of missing alt text was not identified, and the end user can confidently export their design knowing alt text is where it should be.

{% code fullWidth="true" %}
```json
{
      "type": "missingAltText",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": []
}
```
{% endcode %}

#### Example response for a check that returned a warning

The following JSON response shows an example of a missing alt text check that resulted in a warning. This means that within the email, page, or row JSON, an instance of missing alt text was identified, and the end user should resolve the missing alt text in the corresponding target prior to exporting their design.

{% code fullWidth="true" %}
```json
                {
                    "type": "missingAltText",
                    "targetsCount": 5,
                    "checkStatus": "warning",
                    "targets": [
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "f7ba2e08-c88f-4eda-9fc9-ab482a2dcfd0",
                            "widgetLabel": "https://media0.giphy.com/media/wIePCLOwUQ4RW/giphy.gif?cid=20eb4e9dky638ndajzn0mwpk6hqv3oi8ov705jq2nd4c7rll&ep=v1_gifs_trending&rid=giphy.gif&ct=g",
                            "widgetType": "gif",
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "9c38bcc0-71a0-4baa-9b61-43b3c30a620d",
                            "widgetLabel": "laptop-workspace-flat-design-3214756.jpg",
                            "widgetType": "image"
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "c07bcd67-fb72-4218-85d7-1c5e97d5c79c",
                            "widgetLabel": "https://media2.giphy.com/media/in35qBAr9VKLtpPDe0/giphy.gif?cid=20eb4e9drwe6c1smz42ak0w4qims5tolgkij9rrut8vghj1s&ep=v1_stickers_search&rid=giphy.gif&ct=s",
                            "widgetType": "sticker"
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "ab6589c0-414f-4075-ac31-28369511be4d",
                            "widgetLabel": "custom-icon-placeholder.png",
                            "widgetType": "icon"
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "27386d37-df5b-4f5a-b3df-f3e8a2c9d640",
                            "widgetLabel": "facebook",
                            "widgetType": "social"
                        }
                    ]
                }
```
{% endcode %}

The following table lists and defines all the fields related to the `missingAltText` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>Check type, equal to <code>missingAltText</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>The number of widgets missing alt text</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>The status of this check: <code>passed</code> or <code>warning</code></td></tr><tr><td><code>targets</code></td><td>array</td><td>The list of widgets missing alt text</td></tr><tr><td><code>locked</code></td><td>boolean</td><td>If the widget missing alt text is in a locked row</td></tr><tr><td><code>synced</code></td><td>boolean</td><td>If the widget missing alt text is in a synced row</td></tr><tr><td><code>uuid</code></td><td>string</td><td><code>uuid</code> of the row containing this widget</td></tr><tr><td><code>widgetLabel</code></td><td>string</td><td>Label of the widget missing alt text: filename for <code>icon</code>, url for <code>image</code>, <code>gif</code> and <code>sticker</code> and name for <code>social</code></td></tr><tr><td><code>widgetType</code></td><td>string</td><td>Type of the widget missing alt text: <code>image</code>, <code>gif</code>, <code>sticker</code>, <code>icon</code>, <code>social</code></td></tr></tbody></table>

### Missing Link on Copy

This section covers the Missing Link on Copy check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Warning</td></tr><tr><td><strong>Available for</strong></td><td>Email and page messages, email and page templates, rows</td></tr><tr><td><strong>Applicable widgets</strong></td><td>Button, social, menu</td></tr></tbody></table>

Perform this check by adding `{"category":"missingCopyLink"}` to your API call's request body.

#### Example response for a check that passed

The following JSON response shows an example of a missing copy link check that passed. This means that within the email, page, or row JSON, an instance of a missing copy link was not identified, and the end user can confidently export their design knowing copy links are where they should be.

{% code fullWidth="true" %}
```json
{
      "type": "missingCopyLink",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": []
}
```
{% endcode %}

#### Example response for a check that returned a warning

The following JSON response shows an example of a missing copy link check that resulted in a warning. This means that within the email, page, or row JSON, an instance of a missing copy link was identified, and the end user should resolve the missing copy link in the corresponding target prior to exporting their design.

{% code fullWidth="true" %}
```json
                {
                    "type": "missingCopyLink",
                    "targetsCount": 3,
                    "checkStatus": "warning",
                    "targets": [
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "9c38bcc0-71a0-4baa-9b61-43b3c30a620d",
                            "widgetLabel": "Button name 1",
                            "widgetType": "button"
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "c07bcd67-fb72-4218-85d7-1c5e97d5c79c",
                            "widgetLabel": "Social name,
                            "widgetType": "social"
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "ab6589c0-414f-4075-ac31-28369511be4d",
                            "widgetLabel": "Menu name",
                            "widgetType": "menu"
                        }
                    ]
                }
```
{% endcode %}

The following table lists and defines all the fields related to the `missingCopyLink` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>Check type, equal to <code>missingCopyLink</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>The number of widgets missing a link</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>The status of this check: <code>passed</code> or <code>warning</code></td></tr><tr><td><code>targets</code></td><td>array</td><td>The list of widgets miss link</td></tr><tr><td><code>locked</code></td><td>boolean</td><td>If the widget missing link is in a locked row</td></tr><tr><td><code>synced</code></td><td>boolean</td><td>If the widget missing link is in a synced row</td></tr><tr><td><code>uuid</code></td><td>string</td><td><code>uuid</code> of the row containing this widget</td></tr><tr><td><code>widgetLabel</code></td><td>string</td><td>Label of the widget missing link</td></tr><tr><td><code>widgetType</code></td><td>string</td><td>Type of the widget missing alt text: <code>button</code>, <code>menu</code>, <code>social</code></td></tr></tbody></table>

### Missing Link on Images

This section covers the Missing Link on Images check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Suggestion</td></tr><tr><td><strong>Available for</strong></td><td>Email and page messages, email and page templates, rows</td></tr><tr><td><strong>Applicable widgets</strong></td><td>Image, gif, sticker, icon</td></tr></tbody></table>

Perform this check by adding `{"category":"missingImageLink"}` to your API call's request body.

#### Example response for a check that passed

The following JSON response shows an example of a missing image link check that passed. This means that within the email, page, or row JSON, an instance of a missing image link was not identified, and the end user can confidently export their design knowing image links are where they should be.

{% code fullWidth="true" %}
```json
{
      "type": "missingImageLink",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": []
}
```
{% endcode %}

#### Example response for a check that returned a warning

The following JSON response shows an example of a missing image link check that resulted in a warning. This means that within the email, page, or row JSON, an instance of a missing image link was identified, and the end user should resolve the missing image link in the corresponding target prior to exporting their design.

{% code fullWidth="true" %}
```json
                {
                    "type": "missingImageLink",
                    "targetsCount": 4,
                    "checkStatus": "suggestion",
                    "targets": [
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "f7ba2e08-c88f-4eda-9fc9-ab482a2dcfd0",
                            "widgetLabel": "https://media0.giphy.com/media/wIePCLOwUQ4RW/giphy.gif?cid=20eb4e9dky638ndajzn0mwpk6hqv3oi8ov705jq2nd4c7rll&ep=v1_gifs_trending&rid=giphy.gif&ct=g",
                            "widgetType": "gif",
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "9c38bcc0-71a0-4baa-9b61-43b3c30a620d",
                            "widgetLabel": "laptop-workspace-flat-design-3214756.jpg",
                            "widgetType": "image"
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "c07bcd67-fb72-4218-85d7-1c5e97d5c79c",
                            "widgetLabel": "https://media2.giphy.com/media/in35qBAr9VKLtpPDe0/giphy.gif?cid=20eb4e9drwe6c1smz42ak0w4qims5tolgkij9rrut8vghj1s&ep=v1_stickers_search&rid=giphy.gif&ct=s",
                            "widgetType": "sticker"
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "uuid": "ab6589c0-414f-4075-ac31-28369511be4d",
                            "widgetLabel": "custom-icon-placeholder.png",
                            "widgetType": "icon"
                        }
                    ]
                }
```
{% endcode %}

The following table lists and defines all the fields related to the `missingImageLink` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>Check type, equal to <code>missingImageLink</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>The number of widgets miss link</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>The status of this check: <code>passed</code> or <code>suggestion</code></td></tr><tr><td><code>targets</code></td><td>array</td><td>The list of widgets miss link</td></tr><tr><td><code>locked</code></td><td>boolean</td><td>If the widget missing link is in a locked row</td></tr><tr><td><code>synced</code></td><td>boolean</td><td>If the widget missing link is in a synced row</td></tr><tr><td><code>uuid</code></td><td>string</td><td><code>uuid</code> of the row containing this widget</td></tr><tr><td><code>widgetLabel</code></td><td>string</td><td>Label of the widget missing link: filename for <code>icon</code>, url for <code>image</code>, <code>gif</code> and <code>sticker</code></td></tr><tr><td><code>widgetType</code></td><td>string</td><td>Type of the widget missing alt text: <code>image</code>, <code>gif</code>, <code>sticker</code>, <code>icon</code></td></tr></tbody></table>

### Image Overage Weight

This section covers the Image Overage Weight check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

In the example detailed in this section, the weight limit is set to 500KB for emails and rows, and 700KB for pages. The "Content-Length" header in the response of HEAD requests from image, gif, sticker, icon, and social URLs is used to determine if the content size exceeds the specified limits. If the header is missing or the URL cannot be evaluated within 20 seconds, it is considered an error, and the URL is logged for review.

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Suggestion</td></tr><tr><td><strong>Available for</strong></td><td>Email and page messages, email and page templates, rows</td></tr><tr><td><strong>Applicable widgets</strong></td><td>Image, gif, sticker, icon, social</td></tr></tbody></table>

Perform this check by adding `{"category":"overageImageWeight", "limit": 500}` to your API call's request body.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>limit</code></td><td>int</td><td>Other such limit the image weight is considered overage in KB</td></tr></tbody></table>

#### Example response for a check that passed

The following JSON response shows an example of an image weight overage check that passed. This means that within the email, page, or row JSON, an instance of a limit overage was not identified, and the end user can confidently export their design.

<pre class="language-json" data-full-width="true"><code class="lang-json"><strong>{
</strong>      "type": "overageImageWeight",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": [],
       "limit": 500,
       "evaluated": 13,
       "errored": 3
}
</code></pre>

#### Example response for a check that returned a warning

The following JSON response shows an example of an image weight overage check that resulted in a warning. This means that within the email, page, or row JSON, an instance of an image weight overages was identified, and the end user should resolve the overage prior to exporting their design.

{% code fullWidth="true" %}
```json
                {
                    "type": "overageImageWeight",
                    "targetsCount": 5,
                    "checkStatus": "warning",
                    "limit": 500,
                    "evaluated": 13,
                    "errored": 0,
                    "targets": [
                        {
                            "locked": false,
                            "synced": false,
                            "weight": 51.32,
                            "uuid": "f7ba2e08-c88f-4eda-9fc9-ab482a2dcfd0",
                            "widgetLabel": "https://media0.giphy.com/media/wIePCLOwUQ4RW/giphy.gif?cid=20eb4e9dky638ndajzn0mwpk6hqv3oi8ov705jq2nd4c7rll&ep=v1_gifs_trending&rid=giphy.gif&ct=g",
                            "widgetType": "gif",
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "weight": 51.32,
                            "uuid": "9c38bcc0-71a0-4baa-9b61-43b3c30a620d",
                            "widgetLabel": "laptop-workspace-flat-design-3214756.jpg",
                            "widgetType": "image"
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "weight": 51.32,
                            "uuid": "c07bcd67-fb72-4218-85d7-1c5e97d5c79c",
                            "widgetLabel": "https://media2.giphy.com/media/in35qBAr9VKLtpPDe0/giphy.gif?cid=20eb4e9drwe6c1smz42ak0w4qims5tolgkij9rrut8vghj1s&ep=v1_stickers_search&rid=giphy.gif&ct=s",
                            "widgetType": "sticker"
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "weight": 51.32,
                            "uuid": "ab6589c0-414f-4075-ac31-28369511be4d",
                            "widgetLabel": "custom-icon-placeholder.png",
                            "widgetType": "icon"
                        },
                        {
                            "locked": false,
                            "synced": false,
                            "weight": 51.32,
                            "uuid": "27386d37-df5b-4f5a-b3df-f3e8a2c9d640",
                            "widgetLabel": "facebook",
                            "widgetType": "social"
                        }
                    ]
                }
```
{% endcode %}

The following table lists and defines all the fields related to the `overageImageWeight` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>Check type, equal to <code>overageImageWeight</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>The number of widgets miss alt text</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>The status of this check: <code>passed</code> or <code>warning</code></td></tr><tr><td><code>limit</code></td><td>integer</td><td>The limit given in the request</td></tr><tr><td><code>evaluated</code></td><td>integer</td><td>The number of evaluated images</td></tr><tr><td><code>errored</code></td><td>integer</td><td>The number of images impossible to get the content-length in head requests</td></tr><tr><td><code>targets</code></td><td>array</td><td>The list of widgets miss alt text</td></tr><tr><td><code>locked</code></td><td>boolean</td><td>if the widget missing alt text is in a locked row</td></tr><tr><td><code>synced</code></td><td>boolean</td><td>If the widget missing alt text is in a synced row</td></tr><tr><td><code>weight</code></td><td>float</td><td>The weight of the image in KB</td></tr><tr><td><code>uuid</code></td><td>string</td><td><code>uuid</code> of the row containing this widget</td></tr><tr><td><code>widgetLabel</code></td><td>string</td><td>Label of the widget missing alt text</td></tr><tr><td><code>widgetType</code></td><td>string</td><td>Type of the widget missing alt text: <code>image</code>, <code>gif</code>, <code>sticker</code>, <code>icon</code>, <code>social</code></td></tr></tbody></table>

### Missing Email Details

This section covers the Missing Email Details check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Suggestion</td></tr><tr><td><strong>Available for</strong></td><td>Email messages</td></tr><tr><td><strong>Use general features in JSON</strong></td><td>Head</td></tr></tbody></table>

Perform this check by adding `{"category": "missingDetailsEmail"}` to your API call's request body.

#### Example response for a check that passed

The following JSON response shows an example of a missing email details check that passed. This means that within the email, an instance of missing email details was not identified, and the end user can confidently export their design.

{% code fullWidth="true" %}
```json
{
      "type": "missingDetailsEmail",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": [],
}
```
{% endcode %}

#### Example response for a check that returned a warning

The following JSON response shows an example of a missing email details check that resulted in a warning. This means that within the email, an instance of a missing email details was identified, and the end user should resolve the missing email details prior to exporting their design.

{% code fullWidth="true" %}
```json
{
        "type": "missingDetailsEmail",
        "targetsCount": 2,
        "checkStatus": "suggestion",
        "targets": [{"detailType": "subject"}, {"detailType": "preheader"}],
}                            
```
{% endcode %}

The following table lists and defines all the fields related to the `missingDetailsEmail` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>Check type, equal to <code>missingDetailsEmail</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>The number of missing email details</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>The status of this check: <code>passed</code> or <code>suggestion</code></td></tr><tr><td><code>targets</code></td><td>array</td><td>The list of missing details</td></tr><tr><td><code>detailType</code></td><td>string</td><td>Type of the widget missing alt text: <code>subject</code>, <code>preheader</code></td></tr></tbody></table>

### Missing Page Details

This section covers the Missing Page Details check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Suggestion</td></tr><tr><td><strong>Available for</strong></td><td>Page messages</td></tr><tr><td><strong>Use general features in JSON</strong></td><td>Head</td></tr></tbody></table>

Perform this check by adding `{"category": "missingDetailsPage"}` to your API call's request body.

#### Example response for a check that passed

The following JSON response shows an example of a missing page details check that passed. This means that within the page, an instance of missing page details was not identified, and the end user can confidently export their design.

{% code fullWidth="true" %}
```json
{
      "type": "missingDetailsPage",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": [],
}
```
{% endcode %}

#### Example response for a check that returned a warning

The following JSON response shows an example of a missing page details check that resulted in a warning. This means that within the page, an instance of a missing page details was identified, and the end user should resolve the missing details prior to exporting their design.

{% code fullWidth="true" %}
```json
{
        "type": "missingDetailsPage",
        "targetsCount": 2,
        "checkStatus": "suggestion",
        "targets": [{"detailType": "title"}, {"detailType": "description"}],
}
```
{% endcode %}

The following table lists and defines all the fields related to the `missingDetailsPage` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>Check type, equal to <code>missingDetailsPage</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>The number of missing page details</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>The status of this check: <code>passed</code> or <code>suggestion</code></td></tr><tr><td><code>targets</code></td><td>array</td><td>The list of missing details</td></tr><tr><td><code>detailType</code></td><td>string</td><td>Type of the widget missing text: <code>title</code>, <code>description</code></td></tr></tbody></table>

### HTML Overage Size

This section covers the HTML Overage Weight check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

In the example detailed in this section, the weight limit is set to 80KB for emails and rows, and 700KB for pages. The given JSON HTML is translated and the weight is checked against the specified limit, with the "beautified" boolean determining whether the check applies to the beautified HTML or not. If the weight exceeds the limit, it is considered an error and should be flagged for review.

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Warning</td></tr><tr><td><strong>Available for</strong></td><td>Email messages</td></tr><tr><td><strong>Use general features in JSON</strong></td><td>displayConditions</td></tr></tbody></table>

Perform this check by adding `{"category":"overageHtmlWeight", "limit": 20, "beautified": true}` to your API call's request body.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>limit</code></td><td>int</td><td>Other such limit the image weight is considered overage in KB.</td></tr><tr><td><code>beautified</code> </td><td><p>string</p><p>Optional, default true</p></td><td>The weight is considered on beautified html or minified HTML</td></tr></tbody></table>

#### Example response for a check that passed

The following JSON response shows an example of an HTML weight overage check that passed. This means that within the email, an instance of a limit overage was not identified, and the end user can confidently export their design.

{% code fullWidth="true" %}
```json
{
                    "type": "overageHtmlWeight",
                    "targets": [],
                    "maxWeight": 11.2,
                    "displayConditions": false,
                    "targetsCount": 0,
                    "checkStatus": "passed",
                    "processed": true,
                    "limit": 80
}
```
{% endcode %}

#### Example response for a check that returned a warning

The following JSON response shows an example of an HTML weight overage check that resulted in a warning. This means that within the email, an instance of an HTML weight overages was identified, and the end user should resolve the overage prior to exporting their design.

{% code fullWidth="true" %}
```json
{
                    "type": "overageHtmlWeight",
                    "targets": [
                        {"weight": 11.2, "beautified": true},
                    ],
                    "maxWeight": 11.2,
                    "displayConditions": false,
                    "targetsCount": 1,
                    "checkStatus": "warning",
                    "processed": true,
                    "limit": 80
}                         
```
{% endcode %}

The following table lists and defines all the fields related to the `overageHtmlWeight` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>Check type, equal to <code>overageHtmlWeight</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>The number of widgets miss alt text</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>The status of this check: <code>passed</code> or <code>warning</code></td></tr><tr><td><code>maxWeight</code></td><td>float or null</td><td>The max weight on the generated html files. null if the parser does not response</td></tr><tr><td><code>displayConditions</code></td><td>boolean</td><td>If the given json includes display conditions</td></tr><tr><td><code>processed</code></td><td>boolean</td><td>If the check has been processed. It is <code>false</code> when the parser does not response</td></tr><tr><td><code>limit</code></td><td>integer</td><td>The limit given in the request</td></tr><tr><td><code>targets</code></td><td>array</td><td>The list of html files generated if the parser is responding and at least 1 has the weight other the limit</td></tr><tr><td><code>weight</code></td><td>float</td><td>The weight of the generated HTML in KB</td></tr><tr><td><code>beautified</code></td><td>boolean</td><td>If the coupled weight is related on beautified HTML</td></tr></tbody></table>

### Missing Headings

This check verifies the presence of headings within the template. Headings matter because they give every reader—especially people using screen readers—a clear, navigable map of a template's content and hierarchy. If no heading are found, a warning will be issued. &#x20;

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td>Type</td><td>Warning</td></tr><tr><td>Available for</td><td>email and page messages, email and page templates</td></tr><tr><td>Use data on widgets</td><td>heading</td></tr><tr><td>Use general features in JSON</td><td>--</td></tr></tbody></table>

On requests in checks list: `{"category":"missingHeadings"}`

#### Passed check response

{% code fullWidth="true" %}
```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "missingHeadings",
                "targetsCount": 0,
                "checkStatus": "passed",
                "targets": []
            }
        ],
        "checksFailedCount": 0,
        "checksWarningCount": 0,
        "checksSuggestionCount": 0,
        "status": "passed"
    }
]
```
{% endcode %}

#### Warning check response

{% code fullWidth="true" %}
```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "missingHeadings",
                "targetsCount": 1,
                "checkStatus": "warning",
                "targets": [
                    {
                        "detailType": "no-heading"
                    }
                ]
            }
        ],
        "checksFailedCount": 1,
        "checksWarningCount": 1,
        "checksSuggestionCount": 0,
        "status": "warning"
    }
]
```
{% endcode %}

The following table lists and defines all the fields related to the `missingHeadings` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>check type, equal to <code>missingHeadings</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>the number of missing headings warnings</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>the status of this check: <code>passed</code> or <code>warning</code></td></tr><tr><td><code>targets</code></td><td>array</td><td>the list of missing headings warnings</td></tr></tbody></table>

### Overage Headings

This check verifies whether the template contains a proper **H1 heading**.

* If **no H1** is found, a suggestion is issued.
* If **more than one H1** is found, a suggestion is also issued.

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td>Type</td><td>Suggestion</td></tr><tr><td>Available for</td><td>email and page messages, email and page templates</td></tr><tr><td>Use data on widgets</td><td>heading</td></tr><tr><td>Use general features in JSON</td><td>--</td></tr></tbody></table>

On requests in checks list: `{"category":"overageHeadings"}`

#### Passed check response

{% code fullWidth="true" %}
```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "overageHeadings",
                "targetsCount": 0,
                "checkStatus": "passed",
                "targets": []
            }
        ],
        "checksFailedCount": 0,
        "checksWarningCount": 0,
        "checksSuggestionCount": 0,
        "status": "passed"
    }
]
```
{% endcode %}

#### Suggestion check response - No H1 headings in the template

{% code fullWidth="true" %}
```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "overageHeadings",
                "targetsCount": 1,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "detailType": "no-h1-heading"
                    }
                ]
            }
        ],
        "checksFailedCount": 1,
        "checksWarningCount": 0,
        "checksSuggestionCount": 1,
        "status": "suggestion"
    }
]
```
{% endcode %}

#### Suggestion check response - More than one H1 headings in the template

{% code fullWidth="true" %}
```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "overageHeadings",
                "targetsCount": 2,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "uuid": "5ea9388b-0dc5-4354-917d-638442bf63d2",
                        "widgetType": "heading",
                        "widgetLabel": "Title 1",
                        "locked": false,
                        "synced": false,
                        "title": "h1"
                    },
                    {
                        "uuid": "463d7acb-2e47-4b97-946b-8cd443af8eb0",
                        "widgetType": "heading",
                        "widgetLabel": "Title 2",
                        "locked": false,
                        "synced": false,
                        "title": "h1"
                    }
                ]
            }
        ],
        "checksFailedCount": 2,
        "checksWarningCount": 0,
        "checksSuggestionCount": 2,
        "status": "suggestion"
    }
]
```
{% endcode %}

The following table lists and defines all the fields related to the `overageHeadings` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>check type, equal to <code>overageHeadings</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>the number of overage headings suggestions</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>the status of this check: <code>passed</code> or <code>suggestion</code></td></tr><tr><td><code>targets</code></td><td>array</td><td>the list of overage headings suggestions</td></tr><tr><td><code>locked</code></td><td>boolean</td><td>if the heading widget is in a locked row</td></tr><tr><td><code>synced</code></td><td>boolean</td><td>if the heading widget is in a synced row</td></tr><tr><td><code>uuid</code></td><td>string</td><td>uuid of the row containing this widget</td></tr><tr><td><code>widgetLabel</code></td><td>string</td><td>label of the heading widget</td></tr><tr><td><code>widgetType</code></td><td>string</td><td><code>heading</code></td></tr><tr><td><code>title</code></td><td>string</td><td>title of the heading widget</td></tr></tbody></table>

### Missing Main Language

This check verifies the presence of the language property within the template (Settings > Metadata). The HTML language tag tells assistive technologies, like screen readers, what language the content is in, so words are pronounced correctly. If no language is set, a warning will be issued.

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding Options</th></tr></thead><tbody><tr><td>Type</td><td>Warning</td></tr><tr><td>Available for</td><td>email and page messages, email and page templates</td></tr><tr><td>Use data on widgets</td><td>--</td></tr><tr><td>Use general features in JSON</td><td>head</td></tr></tbody></table>

On requests in checks list: `{"category":"missingMainLanguage"}`

#### Passed check response

{% code fullWidth="true" %}
```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "missingMainLanguage",
                "targetsCount": 0,
                "checkStatus": "passed",
                "targets": []
            }
        ],
        "checksFailedCount": 0,
        "checksWarningCount": 0,
        "checksSuggestionCount": 0,
        "status": "passed"
    }
]
```
{% endcode %}

#### Warning check response

{% code fullWidth="true" %}
```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "missingMainLanguage",
                "targetsCount": 1,
                "checkStatus": "warning",
                "targets": [
                    {
                        "detailType": "no-main-language"
                    }
                ]
            }
        ],
        "checksFailedCount": 1,
        "checksWarningCount": 1,
        "checksSuggestionCount": 0,
        "status": "warning"
    }
]
```
{% endcode %}

The following table lists and defines all the fields related to the `missingMainLanguage` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>check type, equal to <code>missingMainLanguage</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>the number of missing main language warnings</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>the status of this check: <code>passed</code> or <code>warning</code></td></tr><tr><td><code>targets</code></td><td>array</td><td>the list of missing main language warnings</td></tr></tbody></table>

### Insufficient color contrast  <a href="#insufficient-color-contrast-wip-not-released-yet" id="insufficient-color-contrast-wip-not-released-yet"></a>

This check identifies color contrast issues in selected widgets within the template. If one or more issues are detected, a warning is issued.

According to **WCAG 2.0 Level AA**:

* **Normal text** must have a contrast ratio of at least **4.5:1**.
* **Large-scale text** (≥ 24px, or ≥ 19px bold) must have a contrast ratio of at least **3:1**.

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td>Type</td><td>Warning</td></tr><tr><td>Available for</td><td>email and page messages, email and page templates, rows</td></tr><tr><td>Use data on widgets</td><td>button, heading</td></tr><tr><td>Use general features in JSON</td><td>--</td></tr></tbody></table>

On requests in checks list: `{"category":"insufficientColorContrast"}`

#### Passed check response

{% code fullWidth="true" %}
```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "insufficientColorContrast",
                "targetsCount": 0,
                "checkStatus": "passed",
                "targets": []
            }
        ],
        "checksFailedCount": 0,
        "checksWarningCount": 0,
        "checksSuggestionCount": 0,
        "status": "passed"
    }
]
```
{% endcode %}

#### Warning check response - More than one color contrast issue in the template

{% code fullWidth="true" %}
```json
[
    {
        "checks": [
            {
                "checkStatus": "warning",
                "targets": [
                    {
                        "colors": [
                            {
                                "backgroundColor": "#5aff47",
                                "color": "#ff0000",
                                "contrastRatio": 3.01,
                                "label": "hover",
                            },
                        ],
                        "locked": False,
                        "synced": False,
                        "uuid": "7e1fd777-f64f-45a9-8a96-685694c77d60",
                        "widgetLabel": "Button 1",
                        "widgetType": "button",
                    },
                    {
                        "colors": [
                            {
                                "backgroundColor": "#5aff47",
                                "color": "#ff0000",
                                "contrastRatio": 3.01,
                                "label": "default",
                            },
                        ],
                        "locked": False,
                        "synced": False,
                        "uuid": "fd4b8232-43b2-4f78-b322-4d3c21b68d21",
                        "widgetLabel": "Button 2",
                        "widgetType": "button",
                    },
                    {
                        "colors": [
                            {
                                "backgroundColor": "#5aff47",
                                "color": "#ff0000",
                                "contrastRatio": 3.01,
                                "label": "default",
                            },
                        ],
                        "locked": False,
                        "synced": False,
                        "uuid": "4a3a0049-f236-44dd-b4b8-4896ffbc15d6",
                        "widgetLabel": "Heading 1",
                        "widgetType": "heading",
                    },
                ],
                "targetsCount": 3,
                "type": "insufficientColorContrast",
            },
        ],
        "checksFailedCount": 3,
        "checksSuggestionCount": 0,
        "checksWarningCount": 3,
        "language": "default",
        "status": "warning",
    },
]
```
{% endcode %}

The following table lists and defines all the fields related to the `insufficientColorContrast` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>check type, equal to <code>insufficientColorContrast</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>the number of widgets with warnings</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>the status of this check: <code>passed</code> or <code>warning</code></td></tr><tr><td><code>targets</code></td><td>array</td><td>the list of widgets with warnings</td></tr><tr><td><code>locked</code></td><td>boolean</td><td>if the widget is in a locked row</td></tr><tr><td><code>synced</code></td><td>boolean</td><td>if the widget is in a synced row</td></tr><tr><td><code>uuid</code></td><td>string</td><td>uuid of the row containing this widget</td></tr><tr><td><code>widgetLabel</code></td><td>string</td><td>label of the widget</td></tr><tr><td><code>widgetType</code></td><td>string</td><td><code>button</code>, <code>heading</code></td></tr><tr><td><code>colors</code></td><td>array</td><td>list of color pairs with warnings. Each element contains the following fields: <code>backgroundColor, color, contrastRatio, label</code></td></tr><tr><td><code>backgroundColor</code></td><td>string</td><td>color in hexadecimal format</td></tr><tr><td><code>color</code></td><td>string</td><td>color in hexadecimal format</td></tr><tr><td><code>contrastRatio</code></td><td>float</td><td>contrast ratio between <code>color</code> and <code>backgroundColor</code></td></tr><tr><td><code>label</code></td><td>string</td><td>description of the color pairs</td></tr></tbody></table>

### Highlight unreachable web link

This check highlights web links that aren't working properly, helping users catch and fix broken links.

The reachability of a web link is checked using **HEAD requests**. A link is considered reachable if it returns an HTTP status code in the **2xx range**.

If a link cannot be assessed, it is added to the **ignored** array. Each ignored element includes a **reasons** array, which lists one or more of the following values explaining why reachability could not be determined:

* **missingChecked** – required information was not available for the check
* **missingRelated** – related data needed for validation was missing
* **notApplicable** – the check did not apply to this case
* **urlValidation** – the URL itself was invalid

<table data-full-width="true"><thead><tr><th>Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td>Type</td><td>Warning</td></tr><tr><td>Available for</td><td>email and page messages, email and page templates, rows</td></tr><tr><td>Use data on widgets</td><td>button, social, menu, image, gif, sticker, icon</td></tr><tr><td>Use general features in JSON</td><td>--</td></tr></tbody></table>

On requests in checks list: `{"category":"unreachableWebLink"}`

#### Passed check response

{% code fullWidth="true" %}
```json
{
      "type": "unreachableWebLink",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": [],
       "passed": [
           {
               "checkedElement": "https://beefree.io",
               "locked": false,
               "synced": false,
               "uuid": "ab6589c0-414f-4075-ac31-28369511be4d",
               "widgetLabel": "icon-placeholder.png",
               "widgetType": "icon"
           }
       ],
       "ignored": [
           {
               "checkedElement": "",
               "locked": false,
               "reasons": ["missingChecked"],
               "synced": false,
               "uuid": "27386d37-df5b-4f5a-b3df-f3e8a2c9d640",
               "widgetLabel": "Menu item name",
               "widgetType": "menu"
           }
       ]
}
```
{% endcode %}

#### Warning check response

{% code fullWidth="true" %}
```json
{
    "type": "unreachableWebLink",
    "targetsCount": 1,
    "checkStatus": "warning",
    "targets": [
        {
            "checkedElement": "https://beefree.io/unreachable-link",
            "locked": false,
            "synced": false,
            "uuid": "9c38bcc0-71a0-4baa-9b61-43b3c30a620d",
            "widgetLabel": "Button name 1",
            "widgetType": "button"
        }
    ],
    "passed": [
        {
            "checkedElement": "https://beefree.io",
            "locked": false,
            "synced": false,
            "uuid": "ab6589c0-414f-4075-ac31-28369511be4d",
            "widgetLabel": "icon-placeholder.png",
            "widgetType": "icon"
        }
    ],
    "ignored": [
        {
            "checkedElement": "beefree.io",
            "locked": false,
            "reasons": ["urlValidation"],
            "synced": false,
            "uuid": "27386d37-df5b-4f5a-b3df-f3e8a2c9d640",
            "widgetLabel": "Menu item name",
            "widgetType": "menu"
        }
    ]
}
```
{% endcode %}

The following table lists and defines all the fields related to the `unreachableWebLink` check.

<table data-full-width="true"><thead><tr><th>Field</th><th>Data type</th><th>Description</th></tr></thead><tbody><tr><td><code>type</code></td><td>string</td><td>check type, equal to <code>unreachableWebLink</code></td></tr><tr><td><code>targetsCount</code></td><td>integer</td><td>the number of unreachable web links</td></tr><tr><td><code>checkStatus</code></td><td>string</td><td>the status of this check: <code>passed</code> or <code>warning</code></td></tr><tr><td><code>targets</code></td><td>array</td><td>the list of unreachable web links</td></tr><tr><td><code>passed</code></td><td>array</td><td>the list of reachable web links</td></tr><tr><td><code>ignored</code></td><td>array</td><td>the list of ignored links</td></tr><tr><td><code>locked</code></td><td>boolean</td><td>if the link is in a locked row</td></tr><tr><td><code>synced</code></td><td>boolean</td><td>if the link is in a synced row</td></tr><tr><td><code>uuid</code></td><td>string</td><td>uuid of the widget containing the link</td></tr><tr><td><code>widgetLabel</code></td><td>string</td><td>label of the element in the widget containing the link</td></tr><tr><td><code>widgetType</code></td><td>string</td><td>type of the widget: <code>button</code>, <code>menu</code>, <code>social</code>, <code>image</code>, <code>gif</code>, <code>sticker</code>, <code>icon</code></td></tr><tr><td><code>reasons</code></td><td>array</td><td>For ignored elements, one or more of the following values: <code>missingChecked</code>, <code>missingRelated</code>, <code>notApplicable</code>, <code>urlValidation</code></td></tr></tbody></table>

## Frontend Visual Feedback and Cues

This section discusses how to perform API calls on the backend in order to run checks against email, page, and row JSON. An important part of connecting the backend API calls to frontend feedback is the response body of these API calls. When a check is performed against the JSON, if an issue is identified, the `target` in the API response specifies the element that needs attention. This target is what connects to [Frontend Commands](../../other-customizations/frontend-commands.md), the `execCommand` method and actions (`select`, `highlight`, `scroll`, and `focus`), and provides feedback visually to the end users on the frontend.

The following code snippet provides an example email check response from an API call to the `v1/message/check` endpoint.

<details>

<summary>Example email check response (click to expand section)</summary>

Example response

```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "missingAltText",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "english Snapchat",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingImageLink",
                "targetsCount": 4,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "uuid": "b17e02eb-f92d-4c1c-b012-a1c91a865756",
                        "widgetType": "gif",
                        "widgetLabel": "https://media1.giphy.com/media/v1.Y2lkPTIwZWI0ZTlkbmtibHF4emFxbTdmZjlzdmZ6M3ptaWxhb2xxdzc4cm1nZ2gxZnI3eSZlcD12MV9naWZzX3RyZW5kaW5nJmN0PWc/cYZkY9HeKgofpQnOUl/giphy.gif",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "1f4850b4-4146-4649-95ef-17c40214ce69",
                        "widgetType": "image",
                        "widgetLabel": "baseball-usa-lol-lol-lol-lol-lol-6557888.jpg",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "231445c3-8b29-44fc-8c36-08f734bdacb9",
                        "widgetType": "sticker",
                        "widgetLabel": "https://media3.giphy.com/media/tr4TTyG4BjxfDioymO/giphy.gif?cid=20eb4e9d0msqngsoluirfx8m5m93cqwa5xyj7l0lkud65cmo&ep=v1_stickers_trending&rid=giphy.gif&ct=s",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingCopyLink",
                "targetsCount": 1,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "english Custom",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "overageImageWeight",
                "targetsCount": 1,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "b17e02eb-f92d-4c1c-b012-a1c91a865756",
                        "widgetType": "gif",
                        "widgetLabel": "https://media1.giphy.com/media/v1.Y2lkPTIwZWI0ZTlkbmtibHF4emFxbTdmZjlzdmZ6M3ptaWxhb2xxdzc4cm1nZ2gxZnI3eSZlcD12MV9naWZzX3RyZW5kaW5nJmN0PWc/cYZkY9HeKgofpQnOUl/giphy.gif",
                        "locked": false,
                        "synced": false,
                        "weight": 3942.2
                    }
                ],
                "limit": 500,
                "evaluated": 10,
                "errored": 0
            },
            {
                "type": "missingDetailsEmail",
                "targetsCount": 2,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "detailType": "subject"
                    },
                    {
                        "detailType": "preheader"
                    }
                ]
            },
            {
                "type": "overageHtmlWeight",
                "targetsCount": 0,
                "checkStatus": "passed",
                "targets": [],
                "limit": 80,
                "processed": true,
                "maxWeight": 14.94,
                "displayConditions": false
            }
        ],
        "checksFailedCount": 10,
        "status": "warning"
    },
    {
        "language": "it-IT",
        "checks": [
            {
                "type": "missingAltText",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "italian Snapchat",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingImageLink",
                "targetsCount": 1,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingCopyLink",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "italian Custom",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "df1b6f51-d8a7-43ae-a5b9-7699918eccdd",
                        "widgetType": "button",
                        "widgetLabel": "Button italian",
                        "locked": false,
                        "synced": false
                    }
                ]
            }
        ],
        "checksFailedCount": 5,
        "status": "warning"
    }
]
```

</details>

## Check Endpoints

This section lists and describes each of the Check endpoints. You can use this section to learn about endpoint and how they work. You can also test each endpoint in the interactive testing environment available by clicking **Test it**.&#x20;

### Email

This section includes details on how to make an API call using the email check endpoint. In the following environment, you can reference comprehensive endpoint details and use the interactive testing environment to get started with the endpoint.

{% openapi-operation spec="message-check" path="/v1/message/check" method="post" %}
[OpenAPI message-check](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/a0a803fcab82fc94a75d76e02422bbaee4b3d159b979391ed8095e475d723f49.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250910%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250910T193701Z&X-Amz-Expires=172800&X-Amz-Signature=aad443b328099b9f70e4d215b7486415e179623745940e188967bc051e32a74f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

<details>

<summary>Example Email Response</summary>

Reference the following example email response:

```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "overageImageWeight",
                "targetsCount": 1,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "b17e02eb-f92d-4c1c-b012-a1c91a865756",
                        "widgetType": "gif",
                        "widgetLabel": "https://media1.giphy.com/media/v1.Y2lkPTIwZWI0ZTlkbmtibHF4emFxbTdmZjlzdmZ6M3ptaWxhb2xxdzc4cm1nZ2gxZnI3eSZlcD12MV9naWZzX3RyZW5kaW5nJmN0PWc/cYZkY9HeKgofpQnOUl/giphy.gif",
                        "locked": false,
                        "synced": false,
                        "weight": 3942.2
                    }
                ],
                "limit": 500,
                "evaluated": 10,
                "errored": 0
            },
            {
                "type": "missingAltText",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "english Snapchat",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingCopyLink",
                "targetsCount": 1,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "english Custom",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingDetailsEmail",
                "targetsCount": 2,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "detailType": "subject"
                    },
                    {
                        "detailType": "preheader"
                    }
                ]
            },
            {
                "type": "missingImageLink",
                "targetsCount": 4,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "uuid": "b17e02eb-f92d-4c1c-b012-a1c91a865756",
                        "widgetType": "gif",
                        "widgetLabel": "https://media1.giphy.com/media/v1.Y2lkPTIwZWI0ZTlkbmtibHF4emFxbTdmZjlzdmZ6M3ptaWxhb2xxdzc4cm1nZ2gxZnI3eSZlcD12MV9naWZzX3RyZW5kaW5nJmN0PWc/cYZkY9HeKgofpQnOUl/giphy.gif",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "1f4850b4-4146-4649-95ef-17c40214ce69",
                        "widgetType": "image",
                        "widgetLabel": "baseball-usa-lol-lol-lol-lol-lol-6557888.jpg",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "231445c3-8b29-44fc-8c36-08f734bdacb9",
                        "widgetType": "sticker",
                        "widgetLabel": "https://media3.giphy.com/media/tr4TTyG4BjxfDioymO/giphy.gif?cid=20eb4e9d0msqngsoluirfx8m5m93cqwa5xyj7l0lkud65cmo&ep=v1_stickers_trending&rid=giphy.gif&ct=s",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "overageHtmlWeight",
                "targetsCount": 0,
                "checkStatus": "passed",
                "targets": [],
                "limit": 80,
                "processed": true,
                "maxWeight": 14.94,
                "displayConditions": false
            }
        ],
        "checksFailedCount": 10,
        "status": "warning"
    },
    {
        "language": "it-IT",
        "checks": [
            {
                "type": "missingAltText",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "italian Snapchat",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingCopyLink",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "italian Custom",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "df1b6f51-d8a7-43ae-a5b9-7699918eccdd",
                        "widgetType": "button",
                        "widgetLabel": "Button italian",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingImageLink",
                "targetsCount": 1,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    }
                ]
            }
        ],
        "checksFailedCount": 5,
        "status": "warning"
    }
]
```

</details>

### Page

This section includes details on how to make an API call using the page check endpoint. In the following environment, you can reference comprehensive endpoint details and use the interactive testing environment to get started with the endpoint.

{% openapi-operation spec="page-check" path="/v1/page/check" method="post" %}
[OpenAPI page-check](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/4308febd44d915cc101689a737e2381eb1c6723b5e3d523e010547c938a72ba9.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250910%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250910T193701Z&X-Amz-Expires=172800&X-Amz-Signature=f561b3f3def19f20014814a91044886cfa0b7eda4dafe424ecd6d52c8c7e96ee&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

<details>

<summary>Example Page Response</summary>

Reference an example page response:

```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "missingImageLink",
                "targetsCount": 4,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "uuid": "b17e02eb-f92d-4c1c-b012-a1c91a865756",
                        "widgetType": "gif",
                        "widgetLabel": "https://media1.giphy.com/media/v1.Y2lkPTIwZWI0ZTlkbmtibHF4emFxbTdmZjlzdmZ6M3ptaWxhb2xxdzc4cm1nZ2gxZnI3eSZlcD12MV9naWZzX3RyZW5kaW5nJmN0PWc/cYZkY9HeKgofpQnOUl/giphy.gif",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "1f4850b4-4146-4649-95ef-17c40214ce69",
                        "widgetType": "image",
                        "widgetLabel": "baseball-usa-lol-lol-lol-lol-lol-6557888.jpg",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "231445c3-8b29-44fc-8c36-08f734bdacb9",
                        "widgetType": "sticker",
                        "widgetLabel": "https://media3.giphy.com/media/tr4TTyG4BjxfDioymO/giphy.gif?cid=20eb4e9d0msqngsoluirfx8m5m93cqwa5xyj7l0lkud65cmo&ep=v1_stickers_trending&rid=giphy.gif&ct=s",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingAltText",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "english Snapchat",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingDetailsPage",
                "targetsCount": 0,
                "checkStatus": "passed",
                "targets": []
            },
            {
                "type": "overageImageWeight",
                "targetsCount": 1,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "b17e02eb-f92d-4c1c-b012-a1c91a865756",
                        "widgetType": "gif",
                        "widgetLabel": "https://media1.giphy.com/media/v1.Y2lkPTIwZWI0ZTlkbmtibHF4emFxbTdmZjlzdmZ6M3ptaWxhb2xxdzc4cm1nZ2gxZnI3eSZlcD12MV9naWZzX3RyZW5kaW5nJmN0PWc/cYZkY9HeKgofpQnOUl/giphy.gif",
                        "locked": false,
                        "synced": false,
                        "weight": 3942.2
                    }
                ],
                "limit": 500,
                "evaluated": 10,
                "errored": 0
            },
            {
                "type": "missingCopyLink",
                "targetsCount": 1,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "english Custom",
                        "locked": false,
                        "synced": false
                    }
                ]
            }
        ],
        "checksFailedCount": 8,
        "status": "warning"
    },
    {
        "language": "it-IT",
        "checks": [
            {
                "type": "missingImageLink",
                "targetsCount": 1,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingAltText",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "italian Snapchat",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingCopyLink",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "italian Custom",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "df1b6f51-d8a7-43ae-a5b9-7699918eccdd",
                        "widgetType": "button",
                        "widgetLabel": "Button italian",
                        "locked": false,
                        "synced": false
                    }
                ]
            }
        ],
        "checksFailedCount": 5,
        "status": "warning"
    }
]
```

</details>

### Row

This section includes details on how to make an API call using the row check endpoint. In the following environment, you can reference comprehensive endpoint details and use the interactive testing environment to get started with the endpoint.

{% openapi-operation spec="row-check" path="/v1/row/check" method="post" %}
[OpenAPI row-check](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/fd96add5eb3171c8641c68e85b13ca24fd76b94debf20b7a3b25a7b5e4c01264.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250910%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250910T193701Z&X-Amz-Expires=172800&X-Amz-Signature=1c99d099f986ec24caa065ae011393b3d5ee890898e04c29f29f01782ca8099c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

<details>

<summary>Example row response</summary>

Reference an example row response

```json
[
    {
        "language": "default",
        "checks": [
            {
                "type": "overageImageWeight",
                "targetsCount": 1,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "b17e02eb-f92d-4c1c-b012-a1c91a865756",
                        "widgetType": "gif",
                        "widgetLabel": "https://media1.giphy.com/media/v1.Y2lkPTIwZWI0ZTlkbmtibHF4emFxbTdmZjlzdmZ6M3ptaWxhb2xxdzc4cm1nZ2gxZnI3eSZlcD12MV9naWZzX3RyZW5kaW5nJmN0PWc/cYZkY9HeKgofpQnOUl/giphy.gif",
                        "locked": false,
                        "synced": false,
                        "weight": 3942.2
                    }
                ],
                "limit": 500,
                "evaluated": 10,
                "errored": 0
            },
            {
                "type": "missingImageLink",
                "targetsCount": 4,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "uuid": "b17e02eb-f92d-4c1c-b012-a1c91a865756",
                        "widgetType": "gif",
                        "widgetLabel": "https://media1.giphy.com/media/v1.Y2lkPTIwZWI0ZTlkbmtibHF4emFxbTdmZjlzdmZ6M3ptaWxhb2xxdzc4cm1nZ2gxZnI3eSZlcD12MV9naWZzX3RyZW5kaW5nJmN0PWc/cYZkY9HeKgofpQnOUl/giphy.gif",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "1f4850b4-4146-4649-95ef-17c40214ce69",
                        "widgetType": "image",
                        "widgetLabel": "baseball-usa-lol-lol-lol-lol-lol-6557888.jpg",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "231445c3-8b29-44fc-8c36-08f734bdacb9",
                        "widgetType": "sticker",
                        "widgetLabel": "https://media3.giphy.com/media/tr4TTyG4BjxfDioymO/giphy.gif?cid=20eb4e9d0msqngsoluirfx8m5m93cqwa5xyj7l0lkud65cmo&ep=v1_stickers_trending&rid=giphy.gif&ct=s",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingAltText",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "english Snapchat",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingCopyLink",
                "targetsCount": 1,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "english Custom",
                        "locked": false,
                        "synced": false
                    }
                ]
            }
        ],
        "checksFailedCount": 8,
        "status": "warning"
    },
    {
        "language": "it-IT",
        "checks": [
            {
                "type": "missingImageLink",
                "targetsCount": 1,
                "checkStatus": "suggestion",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingAltText",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "8c2fda6f-3fe2-4e04-9018-72ee4c348085",
                        "widgetType": "icon",
                        "widgetLabel": "custom-icon-placeholder.png",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "italian Snapchat",
                        "locked": false,
                        "synced": false
                    }
                ]
            },
            {
                "type": "missingCopyLink",
                "targetsCount": 2,
                "checkStatus": "warning",
                "targets": [
                    {
                        "uuid": "ec01e2b4-5716-455c-a8ef-732a8e0ff561",
                        "widgetType": "social",
                        "widgetLabel": "italian Custom",
                        "locked": false,
                        "synced": false
                    },
                    {
                        "uuid": "df1b6f51-d8a7-43ae-a5b9-7699918eccdd",
                        "widgetType": "button",
                        "widgetLabel": "Button italian",
                        "locked": false,
                        "synced": false
                    }
                ]
            }
        ],
        "checksFailedCount": 5,
        "status": "warning"
    }
]
```

</details>
