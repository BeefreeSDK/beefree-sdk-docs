# Content Services API Reference

The Content Services API Reference provides a comprehensive guide to utilizing the Content Services API, which leverages the REST architecture and HTTP protocol for making API calls. This reference document outlines the available collections, including `/message`, `/page`, `/popup`, `/amp`, `/template`, and `/ai`, detailing the resources for each collection. For every resource, this document includes its description, parameters, and example responses and requests.

## API Key

To use the Content Services API you will first need to obtain a your API Key from the Beefree SDK Console.&#x20;

To obtain an API Key, take the following steps:

1. Log into the [Beefree SDK Console](https://dam.beefree.io/devmain)
2. Locate the application that you wish to work with, and click on **Details**
3. Locate the Content Services API section and click **Create New API Key**
4. Acknowledge the message that reminds you that if you exceed the [number of API calls included in your plan](https://dam.beefree.io/devmain), you may be charged for overages and click **Create Key**

Your API key will appear under the **Content services API** section of your application details.

<figure><img src="../../.gitbook/assets/CleanShot 2025-03-13 at 14.58.00.png" alt=""><figcaption></figcaption></figure>

The Content Services API uses API Keys to authenticate requests for resources.  You can manage your API Keys within the Beefree SDK Console.  All requests must be made over HTTPS and contain the following HTTP Header:

**`Authorization:`**` ``Bearer {token}`

## Rate Limits

API requests rate limits exist independently of API key’s monthly usage allowance.

By default, the API has the following rate limits:

* **Per minute:** 500 requests
* **Per second:**  100 requests
* **X-Rate-Limit:** An integer representing the total number of requests available per cycle. Exceeding the limit per cycle results in a 429 error.  (e.g. 500)
* **X-Rate-Limit-Remaining:** An integer representing the number of remaining requests before the next cycle begins, and the count resets. (e.g. 100)
* **X-Rate-Limit-Reset:** A Unix timestamp representing the time the next cycle will begin, and the count will reset.
* **Retry-After:** A Unix timestamp representing the time the application may resume submitting requests.

## API Root

All API access is over HTTPS, and accessed from the following URL:

`https://api.getbee.io/v1/{collection}/{resource}`

## Collections

The following table lists the available collection option and corresponding resources for each collection.

| Collection    | Available Resources                                     |
| ------------- | ------------------------------------------------------- |
| `/message`    | `html`, `pdf`, `images`, `merge`, `index`, `plain-text` |
| `/page`       | `html`, `pdf`, `images`, `merge`, `index`               |
| `/popup`      | `html`                                                  |
| `/amp`        | `html`                                                  |
| `/template`   | `brand`                                                 |
| `/ai`         | `metadata`, `sms`, `summary`                            |
| `/conversion` | `email-to-page`, `page-to-email`                        |

### Example URLs

The following table provides a few examples of URLs you can use to make specific types of requests.

<table><thead><tr><th width="160">Type</th><th>Action</th><th>Example URL</th></tr></thead><tbody><tr><td>Email</td><td>Request HTML for email</td><td><code>https://api.getbee.io/v1/message/html</code></td></tr><tr><td>Landing Page</td><td>Request HTML for a landing page</td><td><code>https://api.getbee.io/v1/page/html</code></td></tr><tr><td>Popup</td><td>Request HTML for a popup</td><td><code>https://api.getbee.io/v1/popup/html</code></td></tr><tr><td>AMP</td><td>Request HTML for AMP</td><td><code>https://api.getbee.io/v1/amp/html</code></td></tr></tbody></table>

## Resources

The following section provides detailed information for each of the resources associated with each collection mentioned in the previous section.

### HTML <a href="#html" id="html"></a>

**URL:** `https://api.getbee.io/v1/{collection}/html`

{% openapi src="../../.gitbook/assets/html_endpoint.yaml" path="/v1/{collection}/html" method="post" %}
[html_endpoint.yaml](../../.gitbook/assets/html_endpoint.yaml)
{% endopenapi %}



{% hint style="info" %}
Include the optional `newbutton` query string parameter and set its value to `true` to generate HTML button results optimized for Outlook. Reference [HTML Outlook Button Rendering](../../rendering/html-outlook-button.md) for additional details.
{% endhint %}

### Plain Text

**Endpoint:** `/message/plain-text`

{% openapi src="../../.gitbook/assets/plain_text_endpoint.yaml" path="/v1/{collection}/plain-text" method="post" %}
[plain_text_endpoint.yaml](../../.gitbook/assets/plain_text_endpoint.yaml)
{% endopenapi %}

### PDF <a href="#pdf" id="pdf"></a>

**URL:** `https://api.getbee.io/v1/{collection}/pdf`

{% openapi src="../../.gitbook/assets/pdf_endpoint.yaml" path="/v1/{collection}/pdf" method="post" %}
[pdf_endpoint.yaml](../../.gitbook/assets/pdf_endpoint.yaml)
{% endopenapi %}

{% hint style="info" %}
**Note:** The response is a JSON string that will contain the URL of the temporary location of the PDF document. The file is available for 24 hours.
{% endhint %}

### Image <a href="#image" id="image"></a>

**URL:** `https://api.getbee.io/v1/{collection}/image`

Prior to using the image endpoint, ensure you reference the following information.

The HTML is rendered in a fixed window size of 1920x1080 to generate a screenshot, with default viewport widths of 320 pixels for mobile and 1024 pixels for desktop, which may cause cropped previews if the content exceeds these dimensions. A clipping size of 1920x1080 is applied, but it can be customized, and the scale factor adjusts to align the viewport and clipping dimensions. For improved results, using auto height with the size parameter is recommended.

| Name         | Type    | Description                                                                                                                                                                                                                                                                                                                        |
| ------------ | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| html\*       | String  | A Beefree HTML message.                                                                                                                                                                                                                                                                                                            |
| size         | String  | Use “size” instead of “width” and “height” when you only know the width and want the height automatically calculated. **Required** if width and height are not defined.                                                                                                                                                            |
| width        | Integer | The image width in pixels. **Required** if size is not defined.                                                                                                                                                                                                                                                                    |
| height       | Integer | The image height in pixels. Default applies a proportional value based on the given width, keeping the image aspect ratio. When the value is not proportional to the given width, either will occur: If it’s higher, the proportional value applies, or, if it’s lower, the image is cropped. **Required** if size is not defined. |
| file\_type\* | String  | Accepts jpg or png.                                                                                                                                                                                                                                                                                                                |

{% openapi src="../../.gitbook/assets/image_endpoint.yaml" path="/v1/{collection}/image" method="post" %}
[image_endpoint.yaml](../../.gitbook/assets/image_endpoint.yaml)
{% endopenapi %}

### Merge <a href="#merge" id="merge"></a>

**URL:** `https://api.getbee.io/v1/{collection}/merge`

{% openapi src="../../.gitbook/assets/merge_endpoint.yaml" path="/v1/{collection}/merge" method="post" %}
[merge_endpoint.yaml](../../.gitbook/assets/merge_endpoint.yaml)
{% endopenapi %}

### Merge Rows <a href="#merge" id="merge"></a>

**URL:** `https://api.getbee.io/v1/{collection}/merge-rows`

{% openapi src="../../.gitbook/assets/merge_rows_endpoint.yaml" path="/v1/{collection}/merge-rows" method="post" %}
[merge_rows_endpoint.yaml](../../.gitbook/assets/merge_rows_endpoint.yaml)
{% endopenapi %}



{% hint style="info" %}
When utilizing this feature, it's important to consider adding a handle to the metadata. This handle serves a crucial role in functions such as `onDeleteRow` and `onEditRow`. In our provided example, we use a handle named `guid`. However, users have the flexibility to choose their own handle name according to their preferences and requirements. When selecting a handle name, we recommend you choose something descriptive and meaningful for ease of identification and management within your workflow.
{% endhint %}

### Synced Rows <a href="#merge" id="merge"></a>

**URL:** `https://api.getbee.io/v1/{collection}/synced-rows`

{% openapi src="../../.gitbook/assets/synced_rows_endpoint.yaml" path="/v1/{collection}/synced-rows" method="post" %}
[synced_rows_endpoint.yaml](../../.gitbook/assets/synced_rows_endpoint.yaml)
{% endopenapi %}

### Index <a href="#index" id="index"></a>

**URL:** `https://api.getbee.io/v1/{collection}/merge/index`

{% openapi src="../../.gitbook/assets/merge_index_endpoint.yaml" path="/v1/{collection}/merge/index" method="post" %}
[merge_index_endpoint.yaml](../../.gitbook/assets/merge_index_endpoint.yaml)
{% endopenapi %}

## AI Collection

{% hint style="warning" %}
**Important:** The [AI collection](content-services-api-reference.md#ai-collection) is only compatible with OpenAI AddOns that were configured before August 1, 2024. We are actively working on making it compatible with AI AddOns and Providers configured after that date, too.
{% endhint %}

The resources in the AI collection accept your template JSON and use generative AI to return text within a JSON object to you.

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

Prior to getting started with the resources in this collection, ensure you have the following:

* **Superpowers** subscription or higher
* **OpenAI AddOn** installed and configured in your Beefree Developer Console
* Content Services **API key**

{% hint style="info" %}
**Note:** OpenAI billing costs apply in addition to the Content Services API billing.
{% endhint %}

### Metadata (Preheader and Subject) <a href="#metadata" id="metadata"></a>

`v1/ai/metadata`

{% openapi src="../../.gitbook/assets/metadata_endpoint.yaml" path="/v1/{collection}/metadata" method="post" %}
[metadata_endpoint.yaml](../../.gitbook/assets/metadata_endpoint.yaml)
{% endopenapi %}

### SMS <a href="#sms" id="sms"></a>

`v1/ai/sms`

{% openapi src="../../.gitbook/assets/sms_endpoint.yaml" path="/v1/{collection}/sms" method="post" %}
[sms_endpoint.yaml](../../.gitbook/assets/sms_endpoint.yaml)
{% endopenapi %}

### Summary

`v1/ai/summary`

{% openapi src="../../.gitbook/assets/summary_endpoint.yaml" path="/v1/{collection}/summary" method="post" %}
[summary_endpoint.yaml](../../.gitbook/assets/summary_endpoint.yaml)
{% endopenapi %}

## Conversion Collection

The Conversion Collection provides you with endpoints that enable you to convert templates from one format to another. With the **Email to Page** endpoint, you can easily convert your email JSON templates into page JSON. The **Page to Email** endpoint lets you turn your page JSON templates into email-ready JSON, with the option to disable the HTML sanitizer if needed.&#x20;

### Email to Page Conversion: Important Behaviors

The Email to Page endpoint converts a JSON template created for email into a JSON template optimized for web pages. During this conversion, the following adjustments are applied:

* **Remove AMP Carousel**\
  Any AMP carousels included in the email template are removed, as these are not supported in the page format.
* **Expand Content Area Width**\
  The content width is expanded to 900px to fit the web page format, removing the width constraints typically applied to emails.
* **Target Attributes**\
  Target attributes will not be processed. Remove all link target attributes or set them to "Open a new page." Links will not be modified during the conversion.
* **Remove Subject and Preheader**\
  Email-specific metadata, such as the subject line and preheader text, is removed since these elements are not relevant in the page format.
* **Retain Comments and Secondary Language**\
  Comments and secondary language data in the email template are preserved in the conversion process.

{% openapi src="../../.gitbook/assets/email-to-page-conversion.yaml" path="/v1/{collection}/email-to-page" method="post" %}
[email-to-page-conversion.yaml](../../.gitbook/assets/email-to-page-conversion.yaml)
{% endopenapi %}

### Page to Email Conversion: Important Behaviors

The Page to Email endpoint transforms a JSON template designed for a web page into a JSON template optimized for email. During this conversion process, the following adjustments are made:

* **Remove Video Row Backgrounds**\
  Video backgrounds applied to page rows are removed because email formats do not support video backgrounds.
* **Replace Embedded Videos with Thumbnails**\
  Embedded videos are replaced with thumbnail images. This ensures recipients can preview the content visually without the compatibility issues of embedded videos.\
  **Note:** Hosted videos will not be converted.
* **Remove Form Blocks**\
  Any form blocks present in the page template are removed.
* **Adjust Design Content Area Width**\
  If the page width exceeds the maximum width supported by the email builder (900px), it is resized to fit within email constraints.
* **Update Link Target Attributes**\
  Target attributes will not be processed. Remove all link target attributes. Links will not be modified during the conversion.
*   **Sanitize Code**\
    The endpoint sanitizes the code to ensure compatibility with email standards. When the sanitizer is disabled, the payload looks like this:

    ```json
    {
      "disableHtmlSanitizer": true,
      "template": { "page": ... }
    }
    ```
* **Handle Multi-Column Layouts**\
  The email builder supports up to 12 columns, which is compatible with the page builder's column configurations.

{% openapi src="../../.gitbook/assets/page-to-emai-conversion.yaml" path="/v1/{collection}/page-to-email" method="post" %}
[page-to-emai-conversion.yaml](../../.gitbook/assets/page-to-emai-conversion.yaml)
{% endopenapi %}

### Simple to Full JSON

{% hint style="info" %}
Simple Schema is available on [Superpowers and Enterprise plans](https://developers.beefree.io/pricing-plans).
{% endhint %}

This section discusses what the `/simple-to-full-json` endpoint is and how you can use it for AI-driven designs. Beefree SDK template JSON is long and includes many properties. For this reason, it does not provide the best structure for training AI models in workflows that include AI-driven design creation. Beefree SDK's [Simple schema](../../data-structures/simple-schema/) is a lightweight alternative that is optimized for training AI models. [Simple schema](../../data-structures/simple-schema/), which is several lines shorter than Beefree SDK's template JSON, is a great solution for AI-generated schemas. This endpoint accepts [Simple schema](../../data-structures/simple-schema/) as the body of the `POST` request, and returns the full Beefree SDK template JSON, which can then be loaded in the Beefree SDK editor for an end user to view and edit accordingly. There are many creative ways to use and implement this endpoint, because it provides a pathway to programmatically creating full Beefree SDK-compatible templates completely outside of the Beefree SDK builder.        &#x20;

#### Request Parameters

The API call accepts a `template` object, which is required to successfully perform the `/simple-to-full-json` API call. The following table describes this required object.

| Name       | Type | Required | Description                                                                                                                                                              |
| ---------- | ---- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `template` | JSON | Yes      | A Beefree SDK template in simple JSON format ([see the schema in GitHub](https://github.com/mailupinc/simple-schema-beefree-sdk/blob/main/simple_template.schema.json)). |

The following code snippet shows the template object as the body of the `POST` request.

```json
{
  “template”:{...}
}
```

{% hint style="info" %}
**Note:** The [simple template JSON schema](https://github.com/mailupinc/simple-schema-beefree-sdk/blob/main/simple_template.schema.json) describes the request parameters, and the template object structure.&#x20;
{% endhint %}

#### Object Parameters Nested within the Template Object

The following table lists and describes both **required** and **optional** object parameters nested within the mandatory `template` object. This `template` object is the body of the `POST` request for the API call.&#x20;

| Name       | Type   | Required | Description                                                                                                                                                                                                        |
| ---------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `type`     | String | ✅ Yes    | Specifies the template type. Possible values include: `email`, `page`, `popup`.                                                                                                                                    |
| `rows`     | Array  | ✅ Yes    | Array containing at least one row. Reference the [simple row schema](https://github.com/mailupinc/simple-schema-beefree-sdk/blob/main/simple_row.schema.json).                                                     |
| `settings` | Object | ❌ No     | Configuration settings. Reference the [Settings Object Parameters](content-services-api-reference.md#settings-object-parameters-request-greater-than-template-greater-than-settings) section for more information. |
| `metadata` | Object | ❌ No     | Metadata information. Reference the [Metadata Object Parameters section](content-services-api-reference.md#metadata-object-parameters-request-greater-than-template-greater-than-metadata) for more information.   |

#### **Settings Object Parameters** <a href="#settings-object-parameters-request-greater-than-template-greater-than-settings" id="settings-object-parameters-request-greater-than-template-greater-than-settings"></a>

The following code snippet shows the optional `settings` object nested within the `template` object in the body of the `POST` request.

```json
{
  “template”:{
    "settings":{...},
    ...
  }
}
```

The following table lists and describes **optional** object parameters nested within the `settings` object. The settings object is nested within the mandatory `template` object.&#x20;

| Name                         | Type    | Required | Description                                                                           |
| ---------------------------- | ------- | -------- | ------------------------------------------------------------------------------------- |
| `linkColor`                  | String  | ❌ No     | The default color of the links within the template.                                   |
| `backgroundColor`            | String  | ❌ No     | The background color of the template.                                                 |
| `contentAreaBackgroundColor` | String  | ❌ No     | The background color of the content area.                                             |
| `width`                      | integer | ❌ No     | **Important:** The width of the template must be between **320** and **1440** pixels. |

#### **Metadata Object Parameters** <a href="#metadata-object-parameters-request-greater-than-template-greater-than-metadata" id="metadata-object-parameters-request-greater-than-template-greater-than-metadata"></a>

The following code snippet shows the optional `metadata` object nested within the `template` object in the body of the `POST` request.

```json
{
  “template”:{
    "metadata":{...},
    ...
  }
}
```

The following table lists and describes **optional** object parameters nested within the `metadata` object. The `metadata` object is nested within the mandatory `template` object. &#x20;

| Name          | Type   | Required | Description                                                      |
| ------------- | ------ | -------- | ---------------------------------------------------------------- |
| `lang`        | string | ❌ No     | The language code of the template (for example, `"en"`, `"fr"`). |
| `title`       | string | ❌ No     | The title of the template.                                       |
| `description` | string | ❌ No     | A short description of the template.                             |
| `subject`     | string | ❌ No     | The subject line of the email (if applicable).                   |
| `preheader`   | string | ❌ No     | The preheader text for the email (if applicable).                |

{% openapi src="../../.gitbook/assets/simple-to-full-json.yaml" path="/v1/{collection}/simple-to-full-json" method="post" %}
[simple-to-full-json.yaml](../../.gitbook/assets/simple-to-full-json.yaml)
{% endopenapi %}
