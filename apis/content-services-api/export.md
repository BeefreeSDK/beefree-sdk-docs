---
description: >-
  This page lists and describes the Export category of endpoints within the
  Content Services API. It also includes interactive testing environments for
  each endpoint in this category.
---

# Export

{% hint style="info" %}
Export endpoints are part of the [Content Services API](./). The Content Services API is available on [Beefree SDK plans that are Essentials or above](https://developers.beefree.io/pricing-plans).
{% endhint %}

## Overview

The Export category is one of the most common uses of the Content Services API. After creating a design in the no-code builder, end users often need to export and share it. These endpoints let you offer multiple export options—including HTML, plain text, PDF, and image formats—so your users can easily distribute their finished designs.

### Available Collection Values for Export Endpoints

The following table lists the collection values available in this category of endpoints, and their corresponding collection options.

Prior to referencing the table, the following example shows how you can replace the **{collection}** placeholder based on the type of content you'd like to export.

#### How to Replace the {collection} Placeholder

The following example URL has a **{collection}** placeholder. This placeholder needs to be filled in with a **Collection Option** prior to making an API call.

`https://api.getbee.io/v1/{collection}/html`

As an example, if you'd like to export an email's HTML using this endpoint, replace **{collection}** with **message**.

The final URL to make the API call will be:

`https://api.getbee.io/v1/message/html`

The following table provides a comprehensive reference of all available options based on what you'd like to export.

| Resource      | Collection Options                                                                                                       |
| ------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `/html`       | <ul><li><code>/message</code></li><li><code>/page</code></li><li><code>/popup</code></li><li><code>/amp</code></li></ul> |
| `/plain-text` | <ul><li><code>/message</code></li></ul>                                                                                  |
| `/pdf`        | <ul><li><code>/message</code></li></ul><ul><li><code>/page</code></li></ul>                                              |
| `/image`      | <ul><li><code>/message</code></li></ul><ul><li><code>/page</code></li></ul>                                              |

## HTML <a href="#html" id="html"></a>

**URL:** `https://api.getbee.io/v1/{collection}/html`

This endpoint allows you to retrieve the full or partial HTML output of a template (email, page, or popup).

{% hint style="info" %}
**Important:** `collection` is a placeholder within the URL. This placeholder can be replaces with any of the `collection` options available for the HTML resource. Reference the [Export Resource and Collection Options table](./#export) for a list of available option.
{% endhint %}

#### How It Works

To generate HTML from a template's JSON:

1. Capture or store the latest JSON output from the builder using [callbacks](../../getting-started/readme/installation/methods-and-events.md) such as `onChange` or `autosave`.
2. Send this JSON payload to the HTML endpoint.
3. Receive the HTML string as the response.

#### Required Request Payload

```json
{
  "page": {
    "body": { ... },
    ...
  }
}
```

* `page` (object, required): The full template structure in Beefree JSON format. This is the same structure returned by the builder or captured from its callbacks.

#### Notes

* This endpoint bypasses the need for the `onSave` callback and can be used at any time post-editing.
* Partial HTML rendering is also supported for specific components or modules (if required by your use case).
* The output HTML reflects the current rendering engine used by Beefree, ensuring up-to-date compatibility.

{% openapi src="../../.gitbook/assets/html_endpoint.yaml" path="/v1/{collection}/html" method="post" %}
[html_endpoint.yaml](../../.gitbook/assets/html_endpoint.yaml)
{% endopenapi %}

## Plain Text

**URL:** `https://api.getbee.io/v1/{collection}/html`

This endpoint allows you to retrieve the full or partial HTML output of a template (email, page, or popup).

{% hint style="info" %}
**Important:** `collection` is a placeholder within the URL. This placeholder can be replaces with any of the `collection` options available for the Plain Text resource. Reference the [Export Resource and Collection Options table](./#export) for a list of available option.
{% endhint %}

#### How It Works

To generate plain text from a template's JSON:

1. Capture or store the latest JSON output from the builder using [callbacks](../../getting-started/readme/installation/methods-and-events.md) such as `onChange` or `autosave`.
2. Send this JSON payload to the `/plain-text` endpoint.
3. Receive the plain text as the response.

{% openapi src="../../.gitbook/assets/plain_text_endpoint.yaml" path="/v1/{collection}/plain-text" method="post" %}
[plain_text_endpoint.yaml](../../.gitbook/assets/plain_text_endpoint.yaml)
{% endopenapi %}

## PDF <a href="#pdf" id="pdf"></a>

**URL:** `https://api.getbee.io/v1/{collection}/pdf`

You can generate a PDF file from valid HTML content using the dedicated PDF generation endpoint. This operation requires a JSON payload with specific fields to configure the output.

{% hint style="info" %}
**Important:** `collection` is a placeholder within the URL. This placeholder can be replaces with any of the `collection` options available for the PDF resource. Reference the [Export Resource and Collection Options table](./#export) for a list of available option.
{% endhint %}

#### Required Request Payload

```json
{
  "page_size": "Full",
  "page_orientation": "landscape",
  "html": "<!DOCTYPE html>...</html>"
}
```

**Field Descriptions**

* **`html`** (string, required): The full HTML content to convert to a PDF. You can obtain the HTML output of a template by calling the [`/html` endpoint](export.md#html) and copying its response into this field.
* **`page_orientation`** (string, required): Sets the orientation of the generated PDF pages.\
  Accepted values:
  * `"portrait"`: vertical layout.
  * `"landscape"`: horizontal layout.
* **`page_size`** (string, required): Defines the dimensions of the PDF output.\
  Accepted values:
  * `"Letter"`: US Letter format.
  * `"A4"`: A4 paper size.
  * `"A3"`: A3 paper size.
  * `"Full"`: a single continuous page with fixed width (900px) and height determined proportionally to the content.

{% hint style="warning" %}
When using `"Letter"`, `"A4"`, or `"A3"`, the content is automatically split across multiple pages.\
Using `"Full"` produces a single, unpaginated scrollable PDF.
{% endhint %}

#### Steps to generate a PDF

To generate a PDF from a template:

1. Call the `/html` endpoint to retrieve the template's HTML.
2. Insert that HTML into the `"html"` field of the request payload.
3. Set your preferred `"page_orientation"` and `"page_size"`.
4. Send the payload to the PDF generation endpoint.

{% openapi src="../../.gitbook/assets/pdf_endpoint.yaml" path="/v1/{collection}/pdf" method="post" %}
[pdf_endpoint.yaml](../../.gitbook/assets/pdf_endpoint.yaml)
{% endopenapi %}

{% hint style="info" %}
**Note:** The response is a JSON string that will contain the URL of the temporary location of the PDF document. The file is available for 24 hours.
{% endhint %}

## Image <a href="#image" id="image"></a>

**URL:** `https://api.getbee.io/v1/{collection}/image`

This endpoint allows you to generate an image file (for example, PNG) from a template's HTML. You can control the image output by specifying the dimensions.

{% hint style="info" %}
**Important:** `collection` is a placeholder within the URL. This placeholder can be replaces with any of the `collection` options available for the Image resource. Reference the [Export Resource and Collection Options table](./#export) for a list of available option.
{% endhint %}

#### Required Request Payload

```json
{
  "html": "<!DOCTYPE html>...</html>",
  "width": 800,
  "height": 600
}
```

{% hint style="info" %}
Note: As an alternative to providing `width` and `height`, you can also provide `size`.
{% endhint %}

#### Rendering

The HTML is rendered using a fixed-size browser window to simulate a real-world preview. Here are the key rendering parameters:

* **Window Size**: `1920 x 1080` pixels (used for clipping/screenshot area)
* **Default Viewports**:
  * Mobile: `320px` width
  * Desktop: `1024px` width
* **Clipping Region**: defaults to `1920 x 1080` pixels
* **Scale Factor**: Automatically calculated to match viewport and clipping dimensions.

You may override the clipping size if your layout requires a custom viewport. If your content exceeds the clipping area, it may be cropped. For improved results, using auto height with the size parameter is recommended.

#### Steps to perform an Image API call

1. Use the [`/html` endpoint](export.md#html) to generate the HTML version of your template.
2. Set the `html` field in your image request payload to the HTML generated.
3. Provide a `width` and `height` values, or a `size` value.
4. Send the payload to the image endpoint.

| Name         | Type    | Description                                                                                                                                                                                                                                                                                                                        |
| ------------ | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| html\*       | String  | A Beefree HTML message.                                                                                                                                                                                                                                                                                                            |
| size         | String  | Use “size” instead of “width” and “height” when you only know the width and want the height automatically calculated. **Required** if width and height are not defined.                                                                                                                                                            |
| width        | Integer | The image width in pixels. **Required** if size is not defined.                                                                                                                                                                                                                                                                    |
| height       | Integer | The image height in pixels. Default applies a proportional value based on the given width, keeping the image aspect ratio. When the value is not proportional to the given width, either will occur: If it’s higher, the proportional value applies, or, if it’s lower, the image is cropped. **Required** if size is not defined. |
| file\_type\* | String  | Accepts jpg or png.                                                                                                                                                                                                                                                                                                                |

{% openapi-operation spec="image-endpoint" path="/v1/{collection}/image" method="post" %}
[OpenAPI image-endpoint](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/9ef1477fd159d69dd4d46a9bcb0a071ad5b3a925ff92efcaebcdfc0c8a935c47.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250910%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250910T191642Z&X-Amz-Expires=172800&X-Amz-Signature=b14e3221374a431cfce7e127503d0903094805532469bff688d2a14a40c43b84&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
