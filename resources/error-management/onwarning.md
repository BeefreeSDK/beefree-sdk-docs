# onWarning

The onWarning callback returns information about a soft error that doesn’t impact the normal usage of the builder. You can use this callback to track these errors, display a message or change any behavior in your application. The callback manages JSON as the output data format.

## Configuration

To handle these warnings, add the onWarning callback to [beeConfig](../../getting-started/readme/installation/configuration-parameters/):

```javascript

onWarning: function(errorMessage) { /* Implements function to handle warning responses */ }

```

### Response

```javascript

{
    "code": alfanumeric,
    "message": string
}

```

### **Example**

```javascript

{
    "code": 1000,
    "message": "Cannot call "send" while template is still loading."
}

```

### Warning codes <a href="#warning-codes" id="warning-codes"></a>

<table><thead><tr><th width="131">Code</th><th width="194.33333333333331">Message</th><th>Detail</th></tr></thead><tbody><tr><td><code>1000</code></td><td>bee.save is unavailable</td><td><ul><li>Cannot call bee.save() while template is still loading. Use the onLoad callback to determine when it’s safe to use the save method.</li><li>After onLoad(), if bee.save() is not accessible, it’s due to an expired token.</li></ul></td></tr><tr><td><code>1610</code></td><td>Unknown module name</td><td>[Grouping Content tiles]Unknown module name.</td></tr><tr><td><code>1620</code></td><td>Duplicate module</td><td>[Grouping Content tiles]Duplicate module</td></tr><tr><td><code>1630</code></td><td>Invalid modulesGroups configuration</td><td>[Grouping Content tiles]Invalid modulesGroups configuration</td></tr><tr><td><code>1701</code></td><td>AMP content detected</td><td>The template loaded in the builder contains AMP content, but the builder is not configured with an AMP-compatible workspace. You can react to this warning by loading a workspace, using the <a href="../../getting-started/readme/installation/configuration-parameters/workspaces.md"><code>loadWorkspace(type)</code> method</a>.<br>Message: <code>AMP content has been loaded</code></td></tr><tr><td><code>1702</code></td><td>Workspace not available in current plan</td><td><p>The workspace you have configured for the builder is not available for your subscription plan.</p><p>Message: <code>Workspaces not available in [${payload}] plan</code></p></td></tr><tr><td><code>1703</code></td><td>Action not available when loading template</td><td>The action you’re trying to perform on the builder instance is not available during the loading of a template.<br>Message: <code>Cannot execute ${payload} during the template Loading</code></td></tr><tr><td><code>1704</code></td><td>Feature not available in current plan</td><td>The feature you have configured for the builder is not available for your subscription plan.<br>Message: <code>[${featureName}] feature is not available in [${plan}] plan</code></td></tr><tr><td><code>1730</code></td><td>Content defaults for the Table module is not valid</td><td>Your <a href="../../other-customizations/appearance/content-defaults.md#table">content defaults</a> are not valid for the table module.</td></tr><tr><td><code>2000</code></td><td>Generic Bump Error</td><td>[Template validation] Default generic bump error</td></tr><tr><td><code>2050</code></td><td>Generic Bump Error with warnings</td><td><p>[Template validation] Generic bump error, with warnings.</p><p></p><p><strong>Note:</strong> This error is dynamic. Depending on the scenario, you will receive a different error message.</p><p></p><p><strong>Use case:</strong> When the Bumper returns 200, but there are some portions of the JSON that should be corrected (for example unrecognized fields). The SDK triggers the <code>onWarning</code>, passing to the host-application an additional "warnings" array, containing the warning messages.</p></td></tr><tr><td><code>2100</code></td><td>Invalid Target Version</td><td>[Template validation] The target version does not exists</td></tr><tr><td><code>2200</code></td><td>[validation error detail]</td><td><p>[Template validation] The JSON didn’t pass the validation.<br>The cause may be:</p><ul><li>Missing keys</li><li>Added unknown keys</li></ul><p>Message e.g.: <code>required key not provided @ data[u'page'][u'body'][u'content'][u'style'][u'color']</code></p></td></tr><tr><td><code>2250</code></td><td>Bump template validation error</td><td>page/rows/0/columns/0/modules/0/descriptor/table/rows: malformed field (each row must contain the same number of cells)</td></tr><tr><td><code>2300</code></td><td>Missing Template Version</td><td>[Template validation] There is no template version in the page</td></tr><tr><td><code>2400</code></td><td>Invalid Template Version</td><td>[Template validation] There is no template version in the page</td></tr><tr><td><code>2500</code></td><td>Transformation Error</td><td>[Template validation] Issues during JSON version migration</td></tr><tr><td><code>2600</code></td><td>Backward Transformation Error</td><td>[Template validation] Issues during JSON version migration</td></tr><tr><td><code>3000</code></td><td>Service Error</td><td>[Template validation] System failure not related with invalid json files</td></tr></tbody></table>

## onError callback <a href="#onerror-callback" id="onerror-callback"></a>

The onError callback returns information about the application errors. You can use this callback to track these errors, display a message or change any behavior in your application. The callback manages JSON as the output data format.

## Configuration

To handle these errors, add the onWarning callback to [beeConfig](../../getting-started/readme/installation/configuration-parameters/):

```javascript

onError: function(errorMessage) { /* Implements function to handle error messages */ } // [optional]

```

### Response

```javascript

{
    "code": alfanumeric,
    "message": string,
    "detail": string
}

```

### **Example**

```javascript

{
    "code": 1200,
    "message": "Template cannot be saved."
    "detail": "Type mismatch: scope is undefined"
}

```

## OnInfo Callback

The `onInfo` callback notifies your application when a user clicks on **Apply** for any AI-generated text suggestion. This feature is specifically designed for the AI Writing Assistant AddOn and provides real-time usage data with each response, without storing or tracking the information.

To configure this in your app, add the `onInfo` callback to your `beeConfig`:

```json
onInfo: function (information) { 
  /* Implement function to handle info events such as when AI-generated text is applied */ 
}
```

### Example Response

Here’s an example of the data you can expect when the user applies AI-generated content:

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

## OnInfo Benefits and Use Cases

* **Enhanced Regeneration**: The `onInfo` callback provides more accurate AI-generated text when users click "Regenerate." For example, if a user is editing an email and the first AI suggestion isn’t quite right, they can click "Regenerate" and receive a more relevant version that better matches the tone of the email campaign.
* **Context Awareness**: When AI responses are applied, the `onInfo` callback ensures that context is preserved. Imagine a user is working on a long-form blog post with multiple sections. The callback helps maintain consistency in style and tone even as the user generates new content for each section.
* **Submit via Enter Key**: With the `submitOnEnterKey` configuration, users can submit AI-generated content quickly by pressing the **Enter** key. For instance, when filling out product descriptions in an e-commerce platform, users can simply hit **Enter** to accept the AI's suggestions, speeding up the process without having to manually click a button.
* **Multilingual Template Support**: The `onInfo` callback ensures that AI-generated text adapts well to multilingual templates. For instance, a marketing team working on a bilingual campaign can trust that the AI suggestions will correctly switch between languages, making it easier to localize content for different markets.
