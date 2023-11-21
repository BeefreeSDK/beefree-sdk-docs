# Methods and Events

1. [Instance Methods](broken-reference)
2. [Instance Events](broken-reference)

### Instance Methods <a href="#instance-methods" id="instance-methods"></a>

Assuming that `beePluginInstance` is the instance of your embedded builder application, here are the methods you can call:

| Method                                    | Description                                                                                                                                                                                                                                                                                                                             |
| ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `beePluginInstance.start(templateToLoad)` | Starts the builder, loading the `templateToLoad` JSON string with the template structure (if specified). If using the NPM package, you have additional options to pass here as defined on [the NPM page.](https://www.npmjs.com/package/@mailupinc/bee-plugin)                                                                          |
| `beePluginInstance.load(template)`        | Loads the JSON template string specified in the `template` parameter.                                                                                                                                                                                                                                                                   |
| `beePluginInstance.reload(template)`      | Loads the JSON template string specified in the `template` parameter. Unlike `beePluginInstance.load(template)`, the reload method does not trigger a loading dialog. This method helps quickly reload a template seamlessly for specific use cases, such as using a custom undo/redo feature or injecting custom content in real-time. |

If you use a paid plan, you can hide the top toolbar and control the builder from your application’s user interface. For example, it’s up to you at that point to have buttons above or below the builder.\
Here’s some useful methods for this scenario:

| Method                                        | Description                                                                                                                                                                            |
| --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `beePluginInstance.preview()`                 | Triggers the message preview behavior within the builder.                                                                                                                              |
| `beePluginInstance.togglePreview()`           | Open/close the message preview behavior within the builder.                                                                                                                            |
| `beePluginInstance.toggleStructure()`         | Controls the visibility of the structure outlines in the message editing portion of the builder.                                                                                       |
| `beePluginInstance.save()`                    | Invokes the `onSave` callback function. The application will pass two files to the function: a JSON file with the message structure (for later editing) and a ready-to-send HTML file. |
| `beePluginInstance.saveAsTemplate()`          | Invokes the `onSaveAsTemplate` callback function. The application will pass to the function a JSON file with the message structure (for later editing).                                |
| `beePluginInstance.send()`                    | Invokes the `onSend` callback function. The application will pass to the function a ready-to-send HTML file.                                                                           |
| `beePluginInstance. toggleMergeTagsPreview()` | Controls the visibility of sample content for merge tags in the message editing portion of the builder.                                                                                |

### Instance Events <a href="#instance-events" id="instance-events"></a>

The top toolbar displayed by default within the builder contains buttons that trigger certain actions. These are the callbacks that are triggered when the buttons are clicked.

| Event                  | Description                                                            | Returned values                                                             |
| ---------------------- | ---------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| **onSave**             | Fired when the Save button is clicked.                                 | JSON and HTML documents                                                     |
| **onSaveAsTemplate**   | Fired when “Save as template” is clicked.                              | JSON document                                                               |
| **onAutoSave**         | Fired automatically based on `autosave` configuration parameter value. | JSON document                                                               |
| **onSend**             | Fired when the “Send a test button” is clicked.                        | HTML document                                                               |
| **onLoad**             | Fired when the JSON is loaded in the builder.                          | JSON document                                                               |
| **onError**            | Fired every time an error occurs.                                      | Error message                                                               |
| **onPreview**          | Fired every time the preview button is pressed.                        | Status (Boolean)                                                            |
| **onTogglePreview**    | Fired every time the preview is opened or closed.                      | Status (Boolean)                                                            |
| **onChange**           | Fired every time a change on the message is performed.                 | [Read More](https://docs.beefree.io/tracking-message-changes/#how-it-works) |
| **onComment**          | Fired every time a thread or comment changes.                          | [Read More](https://docs.beefree.io/commenting/#commenting-callback)        |
| **onFilePickerInsert** | Fired when the “insert” button is clicked.                             | Object with file info                                                       |
| **onFilePickerCancel** | Fired when the “X” button is clicked.                                  | None                                                                        |
