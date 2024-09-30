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

<figure><img src="../../.gitbook/assets/CSAPI_in_dev_portal.png" alt=""><figcaption></figcaption></figure>

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

| Collection  | Available Resources                                   |
| ----------- | ----------------------------------------------------- |
| `/message`  | `html`, `pdf`, `images`, `merge`, `index, plain-text` |
| `/page`     | `html`, `pdf`, `images`, `merge`, `index`             |
| `/popup`    | `html`                                                |
| `/amp`      | `html`                                                |
| `/template` | `brand`                                               |
| `/ai`       | `metadata`, `sms`, `summary`                          |

### Example URLs

The following table provides a few examples of URLs you can use to make specific types of requests.

<table><thead><tr><th width="160">Type</th><th>Action</th><th>Example URL</th></tr></thead><tbody><tr><td>Email</td><td>Request HTML for email</td><td><code>https://api.getbee.io/v1/message/html</code></td></tr><tr><td>Landing Page</td><td>Request HTML for a landing page</td><td><code>https://api.getbee.io/v1/page/html</code></td></tr><tr><td>Popup</td><td>Request HTML for a popup</td><td><code>https://api.getbee.io/v1/popup/html</code></td></tr><tr><td>AMP</td><td>Request HTML for AMP</td><td><code>https://api.getbee.io/v1/amp/html</code></td></tr></tbody></table>

## Resources

The following section provides detailed information for each of the resources associated with each collection mentioned in the previous section.

### HTML <a href="#html" id="html"></a>

**URL:** `https://api.getbee.io/v1/{collection}/html`

{% swagger src="../../.gitbook/assets/html_endpoint.yaml" path="/v1/{collection}/html" method="post" %}
[html_endpoint.yaml](../../.gitbook/assets/html_endpoint.yaml)
{% endswagger %}

### Plain Text

**Endpoint:** `/message/plain-text`

{% swagger src="../../.gitbook/assets/plain_text_endpoint.yaml" path="/v1/message/plain-text" method="post" %}
[plain_text_endpoint.yaml](../../.gitbook/assets/plain_text_endpoint.yaml)
{% endswagger %}

### PDF <a href="#pdf" id="pdf"></a>

**URL:** `https://api.getbee.io/v1/{collection}/pdf`

{% swagger src="../../.gitbook/assets/pdf_endpoint.yaml" path="/v1/{collection}/pdf" method="post" %}
[pdf_endpoint.yaml](../../.gitbook/assets/pdf_endpoint.yaml)
{% endswagger %}

{% hint style="info" %}
**Note:** The response is a JSON string that will contain the URL of the temporary location of the PDF document. The file is available for 24 hours.
{% endhint %}

### Image <a href="#image" id="image"></a>

**URL:** `https://api.getbee.io/v1/{collection}/image`

{% swagger src="../../.gitbook/assets/image_endpoint.yaml" path="/v1/{collection}/image" method="post" %}
[image_endpoint.yaml](../../.gitbook/assets/image_endpoint.yaml)
{% endswagger %}

### Merge <a href="#merge" id="merge"></a>

**URL:** `https://api.getbee.io/v1/{collection}/merge`

{% swagger src="../../.gitbook/assets/merge_endpoint.yaml" path="/v1/{collection}/merge" method="post" %}
[merge_endpoint.yaml](../../.gitbook/assets/merge_endpoint.yaml)
{% endswagger %}

### Merge Rows <a href="#merge" id="merge"></a>

**URL:** `https://api.getbee.io/v1/{collection}/merge-rows`

{% swagger src="../../.gitbook/assets/merge_rows_endpoint.yaml" path="/v1/{collection}/merge-rows" method="post" %}
[merge_rows_endpoint.yaml](../../.gitbook/assets/merge_rows_endpoint.yaml)
{% endswagger %}

{% hint style="info" %}
When utilizing this feature, it's important to consider adding a handle to the metadata. This handle serves a crucial role in functions such as `onDeleteRow` and `onEditRow`. In our provided example, we use a handle named `guid`. However, users have the flexibility to choose their own handle name according to their preferences and requirements. When selecting a handle name, we recommend you choose something descriptive and meaningful for ease of identification and management within your workflow.
{% endhint %}

### Synced Rows <a href="#merge" id="merge"></a>

**URL:** `https://api.getbee.io/v1/{collection}/synced-rows`

{% swagger src="../../.gitbook/assets/synced_rows_endpoint.yaml" path="/v1/{collection}/synced-rows" method="post" %}
[synced_rows_endpoint.yaml](../../.gitbook/assets/synced_rows_endpoint.yaml)
{% endswagger %}

### Index <a href="#index" id="index"></a>

**URL:** `https://api.getbee.io/v1/{collection}/merge/index`

{% swagger src="../../.gitbook/assets/merge_index_endpoint.yaml" path="/v1/{collection}/merge/index" method="post" %}
[merge_index_endpoint.yaml](../../.gitbook/assets/merge_index_endpoint.yaml)
{% endswagger %}

### AI Collection

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

{% swagger src="../../.gitbook/assets/metadata_endpoint.yaml" path="/v1/ai/metadata" method="post" %}
[metadata_endpoint.yaml](../../.gitbook/assets/metadata_endpoint.yaml)
{% endswagger %}

### SMS <a href="#sms" id="sms"></a>

`v1/ai/sms`

{% swagger src="../../.gitbook/assets/sms_endpoint.yaml" path="/v1/ai/sms" method="post" %}
[sms_endpoint.yaml](../../.gitbook/assets/sms_endpoint.yaml)
{% endswagger %}

### Summary

`v1/ai/summary`

{% swagger src="../../.gitbook/assets/summary_endpoint.yaml" path="/v1/ai/summary" method="post" %}
[summary_endpoint.yaml](../../.gitbook/assets/summary_endpoint.yaml)
{% endswagger %}
