# Template Catalog API

{% hint style="info" %}
Access to this feature is available for purchase via your account manager. If you do not currently have an account manager, please contact our sales team for further details.
{% endhint %}

## Access the Template Catalog via API

This documentation aims to guide you in creating a personalized template catalog for your SaaS applications. Leveraging our API, you can seamlessly integrate a diverse range of email and page templates, promoting enhanced user engagement while optimizing the design process within your platform.

<figure><img src="../.gitbook/assets/image1 (2).png" alt=""><figcaption></figcaption></figure>

## Getting Started

### Access and Subscription

To start using the Template Catalog API, first activate your API key in the Beefree SDK Console. After activation, reach out to your dedicated Customer Success Manager (CSM) for further help and setup. Your CSM will guide you through the process and answer any questions you have.

For additional information, you can refer to [Content Services API key configuration](content-services-api-reference.md).

### Activating the API

Activate your API key through the Beefree SDK Console to begin using the Template Catalog API. Once your API key is activated, you can contact your dedicated Customer Success Manager (CSM) representative to request further assistance and enablement. They will be available to guide you through the process and address any additional inquiries.

### Endpoint and Authentication

To begin using the Template Catalog API, access it through the designated endpoint and authenticate all requests by including your API key. This API key is essential for proper authorization and security when interacting with the API.

The Template Catalog API uses API Keys to authenticate requests for resources.  You can manage your API Keys within the Developer Portal.  All requests must be made over HTTPS and contain the following HTTP Header:

```http

Authorization: Bearer {token}

```

### API Root

All API access is over HTTPS, and accessed from the following URL:

| API Root                                                          |
| ----------------------------------------------------------------- |
| `https://api.getbee.io/v1/catalog/templates/?{parameter}={value}` |

### Parameters

| Parameter          | Description                                             | Example        |
| ------------------ | ------------------------------------------------------- | -------------- |
| `search`           | List of terms to search, separated by comma             |                |
| `category`         | Filter by category slug                                 | small-business |
| `collection`       | Filter by collection slug                               | e-commerce     |
| `designer`         | Filter by designer slug                                 |                |
| `tag`              | Filter by tag name                                      |                |
| `template_type`    | Filter by template\_type. Choices are “email” or “page” |                |
| `pagesize`         | Set the item number per page                            | 20             |
| `published_after`  | Filter by published\_at after given date                | 2022-01-01     |
| `published_before` | Filter by published\_at before given date               | 2022-01-01     |

## API Features and Functionality

Our Template Catalog API provides the following essential features to enable seamless integration into your application:&#x20;

* Fetch templates from the Template Catalog API by applying filters like category, industry, etc.&#x20;
* Sort and customize templates to match your application’s requirements and user preferences.

### Fetch a list of all Templates

Retrieve a list of all the Templates within the catalog, applying filters based on request parameters.

You can execute a search by providing a series of terms within the ‘search’ request parameter. This search will operate on template title, description, category name, collection name, designer name, publication date (‘published\_at’), and tags.

The response will encompass a ‘facets’ field, outlining the count of existing Templates across each Category, Collections, Designers, and Tags fields and their sub-fields, considering any applied filters and searches.

The response is paginated, presenting 20 items per page by default. The ‘pagesize’ request parameter enables control over the page size.

#### Sample Request

```markup

GET /v1/catalog/templates/?search=music HTTP/1.1
Host: api.getbee.io
Content-Type: application/json
Authorization: Bearer •••••••

```

#### Sample Response

```json

{
  "count": 1592,
  "next": "https://api.getbee.io/v1/catalog/templates?page=2",
  "previous": null,
  "results": [
      {template_1},
      {template_2},
      ...
      {template_N},
      ...
      {template_20}
      ],
  "facets": }"categories": 		category_1,
		       ...
		      category_N
        ],
        "collections": [
               collection_1,
	           ...
	           collection_N
        ],
        "designers": [
              designer_1,
	          ...
	          designer_N
        ],
        "tags" :[
               tag_1,
               ...
              tag_n
        ]
}

```

### Fetch a single Template

Dive into the details of making API requests to fetch a single template identified by its slug (in the URL).

#### Sample Request

```http

GET /v1/catalog/templates/mens-fashion HTTP/1.1
Host: api.getbee.io
Content-Type: application/json
Authorization: Bearer •••••••

```

#### Sample Response

```json

{
"categories": [
		"product-promotion",
		"fashion"
	],
	"collections": "",
	"description": "Mens Fashion Template for marketing",
	"designer": {
		"avatar_url": https://cloudfront.net/designers/team.jpg",
		"description": "Bee Designers Team",
		"display_name": "BEE Team",
		"id": "bee-team",
	},
	"html_data":"........"
	"html_url": "https://cloudfront.net/templates/default/3.html",
	"id": "mens-fashion",
	"is_blank": false,
	"json_data": {
		"page": {body": {
			"container": {...}
		.....
	}
"order": "00760",
"published_at": "2017-08-28",
"tags": [
	"blue",
	"light",
	"light blue",
	"sans serif",
	"sell",
	"two-column"
],
"template_type": "email",
"thumbnail_large": "https://cloudfront.net/templates/default/3_l.jpg",
"thumbnail": "https://cloudfront.net/templates/default/3.jpg",
"title": "Men's Fashion"
}

```

### Fetch a list of all Categories

You can extract a list of all the Categories present within the catalog. This comprehensive list includes all categories under which templates are classified.

The response that you receive is paginated for ease of reading and navigation. It displays 200 items per page by default, providing a comprehensive view of the catalog content.

However, if you wish to adjust the number of items shown on each page, you can use the ‘pagesize’ request parameter.

#### Sample Request

```http

GET /v1/catalog/categories?search=fashion / HTTP/1.1
Host: api.getbee.io
Content-Type: application/json
Authorization: Bearer •••••••

```

#### Sample Response

```json

{
   "count": 114,
   "next": null,
   "previous": null,
   "results": [
		category_1,
        category_2,
        ....
        category_N,
        ....
       category_200
   ]	
}

```

### Fetch a single Category

Retrieve detailed information about a specific Category using its unique identifier, or slug, which can be found in the URL. This method allows you to access in-depth data related to that particular category, such as its associated templates and related metadata.

#### Sample Request

```http

GET /v1/catalog/categories/fashion-week / HTTP/1.1
Host: api.getbee.io
Content-Type: application/json
Authorization: Bearer •••••••

```

#### Sample Response

```json

{
	"bg_color": "#F8F8F8",
	"fb_color": "#333A45",
	"highlighted": false,
	"icon": null,
	"id": "fashion-week",
	"image": null,
	"name": "Fashion Week",
	"description": "Category for Fashion Week dedicated templates",
	"parent": "seasonal"
}

```

### Fetch a List of Collections

You can pull up a full list of all Collections in the catalog. Collections are groups of templates with similar attributes or purposes. This overview can help you understand the types of template groupings available.

The response will be paginated, with 200 items per page default for easy navigation. However, you can change this default by adjusting the ‘pagesize’ request parameter to suit your viewing preferences.

#### Sample Request

```http

GET /v1/catalog/collections?pagesize=10/ HTTP/1.1
Host: api.getbee.io
Content-Type: application/json
Authorization: Bearer •••••••

```

#### Sample Response

```json

{
   "count": 19,
   "next": https://api.getbee.io/v1/catalog/collections?page=2&pagesize=10",
   "previous": null,
   "results": [
		  collection_1,
          collection_2,
          ....
          collection_N,
          ....
          collection_10
   ]
}

```

### Fetch a single Collection

Access a specific Collection using its unique slug found in the URL. This lets you view detailed information about this particular group of templates, including its associated templates and any related details.

#### Sample Request

```http

GET /v1/catalog/collections/music / HTTP/1.1
Host: api.getbee.io
Content-Type: application/json
Authorization: Bearer •••••••

```

#### Sample Response

```json

{
	"bg_color": "#76D3BA",
	"description": "Music Collection Descriptiom",
	"fg_color": "#262626",
	"highlighted": false,
	"icon_url": "https://cloudfront.net/collections/music_icon.svg",
	"id": "music",
	"image_url": "https://cloudfront.net/collections/music.png",
	"name": "Music",
	"order": "0"
}

```

### Fetch a list of all Designers

Access a complete list of all Designers in the catalog.

The response is paginated, with a standard display of 200 items per page. You can manipulate the ‘pagesize’ request parameter to control the number of items shown per page.

#### Sample Request

```http

GET /v1/catalog/designers/?pagesize=int HTTP/1.1
Host: api.getbee.io
Content-Type: application/json
Authorization: Bearer •••••••

```

### Fetch a single Designer

Retrieve detailed information for a specific Designer, identified by the unique slug present in the URL. This enables the procurement of comprehensive data pertaining to the particular designer, including their portfolio of templates and any associated metadata within the catalog.

#### Sample Request

```http

GET /v1/catalog/designers/:slug/ HTTP/1.1
Host: api.getbee.io
Content-Type: application/json
Authorization: Bearer •••••••

```

### Fetch a list of all Tags

Retrieve a full list of all the Tags in the catalog. Tags are keywords tied to templates, helping you find and sort templates based on certain themes or attributes.

#### Sample Request

```http

GET /v1/catalog/tags/?pagesize=int HTTP/1.1
Host: api.getbee.io
Content-Type: application/json
Authorization: Bearer •••••••

```

## Best Practices

To enhance the performance and user experience of your template catalog, we recommend following these best practices.

## Optimize API Usage

Implement caching mechanisms to reduce API calls and minimize user loading times. Template data do not change often, so you can use a cache TTL of some minutes (10 for example, but even more) without issues.

## Rate Limits

Handle errors gracefully and provide clear error messages to assist in resolving any issues.\
These endpoints have the following rate limits:

* Per minute: 500 requests;
* Per second:  100 requests.

Therefore, we recommend not enforcing excessive automatic tries when you get an error message, otherwise, you may exceed the limit and won’t be able to proceed with more requests.

## Status Codes

The API is a read-only API. The only method is GET, so there are only a few possible errors. The main status codes are:

| Code | Message               |
| ---- | --------------------- |
| 200  | OK                    |
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 404  | Not Found             |
| 500  | Internal Server Error |

## FAQs

Find answers to common queries related to the Template Catalog API, its features, and integration.

#### Do I need to pay extra for new templates?

No, they are included in your subscription. The catalog will be updated with the latest trends at no extra charge.

#### How frequently are new templates available?

We are committed to making fresh new templates available every quarter.

#### Where are the image and media assets stored?

Storing the JSON Template source file is totally in your control, the media assets referenced inside the template are kept in the Beefree SDK S3 Bucket and provisioned using the our CDN.

#### Do the API calls made to the Template Catalog contribute to the total CSAPI count?

No, API calls made to the Template Catalog do not contribute to the total CSAPI count.
