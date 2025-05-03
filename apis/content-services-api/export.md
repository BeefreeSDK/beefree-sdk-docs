---
description: >-
  This page lists and describes the Export category of endpoints within the
  Content Services API. It also includes interactive testing environments for
  each endpoint in this category.
---

# Export

## HTML <a href="#html" id="html"></a>

**URL:** `https://api.getbee.io/v1/{collection}/html`

This endpoint allows you to retrieve the full or partial HTML output of a template (email, page, or popup).

#### How It Works

To generate the HTML from a message JSON:

1. Capture or store the latest JSON output from the builder using callbacks such as `onChange` or `autosave`.
2. Send this JSON payload to the HTML generation endpoint.
3. Receive an HTML string as the response.

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

**Endpoint:** `/message/plain-text`

{% openapi src="../../.gitbook/assets/plain_text_endpoint.yaml" path="/v1/{collection}/plain-text" method="post" %}
[plain_text_endpoint.yaml](../../.gitbook/assets/plain_text_endpoint.yaml)
{% endopenapi %}

## PDF <a href="#pdf" id="pdf"></a>

**URL:** `https://api.getbee.io/v1/{collection}/pdf`

You can generate a PDF file from valid HTML content using the dedicated PDF generation endpoint. This operation requires a JSON payload with specific fields to configure the output.

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

1. Call the `/html` endpoint to retrieve the rendered HTML of the template.
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

This endpoint allows you to generate an image file (e.g., PNG) from a given HTML string. You can control the image output by specifying dimensions.

#### Required Request Payload

```json
{
  "html": "<!DOCTYPE html>...</html>",
  "width": 800,
  "height": 600
}
```

#### Rendering Environment

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

{% openapi src="../../.gitbook/assets/image_endpoint.yaml" path="/v1/{collection}/image" method="post" %}
[image_endpoint.yaml](../../.gitbook/assets/image_endpoint.yaml)
{% endopenapi %}
