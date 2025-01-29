# Template Catalog API

{% hint style="info" %}
This feature is available for purchase with the Core plan and included at no extra cost with the [Superpowers and Enterprise plans](https://developers.beefree.io/pricing-plans). To purchase this feature with the Core plan, or to activate it for free with the Superpowers or Enterprise plans, please reach out to your account manager. If you don’t have an account manager, contact our sales team for more information.
{% endhint %}

## Overview of Template Catalog API

In this Template Catalog Reference, you will learn more about a personalized template catalog for your SaaS applications. Through this API, you can integrate a diverse range of email and page templates, promoting enhanced user engagement while optimizing the design process within your platform.

<figure><img src="../.gitbook/assets/image1 (2).png" alt=""><figcaption></figcaption></figure>

## Getting Started

Learn more about how to get started with the Template Catalog API in this section.

### Access and Subscription

To start using the Template Catalog API, first activate your API key in the Beefree SDK Console. After activation, reach out to your dedicated Customer Success Manager (CSM) for further help and setup. Your CSM will guide you through the process and answer any questions you have.

For additional information, you can refer to [Content Services API key configuration](content-services-api/content-services-api-reference.md).

### Activating the API

Activate your API key through the Beefree SDK Console to begin using the Template Catalog API. Once your API key is activated, you can contact your dedicated Customer Success Manager (CSM) representative to request further assistance and enablement. They will be available to guide you through the process and address any additional inquiries.

### Endpoint and Authentication

To begin using the Template Catalog API, access it through the designated endpoint and authenticate all requests by including your API key. This API key is essential for proper authorization and security when interacting with the API.

The Template Catalog API uses API Keys to authenticate requests for resources.  You can manage your API Keys within the Developer Portal.  All requests must be made over HTTPS and contain the following HTTP Header:

```http

Authorization: Bearer {token}

```

### Base URL

All API access is over HTTPS, and accessed from the following URL:

| Base URL                                                          |
| ----------------------------------------------------------------- |
| `https://api.getbee.io/v1/catalog/templates/?{parameter}={value}` |

## API Features and Functionality

Our Template Catalog API provides the following essential features to enable seamless integration into your application:&#x20;

* Fetch templates from the Template Catalog API by applying filters like category, industry, etc.&#x20;
* Sort and customize templates to match your application’s requirements and user preferences.

### Best Practices

To enhance the performance and user experience of your template catalog, we recommend following these best practices.

## Optimize API Usage

Implement caching mechanisms to reduce API calls and minimize user loading times. Template data do not change often, so you can use a cache TTL of some minutes (10 for example, but even more) without issues.

## Rate Limits

Handle errors gracefully and provide clear error messages to assist in resolving any issues.\
These endpoints have the following rate limits:

* Per minute: 500 requests;
* Per second:  100 requests.

Therefore, we recommend not enforcing excessive automatic tries when you get an error message, otherwise, you may exceed the limit and won’t be able to proceed with more requests.

The API is a read-only API. The only method is `GET`.

## HTTP Status Code Errors

The main HTTP status code errors are:

* `200 OK` - The request has succeeded. The client can read the result of the request in the body and the headers of the response.
* `400 Bad Request` - The server could not understand the request due to invalid syntax.
* `401 Unauthorized` - The client must authenticate itself to get the requested response.
* `403 Forbidden` - The client does not have access rights to the content; the server is refusing to give the requested resource. Unlike 401, the client's identity is known to the server.
* `404 Not Found` - The server can not find the requested resource. In the context of an API, this can mean that the endpoint is valid but the resource itself does not exist.
* `429 Too Many Requests` - The user has sent too many requests in a given amount of time which has led to throttling their request until the window resets.
* `500 Internal Server Error` - The server has encountered a situation it doesn't know how to handle.
* `503 Service Unavailable` - The server is not ready to handle the request. Common causes are a server that is down for maintenance or that is overloaded.

## Headers

The following table displays the headers you need to complete your API request.

<table><thead><tr><th width="358">Key</th><th>Value</th></tr></thead><tbody><tr><td>Content-type</td><td>application/json</td></tr><tr><td>Authorization</td><td>Bearer{{key}}</td></tr></tbody></table>

## Get a list of all Templates

`/v1/catalog/templates`

**HTTP Method:** `GET`

**Description:** Retrieve a list of all the Templates within the catalog, applying filters based on request parameters.

You can execute a search by providing a series of terms within the ‘search’ request parameter. This search will operate on template title, description, category name, collection name, designer name, publication date (‘published\_at’), and tags.

The response will encompass a ‘facets’ field, outlining the count of existing Templates across each Category, Collections, Designers, and Tags fields and their sub-fields, considering any applied filters and searches.

The response is paginated, presenting 20 items per page by default. The ‘pagesize’ request parameter enables control over the page size.

### Request Parameters

The following table displays a list of request parameters.

| Parameter          | Example                 | Description                                              |
| ------------------ | ----------------------- | -------------------------------------------------------- |
| `search`           | activity, beach, summer | List of terms to search, separated by comma              |
| `category`         | small-business          | Filter by category slug                                  |
| `collection`       | e-commerce              | Filter by collection slug                                |
| `designer`         | bee-team                | Filter by designer slug                                  |
| `tag`              | activity, beach, summer | Filter by tag name                                       |
| `template_type`    | email                   | Filter by template\_type. Choiches are "email" or "page" |
| `pagesize`         | 20                      | Set the item number per page                             |
| `published_after`  | 2023-01-01              | Filter by published\_at after given date                 |
| `published_before` | 2023-01-01              | Filter by published\_at before given date                |

{% swagger src="../.gitbook/assets/catalog-templates.yaml" path="/v1/catalog/templates" method="get" %}
[catalog-templates.yaml](../.gitbook/assets/catalog-templates.yaml)
{% endswagger %}

## Fetch a single Template

`/v1/catalog/templates/:slug`

**HTTP Method:** `GET`

**Description:** Fetch a single template identified by its slug (in the URL).

{% swagger src="../.gitbook/assets/catalog-templates-slug.yaml" path="/v1/catalog/templates/:slug" method="get" %}
[catalog-templates-slug.yaml](../.gitbook/assets/catalog-templates-slug.yaml)
{% endswagger %}

## Fetch a list of all Categories

`/v1/catalog/categories`

**HTTP Method:** `GET`

**Description:** Retrieve a list of all the Templates within the catalog, applying filters based on request parameters.

You can extract a list of all the Categories present within the catalog. This comprehensive list includes all categories under which templates are classified.

The response that you receive is paginated for ease of reading and navigation. It displays 200 items per page by default, providing a comprehensive view of the catalog content.

However, if you wish to adjust the number of items shown on each page, you can use the ‘pagesize’ request parameter.

### Request Parameters

The following table displays request parameters.

| Parameter  | Value | Description                  |
| ---------- | ----- | ---------------------------- |
| `pagesize` | int   | Set the item number per page |

{% swagger src="../.gitbook/assets/catalog-categories.yaml" path="/v1/catalog/categories" method="get" %}
[catalog-categories.yaml](../.gitbook/assets/catalog-categories.yaml)
{% endswagger %}

## Fetch a single Category

`/v1/catalog/categories/:slug`

**HTTP Method:** `GET`

**Description:** Retrieve a list of all the Templates within the catalog, applying filters based on request parameters.

Retrieve detailed information about a specific Category using its unique identifier, or slug, which can be found in the URL. This method allows you to access in-depth data related to that particular category, such as its associated templates and related metadata.

{% swagger src="../.gitbook/assets/catalog-categories-slug.yaml" path="/v1/catalog/categories/:slug" method="get" %}
[catalog-categories-slug.yaml](../.gitbook/assets/catalog-categories-slug.yaml)
{% endswagger %}

## Fetch a List of Collections

`/v1/catalog/collections`

**HTTP Method:** `GET`

**Description:** You can pull up a full list of all Collections in the catalog. Collections are groups of templates with similar attributes or purposes. This overview can help you understand the types of template groupings available.

The response will be paginated, with 200 items per page default for easy navigation. However, you can change this default by adjusting the ‘pagesize’ request parameter to suit your viewing preferences.

### Request Parameters

The following table displays request parameters.

| Parameter  | Value | Description                  |
| ---------- | ----- | ---------------------------- |
| `pagesize` | int   | Set the item number per page |

{% swagger src="../.gitbook/assets/catalog-collections.yaml" path="/v1/catalog/collections" method="get" %}
[catalog-collections.yaml](../.gitbook/assets/catalog-collections.yaml)
{% endswagger %}

## Fetch a single Collection

`/v1/catalog/collections/:slug`

**HTTP Method:** `GET`

**Description:** Access a specific Collection using its unique slug found in the URL. This lets you view detailed information about this particular group of templates, including its associated templates and any related details.

{% swagger src="../.gitbook/assets/catalog-collections-slug.yaml" path="/v1/catalog/collections/:slug" method="get" %}
[catalog-collections-slug.yaml](../.gitbook/assets/catalog-collections-slug.yaml)
{% endswagger %}

## Fetch a list of all Designers

`/v1/catalog/designers`

**HTTP Method:** `GET`

**Description:** Access a complete list of all Designers in the catalog.

The response is paginated, with a standard display of 200 items per page. You can manipulate the ‘pagesize’ request parameter to control the number of items shown per page.

### Request Parameters

The following table displays request parameters.

| Parameter  | Value | Description                  |
| ---------- | ----- | ---------------------------- |
| `pagesize` | int   | Set the item number per page |

{% swagger src="../.gitbook/assets/catalog-designers.yaml" path="/v1/catalog/designers" method="get" %}
[catalog-designers.yaml](../.gitbook/assets/catalog-designers.yaml)
{% endswagger %}

## Fetch a single Designer

`/v1/catalog/designers/:slug`

**HTTP Method:** `GET`

**Description:** Retrieve detailed information for a specific Designer, identified by the unique slug present in the URL. This enables the procurement of comprehensive data pertaining to the particular designer, including their portfolio of templates and any associated metadata within the catalog.

{% swagger src="../.gitbook/assets/catalog-designers-slug.yaml" path="/v1/designers/:slug" method="get" %}
[catalog-designers-slug.yaml](../.gitbook/assets/catalog-designers-slug.yaml)
{% endswagger %}

## Fetch a list of all Tags

`/v1/catalog/tags`

**HTTP Method:** `GET`

**Description:** Retrieve a full list of all the Tags in the catalog. Tags are keywords tied to templates, helping you find and sort templates based on certain themes or attributes.

### Request Parameters

The following table displays request parameters.

| Parameter  | Value | Description                  |
| ---------- | ----- | ---------------------------- |
| `pagesize` | int   | Set the item number per page |

{% swagger src="../.gitbook/assets/catalog-tags.yaml" path="/v1/catalog/tags" method="get" %}
[catalog-tags.yaml](../.gitbook/assets/catalog-tags.yaml)
{% endswagger %}

### FAQs

Find answers to common queries related to the Template Catalog API, its features, and integration.

#### Do I need to pay extra for new templates?

No, they are included in your subscription. The catalog will be updated with the latest trends at no extra charge.

#### How frequently are new templates available?

We are committed to making fresh new templates available every quarter.

#### Where are the image and media assets stored?

Storing the JSON Template source file is totally in your control, the media assets referenced inside the template are kept in the Beefree SDK S3 Bucket and provisioned using the CDN.

#### Do the API calls made to the Template Catalog contribute to the total CSAPI count?

No, API calls made to the Template Catalog do not contribute to the total CSAPI count.
