# Edit Single Row Mode

1. [How it works](broken-reference)
2. [Implementing the Save action](broken-reference)

### How it works <a href="#how-it-works" id="how-it-works"></a>

Our builders offer [ready-to-go rows to your end-users](https://docs.beefree.io/custom-rows/), which provide both structure and content to create contents faster. With Edit Single Row mode you can offer an easier way for your users to modify a single row with a tailored UI built to edit the row structure, content, and style settings without worrying about messing up with the overall design of the email campaign, landing page, or pop-up.

Edit Single Row mode complements the [Save Rows](https://docs.beefree.io/save-rows/) as it allows a complete control over the content of individual rows (e.g. the footer that requires to be updated) without the need to intervene into a full template, this will help you in implementing a more effective way to manage libraries of Saved Rows with a streamlined design process.

**Initializing the editor in Edit Single Row Mode**

```


type ClientConfig = {
  workspace?: {
    editSingleRow?: boolean
    // ....
  }
  // ....
}

const beeConfig: ClientConfig = {
  workspace:{
    editSingleRow: true
    // ....
  }
  // ....
}


// Create the instance 
function BeePlugin.create(token, beeConfig, (beePluginInstance) => { 
  //.... 

  beePluginInstance.start(template, { shared: false })
}


```

When a builder application is initialized with this mode enabled the UI will show to the user only properties that pertain to editing a single row, therefore:&#x20;

* the options to insert custom rows, saved rows, or new default rows are disabled,&#x20;
* the _Settings tab_ is unavailable, as those properties are specific to the entire document,
* when a row is selected on the editing stage, the action to _Delete, Duplicate, Comment, Save_ are not available.

![](https://docs.beefree.io/wp-content/uploads/2022/03/image1.png)

### Implementing the Save action <a href="#implementing-the-save-action" id="implementing-the-save-action"></a>

The following describes the recommended workflow to implement the Save action in your host SaaS application when the Single Edit Row mode is enabled.

In case your application uses the default [Toolbar](https://docs.beefree.io/toolbar-options/), you can leverage the save button to trigger the sequence of action to correctly save the row, the workflow is the same as the one documented in [saving-rows-workflow-for-developers](https://docs.beefree.io/save-rows/#saving-rows-workflow-for-developers), in short :

1. The user clicks on the save button
2. A contentDialog of type saveRow will be triggered.

In case your application doesn’t use the default Toolbar you will need to handle the row saving in a different way, following a couple of examples:

* Calling the [save method](https://docs.beefree.io/methods-and-events/#instance-methods). It will trigger the on [onSave](https://docs.beefree.io/methods-and-events/#instance-events) event with two arguments, one of them is the full message JSON that can be saved as a Saved Row (it’s the same JSON returned by the [onSaveRow ](https://docs.beefree.io/methods-and-events/#instance-events)event).

Example:

```


myCustomToolbarButton.onClick(() => beePluginInstance.save())
...

onSave: function (json, html) {
	myCustomApi.saveRow(json)
},


```

* Listening to the [onChange](https://docs.beefree.io/tracking-message-changes/#how-it-works) event. It will receive the updated full message JSON which again can be saved as a Saved Row.

Example:

```


onChange: function (json, response) {
	myCustomApi.saveRow(json)
},


```

**Merging saved rows in existing messages**

An effective way to update saved rows across multiple templates is by implementing the save action in combination with the [CSAPI](https://docs.beefree.io/message-services-api/), to handle a row update across multiple [existing templates](https://docs.beefree.io/message-services-api/#merging-saved-rows-in-existing-messages).
