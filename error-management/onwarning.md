# onWarning

1. [onWarning](broken-reference)
2. [Warning codes](broken-reference)
3. [onError callback](broken-reference)
4. [onInfo callback](broken-reference)
5. [Error codes reference](broken-reference)

The onWarning callback returns information about a soft error that doesn’t impact the normal usage of the builder. You can use this callback to track these errors, display a message or change any behavior in your application. The callback manages JSON as the output data format.

#### Configuration

To handle these warnings, add the onWarning callback to [beeConfig](https://docs.beefree.io/configuration-parameters/):

```


onWarning: function(errorMessage) { /* Implements function to handle warning responses */ }


```

#### Response

```


{
    "code": alfanumeric,
    "message": string
}


```

**Example**

```


{
    "code": 1000,
    "message": "Cannot call "send" while template is still loading."
}


```

#### Warning codes <a href="#warning-codes" id="warning-codes"></a>

| Code   | Message                                    | Detail                                                                                                                                                                                                                                                                                                                                                         |
| ------ | ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `1000` | bee.save is unavailable                    | <ul><li>Cannot call bee.save() while template is still loading. Use the onLoad callback to determine when it’s safe to use the save method.</li><li>After onLoad(), if bee.save() is not accessible, it’s due to an expired token.</li></ul>                                                                                                                   |
|        |                                            |                                                                                                                                                                                                                                                                                                                                                                |
| `1610` | Unknown module name                        | \[Grouping Content tiles]Unknown module name.                                                                                                                                                                                                                                                                                                                  |
|        |                                            |                                                                                                                                                                                                                                                                                                                                                                |
| `1620` | Duplicate module                           | \[Grouping Content tiles]Duplicate module                                                                                                                                                                                                                                                                                                                      |
|        |                                            |                                                                                                                                                                                                                                                                                                                                                                |
| `1630` | Invalid modulesGroups configuration        | \[Grouping Content tiles]Invalid modulesGroups configuration                                                                                                                                                                                                                                                                                                   |
| `1701` | AMP content detected                       | <p>The template loaded in the builder contains AMP content, but the builder is not configured with an AMP-compatible workspace. You can react to this warning by loading a workspace, using the <a href="https://about/workspaces/#switching-workspaces"><code>loadWorkspace(type)</code> method</a>.<br>Message: <code>AMP content has been loaded</code></p> |
| `1702` | Workspace not available in current plan    | <p>The workspace you have configured for the builder is not available for your subscription plan.</p><p>Message: <code>Workspaces not available in [${payload}] plan</code></p>                                                                                                                                                                                |
| `1703` | Action not available when loading template | <p>The action you’re trying to perform on the builder instance is not available during the loading of a template.<br>Message: <code>Cannot execute ${payload} during the template Loading</code></p>                                                                                                                                                           |
| `1704` | Feature not available in current plan      | <p>The feature you have configured for the builder is not available for your subscription plan.<br>Message: <code>[${featureName}] feature is not available in [${plan}] plan</code></p>                                                                                                                                                                       |
| `2000` | Generic Bump Error                         | \[Template validation] Default generic bump error                                                                                                                                                                                                                                                                                                              |
| `2100` | Invalid Target Version                     | \[Template validation] The target version does not exists                                                                                                                                                                                                                                                                                                      |
| `2200` | \[validation error detail]                 | <p>[Template validation] The JSON didn’t pass the validation.<br>The cause may be:</p><ul><li>Missing keys</li><li>Added unknown keys</li></ul><p>Message e.g.: <code>required key not provided @ data[u'page'][u'body'][u'content'][u'style'][u'color']</code></p>                                                                                            |
| `2300` | Missing Template Version                   | \[Template validation] There is no template version in the page                                                                                                                                                                                                                                                                                                |
| `2400` | Invalid Template Version                   | \[Template validation] There is no template version in the page                                                                                                                                                                                                                                                                                                |
| `2500` | Transformation Error                       | \[Template validation] Issues during JSON version migration                                                                                                                                                                                                                                                                                                    |
| `2600` | Backward Transformation Error              | \[Template validation] Issues during JSON version migration                                                                                                                                                                                                                                                                                                    |
| `3000` | Service Error                              | \[Template validation] System failure not related with invalid json files                                                                                                                                                                                                                                                                                      |

### onError callback <a href="#onerror-callback" id="onerror-callback"></a>

The onError callback returns information about the application errors. You can use this callback to track these errors, display a message or change any behavior in your application. The callback manages JSON as the output data format.

#### Configuration

To handle these errors, add the onWarning callback to [beeConfig](https://docs.beefree.io/configuration-parameters/):

```


onError: function(errorMessage) { /* Implements function to handle error messages */ } // [optional]


```

#### Response

```


{
    "code": alfanumeric,
    "message": string,
    "detail": string
}


```

**Example**

```


{
    "code": 1200,
    "message": "Template cannot be saved."
    "detail": "Type mismatch: scope is undefined"
}


```

### onInfo callback <a href="#oninfo-callback" id="oninfo-callback"></a>

This callback relates specifically to the [OpenAI AddOn](https://docs.beefree.io/openai-addon-customization/). The AddOn will transmit the usage data provided by OpenAI with each prompt response, without storing or tracking the data.

#### Configuration

To handle these errors, add the onInfo callback to [beeConfig](https://docs.beefree.io/configuration-parameters/):

```


onInfo: function(information) { 
/* Implements function to handle warning responses */ 
}


```

#### Response

```


{
  code: number,
  message: `string’,
  detail: object,
}


```

**Example**

```


AddOn Information
{
  code: 1000,
message: `Token usage for addon handle: ai-integration’,
  detail: {
    handle: ‘ai-integration’,
    promptId: ‘60bcc837-674c-4226-adad-91ee2a603b57’,
    usage: {
      prompt_tokens: 50,
      completion_tokens: 100,
      total_tokens: 150,
      uid: ‘string’
    },
  },
}


```

#### Error codes reference <a href="#error-codes-reference" id="error-codes-reference"></a>

Please refer to the following pages to have the full list of error codes:

* [Beefree SDK Builder errors](https://docs.beefree.io/editor-errors/)
* [Custom File System Provider errors](https://docs.beefree.io/file-system-provider-errors/)
* [Template validation/update errors](https://docs.beefree.io/template-validation-errors/)
