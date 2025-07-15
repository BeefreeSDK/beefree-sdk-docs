---
description: >-
  This page lists and describes the Convert category of endpoints within the
  Content Services API. It also includes interactive testing environments for
  each endpoint in this category.
---

# Convert

## Conversion Collection

The Conversion Collection provides you with endpoints that enable you to convert templates from one format to another. With the [Email to Page](convert.md#email-to-page-conversion-important-behaviors) endpoint, you can easily convert your email JSON templates into page JSON. The [Page to Email](convert.md#page-to-email-conversion-important-behaviors) endpoint lets you turn your page JSON templates into email-ready JSON, with the option to disable the HTML sanitizer if needed. The Simple to Full JSON endpoint enables you to convert [Simple Schema](../../data-structures/simple-schema/) templates into full Beefree JSON templates that can be loaded in the builder.

{% hint style="info" %}
**Important:** For all endpoints in this category, the value for `collection` is `conversion`. When making API calls, replace the `collection` placeholder within the URL with `conversion` to execute the call.
{% endhint %}

## Email to Page Conversion: Important Behaviors

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

## Page to Email Conversion: Important Behaviors

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

## Simple to Full JSON

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

| Name       | Type   | Required | Description                                                                                                                                                                                 |
| ---------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`     | String | ✅ Yes    | Specifies the template type. Possible values include: `email`, `page`, `popup`.                                                                                                             |
| `rows`     | Array  | ✅ Yes    | Array containing at least one row. Reference the [simple row schema](https://github.com/mailupinc/simple-schema-beefree-sdk/blob/main/simple_row.schema.json).                              |
| `settings` | Object | ❌ No     | Configuration settings. Reference the [Settings Object Parameters](convert.md#settings-object-parameters-request-greater-than-template-greater-than-settings) section for more information. |
| `metadata` | Object | ❌ No     | Metadata information. Reference the [Metadata Object Parameters section](convert.md#metadata-object-parameters-request-greater-than-template-greater-than-metadata) for more information.   |

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

{% openapi-operation spec="simple-to-full-json" path="/v1/{collection}/simple-to-full-json" method="post" %}
[OpenAPI simple-to-full-json](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/9cfe21ce15319f492d5c8677e6dceace21a4991dc1a3965f3f56d170861800aa.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250715%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250715T222648Z&X-Amz-Expires=172800&X-Amz-Signature=b219ad141fbc3cfdb731133c4e839f7b4f6f716ca299fc68e9cdae93971bbbe6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
