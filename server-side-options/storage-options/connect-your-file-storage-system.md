# Connect your file storage system

As you may have noticed, when you create a new Beefree application, it comes with a default cloud storage option for files (images or files that the message uses or links to). This approach may fit well for applications that offer content creation for the first time, especially if they don’t need to share these files with other areas of the host application.

If you do want users to be able to access the same image and file directories that they use elsewhere in your application, we have a solution.

We created a way to connect to a custom file system provider, **allowing you to use your own file storage**, no matter which technology you use. A **custom file system provider** is an API that will allow the a Beefree application to perform actions with files outside of the Beefree system, connecting your file system to the [Beefree File Manager](../../file-manager-application-overview/).

It can be built with your preferred technology: just be sure to follow our instructions to ensure successful communication between the two systems.

Once successfully connected, when a user uploads a file or creates a new folder in the Beefree File Manager, this API will perform these actions in your storage, instead of our default cloud storage. Directories permissions, root directory to use, how thumbnails for images are generated, etc.: you decide.

## Getting Started: data formats <a href="#getting-started-data-formats" id="getting-started-data-formats"></a>

In order to let your Beefree application consume your FSP (File system provider) API, you will need to provide a Base URL to reach the API.

`Base URL: https://myfsp.com/path/to/your/base/endpoint`

Note that:

* the Base URL **must not** end with a trailing slash (/)
* it must be hosted on the HTTPS protocol

The API uses JSON as the input and output data format: Responses are [JSEND standard compliant](https://dam.beefree.io/jsend).

In case of a succesful response, the API returns a “success” status code (ex. `200 OK`) and a JSON object like this one:

```json

{
  "status": "success",
  "data": { /* ... */ }
}

```

In case of an unexpected error occured during request processing (i.e. missing mandatory request data), the API returns an “error” status code and a JSON object like this one:

```json

{"status":"error","message":"something went wrong accessing backend filesystem"}

```

In case of request failure, the API returns the error codes described in the error messages section.

## Authentication <a href="#authentication" id="authentication"></a>

Authentication is managed using Basic Authentication type. The Beefree system’s resource server works as a proxy for FSP (File system provider) and consumes FSP API endpoints adding the following fields to HTTP Request Headers. Please note that  **the API must use HTTPS** to grant secure connections and safe data transfer.

User information is segmented by [UID parameter](../../readme/installation/how-the-uid-parameter-works.md).

```http

Authorization: Basic base64(username:password)
X-BEE-ClientId: ClientId
X-BEE-Uid: uid

```

| Field              | Description                                                                                           |
| ------------------ | ----------------------------------------------------------------------------------------------------- |
| **Authorization**  | Authentication used is Basic. A string formatted as username:password and encoded in base64 is passed |
| **X-BEE-ClientId** | The ClientId (to identify the integrator)                                                             |
| **X-BEE-Uid**      | The uid (ex. useful to identify the user of an integrator)                                            |

The integrator must save…

* Username
* Password
* Base URL

… in the **Configuration** section of the [Beefree SDK Console](https://developers.beefree.io/).

## File System operations <a href="#file-system-operations" id="file-system-operations"></a>

This section will show samples of successful requests to FSP (File system provider) API. A response contains meta data about directory and files.

### Meta data

We can define:

* Common meta
* File-specific meta
* Directory-specific meta

### **Common Meta**

| Field           | Description                                                                                               | Type     | Example                                                                          |
| --------------- | --------------------------------------------------------------------------------------------------------- | -------- | -------------------------------------------------------------------------------- |
| `mime-type`     | application/directory for directories and specific mime-type for files                                    | `string` | “application/directory”, “images/png”, …                                         |
| `name`          | resource name                                                                                             | `string` | “my file.jpg”                                                                    |
| `path`          | absolute path to resource in FSP                                                                          | `string` | “/absolute/path/to/my file.jpg”, “/absolute/path/to/my directory/”, …            |
| `last-modified` | UNIX time with (milliseconds) of last modification of this resource                                       | `int`    | <p><code>1445401740000</code><br>(stands for: Wed, 21 Oct 2015 04:29:00 GMT)</p> |
| `size`          | size (in byte) of the resource, this is zero (0) for directories                                          | `int`    | `2048`                                                                           |
| `permissions`   | defines the access grants to the resource, can be `ro` for read-only access or `rw` for read-write access | `string` | `ro` or `rw`                                                                     |
| `extra`         | generic extra data (for future extensions)                                                                | `object` |                                                                                  |

### **File specific Meta**

| Field        | Description                              | Notes                                              | Type     |
| ------------ | ---------------------------------------- | -------------------------------------------------- | -------- |
| `public-url` | Public url of this file                  | This field **must** be url-encoded                 | `string` |
| `thumbnail`  | Public url of the thumbnail of this file | This field is optional and **must** be url-encoded | `string` |

### **Directory specific Meta**

| Field        | Description                                     | Notes                                                                               | Type     |
| ------------ | ----------------------------------------------- | ----------------------------------------------------------------------------------- | -------- |
| `item-count` | number of contained items (directories + files) | This parameter is optional, if you don’t have this data, feel free to pass zero `0` | `string` |

## Listing Directories

### **Request**

```http

GET /
Authorization: Basic 5AMPL3
X-BEE-ClientId: BeeFree
X-BEE-Uid: 1111-2222-333-444

```

### **Response**

```json


{"status":"success","data":{"meta":{"mime-type":"application\/directory","name":"root","path":"\/","last-modified":1432982102000,"size":0,"permissions":"ro","item-count":2,"extra":[]},"items":[{"mime-type":"application\/directory","name":"shared","path":"\/shared\/","last-modified":1432984102000,"size":0,"permissions":"ro","item-count":13,"extra":[]},{"mime-type":"application\/directory","name":"mydir","path":"\/mydir\/","last-modified":1432982102000,"size":0,"permissions":"rw","item-count":3,"extra":[]}]}}


```

Each resource returned by the API has a `meta` field with metadata. Directory content is returned into `items` field as array of metadata of contained resources.

### **Resource access notes**

Some notes about resources access management in the previous example:

* `/shared/` cannot be renamed, because it is contained in a `ro` directory
* `/mydir/` cannot be renamed, because it is contained in a `ro` directory
* user cannot “CRUD” resources in `/shared/`, because it is `ro`
* user can “CRUD” resources in `/mydir/`, because it is `rw`

## Listing Directory content

### **Request**

```http

GET /mydir/
Authorization: Basic 5AMPL3
X-BEE-ClientId: BeeFree
X-BEE-Uid: 1111-2222-333-444

```

### **Response**

```json


{"status":"success","data":{"meta":{"mime-type":"application\/directory","name":"mydir","path":"\/mydir\/","last-modified":1432982102000,"size":0,"permissions":"rw","item-count":3,"extra":[]},"items":[{"mime-type":"application\/directory","name":"docs","path":"\/mydir\/docs\/","last-modified":1432984102000,"size":0,"permissions":"rw","item-count":4,"extra":[]},{"mime-type":"image\/png","name":"my pic1.png","path":"\/mydir\/my pic1.png","last-modified":1432982102000,"size":100000,"permissions":"rw","public-url":"https:\/\/resources-bucket.s3.amazonaws.com\/1111-2222-333-444\/my%20pic1.png","thumbnail":"https:\/\/my-thumbnail-service.com\/my%20pic1.png","extra":[]},{"mime-type":"image\/png","name":"my pic2.png","path":"\/mydir\/my pic2.png","last-modified":1432982102000,"size":200000,"permissions":"rw","public-url":"https:\/\/resources-bucket.s3.amazonaws.com\/1111-2222-333-444\/my%20pic2.png","thumbnail":"https:\/\/my-thumbnail-service.com\/my%20pic2.png","extra":[]}]}}


```

## Creating a new directory

### **Request**

```http

POST /mydir/new%20dir/
Authorization: Basic 5AMPL3
X-BEE-ClientId: BeeFree
X-BEE-Uid: 1111-2222-333-444

```

### **Response**

```json


{"status":"success","data":{"meta":{"mime-type":"application\/directory","name":"new dir","path":"\/mydir\/new dir","last-modified":1432982102000,"size":0,"permissions":"rw","item-count":0,"extra":[]}}}


```

## **Create operation notes:**

* in order for the create directory operation to succeed, the **containing** directory **must** exist, and the **contained** (new) directory **must not** exist
* directory names will match the following regular expression: \[ a-zA-Z0-9.\_- \\(\\)]+

## Deleting a directory

You can only delete empty directories.

### **Request**

```http

DELETE /my%20dir/docs/
Authorization: Basic 5AMPL3
X-BEE-ClientId: BeeFree
X-BEE-Uid: 1111-2222-333-444

```

### **Response**

```json

{"status":"success","data":null}

```

## Uploading a file

### **Request**

```http

POST /mydir/my%20pic3.png
Authorization: Basic 5AMPL3
X-BEE-ClientId: BeeFree
X-BEE-Uid: 1111-2222-333-444
Content-Type: application/json
 
{
  "source": "http://www.remotehost.com/remotepic.png"
}

```

### **Response**

```json

{"status":"success","data":{"meta":{"mime-type":"image\/png","name":"my pic3.png","path":"\/mydir\/my pic3.png","last-modified":1432982102000,"size":400000,"permissions":"rw","public-url":"https:\/\/resources-bucket.s3.amazonaws.com\/1111-2222-333-444\/my%20pic3.png","thumbnail":"https:\/\/my-thumbnail-service.com\/my%20pic3.png","extra":[]}}}

```

## **Upload operation notes**

* in order for the upload file operation to succeed, the **containing** directory **must** exist
* if the uploaded file already exists, it’s in charge of FSP API do decide if:
  * silently overwrite old file with the new one;
  * create a new file with a different name, in this case returned metadata must be coherent with the new file created;
  * return a 403 FORBIDDEN error;
* uploads are proxied by Beefree’s resource APIs, which are in charge of enforcing the maximum file size (20 Mb) and the maximum image size.
* uploads from stage will be POSTed to “/editor\_images/{filename}”
* uploads from page builder favicons will be POSTed to “/favicon\_images/{filename}”
* the name of files uploaded from stage will match the following regular expression: \[ a-zA-Z0-9.\_- \\(\\)]+

## Deleting a file

### **Request**

```http

DELETE /mydir/my%20pic2.png
Authorization: Basic 5AMPL3
X-BEE-ClientId: BeeFree
X-BEE-Uid: 1111-2222-333-444

```

### **Response**

```json

{"status":"success","data":null}

```

{% hint style="info" %}
**The trailing slash (/) on the request matters!**\
\
The FSP API uses the trailing slash (/) on the resource path to understand if the required resource is a file (no trailing slash) or a directory (with trailing slash).\
\
For example, if the FSP API receives a GET request for `/sample.jpg` it will return `sample.jpg` file metadata, whereas if it receives a GET request for `/sample.jpg/` it will return a list of the content located in the `sample.jpg` directory.
{% endhint %}

## Status codes <a href="#status-codes" id="status-codes"></a>

The FSP (File system provider) API uses standard HTTP status codes to manage success and error responses. Status codes include:

| Action            | On success    | On error                  | On failure                                                                                                                          |
| ----------------- | ------------- | ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| List directory    | `200 OK`      | `503 Service unavailable` | <p><code>401 Unauthorized</code><br><code>404 Not Found</code></p>                                                                  |
| Create directory  | `201 Created` | `503 Service unavailable` | <p><code>401 Unauthorized</code><br><code>403 Forbidden</code><br>(parent is read-only or non-existent; new dir already exists)</p> |
| Delete directory  | `200 OK`      | `503 Service unavailable` | <p><code>401 Unauthorized</code><br><code>403 Forbidden</code>(if parent is read-only)<br><code>404 Not Found</code></p>            |
| Get file metadata | `200 OK`      | `503 Service unavailable` | <p><code>401 Unauthorized</code><br><code>404 Not Found</code></p>                                                                  |
| Upload file       | `201 Created` | `503 Service unavailable` | <p><code>401 Unauthorized</code><br><code>403 Forbidden</code>(if parent is read-only or non-existent)</p>                          |
| Delete file       | `200 OK`      | `503 Service unavailable` | <p><code>401 Unauthorized</code><br><code>403 Forbidden</code>(if parent is read-only)<br><code>404 Not Found</code></p>            |

## Error codes <a href="#error-codes" id="error-codes"></a>

In case of errors, the API returns a JSON object structured like this:

```


{"code":3200,"message":"Resource Not Found","details":"http:\/\/myfsp.com\/docs\/errorcodes\/404"}


```

To read the full list of possible errors, please refer to [this page](../../error-management/file-system-provider-errors.md).

## Displaying thumbnails <a href="#displaying-thumbnails" id="displaying-thumbnails"></a>

Thumbnail generation is up to the developer of the file system provider.

In case you don’t want to develop your own thumbnail generation procedure, you can use a service like [http://rethumb.com](http://rethumb.com/) to create a thumbnail URL.

The `thumbnail` field is optional, so if you don’t want a thumbnail for your file, do not pass the field and the Beefree system will show you a generic icon based on the mime type you passed.

The thumbnail image must be contained in a 200px by 200px virtual square (see pictures below).

<figure><img src="../../.gitbook/assets/thumb.png" alt=""><figcaption></figcaption></figure>
