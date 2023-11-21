# File System Provider errors

#### Example Response

```


{"code":3200,"message":"Resource Not Found","details":"http:\/\/myfsp.com\/docs\/errorcodes\/404"}


```

#### Error Codes

| Code                  | Message                                           | HTTP Status               | Details                                                       |
| --------------------- | ------------------------------------------------- | ------------------------- | ------------------------------------------------------------- |
| `3001`                | FSP Error                                         | 503 Service Unavailable   | Default generic FSP Error                                     |
| `3100`                | Something went wrong accessing backend filesystem | 503 Service Unavailable   | Default generic Error                                         |
| `3200`                | Resource not found                                | 404 Not Found             | File or directory not found                                   |
| `3300`                | Permission denied                                 | 403 Forbidden             | Permission denied to access a file or a directory             |
| `3400`                | Resource Already Exists                           | 409 Conflict              | File or directory already exists                              |
| `3450`                | File Not Uploaded                                 | 422 Unprocessable Entity  | Error during file upload                                      |
| `3500`                | Request Error                                     | 400 Bad Request           | Server could not understand the request due to invalid syntax |
| `3600`                | User Error                                        | 403 Forbidden             | Not a valid S3 custom storage                                 |
| `3650`                | Wrong Username or Password                        | 401 Unauthorized          | Wrong user credentials                                        |
| from `3900` to `3999` | _Custom error message_                            | _Custom HTTP status code_ |                                                               |

#### Displaying custom errors from your FSP API

You can return custom errors from your application that will be displayed in the file manager.

To do that we reserved codes from _3900_ to _3999_.\
An error sent with an error code number in this range displays the message as the error title and the details as the error text.

**Example:**

1. Your file storage doesn’t support file names with the character “?”
2. The front end doesn’t stop the upload, as this character is allowed by other APIs and storages
3. When your API gets the file, returns the following error:\
   **Code:** 39105\
   **HTTP Status:** 400\
   **Message:** Upload error\
   **Details:** The file name is not allowed. Please make sure it does not contain one or more of these characters: \ / < > ? |
4. The file manager inside the editor displays:\
   ![](https://docs.beefree.io/wp-content/uploads/2018/05/FSP\_custom\_error-300x68.jpg)
