# Template Schema

## Simple to Full JSON

This section discusses what the `/simple-to-full-json` endpoint is and how you can use it for AI-driven designs. This endpoint accepts [Simple schema](./) as the body of the `POST` request, and returns the full Beefree SDK template JSON, which can then be loaded in the Beefree SDK editor for an end user to view and edit accordingly. There are many creative ways to use and implement this endpoint, because it provides a pathway to programmatically creating full Beefree SDK-compatible templates completely outside of the Beefree SDK builder.        &#x20;

{% hint style="success" %}
Reference the [Simple Schema GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/tree/main) for more information.
{% endhint %}

#### Request Parameters

The API call accepts a `template` object, which is required to successfully perform the `/simple-to-full-json` API call. The following table describes this required object.

| Name       | Type | Required | Description                                                                                                                                                              |
| ---------- | ---- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `template` | JSON | Yes      | A Beefree SDK template in simple JSON format ([see the schema in GitHub](https://github.com/mailupinc/simple-schema-beefree-sdk/blob/main/simple_template.schema.json)). |

The following code snippet shows the template object as the body of the `POST` request.

```json
{
  “template”:{...}
}
```

{% hint style="info" %}
**Note:** The [simple template JSON schema](https://github.com/BeefreeSDK/beefree-sdk-simple-schema/blob/main/simple_template.schema.json) describes the request parameters, and the template object structure.&#x20;
{% endhint %}

#### Object Parameters Nested within the Template Object

The following table lists and describes both **required** and **optional** object parameters nested within the mandatory `template` object. This `template` object is the body of the `POST` request for the API call.&#x20;

| Name       | Type   | Required | Description                                                                                                                                                                                         |
| ---------- | ------ | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`     | String | ✅ Yes    | Specifies the template type. Possible values include: `email`, `page`, `popup`.                                                                                                                     |
| `rows`     | Array  | ✅ Yes    | Array containing at least one row. Reference the [simple row schema](https://github.com/mailupinc/simple-schema-beefree-sdk/blob/main/simple_row.schema.json).                                      |
| `settings` | Object | ❌ No     | Configuration settings. Reference the [Settings Object Parameters](template-schema.md#settings-object-parameters-request-greater-than-template-greater-than-settings) section for more information. |
| `metadata` | Object | ❌ No     | Metadata information. Reference the [Metadata Object Parameters section](template-schema.md#metadata-object-parameters-request-greater-than-template-greater-than-metadata) for more information.   |

#### **Settings Object Parameters** <a href="#settings-object-parameters-request-greater-than-template-greater-than-settings" id="settings-object-parameters-request-greater-than-template-greater-than-settings"></a>

The following code snippet shows the optional `settings` object nested within the `template` object in the body of the `POST` request.

```json
{
  “template”:{
    "settings":{...},
    ...
  }
}
```

The following table lists and describes **optional** object parameters nested within the `settings` object. The settings object is nested within the mandatory `template` object.&#x20;

| Name                         | Type    | Required | Description                                                                           |
| ---------------------------- | ------- | -------- | ------------------------------------------------------------------------------------- |
| `linkColor`                  | String  | ❌ No     | The default color of the links within the template.                                   |
| `backgroundColor`            | String  | ❌ No     | The background color of the template.                                                 |
| `contentAreaBackgroundColor` | String  | ❌ No     | The background color of the content area.                                             |
| `width`                      | integer | ❌ No     | **Important:** The width of the template must be between **320** and **1440** pixels. |

#### **Metadata Object Parameters** <a href="#metadata-object-parameters-request-greater-than-template-greater-than-metadata" id="metadata-object-parameters-request-greater-than-template-greater-than-metadata"></a>

The following code snippet shows the optional `metadata` object nested within the `template` object in the body of the `POST` request.

```json
{
  “template”:{
    "metadata":{...},
    ...
  }
}
```

The following table lists and describes **optional** object parameters nested within the `metadata` object. The `metadata` object is nested within the mandatory `template` object. &#x20;

| Name          | Type   | Required | Description                                                      |
| ------------- | ------ | -------- | ---------------------------------------------------------------- |
| `lang`        | string | ❌ No     | The language code of the template (for example, `"en"`, `"fr"`). |
| `title`       | string | ❌ No     | The title of the template.                                       |
| `description` | string | ❌ No     | A short description of the template.                             |
| `subject`     | string | ❌ No     | The subject line of the email (if applicable).                   |
| `preheader`   | string | ❌ No     | The preheader text for the email (if applicable).                |

The following JSON Schema is related to the request parameters for this endpoint, as mentioned in the above table we accept only a `template` object, which is mandatory. The following JSON Schema describes the request parameters as well as the template object structure, going in depth on the possible properties of the template object.

```json
{
  "$schema": "http://json-schema.org/draft-07/schema",
  "$id": "simple_template.schema.json",
  "title": "Simple Template",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "template": {
    "additionalProperties": false,
      "type": "object",
      "required": ["type", "rows"],
      "properties": {
        "type": {
          "type": "string",
          "enum": ["email", "page", "popup"]
        },
        "rows": {
          "type": "array",
          "minItems": 1,
          "items": {
            "$ref": "simple_row.schema.json"
          }
        },
        "settings":{
          "additionalProperties": false,
          "type": "object",
          "properties":{
            "linkColor":{
              "type": "string"
            },
            "background-color":{
              "type": "string"
            },
            "contentAreaBackgroundColor":{
              "type": "string"
            },
            "width": {
              "type": "integer",
              "minimum": 320,
              "maximum": 1440
            }
          }
        },
        "metadata":{
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "lang": {
              "type": "string"
            },
            "title": {
              "type": "string"
            },
            "description": {
              "type": "string"
            },
            "subject": {
              "type": "string"
            },
            "preheader": {
              "type": "string"
            }
          }
        }
      }
    }
  },
  "required": ["template"]
}
```
