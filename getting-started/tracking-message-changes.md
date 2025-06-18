# Tracking Message Changes

{% hint style="info" %}
This feature is available on Beefree SDK [paid plans](https://dam.beefree.io/pluginpricing) only.
{% endhint %}

## Overview of Tracking Message Changes <a href="#overview" id="overview"></a>

This page discusses how to effectively track message and UI changes in Beefree SDK. It explains how you can use the `onChange` function to monitor real-time JSON updates, enabling efficient application updates and debugging, if needed. It also covers how to implement the `onRemoteChange` function to track edits made by other users for [Collaborative Editing](../other-customizations/collaborative-editing/).

In addition to these, the `onViewChange` callback offers a way to monitor changes in the SDK’s interface — such as when users open or close the File Manager, Preview, or Image Editor. This allows you to better understand user behavior, enhance session monitoring, and potentially optimize UX flows based on user navigation.

By leveraging these three callbacks — `onChange`, `onRemoteChange`, and `onViewChange` — you can develop a comprehensive workflow for tracking both content and interaction changes your end users make, whether they are within a single session or a collaborative editing session.

### Callback Reference for Tracking Changes

The following table provides a quick reference of callbacks related to tracking changes.

| Event            | Description                                                                                         | Returned Values                                                    |
| ---------------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| `onChange`       | Fired when the message JSON is updated locally.                                                     | The new message JSON object.                                       |
| `onRemoteChange` | Fired when changes are made to the message by a different user in a collaborative session.          | The updated JSON from the remote user.                             |
| `onViewChange`   | Fired when the user navigates between different views in the SDK interface (e.g., opening preview). | One of: `'fileManager'`, `'editor'`, `'preview'`, `'imageEditor'`. |

#### This page explores and answers the following questions:

* How can I monitor what my customers do in the builder?
* How can I tell when a message has actually been updated?
* How can I tell when a collaborative editing session has been updated?
* How can I track which part of the UI a user is interacting with?

### Use Cases for Tracking Message Changes

This section includes use cases for the `onChange`, `onRemoteChange`, and `onViewChange` callbacks.&#x20;

#### Usage Tracking

Understanding how users interact with the builder helps improve UX, prioritize development, and identify friction points.\
The `onChange` callback lets your app detect when users are actively editing a message, using specific features, or possibly reproducing a reported issue.

Use it to:

* Detect active vs. abandoned editing sessions
* Monitor usage of new features
* Investigate and reproduce bugs

#### Autosave

Unlike the default [autosave](readme/installation/configuration-parameters/) (which triggers at fixed intervals regardless of changes), `onChange` enables saving only when actual edits occur. This reduces false-positive recovery dialogs and improves the message recovery experience.

#### History

Tracking changes over time allows users to compare and restore previous message versions — especially helpful in collaborative environments where mistakes can lead to lost work.

#### Content Checks

When users edit text or images, `onChange` returns the updated content, enabling your app to run validations or custom logic.

Example use cases:

* Content suggestions
* Blocking restricted content
* Validating links and their reputation
* Checking custom HTML
* Handling conditional syntax with custom workflows

## Prerequisites

To enable tracking message changes, you need to add the following in the [beeConfig](readme/installation/configuration-parameters/):

* Add `trackChanges`  and set it to `true`.
* The `onChange` callback, with the related response function.
* (Optional) Add and set the `onRemoteChange` boolean to `true` for multi-user message tracking during [collaborative editing session](../other-customizations/collaborative-editing/).

**Enable "onChange" Event**

Set the following parameter to `true` in the `beeConfig` file to enable `onChange`.

```javascript
trackChanges: true, // boolean
```

### onChange <a href="#how-it-works" id="how-it-works"></a>

When you enable `onChange` and your end users edit their message, the callback provides you with:

* Information on the new content or section
* The action that was performed on existing content
* The JSON update (as the entire page, as well as JSON patches)

<details>

<summary>onChange JSON example</summary>

The following JSON displays an example of what you can expect to receive from the `onChange` callback.

```json
{
    "message": {
        "page": {
            "body": {
                "container": {
                    "style": {
                        "background-color": "#FFFFFF"
                    }
                },
                "content": {
                    "computedStyle": {
                        "linkColor": "#0068A5",
                        "messageBackgroundColor": "transparent",
                        "messageWidth": "500px"
                    },
                    "style": {
                        "color": "#000000",
                        "font-family": "Arial, Helvetica, sans-serif"
                    }
                },
                "type": "mailup-bee-page-properties",
                "webFonts": []
            },
            "description": "Empty template for BEE",
            "rows": [
                {
                    "columns": [
                        {
                            "grid-columns": 12,
                            "modules": [
                                {
                                    "type": "mailup-bee-newsletter-modules-heading",
                                    "descriptor": {
                                        "heading": {
                                            "title": "h1",
                                            "text": "<span class=\"tinyMce-placeholder\">hello</span>",
                                            "style": {
                                                "color": "#555555",
                                                "font-size": "23px",
                                                "font-family": "inherit",
                                                "link-color": "#0068A5",
                                                "line-height": "120%",
                                                "text-align": "center",
                                                "direction": "ltr",
                                                "font-weight": "700",
                                                "letter-spacing": "0px"
                                            }
                                        },
                                        "style": {
                                            "width": "100%",
                                            "text-align": "center",
                                            "padding-top": "0px",
                                            "padding-right": "0px",
                                            "padding-bottom": "0px",
                                            "padding-left": "0px"
                                        },
                                        "mobileStyle": {}
                                    },
                                    "uuid": "e4b98f50-b74c-45a8-a184-e5622cdd62fe",
                                    "locked": false
                                }
                            ],
                            "style": {
                                "background-color": "transparent",
                                "border-bottom": "0px solid transparent",
                                "border-left": "0px solid transparent",
                                "border-right": "0px solid transparent",
                                "border-top": "0px solid transparent",
                                "padding-bottom": "5px",
                                "padding-left": "0px",
                                "padding-right": "0px",
                                "padding-top": "5px"
                            },
                            "uuid": "bb75ccd1-db9a-4c93-9cf4-85644245b25d"
                        }
                    ],
                    "container": {
                        "style": {
                            "background-color": "transparent",
                            "background-image": "none",
                            "background-position": "top left",
                            "background-repeat": "no-repeat"
                        }
                    },
                    "content": {
                        "computedStyle": {
                            "hideContentOnDesktop": false,
                            "hideContentOnMobile": false,
                            "rowColStackOnMobile": true,
                            "rowReverseColStackOnMobile": false,
                            "verticalAlign": "top"
                        },
                        "style": {
                            "background-color": "transparent",
                            "background-image": "none",
                            "background-position": "top left",
                            "background-repeat": "no-repeat",
                            "color": "#000000",
                            "width": "500px"
                        }
                    },
                    "empty": false,
                    "locked": false,
                    "synced": false,
                    "type": "row-1-columns-12",
                    "uuid": "fd68e622-bad7-4cca-84e2-a0315d4ffba7"
                }
            ],
            "template": {
                "name": "template-base",
                "type": "basic",
                "version": "2.0.0"
            },
            "title": "Empty Template"
        },
        "comments": {}
    },
    "changes": {
        "code": "1323",
        "value": "<span class=\"tinyMce-placeholder\">hello</span>",
        "description": "Text edited",
        "patches": [
            {
                "op": "add",
                "path": "/rows/0/columns/0/modules/0",
                "value": {
                    "type": "mailup-bee-newsletter-modules-heading",
                    "descriptor": {
                        "heading": {
                            "title": "h1",
                            "text": "<span class=\"tinyMce-placeholder\">hello</span>",
                            "style": {
                                "color": "#555555",
                                "font-size": "23px",
                                "font-family": "inherit",
                                "link-color": "#0068A5",
                                "line-height": "120%",
                                "text-align": "center",
                                "direction": "ltr",
                                "font-weight": "700",
                                "letter-spacing": "0px"
                            }
                        },
                        "style": {
                            "width": "100%",
                            "text-align": "center",
                            "padding-top": "0px",
                            "padding-right": "0px",
                            "padding-bottom": "0px",
                            "padding-left": "0px"
                        },
                        "mobileStyle": {}
                    },
                    "uuid": "e4b98f50-b74c-45a8-a184-e5622cdd62fe",
                    "locked": false
                }
            }
        ]
    }
}
```

</details>

{% hint style="info" %}
**Note:** `onChange` is also the foundation on which the [Undo, Redo & Edit History](../server-side-configurations/server-side-options/undo-and-changes-history.md) feature was built on.
{% endhint %}

#### Example Function

The following code provides an example callback function for `onChange`.

```javascript
onChange: function (jsonFile, response) {
  console.log('json', jsonFile);
  console.log('response', response);
},
```

### **onRemoteChange**

The `onRemoteChange` callback is a bit different than `onChange`, because it monitors and tracks the changes of other users (those who are not the primary user) during [collaborative editing sessions](../other-customizations/collaborative-editing/). Using this callback allows you to monitor the changes of all end users in the same session.

Consider the following when using the `onRemoteChange` callback:

* `onChange` and `onRemoteChange` have the same [prerequisites](tracking-message-changes.md#prerequisites).
* `onChange` and `onRemoteChange` have the same [callback response schema structure](tracking-message-changes.md#callback-response-schema).

The following code provides an example callback function for `onRemoteChange`.

```javascript
onRemoteChange: function (jsonFile, response) {
  console.log('json', jsonFile);
  console.log('response', response);
},
```

<details>

<summary>onRemoteChange JSON example</summary>

The following JSON displays an example of the onRemoteChange callback response.

```json
{
    "message": {
        "page": {
            "body": {
                "container": {
                    "style": {
                        "background-color": "#FFFFFF"
                    }
                },
                "content": {
                    "computedStyle": {
                        "linkColor": "#0068A5",
                        "messageBackgroundColor": "transparent",
                        "messageWidth": "500px"
                    },
                    "style": {
                        "color": "#000000",
                        "font-family": "Arial, Helvetica, sans-serif"
                    }
                },
                "type": "mailup-bee-page-properties",
                "webFonts": []
            },
            "description": "Empty template for BEE",
            "rows": [
                {
                    "columns": [
                        {
                            "grid-columns": 12,
                            "modules": [
                                {
                                    "type": "mailup-bee-newsletter-modules-heading",
                                    "descriptor": {
                                        "heading": {
                                            "title": "h1",
                                            "text": "<span class=\"tinyMce-placeholder\">I'm a new title block</span>",
                                            "style": {
                                                "color": "#555555",
                                                "font-size": "23px",
                                                "font-family": "inherit",
                                                "link-color": "#0068A5",
                                                "line-height": "120%",
                                                "text-align": "center",
                                                "direction": "ltr",
                                                "font-weight": "700",
                                                "letter-spacing": "0px"
                                            }
                                        },
                                        "style": {
                                            "width": "100%",
                                            "text-align": "center",
                                            "padding-top": "0px",
                                            "padding-right": "0px",
                                            "padding-bottom": "0px",
                                            "padding-left": "0px"
                                        },
                                        "mobileStyle": {}
                                    },
                                    "uuid": "e4b98f50-b74c-45a8-a184-e5622cdd62fe",
                                    "locked": false
                                }
                            ],
                            "style": {
                                "background-color": "transparent",
                                "border-bottom": "0px solid transparent",
                                "border-left": "0px solid transparent",
                                "border-right": "0px solid transparent",
                                "border-top": "0px solid transparent",
                                "padding-bottom": "5px",
                                "padding-left": "0px",
                                "padding-right": "0px",
                                "padding-top": "5px"
                            },
                            "uuid": "bb75ccd1-db9a-4c93-9cf4-85644245b25d"
                        }
                    ],
                    "container": {
                        "style": {
                            "background-color": "transparent",
                            "background-image": "none",
                            "background-position": "top left",
                            "background-repeat": "no-repeat"
                        }
                    },
                    "content": {
                        "computedStyle": {
                            "hideContentOnDesktop": false,
                            "hideContentOnMobile": false,
                            "rowColStackOnMobile": true,
                            "rowReverseColStackOnMobile": false,
                            "verticalAlign": "top"
                        },
                        "style": {
                            "background-color": "transparent",
                            "background-image": "none",
                            "background-position": "top left",
                            "background-repeat": "no-repeat",
                            "color": "#000000",
                            "width": "500px"
                        }
                    },
                    "empty": false,
                    "locked": false,
                    "synced": false,
                    "type": "row-1-columns-12",
                    "uuid": "fd68e622-bad7-4cca-84e2-a0315d4ffba7"
                }
            ],
            "template": {
                "name": "template-base",
                "type": "basic",
                "version": "2.0.0"
            },
            "title": "Empty Template"
        }
    },
    "changes": {
        "code": "1300",
        "description": "Title dropped",
        "patches": [
            {
                "op": "add",
                "path": "/rows/0/columns/0/modules/0",
                "value": {
                    "type": "mailup-bee-newsletter-modules-heading",
                    "descriptor": {
                        "heading": {
                            "title": "h1",
                            "text": "<span class=\"tinyMce-placeholder\">I'm a new title block</span>",
                            "style": {
                                "color": "#555555",
                                "font-size": "23px",
                                "font-family": "inherit",
                                "link-color": "#0068A5",
                                "line-height": "120%",
                                "text-align": "center",
                                "direction": "ltr",
                                "font-weight": "700",
                                "letter-spacing": "0px"
                            }
                        },
                        "style": {
                            "width": "100%",
                            "text-align": "center",
                            "padding-top": "0px",
                            "padding-right": "0px",
                            "padding-bottom": "0px",
                            "padding-left": "0px"
                        },
                        "mobileStyle": {}
                    },
                    "uuid": "e4b98f50-b74c-45a8-a184-e5622cdd62fe",
                    "locked": false
                }
            }
        ],
        "value": ""
    }
}
```

</details>

### **onViewChange**

The `onViewChange` callback differs from `onChange` and `onRemoteChange` because it doesn't track content changes in the message itself — instead, it fires when the user interacts with different interface views inside the Beefree SDK. This includes navigating to the File Manager, opening the Preview mode, or launching the Image Editor. It’s especially useful for understanding user behavior, enhancing user experience analytics, or conditionally triggering application logic based on view changes.

Consider the following when using the `onViewChange` callback:

* `onViewChange` does **not** return a message JSON object like `onChange` or `onRemoteChange`.
* It returns a single string representing the current view.
* Typical values include:
  * `'fileManager'` – when the File Manager is opened
  * `'editor'` – when the user returns to the main editor (including on initial load)
  * `'preview'` – when the Preview mode is opened
  * `'imageEditor'` – when the Image Editor is opened

The following code provides an example callback function for `onViewChange`:

```javascript
onViewChange: function (view) {
  console.log('Current SDK view:', view);
}
```

### **Configure onChange and onRemoteChange**

{% hint style="info" %}
**Note:** This section discusses how to configure both `onChange` and `onRemoteChange`. Please keep in mind that the configurations apply to both callbacks.
{% endhint %}

This section discusses how to configure `onChange` and `onRemoteChange`.

This parameter defines when the tracking is active in the builder.

#### **onChange Event**

```javascript

onChange: function (jsonFile, response) { // do something with response... },

```

The `onChange` callback is triggered every time the builder tracks a change in the message. It returns the message JSON and a response JSON which contains all the information needed to handle any of the use cases described above.

#### **Callback response schema**

```javascript

{
    "code": "01", // See content and action codes bellow
    "description": "string",
    "value": "string", // See the chart below
    "patches": {...} // JSON patch formatted object
}

```

#### Callback Parameters <a href="#callback-parameters" id="callback-parameters"></a>

The following table lists the parameters in the onChange and onRemoteChange callback response schema and their corresponding types and values.&#x20;

<table><thead><tr><th>Parameter</th><th width="155.33333333333331">Type</th><th>Value</th></tr></thead><tbody><tr><td><code>code</code></td><td>string</td><td>Unique identifier for the event created by combining the content code with the action code.</td></tr><tr><td><code>description</code></td><td>string</td><td>A text description of the event in the chosen language. (e.g. Image Block Padding Left: 5px)</td></tr><tr><td><code>value</code></td><td>string</td><td>If available, this is the new value. (e.g. If padding changes to 5px, then the value returned is “5px”)</td></tr><tr><td><code>patches</code></td><td>array</td><td>An array of patches in the JSON Patch specification. JSON Patch is specified in <a href="https://datatracker.ietf.org/doc/html/rfc6902">RFC 6902</a> from the IETF.</td></tr></tbody></table>

## Content Codes <a href="#content-codes" id="content-codes"></a>

| Code   | Content               |
| ------ | --------------------- |
| **01** | Text Block            |
| **02** | Image Block           |
| **03** | Button Block          |
| **04** | Divider Block         |
| **05** | Social Block          |
| **06** | Dynamic Content Block |
| **07** | HTML Block            |
| **08** | Video Block           |
| **09** | Form                  |
| **10** | Icons                 |
| **11** | Menu                  |
| **14** | Row                   |
| **16** | Message               |
| **18** | Spacer                |
| **22** | Paragraph             |
| **23** | List                  |
| **26** | Table                 |

## Common Actions <a href="#common-actions" id="common-actions"></a>

| Code    | Action                        |
| ------- | ----------------------------- |
| **00**  | Dropped                       |
| **01**  | Dragged                       |
| **02**  | Deleted                       |
| **03**  | Duplicated                    |
| **04**  | Changed                       |
| **05**  | Opened                        |
| **06**  | Closed                        |
| **07**  | Locked                        |
| **08**  | Saved                         |
| **09**  | Restored                      |
| **10**  | Content area background color |
| **11**  | Do not stack on mobile        |
| **12**  | Row background image          |
| **13**  | Background Center             |
| **14**  | Background Repeat             |
| **15**  | Background Full width         |
| **16**  | Row Display condition         |
| **17**  | Reverse stack order on mobile |
| **20**  | Text color                    |
| **21**  | Link color                    |
| **23**  | Text edited                   |
| **24**  | Line height                   |
| **25**  | Content area width            |
| **27**  | Background color              |
| **28**  | Default font                  |
| **30**  | Padding All sides             |
| **31**  | Padding Left                  |
| **32**  | Padding Right                 |
| **33**  | Padding Top                   |
| **34**  | Padding Bottom                |
| **40**  | Hide on mobile                |
| **41**  | Video url                     |
| **42**  | Play icon type                |
| **43**  | Play icon color               |
| **44**  | Play icon size                |
| **50**  | Align                         |
| **51**  | Automatic image resizing      |
| **52**  | Full width on mobile          |
| **53**  | Image width                   |
| **60**  | Alternate text                |
| **61**  | Dynamic image src             |
| **62**  | Dynamic image toggle          |
| **63**  | Change image                  |
| **64**  | Image link                    |
| **70**  | Button Align                  |
| **71**  | Button Link type              |
| **72**  | Button width                  |
| **73**  | Button Auto width             |
| **74**  | Button Background color       |
| **75**  | Border radius                 |
| **80**  | HTML edited                   |
| **81**  | Border All sides              |
| **82**  | Border Left                   |
| **83**  | Border Right                  |
| **84**  | Border Top                    |
| **85**  | Border Bottom                 |
| **90**  | Divider Line toggle           |
| **91**  | Divider Width                 |
| **92**  | Divider Height                |
| **93**  | Divider Align                 |
| **95**  | Icon Name                     |
| **96**  | Icon Alternate text           |
| **97**  | Icon Url                      |
| **98**  | Icon spacing                  |
| **99**  | Icon Align                    |
| **128** | Background Video              |
| **129** | Paragraph Spacing             |
| **130** | Font Weight                   |
| **131** | List Type                     |
| **132** | Start List                    |
| **133** | List Spacing                  |
| **134** | List Indent                   |
| **135** | List Style Position           |

## Complete Event Chart <a href="#complete-event-chart" id="complete-event-chart"></a>

<table><thead><tr><th width="139">Code</th><th>Description</th><th width="146">Type</th><th>Value</th></tr></thead><tbody><tr><td><strong>0100</strong></td><td>Text dropped</td><td>module</td><td></td></tr><tr><td><strong>0101</strong></td><td>Text dragged</td><td>module</td><td></td></tr><tr><td><strong>0102</strong></td><td>Text deleted</td><td>module</td><td></td></tr><tr><td><strong>0103</strong></td><td>Text duplicated</td><td>module</td><td></td></tr><tr><td><strong>0120</strong></td><td>Text color {{value}}</td><td>string</td><td>Hex color code (e.g. #FFFFFF)</td></tr><tr><td><strong>0121</strong></td><td>Link color {{value}}</td><td>string</td><td>Hex color code (e.g. #FFFFFF)</td></tr><tr><td><strong>0123</strong></td><td>Text edited</td><td>string</td><td>HTML</td></tr><tr><td><strong>0124</strong></td><td>Line height {{value}}</td><td>string</td><td>Value as percent (e.g. 150%)</td></tr><tr><td><strong>0130</strong></td><td>Padding Add sides {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0131</strong></td><td>Padding Left {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0132</strong></td><td>Padding Right {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0133</strong></td><td>Padding Top {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0134</strong></td><td>Padding Bottom {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0140</strong></td><td>Hide on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0200</strong></td><td>Image dropped</td><td>module</td><td></td></tr><tr><td><strong>0201</strong></td><td>Image dragged</td><td>module</td><td></td></tr><tr><td><strong>0202</strong></td><td>Image deleted</td><td>module</td><td></td></tr><tr><td><strong>0203</strong></td><td>Image duplicated</td><td>module</td><td></td></tr><tr><td><strong>0230</strong></td><td>Padding Add sides {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0231</strong></td><td>Padding Left {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0232</strong></td><td>Padding Right {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0233</strong></td><td>Padding Top {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0234</strong></td><td>Padding Bottom {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0240</strong></td><td>Hide on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0250</strong></td><td>Align {{value}}</td><td>string</td><td>left | right | center</td></tr><tr><td><strong>0251</strong></td><td>Automatic image resizing</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0252</strong></td><td>Full width on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0253</strong></td><td>Image width {{value}}</td><td>string</td><td>%</td></tr><tr><td><strong>0260</strong></td><td>Alternate Text</td><td>string</td><td>text value</td></tr><tr><td><strong>0261</strong></td><td>Dynamic image</td><td>string</td><td>Image path</td></tr><tr><td><strong>0262</strong></td><td>Dynamic image toggle</td><td>boolean</td><td>false (only triggered when disabled)</td></tr><tr><td><strong>0263</strong></td><td>Change image</td><td>string</td><td>Image path</td></tr><tr><td><strong>0264</strong></td><td>Image link</td><td>string</td><td>Url</td></tr><tr><td><strong>0300</strong></td><td>Button dropped</td><td>module</td><td></td></tr><tr><td><strong>0301</strong></td><td>Button dragged</td><td>module</td><td></td></tr><tr><td><strong>0302</strong></td><td>Button deleted</td><td>module</td><td></td></tr><tr><td><strong>0303</strong></td><td>Button duplicated</td><td>module</td><td></td></tr><tr><td><strong>0320</strong></td><td>Text color {{value}}</td><td>string</td><td>Hex color code (e.g. #FFFFFF)</td></tr><tr><td><strong>0324</strong></td><td>Line height {{value}}</td><td>string</td><td>Value as percent (e.g. 150%)</td></tr><tr><td><strong>0330</strong></td><td>Padding Add sides {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0331</strong></td><td>Padding Left {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0332</strong></td><td>Padding Right {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0333</strong></td><td>Padding Top {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0334</strong></td><td>Padding Bottom {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0340</strong></td><td>Hide on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0370</strong></td><td>Align {{value}}</td><td>string</td><td>left | right | center</td></tr><tr><td><strong>0371</strong></td><td>Link type {{value}}</td><td>string</td><td>Url</td></tr><tr><td><strong>0372</strong></td><td>Button width {{value}}</td><td>string</td><td>%</td></tr><tr><td><strong>0373</strong></td><td>Auto width</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0374</strong></td><td>Background color {{value}}</td><td>string</td><td>Hex Color Code (e.g. #FFFFFF)</td></tr><tr><td><strong>0375</strong></td><td>Border radius</td><td>string</td><td>Value in pixels (e.g. 5px)</td></tr><tr><td><strong>0381</strong></td><td>Border Add sides {{value}}</td><td>string</td><td>Value in pixels | Border Style | Hex color (e.g. 1px solid #C7702E)</td></tr><tr><td><strong>0382</strong></td><td>Border Left {{value}}</td><td>string</td><td>Value in pixels | Border Style | Hex color 1px solid #C7702E</td></tr><tr><td><strong>0383</strong></td><td>Border Right {{value}}</td><td>string</td><td>Value in pixels | Border Style | Hex color 1px solid #C7702E</td></tr><tr><td><strong>0384</strong></td><td>Border Top {{value}}</td><td>string</td><td>Value in pixels | Border Style | Hex color 1px solid #C7702E</td></tr><tr><td><strong>0385</strong></td><td>Border Bottom {{value}}</td><td>string</td><td>Value in pixels | Border Style | Hex color 1px solid #C7702E</td></tr><tr><td><strong>0400</strong></td><td>Divider dropped</td><td>module</td><td></td></tr><tr><td><strong>0401</strong></td><td>Divider dragged</td><td>module</td><td></td></tr><tr><td><strong>0402</strong></td><td>Divider deleted</td><td>module</td><td></td></tr><tr><td><strong>0403</strong></td><td>Divider duplicated</td><td>module</td><td></td></tr><tr><td><strong>0430</strong></td><td>Padding Add sides {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0431</strong></td><td>Padding Left {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0432</strong></td><td>Padding Right {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0433</strong></td><td>Padding Top {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0434</strong></td><td>Padding Bottom {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0440</strong></td><td>Hide on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0490</strong></td><td>Line</td><td>string</td><td>Value in pixels | Border Style | Hex color 1px solid #C7702E</td></tr><tr><td><strong>0491</strong></td><td>Width {{value}}</td><td>string</td><td>Value as percent (e.g. 150%)</td></tr><tr><td><strong>0492</strong></td><td>Height {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0493</strong></td><td>Align {{value}}</td><td>string</td><td>left | right | center</td></tr><tr><td><strong>0500</strong></td><td>Social dropped</td><td>module</td><td></td></tr><tr><td><strong>0501</strong></td><td>Social dragged</td><td>module</td><td></td></tr><tr><td><strong>0502</strong></td><td>Social deleted</td><td>module</td><td></td></tr><tr><td><strong>0503</strong></td><td>Social duplicated</td><td>module</td><td></td></tr><tr><td><strong>0530</strong></td><td>Padding Add sides {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0531</strong></td><td>Padding Left {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0532</strong></td><td>Padding Right {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0533</strong></td><td>Padding Top {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0534</strong></td><td>Padding Bottom {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0540</strong></td><td>Hide on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0595</strong></td><td>Name {{value}}</td><td>string</td><td>Icon Name</td></tr><tr><td><strong>0596</strong></td><td>Alternate Text {{value}}</td><td>string</td><td>Icon Alternate text</td></tr><tr><td><strong>0597</strong></td><td>Image Url</td><td>string</td><td>Icon Url</td></tr><tr><td><strong>0598</strong></td><td>Icon spacing {{value}}</td><td>string</td><td>Value in pixels (e.g. 0 0 5px 15px)</td></tr><tr><td><strong>0599</strong></td><td>Align {{value}}</td><td>string</td><td>left | right | center</td></tr><tr><td><strong>0600</strong></td><td>Dynamic content dropped</td><td>module</td><td></td></tr><tr><td><strong>0601</strong></td><td>Dynamic content dragged</td><td>module</td><td></td></tr><tr><td><strong>0602</strong></td><td>Dynamic content deleted</td><td>module</td><td></td></tr><tr><td><strong>0603</strong></td><td>Dynamic content duplicated</td><td>module</td><td></td></tr><tr><td><strong>0604</strong></td><td>Dynamic content changed</td><td>string</td><td>value</td></tr><tr><td><strong>0640</strong></td><td>Hide on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0700</strong></td><td>HTML dropped</td><td>module</td><td></td></tr><tr><td><strong>0701</strong></td><td>HTML dragged</td><td>module</td><td></td></tr><tr><td><strong>0702</strong></td><td>HTML deleted</td><td>module</td><td></td></tr><tr><td><strong>0703</strong></td><td>HTML duplicated</td><td>module</td><td></td></tr><tr><td><strong>0740</strong></td><td>Hide on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0780</strong></td><td>HTML edited</td><td>string</td><td>HTML</td></tr><tr><td><strong>0800</strong></td><td>Video dropped</td><td>module</td><td></td></tr><tr><td><strong>0801</strong></td><td>Video dragged</td><td>module</td><td></td></tr><tr><td><strong>0802</strong></td><td>Video deleted</td><td>module</td><td></td></tr><tr><td><strong>0803</strong></td><td>Video duplicated</td><td>module</td><td></td></tr><tr><td><strong>0830</strong></td><td>Padding Add sides {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0831</strong></td><td>Padding Left {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0832</strong></td><td>Padding Right {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0833</strong></td><td>Padding Top {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0834</strong></td><td>Padding Bottom {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>0840</strong></td><td>Hide on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>0841</strong></td><td>Video url</td><td>string</td><td>Video Url</td></tr><tr><td><strong>0842</strong></td><td>Play icon type {{value}}</td><td>string</td><td>Play icon type (e.g. Round outline)</td></tr><tr><td><strong>0843</strong></td><td>Play icon color {{value}}</td><td>string</td><td>light | dark</td></tr><tr><td><strong>0844</strong></td><td>Play icon size {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>1400</strong></td><td>Row dropped</td><td>row</td><td></td></tr><tr><td><strong>1401</strong></td><td>Row dragged</td><td>row</td><td></td></tr><tr><td><strong>1402</strong></td><td>Row deleted</td><td>row</td><td></td></tr><tr><td><strong>1403</strong></td><td>Row duplicated</td><td>row</td><td></td></tr><tr><td><strong>1410</strong></td><td>Content background color {{value}}</td><td>string</td><td>Hex Color Code (e.g. #FFFFFF)</td></tr><tr><td><strong>1411</strong></td><td>Do not stack on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>1412</strong></td><td>Row background image</td><td>string</td><td>Image path</td></tr><tr><td><strong>1413</strong></td><td>Center</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>1414</strong></td><td>Repeat</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>1415</strong></td><td>Full width</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>1416</strong></td><td>Display Condition</td><td>object</td><td>Display condition object</td></tr><tr><td><strong>1417</strong></td><td>Reverse stack order on mobile</td><td>boolean</td><td>true | false</td></tr><tr><td><strong>1430</strong></td><td>Padding Add sides {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>1431</strong></td><td>Padding Left {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>1432</strong></td><td>Padding Right {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>1433</strong></td><td>Padding Top {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>1434</strong></td><td>Padding Bottom {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>1474</strong></td><td>Background color {{value}}</td><td>string</td><td>Hex Color Code (e.g. #FFFFFF)</td></tr><tr><td><strong>1481</strong></td><td>Border Add sides {{value}}</td><td>string</td><td>Value in pixels | Border Style | Hex color 1px solid #C7702E</td></tr><tr><td><strong>1482</strong></td><td>Border Left {{value}}</td><td>string</td><td>Value in pixels | Border Style | Hex color 1px solid #C7702E</td></tr><tr><td><strong>1483</strong></td><td>Border Right {{value}}</td><td>string</td><td>Value in pixels | Border Style | Hex color 1px solid #C7702E</td></tr><tr><td><strong>1484</strong></td><td>Border Top {{value}}</td><td>string</td><td>Value in pixels | Border Style | Hex color 1px solid #C7702E</td></tr><tr><td><strong>1485</strong></td><td>Border Bottom {{value}}</td><td>string</td><td>Value in pixels | Border Style | Hex color 1px solid #C7702E</td></tr><tr><td><strong>1625</strong></td><td>Content area width {{value}}</td><td>string</td><td>Value in pixels (e.g. 25px)</td></tr><tr><td><strong>1626</strong></td><td>Background color {{value}}</td><td>string</td><td>Hex Color Code (e.g. #FFFFFF)</td></tr><tr><td><strong>1627</strong></td><td>Content area background color: {{value}}</td><td>string</td><td>Hex Color Code (e.g. #FFFFFF)</td></tr><tr><td><strong>1628</strong></td><td>Default font</td><td>string</td><td>Font</td></tr><tr><td><strong>1529</strong></td><td>Link color {{value}}</td><td>string</td><td>Hex Color Code (e.g. #FFFFFF)</td></tr><tr><td><strong>1605</strong></td><td>Message opened</td><td>page</td><td>JSON template</td></tr><tr><td><strong>1609</strong></td><td>Message restored (e.g. undo or redo history)</td><td>page</td><td>JSON template</td></tr><tr><td><strong>13130</strong></td><td>Button Font Weight</td><td>string</td><td></td></tr><tr><td><strong>14128</strong></td><td>Row Background Video</td><td>string</td><td>Video URL</td></tr><tr><td><strong>22130</strong></td><td>Paragraph Font Weight</td><td>string</td><td>Font Weight value</td></tr></tbody></table>
