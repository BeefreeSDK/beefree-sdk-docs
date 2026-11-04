# Warning, Error, and Info Callbacks

## `onWarning` Callback

The `onWarning` callback returns information about a soft error that doesn’t impact the normal usage of the builder. You can use this callback to track these errors, display a message or change any behavior in your application. The callback manages JSON as the output data format.

### Configuration

To handle these warnings, add the onWarning callback to [beeConfig](../../getting-started/readme/installation/configuration-parameters/):

{% code collapsedlinecount="10" %}
```javascript

onWarning: function(errorMessage) { /* Implements function to handle warning responses */ }

```
{% endcode %}

### Response

{% code collapsedlinecount="10" %}
```javascript

{
    "code": alfanumeric,
    "message": string
}

```
{% endcode %}

### **Example**

{% code collapsedlinecount="10" %}
```javascript

{
    "code": 1000,
    "message": "Cannot call "send" while template is still loading."
}

```
{% endcode %}

### Warning codes <a href="#warning-codes" id="warning-codes"></a>

<table><thead><tr><th width="131">Code</th><th width="194.33333333333331">Message</th><th>Detail</th></tr></thead><tbody><tr><td><code>1000</code></td><td>bee.save is unavailable</td><td><ul><li>Cannot call bee.save() while template is still loading. Use the onLoad callback to determine when it’s safe to use the save method.</li><li>After onLoad(), if bee.save() is not accessible, it’s due to an expired token.</li></ul></td></tr><tr><td><code>1610</code></td><td>Unknown module name</td><td>[Grouping Content tiles]Unknown module name.</td></tr><tr><td><code>1620</code></td><td>Duplicate module</td><td>[Grouping Content tiles]Duplicate module</td></tr><tr><td><code>1630</code></td><td>Invalid modulesGroups configuration</td><td>[Grouping Content tiles]Invalid modulesGroups configuration</td></tr><tr><td><code>1701</code></td><td>AMP content detected</td><td>The template loaded in the builder contains AMP content, but the builder is not configured with an AMP-compatible workspace. You can react to this warning by loading a workspace, using the <a href="../../getting-started/readme/installation/configuration-parameters/workspaces.md"><code>loadWorkspace(type)</code> method</a>.<br>Message: <code>AMP content has been loaded</code></td></tr><tr><td><code>1702</code></td><td>Workspace not available in current plan</td><td><p>The workspace you have configured for the builder is not available for your subscription plan.</p><p>Message: <code>Workspaces not available in [${payload}] plan</code></p></td></tr><tr><td><code>1703</code></td><td>Action not available when loading template</td><td>The action you’re trying to perform on the builder instance is not available during the loading of a template.<br>Message: <code>Cannot execute ${payload} during the template Loading</code></td></tr><tr><td><code>1704</code></td><td>Feature not available in current plan</td><td>The feature you have configured for the builder is not available for your subscription plan.<br>Message: <code>[${featureName}] feature is not available in [${plan}] plan</code></td></tr><tr><td><code>1730</code></td><td>Content defaults for the Table module is not valid</td><td>Your <a href="../../other-customizations/appearance/content-defaults.md#table">content defaults</a> are not valid for the table module.</td></tr><tr><td><code>2000</code></td><td>Generic Bump Error</td><td>[Template validation] Default generic bump error</td></tr><tr><td><code>2050</code></td><td>Generic Bump Error with warnings</td><td><p>[Template validation] Generic bump error, with warnings.</p><p><strong>Note:</strong> This error is dynamic. Depending on the scenario, you will receive a different error message.</p><p><strong>Use case:</strong> When the Bumper returns 200, but there are some portions of the JSON that should be corrected (for example unrecognized fields). The SDK triggers the <code>onWarning</code>, passing to the host-application an additional "warnings" array, containing the warning messages.</p></td></tr><tr><td><code>2100</code></td><td>Invalid Target Version</td><td>[Template validation] The target version does not exists</td></tr><tr><td><code>2200</code></td><td>[validation error detail]</td><td><p>[Template validation] The JSON didn’t pass the validation.<br>The cause may be:</p><ul><li>Missing keys</li><li>Added unknown keys</li></ul><p>Message e.g.: <code>required key not provided @ data[u'page'][u'body'][u'content'][u'style'][u'color']</code></p></td></tr><tr><td><code>2250</code></td><td>Bump template validation error</td><td>page/rows/0/columns/0/modules/0/descriptor/table/rows: malformed field (each row must contain the same number of cells)</td></tr><tr><td><code>2300</code></td><td>Missing Template Version</td><td>[Template validation] There is no template version in the page</td></tr><tr><td><code>2400</code></td><td>Invalid Template Version</td><td>[Template validation] There is no template version in the page</td></tr><tr><td><code>2500</code></td><td>Transformation Error</td><td>[Template validation] Issues during JSON version migration</td></tr><tr><td><code>2600</code></td><td>Backward Transformation Error</td><td>[Template validation] Issues during JSON version migration</td></tr><tr><td><code>3000</code></td><td>Service Error</td><td>[Template validation] System failure not related with invalid json files</td></tr><tr><td><code>3001</code></td><td>loadConfig request was debounced due to rapid consecutive calls</td><td></td></tr></tbody></table>

## `onError` callback <a href="#onerror-callback" id="onerror-callback"></a>

The `onError` callback returns information about the application errors. You can use this callback to track these errors, display a message or change any behavior in your application. The callback manages JSON as the output data format.

### Configuration

To handle these errors, add the `onError` callback to [beeConfig](../../getting-started/readme/installation/configuration-parameters/):

{% code collapsedlinecount="10" %}
```javascript

onError: function(errorMessage) { /* Implements function to handle error messages */ } // [optional]

```
{% endcode %}

### Response

{% code collapsedlinecount="10" %}
```javascript

{
    "code": alfanumeric,
    "message": string,
    "detail": string
}

```
{% endcode %}

### **Example**

{% code collapsedlinecount="10" %}
```javascript

{
    "code": 1200,
    "message": "Template cannot be saved."
    "detail": "Type mismatch: scope is undefined"
}

```
{% endcode %}

## **Extend onError**

The `extendedOnError` feedback in Beefree SDK includes API-related failures, giving you additional insights and more control over error handling. With this optional extension, you can improve debugging, frontend error handling, and track issues more effectively.

You can extend `onError` to report API-related errors.

Take the following steps to extend `onError`:

1. Add the [`onError` callback](warning-error-info-callbacks.md#onerror-callback) to your beeConfig.
2. Configure your callback function.
3. Add `extendedOnError` to your `beeConfig` file.
4. Set the boolean `extendedOnError` boolean to `true`.

The following code snippet provides an example of how this looks in the `beeConfig`:

{% code collapsedlinecount="10" %}
```javascript
const beeConfig = {
    ...
    extendedOnError: true // [optional, default/fallback: false]
    ...
};  
```
{% endcode %}

### **Error code and message**

This section lists and describes the possible error code and their corresponding codes, messages, and fixes.

| Error               | Code   | Message                             | Detail                                                                                                           |
| ------------------- | ------ | ----------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `API_GENERIC_ERROR` | `9900` | `A generic network error occurred.` | `A network error occurred while calling service TEST` [https://beefree.io/test-url](https://beefree.io/test-url) |

**Sample Error Message**

{% code collapsedlinecount="10" %}
```json
{
  code: 9900,
  message: 'A generic network error occurred.',
  detail: 'A network error occurred while calling service TEST https://beefree.io/test-url',
  data: {
    // an extract of Axios HTTP error details
    "message":"Request failed with status code 404",
    "status":404,
    "code":"ERR_BAD_REQUEST",
    "url":"https://beefree.io/test-url",
    "method":"get",
    "headers":{"Accept":"application/json, text/plain, */*"}
  },
}
```
{% endcode %}

## `onInfo` Callback

The `onInfo` callback reports information from the AI AddOns: real-time usage data with each response, without storing or tracking the information, and events such as a user clicking **Apply** on an AI-generated text suggestion. Tell the AddOns apart by `detail.handle`.

| Code   | Handle           | AddOn                                                                                      | Sent when                                                  |
| ------ | ---------------- | ------------------------------------------------------------------------------------------ | ---------------------------------------------------------- |
| `1000` | `ai-integration` | [AI Writing Assistant](../../ai-and-mcp/ai-addons/ai-writing-assistant/)                   | A prompt generates content (token usage).                  |
| `1001` | `ai-integration` | [AI Writing Assistant](../../ai-and-mcp/ai-addons/ai-writing-assistant/)                   | The user applies AI-generated content.                     |
| `1000` | `ai-alt-text`    | [Alternate Text Generation with AI](../../ai-and-mcp/ai-addons/generate-alt-text-with-ai/) | Alternate text is generated (images processed).            |
| `1000` | `ai-agent`       | [AI Co-Pilot](../../ai-and-mcp/ai-co-pilot-beta/)                                          | Each request of a prompt to the AI provider (token usage). |
| `1010` | `ai-agent`       | [AI Co-Pilot](../../ai-and-mcp/ai-co-pilot-beta/)                                          | The chat history changes.                                  |

The `usage` object has a different shape for each AddOn: check `detail.handle` before reading it.

To configure this in your app, add the `onInfo` callback to your [beeConfig](../../getting-started/readme/installation/configuration-parameters/):

{% code collapsedlinecount="10" %}
```javascript
onInfo: function (information) { 
  /* Implement function to handle info events such as when AI-generated text is applied */ 
}
```
{% endcode %}

### Response

{% code collapsedlinecount="10" %}
```javascript
{
  code: number,
  message: string,
  detail: object,
}
```
{% endcode %}

### Example Response on prompt generation

Here’s an example of the data you can expect when the user asks to generate content:

{% code collapsedlinecount="10" %}
```javascript

AddOn Information
{
  "code": 1000,
  "message": "Token usage for addon handle: ai-integration",
  "detail": {
    "handle": "ai-integration",
    "promptId": "60bcc837-674c-4226-adad-91ee2a603b57",
    "usage": {
      "prompt_tokens": 50,
      "completion_tokens": 100,
      "total_tokens": 150,
      "uid": "string"
    },
  },
}

```
{% endcode %}

### Example Response on prompt apply

Here’s an example of the data you can expect when the user applies AI-generated content:

{% code collapsedlinecount="10" %}
```json
{
    "code": 1001,
    "message": "Prompt '60bcc837-674c-4226-adad-91ee2a603b57' has been applied",
    "detail": {
      "handle": "ai-integration",
      "promptId": "60bcc837-674c-4226-adad-91ee2a603b57",
      "moduleId": "9c2c6e63-f9c3-4e8d-9e3e-f9a658fefe46",
      "content": "Discover the Best Email Editor"
    }
}
```
{% endcode %}

### Example Response on AI Co-Pilot token usage

Here’s an example of the data you can expect for each request the [AI Co-Pilot](../../ai-and-mcp/ai-co-pilot-beta/) sends to the AI provider. A prompt can send several requests, all with the same `promptId`: add them up to get the usage of the prompt. See [Tracking token usage](../../ai-and-mcp/ai-co-pilot-beta/#tracking-token-usage-oninfo-code-1000) for the fields of `usage`.

{% code collapsedlinecount="10" %}
```json
{
    "code": 1000,
    "message": "Token usage for addon handle: ai-agent",
    "detail": {
      "handle": "ai-agent",
      "promptId": "Xw3kP9qLm2Rt7VbN",
      "usage": {
        "inputTokens": 5120,
        "inputTokenDetails": { "noCacheTokens": 1024, "cacheReadTokens": 4096, "cacheWriteTokens": 0 },
        "outputTokens": 380,
        "outputTokenDetails": { "textTokens": 380, "reasoningTokens": 0 },
        "totalTokens": 5500
      }
    }
}
```
{% endcode %}

### Example Response on AI Co-Pilot chat history change

Here’s an example of the data you can expect when the [AI Co-Pilot](../../ai-and-mcp/ai-co-pilot-beta/) chat history changes. `messages` is the full conversation: persist it and pass it back as `initialMessages` to restore the chat in the next session.

{% code collapsedlinecount="10" %}
```javascript
{
    "code": 1010,
    "message": "Messages changed for addon handle: ai-agent",
    "detail": {
      "handle": "ai-agent",
      "messages": [ /* full chat history */ ]
    }
}
```
{% endcode %}
