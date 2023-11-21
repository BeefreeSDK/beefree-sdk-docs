# Content Services API Reference

1. [API key](broken-reference)
2. [Authorization](broken-reference)
3. [Rate Limits](broken-reference)
4. [HTTP Headers](broken-reference)
5. [API Root](broken-reference)
6. [HTML](broken-reference)
7. [PDF](broken-reference)
8. [Image](broken-reference)
9. [Merge](broken-reference)
10. [Index](broken-reference)

### API key <a href="#api-key" id="api-key"></a>

To use the Content Services API you will need to obtain an API key. To do so:

1. Log into the [Beefree SDK Console](https://dam.beefree.io/devmain)
2. Locate the application that you wish to work with, and click on _Details_
3. Locate the Content Services API section and click on _Create New API Key_
4. Acknowledge the message that reminds you that if you exceed the [number of API calls included in your plan](https://dam.beefree.io/devmain), you may be charged for overages and click on _Create Key_
5. You’re done!

![](https://docs.beefree.io/wp-content/uploads/2020/03/CSAPI\_in\_dev\_portal.png)

The Content Services API uses API Keys to authenticate requests for resources.  You can manage your API Keys within the Beefree SDK Console.  All requests must be made over HTTPS and contain the following HTTP Header:\
**Authorization:** Bearer {token}

### Rate Limits <a href="#rate-limits" id="rate-limits"></a>

API requests rate limits exist independently of API key’s monthly usage allowance.

By default, the API has the following rate limits:

* **Per minute:** 500 requests
* **Per second:**  100 requests
* **X-Rate-Limit:** An integer representing the total number of requests available per cycle. Exceeding the limit per cycle results in a 429 error.  (e.g. 500)
* **X-Rate-Limit-Remaining:** An integer representing the number of remaining requests before the next cycle begins, and the count resets. (e.g. 100)
* **X-Rate-Limit-Reset:** A Unix timestamp representing the time the next cycle will begin, and the count will reset.
* **Retry-After:** A Unix timestamp representing the time the application may resume submitting requests.

### API Root <a href="#api-root" id="api-root"></a>

All API access is over HTTPS, and accessed from the following URL:\
https://api.getbee.io/{version}/{collection}/{resource}

**Versions**

| Version | Released on |
| ------- | ----------- |
| V1      | 4/25/2019   |
| Beta    | 4/06/2019   |

**Collections**

| Collection | Available Resources            |
| ---------- | ------------------------------ |
| /message   | html, pdf, images, merge,index |
| /page      | html, pdf, images, merge,index |
| /popup     | html                           |
| /amp       | html                           |

**Example URLs**

Request HTML for email:

https://api.getbee.io/v1/message/html

Request HTML for a landing page:

https://api.getbee.io/v1/page/html

Request HTML for a popup:

https://api.getbee.io/v1/popup/html

Request HTML for AMP:

https://api.getbee.io/v1/amp/html

**Structure**

| api.getbee.io |     |                                                                                                 |       | the api                                      |
| ------------- | --- | ----------------------------------------------------------------------------------------------- | ----- | -------------------------------------------- |
|               | /v1 |                                                                                                 |       | the version of the api                       |
|               |     | <ul><li>/message</li></ul><ul><li>/page</li></ul><ul><li>/popup</li></ul><ul><li>/amp</li></ul> |       | the collection of services                   |
|               |     |                                                                                                 | /html | the resource from the collection of services |

### Resources

#### HTML <a href="#html" id="html"></a>

**POST** /html

**Content-Type:** application/json

**Request**

**Parameters**

| **page**                | object  | required | A Beefree template in JSON format                        |
| ----------------------- | ------- | -------- | -------------------------------------------------------- |
| **beautifyHtmlEnabled** | boolean | required | This flag will force the API to return uncompressed HTML |

**Example**

```


{
  beautifyHtmlEnabled: false,
  page: {
     body: { ... },
     template: { ... },
     rows: { ... },
     title: '',
     description: ''
 }
}


```

**Response**

application/html

The HTML message

**Status Codes**

| 200 | OK                |
| --- | ----------------- |
| 400 | Bad Request       |
| 401 | Unauthorized      |
| 429 | Too many requests |
| 500 | Server error      |

#### PDF <a href="#pdf" id="pdf"></a>

**POST** /pdf

**Content-Type:** application/json

**Request**

**Parameters**

| **html**              | string | required | A full HTML document                                                                                                                                                                                                                  |
| --------------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **page\_size**        | string |          | <p>Accepted values:</p><ul><li>letter (default)</li><li>A4</li><li>A3</li><li>full</li></ul><p><strong>Full:</strong> a single page using 900px as page width. The page_orientation is always portrait when using this page size.</p> |
| **page\_orientation** | string |          | <p>Accepted values:</p><ul><li>landscape (default)</li><li>portrait</li></ul>                                                                                                                                                         |
| **file\_type**        | string |          | <p>Accepted values:</p><ul><li>pdf</li></ul>                                                                                                                                                                                          |

```


{"html":"a","file_type":"pdf","page_size":"full","page_orientation":"portrait"}


```

**Response**

application/json

A JSON string that will contain the URL of the temporary location of the PDF document.

The file is available for 24 hours.

```


{"statusCode":200,"body":{"url":"https:\/\/pro-bee-beepro-pdf.s3.amazonaws.com\/public\/pdf\/87ElCDpHHk.pdf","filename":"87ElCDpHHk.pdf","page_size":"full","page_orientation":"portrait","content_type":"application\/pdf"}}


```

**Status Codes**

| 200 | OK                |
| --- | ----------------- |
| 400 | Bad Request       |
| 401 | Unauthorized      |
| 429 | Too many requests |
| 500 | Server error      |

**Request**

**Parameters**

| **html**                | string  | required | A Beefree HTML message                                                                                                                 |
| ----------------------- | ------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **beautifyHtmlEnabled** | boolean | required | This flag will force the API to return uncompressed HTML. Both page and popup endpoints do not compress HTML so will ignore this flag. |

#### Image <a href="#image" id="image"></a>

**POST** /image

**Content-Type:** application/json

**Request**

**Parameters**

| **html**       | string  | required                        | A Beefree HTML message                                                                                                                                                                                                                                                                                                     |
| -------------- | ------- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **size**       | string  | required if no width and height | Use “size” instead of “width” and “height” when you only know the width and want the height automatically calculated.                                                                                                                                                                                                      |
| **width**      | integer | required if no size             | The image width in pixels                                                                                                                                                                                                                                                                                                  |
| **height**     | integer | required if no size             | <p>The image height in pixels<br><strong>default:</strong> applies a proportional value based on the given width, keeping the image aspect ratio<br>When the value is not proportional to the given width:</p><ul><li>If it’s higher: the proportional value applies</li><li>If it’s lower: the image is cropped</li></ul> |
| **file\_type** | string  | required                        | <p>Accepted values:</p><ul><li>jpg</li><li>png</li></ul>                                                                                                                                                                                                                                                                   |

**Example**

```


{
    "html": "<!DOCTYPE html><html><head><meta charset=\"UTF-8\" /></head><body><div style='width:900px; margin: 30px;'>Hello World!</div></body></html>",
    "width": 215,
    "height": 125,
    "file_type": "jpg"
}


```

**Response**

application/jpg

The raw image data

Check out our [sample code for a JavaScript method to convert an image to data URI here](https://gist.github.com/BEE-Plugin/5913ffa1a649b923962d53946e552194).

**Status Codes**

| 200 | OK                |
| --- | ----------------- |
| 400 | Bad Request       |
| 401 | Unauthorized      |
| 429 | Too many requests |
| 500 | Server error      |

#### Merge <a href="#merge" id="merge"></a>

**POST** /merge

**Content-Type:** application/json

**Request**

**Parameters**

| **source**  | object           | required | A Beefree template in JSON format.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ----------- | ---------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **replace** | array            | required | <p>An array of objects that contain a JSON path and value to replace, as follows:</p><table data-header-hidden><thead><tr><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>value</strong></td><td>string | object</td><td>required</td><td>The value can be an object, such as a saved row. Or, it can be a string, such a hex color code. The value should be the same type as the value you want to match in your match expression.</td></tr><tr><td><strong>path</strong></td><td>string</td><td>required</td><td>A JSON Path to the matching nodes in the source JSON.</td></tr></tbody></table> |
| **value**   | string \| object | required | The value can be an object, such as a saved row. Or, it can be a string, such a hex color code. The value should be the same type as the value you want to match in your match expression.                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **path**    | string           | required | A JSON Path to the matching nodes in the source JSON.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

**Example**

```


{
  "replace": [
    {
      "path": "$..style[?(@ == '#FFFFFF')]",
      "value": "#89cff0"
    },
    {
      "path": "$..rows[?(@.metadata.id=='')]",
      "value": { ... row json }
    }
  ],
  "source": { "page": { ... }  }
}


```

**Response**

application/json

The JSON object containing the following parameters:

| **json**     | object | required | The updated Beefree template in JSON format. In the event of an error, the original source is returned.                                                 |
| ------------ | ------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **html**     | string | required | The HTML message.                                                                                                                                       |
| **warnings** | array  | optional | An array of objects containing information about issues that occurred during the merge. If no warnings exist, then it is safe to save the updated JSON. |

**Example**

```


{
    "html": "...",
    "json": {
        "page": { ...// BEE Template }
    },
    "warnings": [
        {
            "msg": "Your path $..style[?(@ == '#FFFFFF')] did not return any matching nodes",
            "param": "path",
            "location": "replace"
        },
        {
            "msg": "Your path $..style[?(@ == '#89cff0')] did not return any matching nodes",
            "param": "path",
            "location": "replace"
        }
    ]
}


```

**Status Codes**

| 200 | OK                         |
| --- | -------------------------- |
| 400 | Bad Request                |
| 401 | Unauthorized               |
| 422 | Entity cannot be processed |
| 429 | Too many requests          |
| 500 | Server error               |

#### Index <a href="#index" id="index"></a>

**Request**

**Parameters**

**POST** /merge/index

**Content-Type:** application/json

| **source** | object | required | A Beefree template in JSON format. |
| ---------- | ------ | -------- | ---------------------------------- |

**Example**

```


{
    "source": { "page": { ... }  }
}


```

**Response**

application/json

The JSON object containing the following parameters:

| **rows** | array | required | An array of metadata objects containing row details, which can be saved in a database to create a reference (or relational table) to the rows associated with your template. |
| -------- | ----- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**Example**

```


[
  {
    "name": "my saved row A"
    "guid": "some unique value"
  },
  {
    "name": "my saved row B"
    "guid": "some unique value"
  }
]


```

**Status Codes**

| 200 | OK                         |
| --- | -------------------------- |
| 400 | Bad Request                |
| 401 | Unauthorized               |
| 422 | Entity cannot be processed |
| 429 | Too many requests          |
| 500 | Server error               |
