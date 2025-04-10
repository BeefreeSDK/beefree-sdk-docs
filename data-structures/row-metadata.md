# Row Metadata

### Introduction

In the Beefree SDK, reusable or saved rows can include a `metadata` object to help organize and manage them within the builder interface. This metadata is not used for content rendering. Instead, it provides helpful context—like titles, tags, categories, timestamps, and user information—that can be leveraged by the host application.

The `metadata` object is part of the overall Row structure and is intended for internal use by the application to support filtering, sorting, version tracking, and multi-user ownership models.

### What is `metadata`?

The `metadata` object is a plain JSON object that lives inside a row. It stores contextual information about the row, such as:

| Field          | Type                    | Description                                                              |
| -------------- | ----------------------- | ------------------------------------------------------------------------ |
| `name`         | string (required)       | A human-readable title for the row shown in the Rows panel.              |
| `tags`         | string                  | A comma-separated list of keywords used to categorize or filter the row. |
| `category`     | string or number        | An identifier that groups rows into categories.                          |
| `id`           | string or number        | A unique identifier for the row, assigned by the host application.       |
| `idParent`     | string, number, or null | Optional ID of a parent row, if this row is derived from another.        |
| `dateCreated`  | string (ISO 8601)       | When the row was originally created.                                     |
| `dateModified` | string (ISO 8601)       | When the row was last modified.                                          |
| `userId`       | string or number        | ID of the user who created or owns the row.                              |

All fields are optional except `name`, and you can adjust or extend this structure to fit your system’s needs.

### Example: Row with Metadata

```json
{
  "name": "Two-Column Product Row",
  "columns": [ /* column definitions */ ],
  "metadata": {
    "name": "Featured Product",
    "tags": "product, two columns, featured",
    "category": "ecommerce",
    "id": "row_001",
    "idParent": null,
    "dateCreated": "2023-10-02T12:45:00Z",
    "dateModified": "2023-12-01T14:20:30Z",
    "userId": "user_789"
  }
}
```

### Best Practices

* **Use `tags` and `category`** to enable search and filtering in the **Rows** tab.
* **Track changes** using `dateCreated` and `dateModified`.
* **Support multi-user setups** by associating rows with a `userId`.
* **Assign unique IDs** for efficient management of saved or shared rows.
