---
description: >-
  This page lists and describes the File Manager category of endpoints within
  the Content Services API. It also includes interactive testing environments
  for each endpoint in this category.
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# File Manager

{% hint style="info" %}
File Manager endpoints are part of the [Content Services API](./). The Content Services API is available on [Beefree SDK plans that are Essentials or above](https://developers.beefree.io/pricing-plans).
{% endhint %}

## Overview

The File Manager endpoints let your application manage an end user's files and folders from your own server, without opening a builder. They act on the same file system the File Manager displays inside the editor, so anything your application changes through the API your end users will see next time they open it.

A single resource family, `/v1/file`, covers six operations. The following table lists them.

| Operation                                                                | Request                                                          |
| ------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| [List a directory](file-manager.md#list-a-directory)                     | `GET /v1/file/{path}/`                                           |
| [Search files](file-manager.md#search-files)                             | `GET /v1/file/{path}?q={query}`                                  |
| [Create a directory](file-manager.md#create-a-directory)                 | `POST /v1/file/{path}/`                                          |
| [Upload a file](file-manager.md#upload-a-file)                           | `POST /v1/file/{path}/{filename}`                                |
| [Move a file](file-manager.md#move-a-file)                               | `PATCH /v1/file/{path}/{filename}`                               |
| [Delete a file or directory](file-manager.md#delete-a-file-or-directory) | `DELETE /v1/file/{path}/{filename}` or `DELETE /v1/file/{path}/` |

Everything after `/v1/file/` is the path to a file or directory inside your end user's storage, and a trailing slash decides which of the two a request addresses. Reference the [Paths and the trailing slash](file-manager.md#paths-and-the-trailing-slash) section before you write against these endpoints.

Each request counts as one Content Services API call, and these endpoints are subject to the [same rate limits](./#rate-limits) as every other category.

## Headers and authentication

Every request carries your Content Services API key as a bearer token, plus a header identifying the end user whose files you're working with.

```http
Authorization: Bearer {your API key}
X-BEE-Uid: {end-user id}
```

If your application already calls the Content Services API, your existing key works on these endpoints and there's nothing new to provision. Reference the [Authentication page](authentication.md) to learn more about creating and managing keys. A missing or invalid `Authorization` header returns `401`.

### Identify the end user

`X-BEE-Uid` is the same `uid` your application uses when it creates an editor session, so the API and the editor resolve to the same file system. It's required on every call, including a listing of the storage root. A `uid` that has never been used before works fine, since the value identifies a customer of yours rather than a Beefree SDK account, and we don't validate it.

If the header is missing or empty, the request fails with `400`:

```json
{
  "code": 3750,
  "message": "Request Error",
  "details": "Missing x-bee-uid header"
}
```

### Other headers

CDN segmentation, custom domains, and custom file system providers each require additional headers. Send the ones for each feature your application has configured. If you don't use any of them, `Authorization` and `X-BEE-Uid` are all you need. The following table lists the headers by feature.

| Feature                     | Headers                                                                               |
| --------------------------- | ------------------------------------------------------------------------------------- |
| CDN segmentation            | `X-BEE-TENANT-IDENTIFIER`                                                             |
| Custom file system provider | `X-BEE-BUSINESSUID`, `X-BEE-DOCUMENT-ID`, `X-BEE-CUSTOM-HOST`, `X-BEE-AUTHORIZATION`  |
| Custom domain               | `X-BEE-CUSTOM-THIRD-LEVEL-DOMAIN`, `X-BEE-CUSTOM-DOMAIN`, `X-BEE-CUSTOM-MEDIA-DOMAIN` |

`X-BEE-AUTHORIZATION` carries the credentials for your own file system provider, not for Beefree SDK. Your Content Services API key always goes in the `Authorization` header.

### These endpoints are server-to-server only

These endpoints accept a Content Services API key only. The access token your backend obtains from `/loginV2` to start a builder session doesn't work here, and sending one returns `403`:

```json
{
  "status": 403,
  "code": 403,
  "message": "Resource forbidden: API token required."
}
```

{% hint style="danger" %}
Keep secrets on the server. Never expose your Client Secret or Content Services API key to the browser. Calling these endpoints from a browser would expose your API key.
{% endhint %}

## Storage requirements

These endpoints require your application's file storage provider to be updated to the latest version. Requests from an application on an earlier version return `422`:

```json
{
  "code": 3621,
  "message": "Storage configuration error: feature available only on FSPx"
}
```

If you see this error, contact our team and we'll confirm which version your application is on.

Moving files can also be disabled for an individual storage. When it is, [Move a file](file-manager.md#move-a-file) returns `422` with code `3622`, and files come back from a listing with `extra.can-move` set to `false`.

## Paths and the trailing slash

Everything after `/v1/file/` is the path inside the end user's storage.

### The trailing slash chooses the operation

A trailing slash means directory, and no trailing slash means file. This single character changes what a request does. The following table shows the same route with and without it.

| Request                              | Result                                       |
| ------------------------------------ | -------------------------------------------- |
| `POST /v1/file/campaigns/`           | Creates the directory `campaigns`            |
| `POST /v1/file/campaigns/hero.jpg`   | Uploads the file `hero.jpg` into `campaigns` |
| `DELETE /v1/file/campaigns/`         | Deletes `campaigns` if it's empty            |
| `DELETE /v1/file/campaigns/hero.jpg` | Deletes the single file `hero.jpg`           |
| `PATCH /v1/file/campaigns/`          | Refused, because only files can be moved     |

On `GET` the trailing slash isn't enforced, so `GET /v1/file/campaigns` and `GET /v1/file/campaigns/` both work. The path is forwarded as given and normalized by the storage service.

### The storage root and reserved directories

What the root contains depends on whether your application has a [Customer Shared Folder](../../server-side-configurations/server-side-options/storage-options/configure-your-aws-s3-bucket.md#shared-assets) configured.

With a Customer Shared Folder, the root holds two directories and nothing else. Your end user's own files live in `/myfiles`, where every operation is available. The shared files live in `/shared`, which supports listing and searching only; creating, uploading, moving, and deleting return an error. Neither directory can be deleted.

Without one, your end users work directly in the root, uploading files and creating directories there.

Either way, the root itself can't be created, moved, or deleted.

* `GET /v1/file` and `GET /v1/file/` both list the root.
* `POST /v1/file`, `PATCH /v1/file`, and `DELETE /v1/file` return `404`, because there's no such route.
* `POST /v1/file/`, `PATCH /v1/file/`, and `DELETE /v1/file/` return `400` with a `details` message explaining that a path is required.&#x20;

To upload to the root, use a single-segment path: `POST /v1/file/hero.jpg`.

### Valid paths

Path segments are validated and re-encoded before they're forwarded to storage.

Paths and file names can contain spaces, `&`, `%`, non-ASCII characters, and emoji. `/my folder/a&b.txt` and `/😀/x.png` are both valid, and a literal `%` stays a literal `%`.

Two things are rejected with `400` and `details` of `Invalid path`:

* Any `.` or `..` segment, including percent-encoded forms such as `%2e%2e%2f`.
* An empty inner segment, which means a leading `//` as in `//foo`, or a repeated slash as in `a//b`. A repeated slash matters because `a//b` addresses a different location in storage than `a/b`.&#x20;

Paths are case-sensitive, and so is the route itself. `/V1/File/...` returns `404`.

## Responses and errors

A successful call returns `200`, with the payload of the operation in `data`. For a listing or a search, `data` carries the items. For a write operation, it carries the metadata of what you wrote.

```json
{
  "status": "success",
  "data": { }
}
```

### Read code, not just the HTTP status

Three different error bodies can reach your client, so read `code` rather than relying on the status alone. Logical failures, such as a name collision or a missing source file, arrive as `400` with the storage error body preserved.

| code          | Raised by                                                                                          | Where the detail is                                      |
| ------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| `3750`        | The API layer rejecting the request                                                                | `details`, a string. `message` is always `Request Error` |
| `3500`        | Field validation in the storage layer                                                              | `details`, an object with one key per invalid field      |
| Anything else | Storage or your file storage provider, such as `3400` for a collision or `3200` for a missing file | `message`. `details` may be present but empty            |

```json
{
  "code": 3750,
  "message": "Request Error",
  "details": "conflict_strategy is required and must be one of keep, replace, ask"
}
```

### HTTP status codes

The following table lists the statuses these endpoints return.

| Status | Meaning                                                                                                                                           |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `200`  | Success                                                                                                                                           |
| `400`  | The request was rejected with code `3750`, a field failed validation, or the operation failed logically and the body carries its own `code`       |
| `401`  | `Authorization` missing or invalid                                                                                                                |
| `403`  | An access token was used instead of an API key                                                                                                    |
| `404`  | No such route, which means a bare `/v1/file` on `POST`, `PATCH`, or `DELETE`, or a wrong-cased path                                               |
| `413`  | Upload body larger than the maximum upload size                                                                                                   |
| `422`  | Rejected by storage, such as `3621` when the file storage provider needs updating, `3622` when moving is disabled, or `4220` for a dangerous file |
| `429`  | Rate limit exceeded. The body is plain text, not the JSON envelope                                                                                |
| `500`  | Unexpected failure                                                                                                                                |

## List a directory <a href="#list-a-directory" id="list-a-directory"></a>

{% openapi-operation spec="list-a-directory" path="/v1/file/{path}" method="get" %}
[OpenAPI list-a-directory](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/c482e20d83003b5567585a5873d70b55628733ac144d9eb7ef008127a50be195.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260916%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260916T204804Z&X-Amz-Expires=172800&X-Amz-Signature=e781cefecb183289ca60255cbe3615ce1ad45babab0ec96d91aed81e6ff78a9e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

## Search files <a href="#search-files" id="search-files"></a>

{% openapi-operation spec="search-files" path="/v1/file/{path}" method="get" %}
[OpenAPI search-files](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/927850588e424820f02fc7bdafd383bc753b02dd2a8830212a4a03b74a7fd11e.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260916%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260916T204804Z&X-Amz-Expires=172800&X-Amz-Signature=edf085de9447460366f82af81c24c9c2afca8bdef79bcc35f57d8a8c1b6cf432&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

## Create a directory <a href="#create-a-directory" id="create-a-directory"></a>

{% openapi-operation spec="create-directory" path="/v1/file/{path}/" method="post" %}
[OpenAPI create-directory](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/2e0d2e944b07358577818424f25fbee9cc48653fc51b01407a1832ae9eca3980.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260916%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260916T204804Z&X-Amz-Expires=172800&X-Amz-Signature=bc62141a332f38495d54568753d300fcda64f5e8280eff9281704dc96340b77a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

## Upload a file

{% openapi-operation spec="upload-a-file" path="/v1/file/{path}/{filename}" method="post" %}
[OpenAPI upload-a-file](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/08c674d3f4b3d25910548c51ffd5af96a754aa67429943f8b13aa430dab03d63.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260916%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260916T204804Z&X-Amz-Expires=172800&X-Amz-Signature=8c119bfe8cd63496b45e76e0a06265687658de9e8a873d2211bb15118c8209c2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

## Move a file

{% openapi-operation spec="move-a-file" path="/v1/file/{path}/{filename}" method="patch" %}
[OpenAPI move-a-file](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/b8d22ba0daf92b9e2c49e8aee121a836495570729b55f94816a1d365bcf0b608.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260916%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260916T204804Z&X-Amz-Expires=172800&X-Amz-Signature=8bd4de1c95a430c0621de1475eeea95252c8cd11a415009e2b665be632124089&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

## Delete a file or directory

{% openapi-operation spec="delete-file" path="/v1/file/{path}/{filename}" method="delete" %}
[OpenAPI delete-file](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/2f73a62c7c828e48a61707a6faa02adc4437be90f4a5af8ffb30bb2ce5a236da.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260916%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260916T204804Z&X-Amz-Expires=172800&X-Amz-Signature=08c86eb56f96748173d6ed1e30485cb4b4532141eadbade80e0b0fbe89561861&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

## Limitations

Consider the following when working with the File Manager endpoints:

* Every operation requires your application's file storage provider to be updated to the latest version.
* Directories can't be moved, and files can't be renamed.
* A directory is deleted only when it's empty.
* Search matches file names, not file contents or meaning, and returns at most 200 results with no pagination.
* Search isn't available on applications configured with custom storage.
* Listings return every item in a directory, with no pagination.
* The default maximum upload size is 20 MB.
* Creating, uploading, moving, and deleting are unavailable in the Customer Shared Folder (`/shared`).
