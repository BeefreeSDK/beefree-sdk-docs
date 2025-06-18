---
description: Learn more about how to use the Check endpoints.
---

# Check

## Overview

The Check group consists of three endpoints that scan a template's JSON or a row's JSON, to identify and report critical design elements that are missing. With these endpoints, you can bring design QA functionality into your application. They automatically check a design for common mistakes (including missing links, missing alt text, overly large images, or HTML file sizes that might cause your users' emails to get clipped in Gmail). This is possible through a `POST` request where you define the `language`, types of `checks` to perform, and the `template` or `row` JSON to check. The response will report any instances within the JSON where an item is missing, a limit is exceeded, and so on. It’ll also include the location (called `target` in the response body) of the item that needs attention within the JSON. For example, the `uuid` of an image module that is missing alt text. &#x20;

When coupled with [Frontend Commands](../../other-customizations/frontend-commands.md), these endpoints act as a core pillar of an interactive feedback experience for your end users. Frontend Commands work by displaying visual cues within the user interface. These cues navigate end users to the part of the design and builder that requires their attention. From there, they can easily apply the changes, perform an additional check if they’d like, and export their designs.&#x20;

Overall, the Check endpoints identify critical design elements, while [Frontend Commands](../../other-customizations/frontend-commands.md) help your end users navigate to the elements that need fixing. Together, they create a tool kit that helps your end users create error-free designs, and support them in ensuring their content is complete and ready for their audiences to consume and enjoy.

For a comprehensive list of all the available checks, reference the [Available Checks section](check.md#available-checks) of this page.&#x20;

## How the Endpoints Work&#x20;

The Check endpoints accept three parameters in the request body: `languages`, `checks`, and `template` or `row`. Reference the descriptions for each parameter below:

* `languages`: Define the language of the template.
* `checks`: Define the checks you want to perform on the template or row JSON. Do this by adding the category, the check, and the details for the check if applicable. The following code snippet displays an example of this.

```json
"checks": [
    {
        "category": "missingAltText" // Checks for images missing the 'alt' attribute for accessibility.
    },
    {
        "category": "missingImageLink" // Ensures that clickable images have a valid href/link target.
    },
    {
        "category": "missingCopyLink" // Validates that "Copy" CTAs (like copy-to-clipboard buttons) are correctly linked or wired.
    },
    {
        "category": "overageImageWeight", // Flags images whose file size exceeds the limit.
        "limit": 500 // Size limit in kilobytes (KB). Images above this threshold trigger a warning.
    },
    {
        "category": "missingDetailsEmail" // Checks that required email details (e.g. footer info, contact address) are included in the template.
    },
    {
        "category": "overageHtmlWeight", // Detects if the total HTML weight is too large.
        "limit": 80, // Maximum allowed HTML size in kilobytes (KB).
        "beautified": true // Indicates the HTML should be beautified (formatted) before measuring its size.
    }
]
```

* `template` or `row`: Include the JSON for either an email template, a page template, or a row. This is the JSON that will be checked in ways defined in the checks section of the `POST` request.

{% hint style="info" %}
**IMPORTANT:** While the example in this section is for an email template, you can use these endpoints to provide feedback on:

* [Email designs](check.md#email)
* [Page designs](check.md#page)
* [Rows within designs](broken-reference)

The [Check Endpoints section](check.md#check-endpoints) provides both an interactive testing environment for these endpoints, and example request bodies you can use to get started with each of the three Check endpoints.
{% endhint %}

### Authentication

To use these endpoints, [authenticate by creating a Content Services API key](authentication.md) in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu). For steps on how to obtain a Content Services API key, visit the [Content Services API Authentication page](authentication.md).

## Available Checks

Reference the available checks you can perform using the Check endpoints in this section. You can perform checks on:

* **Email template JSON:** Use the `v1/message/check` endpoint to perform a check on email template JSON.
* **Page template JSON:** Use the `v1/page/check` endpoint to perform a check on page template JSON.
* **Row JSON within a template:** Use the `v1/row/check` endpoint to perform a check on row JSON within a template.

This section covers the available checks you can perform using these endpoints. Each check listed in this section will include which endpoints it applies to, how it looks in an example API request, and how it looks in an example response. It also explains each field and includes its corresponding data type and description.&#x20;

Comprehensively, across all endpoints, the available checks are the following:

* [Missing alt text](check.md#missing-alt-text): Shown as `missingAltText` in requests and responses.&#x20;
* [Missing link on copy](check.md#missing-link-on-copy): Shown as `missingCopyLink` in requests and responses.&#x20;
* [Missing link on images](check.md#missing-link-on-images): Shown as `missingImageLink` in requests and responses.&#x20;
* [Image overage weight](check.md#image-overage-weight): Shown as `overageImageWeight` in requests and responses.&#x20;
* [Missing email details](check.md#missing-email-details): Shown as `missingEmailDetail` in requests and responses.&#x20;
* [Missing page details](check.md#missing-page-details): Shown as `missingDetailsPage` in requests and responses&#x20;
* [HTML overage size:](check.md#html-overage-size) Shown as `overageHtmlWeight` in requests and responses.

### Missing Alt Text

This section covers the Missing Alt Text check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

<table><thead><tr><th width="213.6796875">Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Warning</td></tr><tr><td><strong>Available for</strong></td><td>Email and page messages, email and page templates, rows</td></tr><tr><td><strong>Applicable widgets</strong></td><td>Image, gif, sticker, icon, social</td></tr></tbody></table>

Perform this check by adding `{"category":"missingAltText"}` to your API call's request body.

#### Example response for a check that passed

The following JSON response shows an example of a missing alt text check that passed. This means that within the email, page, or row JSON, an instance of missing alt text was not identified, and the end user can confidently export their design knowing alt text is where it should be.

```json
{
      "type": "missingAltText",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": []
}
```

#### Example response for a check that returned a warning

The following JSON response shows an example of a missing alt text check that resulted in a warning. This means that within the email, page, or row JSON, an instance of missing alt text was identified, and the end user should resolve the missing alt text in the corresponding target prior to exporting their design.

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

The following table lists and defines all the fields related to the `missingAltText` check.

| Field          | Data type | Description                                                                                                           |
| -------------- | --------- | --------------------------------------------------------------------------------------------------------------------- |
| `type`         | string    | Check type, equal to `missingAltText`                                                                                 |
| `targetsCount` | integer   | The number of widgets missing alt text                                                                                |
| `checkStatus`  | string    | The status of this check: `passed` or `warning`                                                                       |
| `targets`      | array     | The list of widgets missing alt text                                                                                  |
| `locked`       | boolean   | If the widget missing alt text is in a locked row                                                                     |
| `synced`       | boolean   | If the widget missing alt text is in a synced row                                                                     |
| `uuid`         | string    | `uuid` of the row containing this widget                                                                              |
| `widgetLabel`  | string    | Label of the widget missing alt text: filename for `icon`, url for `image`, `gif` and `sticker` and name for `social` |
| `widgetType`   | string    | Type of the widget missing alt text: `image`, `gif`, `sticker`, `icon`, `social`                                      |

### Missing Link on Copy

This section covers the Missing Link on Copy check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

<table><thead><tr><th width="213.6796875">Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Warning</td></tr><tr><td><strong>Available for</strong></td><td>Email and page messages, email and page templates, rows</td></tr><tr><td><strong>Applicable widgets</strong></td><td>Button, social, menu</td></tr></tbody></table>

Perform this check by adding `{"category":"missingCopyLink"}` to your API call's request body.

#### Example response for a check that passed

The following JSON response shows an example of a missing copy link check that passed. This means that within the email, page, or row JSON, an instance of a missing copy link was not identified, and the end user can confidently export their design knowing copy links are where they should be.

```json
{
      "type": "missingCopyLink",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": []
}
```

#### Example response for a check that returned a warning

The following JSON response shows an example of a missing copy link check that resulted in a warning. This means that within the email, page, or row JSON, an instance of a missing copy link was identified, and the end user should resolve the missing copy link in the corresponding target prior to exporting their design.

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

The following table lists and defines all the fields related to the `missingCopyLink` check.

| Field          | Data type | Description                                                     |
| -------------- | --------- | --------------------------------------------------------------- |
| `type`         | string    | Check type, equal to `missingCopyLink`                          |
| `targetsCount` | integer   | The number of widgets missing a link                            |
| `checkStatus`  | string    | The status of this check: `passed` or `warning`                 |
| `targets`      | array     | The list of widgets miss link                                   |
| `locked`       | boolean   | If the widget missing link is in a locked row                   |
| `synced`       | boolean   | If the widget missing link is in a synced row                   |
| `uuid`         | string    | `uuid` of the row containing this widget                        |
| `widgetLabel`  | string    | Label of the widget missing link                                |
| `widgetType`   | string    | Type of the widget missing alt text: `button`, `menu`, `social` |

### Missing Link on Images

This section covers the Missing Link on Images check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

<table><thead><tr><th width="213.6796875">Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Suggestion</td></tr><tr><td><strong>Available for</strong></td><td>Email and page messages, email and page templates, rows</td></tr><tr><td><strong>Applicable widgets</strong></td><td>Image, gif, sticker, icon</td></tr></tbody></table>

Perform this check by adding `{"category":"missingImageLink"}` to your API call's request body.

#### Example response for a check that passed

The following JSON response shows an example of a missing image link check that passed. This means that within the email, page, or row JSON, an instance of a missing image link was not identified, and the end user can confidently export their design knowing image links are where they should be.

```json
{
      "type": "missingImageLink",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": []
}
```

#### Example response for a check that returned a warning

The following JSON response shows an example of a missing image link check that resulted in a warning. This means that within the email, page, or row JSON, an instance of a missing image link was identified, and the end user should resolve the missing image link in the corresponding target prior to exporting their design.

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

The following table lists and defines all the fields related to the `missingImageLink` check.

| Field          | Data type | Description                                                                                 |
| -------------- | --------- | ------------------------------------------------------------------------------------------- |
| `type`         | string    | Check type, equal to `missingImageLink`                                                     |
| `targetsCount` | integer   | The number of widgets miss link                                                             |
| `checkStatus`  | string    | The status of this check: `passed` or `suggestion`                                          |
| `targets`      | array     | The list of widgets miss link                                                               |
| `locked`       | boolean   | If the widget missing link is in a locked row                                               |
| `synced`       | boolean   | If the widget missing link is in a synced row                                               |
| `uuid`         | string    | `uuid` of the row containing this widget                                                    |
| `widgetLabel`  | string    | Label of the widget missing link: filename for `icon`, url for `image`, `gif` and `sticker` |
| `widgetType`   | string    | Type of the widget missing alt text: `image`, `gif`, `sticker`, `icon`                      |

### Image Overage Weight

This section covers the Image Overage Weight check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

In the example detailed in this section, the weight limit is set to 500KB for emails and rows, and 700KB for pages. The "Content-Length" header in the response of HEAD requests from image, gif, sticker, icon, and social URLs is used to determine if the content size exceeds the specified limits. If the header is missing or the URL cannot be evaluated within 20 seconds, it is considered an error, and the URL is logged for review.

<table><thead><tr><th width="213.6796875">Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Suggestion</td></tr><tr><td><strong>Available for</strong></td><td>Email and page messages, email and page templates, rows</td></tr><tr><td><strong>Applicable widgets</strong></td><td>Image, gif, sticker, icon, social</td></tr></tbody></table>

Perform this check by adding `{"category":"overageImageWeight", "limit": 500}` to your API call's request body.

| Field   | Data type | Description                                                   |
| ------- | --------- | ------------------------------------------------------------- |
| `limit` | int       | Other such limit the image weight is considered overage in KB |

#### Example response for a check that passed

The following JSON response shows an example of an image weight overage check that passed. This means that within the email, page, or row JSON, an instance of a limit overage was not identified, and the end user can confidently export their design.

```json
{
      "type": "overageImageWeight",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": [],
       "limit": 500,
       "evaluated": 13,
       "errored": 3
}
```

#### Example response for a check that returned a warning

The following JSON response shows an example of an image weight overage check that resulted in a warning. This means that within the email, page, or row JSON, an instance of an image weight overages was identified, and the end user should resolve the overage prior to exporting their design.

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

The following table lists and defines all the fields related to the `overageImageWeight` check.

| Field          | Data type | Description                                                                      |
| -------------- | --------- | -------------------------------------------------------------------------------- |
| `type`         | string    | Check type, equal to `overageImageWeight`                                        |
| `targetsCount` | integer   | The number of widgets miss alt text                                              |
| `checkStatus`  | string    | The status of this check: `passed` or `warning`                                  |
| `limit`        | integer   | The limit given in the request                                                   |
| `evaluated`    | integer   | The number of evaluated images                                                   |
| `errored`      | integer   | The number of images impossible to get the content-length in head requests       |
| `targets`      | array     | The list of widgets miss alt text                                                |
| `locked`       | boolean   | if the widget missing alt text is in a locked row                                |
| `synced`       | boolean   | If the widget missing alt text is in a synced row                                |
| `weight`       | float     | The weight of the image in KB                                                    |
| `uuid`         | string    | `uuid` of the row containing this widget                                         |
| `widgetLabel`  | string    | Label of the widget missing alt text                                             |
| `widgetType`   | string    | Type of the widget missing alt text: `image`, `gif`, `sticker`, `icon`, `social` |

### Missing Email Details

This section covers the Missing Email Details check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

<table><thead><tr><th width="213.6796875">Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Suggestion</td></tr><tr><td><strong>Available for</strong></td><td>Email messages</td></tr><tr><td><strong>Use general features in JSON</strong></td><td>Head</td></tr></tbody></table>

Perform this check by adding `{"category": "missingDetailsEmail"}` to your API call's request body.

#### Example response for a check that passed

The following JSON response shows an example of a missing email details check that passed. This means that within the email, an instance of missing email details was not identified, and the end user can confidently export their design.

```json
{
      "type": "missingDetailsEmail",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": [],
}
```

#### Example response for a check that returned a warning

The following JSON response shows an example of a missing email details check that resulted in a warning. This means that within the email, an instance of a missing email details was identified, and the end user should resolve the missing email details prior to exporting their design.

```json
{
        "type": "missingDetailsEmail",
        "targetsCount": 2,
        "checkStatus": "suggestion",
        "targets": [{"detailType": "subject"}, {"detailType": "preheader"}],
}                            
```

The following table lists and defines all the fields related to the `missingDetailsEmail` check.

| Field          | Data type | Description                                                 |
| -------------- | --------- | ----------------------------------------------------------- |
| `type`         | string    | Check type, equal to `missingDetailsEmail`                  |
| `targetsCount` | integer   | The number of missing email details                         |
| `checkStatus`  | string    | The status of this check: `passed` or `suggestion`          |
| `targets`      | array     | The list of missing details                                 |
| `detailType`   | string    | Type of the widget missing alt text: `subject`, `preheader` |

### Missing Page Details

This section covers the Missing Page Details check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

<table><thead><tr><th width="213.6796875">Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Suggestion</td></tr><tr><td><strong>Available for</strong></td><td>Page messages</td></tr><tr><td><strong>Use general features in JSON</strong></td><td>Head</td></tr></tbody></table>

Perform this check by adding `{"category": "missingDetailsPage"}` to your API call's request body.

#### Example response for a check that passed

The following JSON response shows an example of a missing page details check that passed. This means that within the page, an instance of missing page details was not identified, and the end user can confidently export their design.

```json
{
      "type": "missingDetailsPage",
       "targetsCount": 0,
       "checkStatus": "passed",
       "targets": [],
}
```

#### Example response for a check that returned a warning

The following JSON response shows an example of a missing page details check that resulted in a warning. This means that within the page, an instance of a missing page details was identified, and the end user should resolve the missing details prior to exporting their design.

```json
{
        "type": "missingDetailsPage",
        "targetsCount": 2,
        "checkStatus": "suggestion",
        "targets": [{"detailType": "title"}, {"detailType": "description"}],
}
```

The following table lists and defines all the fields related to the `missingDetailsPage` check.

| Field          | Data type | Description                                             |
| -------------- | --------- | ------------------------------------------------------- |
| `type`         | string    | Check type, equal to `missingDetailsPage`               |
| `targetsCount` | integer   | The number of missing page details                      |
| `checkStatus`  | string    | The status of this check: `passed` or `suggestion`      |
| `targets`      | array     | The list of missing details                             |
| `detailType`   | string    | Type of the widget missing text: `title`, `description` |

### HTML Overage Size

This section covers the HTML Overage Weight check, detailing the process of adding the check to the `POST` API call, and how it appears in example responses. It includes examples of both a successful check and one that returns a warning.

In the example detailed in this section, the weight limit is set to 80KB for emails and rows, and 700KB for pages. The given JSON HTML is translated and the weight is checked against the specified limit, with the "beautified" boolean determining whether the check applies to the beautified HTML or not. If the weight exceeds the limit, it is considered an error and should be flagged for review.

<table><thead><tr><th width="213.6796875">Check details</th><th>Corresponding options</th></tr></thead><tbody><tr><td><strong>Type</strong></td><td>Warning</td></tr><tr><td><strong>Available for</strong></td><td>Email messages</td></tr><tr><td><strong>Use general features in JSON</strong></td><td>displayConditions</td></tr></tbody></table>

Perform this check by adding `{"category":"overageHtmlWeight", "limit": 20, "beautified": true}` to your API call's request body.

| Field         | Data type                                  | Description                                                    |
| ------------- | ------------------------------------------ | -------------------------------------------------------------- |
| `limit`       | int                                        | Other such limit the image weight is considered overage in KB. |
| `beautified`  | <p>string</p><p>Optional, default true</p> | The weight is considered on beautified html or minified HTML   |

#### Example response for a check that passed

The following JSON response shows an example of an HTML weight overage check that passed. This means that within the email, an instance of a limit overage was not identified, and the end user can confidently export their design.

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

#### Example response for a check that returned a warning

The following JSON response shows an example of an HTML weight overage check that resulted in a warning. This means that within the email, an instance of an HTML weight overages was identified, and the end user should resolve the overage prior to exporting their design.

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

The following table lists and defines all the fields related to the `overageHtmlWeight` check.

| Field               | Data type     | Description                                                                                                |
| ------------------- | ------------- | ---------------------------------------------------------------------------------------------------------- |
| `type`              | string        | Check type, equal to `overageHtmlWeight`                                                                   |
| `targetsCount`      | integer       | The number of widgets miss alt text                                                                        |
| `checkStatus`       | string        | The status of this check: `passed` or `warning`                                                            |
| `maxWeight`         | float or null | The max weight on the generated html files. null if the parser does not response                           |
| `displayConditions` | boolean       | If the given json includes display conditions                                                              |
| `processed`         | boolean       | If the check has been processed. It is `false` when the parser does not response                           |
| `limit`             | integer       | The limit given in the request                                                                             |
| `targets`           | array         | The list of html files generated if the parser is responding and at least 1 has the weight other the limit |
| `weight`            | float         | The weight of the generated HTML in KB                                                                     |
| `beautified`        | boolean       | If the coupled weight is related on beautified HTML                                                        |

## Frontend Visual Feedback and Cues

This page discusses how to perform API calls on the backend in order to run checks again email, page, and row JSON. An important part of connecting the backend API calls to frontend feedback is the response body of these API calls. When a check is performed against the JSON, if an issue is identified, the `target` in the API response specifies the element that needs attention. This target is what connects to [Frontend Commands](../../other-customizations/frontend-commands.md), the `execCommand` method and actions (`select`, `highlight`, `scroll`, and `focus`), and provides feedback visually to the end users on the frontend.

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
[OpenAPI message-check](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/a0a803fcab82fc94a75d76e02422bbaee4b3d159b979391ed8095e475d723f49.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250618%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250618T161121Z&X-Amz-Expires=172800&X-Amz-Signature=03127c13874f053725868618422e686ca27e3ab10506d94146040be509a64155&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
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
[OpenAPI page-check](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/4308febd44d915cc101689a737e2381eb1c6723b5e3d523e010547c938a72ba9.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250618%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250618T161121Z&X-Amz-Expires=172800&X-Amz-Signature=532dc12f3f00795e920952a92560f34dd9fec9bedbbe311d8e165a8abfcc3b68&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
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
[OpenAPI row-check](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/fd96add5eb3171c8641c68e85b13ca24fd76b94debf20b7a3b25a7b5e4c01264.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250618%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250618T161121Z&X-Amz-Expires=172800&X-Amz-Signature=48a0eebcd3a303543a072596b7474860b7d7432c11d7ee1e8059219f287abfdd&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
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
