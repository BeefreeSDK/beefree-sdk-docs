# Change Schema for Comments

## Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. In the Beefree SDK, the **Change Schema** defines the structure for tracking changes in collaborative environments, particularly for managing comment threads within content blocks. These changes are recorded with associated metadata to support real-time collaboration, versioning, and user engagement. This documentation breaks down the schema’s types, payload structure, and practical usage to help you effectively implement comment-based interactions into your system.

### Schema Overview

This section summarizes the purpose and key characteristics of the Change Schema.

* **Schema Name**: Change
* **Purpose**: Tracks various types of comment-related actions such as creation, resolution, editing, or deletion.
* **Mandatory Fields**: `type`, `payload`
* **Restrictions**: Each change type defines its own required payload structure.
* **Related Schemas**:
  * `comment.schema.json` (for individual comment details)
  * `user.schema.json` (for user attribution and metadata)

### Structure Definition

Below is the JSON Schema definition and a detailed breakdown of each property.

#### JSON Schema (Simplified Overview)

```json
{
  "type": "object",
  "properties": {
    "change": {
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "enum": [
            "NEW_COMMENT",
            "COMMENT_THREAD_RESOLVED",
            "COMMENT_THREAD_REOPENED",
            "COMMENT_EDITED",
            "COMMENT_DELETED"
          ]
        },
        "payload": {
          "type": "object"
        }
      },
      "required": ["type", "payload"]
    },
    "comments": {
      "type": "object",
      "additionalProperties": {
        "$ref": "comment.schema.json"
      }
    },
    "threadUsers": {
      "type": "object",
      "properties": {
        "contributors": {
          "type": "array",
          "items": {
            "$ref": "user.schema.json"
          }
        }
      }
    }
  },
  "required": ["change"]
}
```

### Field Descriptions

The following list displays the field descriptions along with their corresponding descriptions.

* **change.type**: Enumerates the type of action taken (e.g., new comment, resolution).
* **change.payload**: Contains the change-specific data. The structure varies based on `type`.
* **comments**: A mapping of `commentId` to its full comment object.
* **threadUsers.contributors**: Lists users involved in the comment thread.

### Usage Examples

Reference a practical example of the schema in the following code snippet.

#### Example: New Comment

```json
{
  "change": {
    "type": "NEW_COMMENT",
    "payload": {
      "commentId": "a2c555e4-72f7-4e7f-96cd-537e5eb2069c",
      "comment": {
        "content": "add new Text block and logo here!",
        "parentCommentId": null,
        "elementId": "73dcc71b-1ba7-458d-81b8-59ec54e534a5",
        "mentions": [],
        "responses": [],
        "timestamp": "2022-04-05T13:53:28.089Z",
        "author": {
          "userHandle": "0.6379069806343958",
          "username": "John Doe",
          "userColor": "#ff4400"
        }
      }
    }
  },
  "comments": {
    "a2c555e4-72f7-4e7f-96cd-537e5eb2069c": {
      "content": "add new Text block and logo here!",
      "parentCommentId": null,
      "elementId": "73dcc71b-1ba7-458d-81b8-59ec54e534a5",
      "mentions": [],
      "responses": [],
      "timestamp": "2022-04-05T13:53:28.089Z",
      "author": {
        "userHandle": "0.6379069806343958",
        "username": "John Doe",
        "userColor": "#ff4400"
      }
    }
  },
  "threadUsers": {
    "contributors": [
      {
        "userHandle": "0.6379069806343958",
        "username": "John Doe",
        "userColor": "#ff4400"
      }
    ]
  }
}
```

### Additional Considerations

Consider the following when working with the Change Schema:

* **Thread Management**: Leverage `parentCommentId` to group responses into threads.
* **User Attribution**: Use `userHandle` and `userColor` to personalize the UI.
* **Audit Logging**: This schema can support full history tracking and rollback features.
