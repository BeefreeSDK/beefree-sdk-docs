# Comments Schema

## Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In the Beefree SDK, the **Comments Schema** defines the structure for storing comment threads tied to specific content elements within a template. This schema supports collaborative workflows such as feedback, review, and approval by linking user-generated comments to specific layout components via `elementId`. The host application may choose to manage these comments dynamically or store them statically within saved template versions.

### Schema Overview

This section summarizes the purpose and key characteristics of the Comments Schema.

* **Schema Name**: Comments
* **Purpose**: Stores user comments and threaded responses linked to specific layout elements within a template.
* **Mandatory Fields**: `content`, `elementId`, `timestamp`, `author`
* **Restrictions**: Each comment must be uniquely identified; threaded replies must reference a valid `parentCommentId`.
* **Related Schemas**:
  * `user.schema.json` (for comment authorship)
  * `element.schema.json` (via `elementId`)

### Structure Definition

Below is a generalized representation of the Comments Schema and its property definitions.

#### JSON Schema (Simplified Overview)

```json
{
  "type": "object",
  "patternProperties": {
    "^[a-z0-9-]{36}$": {
      "type": "object",
      "properties": {
        "content": { "type": "string" },
        "parentCommentId": { "type": ["string", "null"] },
        "elementId": { "type": "string" },
        "responses": {
          "type": "array",
          "items": { "type": "string" }
        },
        "timestamp": { "type": "string", "format": "date-time" },
        "author": {
          "type": "object",
          "properties": {
            "uid": { "type": "string" },
            "username": { "type": "string" },
            "userColor": { "type": "string" }
          },
          "required": ["uid", "username", "userColor"]
        },
        "isElementDeleted": { "type": "boolean" }
      },
      "required": ["content", "elementId", "timestamp", "author"]
    }
  }
}
```

### Field Descriptions

* **commentId**: A unique identifier (UUID) used as the key for each comment object.
* **content**: The text content of the comment.
* **parentCommentId**: If present, indicates that the comment is a reply within a thread.
* **elementId**: References the specific content element (e.g., a button or image) that the comment targets.
* **responses**: An array of comment IDs that are direct replies to the current comment.
* **timestamp**: ISO 8601 formatted timestamp indicating when the comment was created.
* **author**: Metadata for the user who posted the comment, including a unique user ID, display name, and color for UI purposes.
* **isElementDeleted**: A flag indicating whether the referenced content element has been removed from the layout.

### Usage Examples

The following is a real-world example of a two-level comment thread.

#### Example: Threaded Comments

```json
{
  "comments": {
    "aab0227f-766d-439d-b3d9-8bf7d04d551f": {
      "content": "Here is a comment",
      "parentCommentId": null,
      "elementId": "ab35241d-dd69-4980-9385-862fedd094e4",
      "responses": [
        "84f11738-a5a2-49db-956a-ae95b4d1db67"
      ],
      "timestamp": "2020-09-07T13:58:43.147Z",
      "author": {
        "uid": "my user id",
        "username": "US Person 2",
        "userColor": "#dddddd"
      },
      "isElementDeleted": false
    },
    "84f11738-a5a2-49db-956a-ae95b4d1db67": {
      "content": "Here is a second comment",
      "parentCommentId": "aab0227f-766d-439d-b3d9-8bf7d04d551f",
      "elementId": "ab35241d-dd69-4980-9385-862fedd094e4",
      "responses": [],
      "timestamp": "2020-09-07T13:59:51.954Z",
      "author": {
        "uid": "my user id 2",
        "username": "US Person 4",
        "userColor": "#dddddd"
      },
      "isElementDeleted": false
    }
  }
}
```

### Additional Considerations

Consider the following when working with the Comments Schema in the Beefree SDK:

* **Dynamic Commenting**: Attaching comments at runtime requires accurate mapping of `elementId` values—typically handled by advanced API interactions.
* **Draft vs. Final**: Host apps may choose to persist comments only for drafts or historical versions of templates.
* **Performance**: For templates with large comment trees, consider lazy-loading responses to optimize rendering.
