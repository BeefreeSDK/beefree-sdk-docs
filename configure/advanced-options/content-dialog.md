# Content Dialog

{% hint style="info" %}
This feature is available on Beefree SDK [paid plans](https://dam.beefree.io/pluginpricing) only.
{% endhint %}

## The problem <a href="#the-problem" id="the-problem"></a>

When designing a message or a landing page with Beefree’s editors, there might be cases in which users of your application insert a [merge tag](smart-merge-tags.md), add a link to an image, or apply a [conditional statement](content-dialog.md#display-conditions).

It’s all good until things scale up. For example…

* What if you have 400 merge tags? You can [feed an array of merge tags](smart-merge-tags.md) to the editor, but that’s not going to cut it.
* What if it’s a 6,000 product database? How will they locate the right one? [Special Links](special-links-and-merge-tags.md) is not the right fit.
* And what if a [display condition](content-dialog.md#display-conditions) needs to be built on-the-fly?

## A flexible solution <a href="#a-flexible-solution" id="a-flexible-solution"></a>

Since the Beefree builders are used in hundreds of applications, and since each of them is facing different user experience challenges like the examples mentioned above, we decided that this was really a case where _one size does **not** fit all_.

So we engineered a solution that puts you in **control** and provides a large amount of **flexibility**.

If your users want to insert a merge tag or a display condition, you control how that will happen. You can overlay a window on top of the editor, for example, and display a simple search box, a list of categories to browse, or a complex configurator to build an advanced conditional statement.

We call this feature _Content Dialog_.

<figure><img src="../../.gitbook/assets/bee_plugin_content_dialog_product_search.png" alt=""><figcaption></figcaption></figure>

## An interactive UI layer <a href="#an-interactive-ui-layer" id="an-interactive-ui-layer"></a>

_Content Dialog_ allows you to build user interfaces for your users to locate & insert merge tags, links, conditional statements, and more. It lets you establish an interaction layer between the editor and your application (e.g. you show a pop-up window) that allows your users to locate/build/insert specific content (merge tags, links, conditional statements, etc.). And you’re in full control of the UI.

For example, imagine you want your customers to be able to quickly locate a link to a product page and assign that link to a button, image, or text. _Content Dialog_ will let you build the right user experience.

Here is a visual example of what you could accomplish in that _find a product link_ scenario.

<figure><img src="../../.gitbook/assets/2Product_Search.jpeg" alt=""><figcaption></figcaption></figure>

The user experience in this interaction layer is entirely up to you. In the example above, the user clicked on “Find a product” (or alike) in the editor, and a modal window was shown, with a search box in it. Since you decide what the user experience will be like, you are fully in control of how users will select and insert:

* a text placeholder ([merge tag](smart-merge-tags.md))
* a dynamic link or a link to specific content ([special link](smart-merge-tags.md))
* a markup placeholder ([merge content](smart-merge-tags.md))
* a conditional statement ([display conditions](display-conditions.md)).

For each type of content, you can define the action that will be triggered in your application (e.g. display a modal window), and the text that will be displayed in the Beefree SDK editor’s UI to trigger that action (e.g. “Locate a merge tag”), keeping a consistent UX with other areas of your application.

## What it does <a href="#what-it-does" id="what-it-does"></a>

_Content Dialog_ introduces new call-to-actions in the editor UI.

Depending on the type of content, the call-to-action will be rendered as a button, a link, or a drop-down choice (see below a detailed list of UI changes).

The text for the action is defined by the host application, so you can use your own wording to provide a better experience.

**An example of a possible workflow when the user clicks on a content dialog action:**

1. The editor will start _waiting mode_ (same as when the _save_ action is triggered)
   * This mode prevents users from further editing and keeps the focus on the user selection
   * The waiting mode is interrupted if the host application cancels the action
2. The host application will display to the user a UI element to select or define a content item
3. When the selection is done, the host application closes the UI and passes it to the editor
4. The editor receives from the host application the selected content and exits _waiting mode_
5. The content is applied to the selected item

**The same example applied to special links (link to a product) in a text selection:**

1. The editor starts _waiting mode_
2. The host application displays an overlay that hides the editor and lists the categories of products to link. The user browses them to find the desired product and selects it.
3. The editor receives the link and exits _waiting mode_
4. The link is applied to the selected text

## How it works <a href="#how-it-works" id="how-it-works"></a>

To set up content dialogs you will need to add the `contentDialog` object to `beeConfig`:

```javascript


contentDialog: {
	specialLinks: {
		label: 'Custom text for links',
		handler: function(resolve, reject) {
			// Your function
		}
	},
	mergeTags: {
		label: 'Custom text for merge tags',
		handler: function(resolve, reject) {
			// Your function
		}
	},
	mergeContents: {
		label: 'Custom text for merge contents',
		handler: function(resolve, reject) {
			// Your function
		}
	},
	rowDisplayConditions: {
		label: 'Custom text for display conditions',
		handler: function(resolve, reject, currentCondition) {
			// Your function
		}
	},
	externalContentURLs: {
            label: 'Custom text for custom rows',
            handler: function(resolve, reject) {
                // Your function
        }
    },
	saveRow: {
    	handler: function (resolve, reject, args) {
        	// Your function
    	}
	},
    editSyncedRow: {
	    label: 'Custom text for synced rows',
        description: 'Custom description for synced rows',
	    notPermittedDescription: 'Custom description for synced rows when not permitted',
        handler: function (resolve, reject, args) => {
        	// Your function
    	}
    }

}


```

For `rowDisplayConditions`, there is a third parameter called `currentCondition`. Use this parameter to return a row's current display condition. This parameter returns an object with the following format:&#x20;

```javascript
{
    label: '',
    description: '',
    before: '',
    after: '',
    type: 'BEE_CUSTOM_DISPLAY_CONDITION'
}
```

**Note:** You do not have to name the parameter `currentCondition`. You can use any name that works best for your application and workflow.

You can add all the dialogs, some of them or only one. Is up to your application to create them for all the users or a segment, as there are no related server-side settings, you can customize them for each editor start.

All the dialogs use the same pattern, but the returned object must match the element pattern (described in the following section).

### **label**

Defines the text displayed in the editor UI.

### **handler**

Is a function with a [Promise](https://dam.beefree.io/mozillapromise)-like signature.\
This function lets you use your own logic to retrieve the desired value.\
Once the value is available, you must call the `resolve(value)` function to pass it to the editor.\
In case you want to cancel the operation, call the `reject()` function.

A resolve or reject call is mandatory. If you miss this step, the editor will remain in waiting mode.\
Error management on the host application must call the reject function to unblock the editor.

### **Examples**

The following code snippet displays and example of applying a link action.

```javascript


contentDialog: {
  specialLinks: {
    label: 'Add an Example Link',
    handler: function(resolve, reject) {
      resolve({
        type: 'custom',
        label: 'external special link',
        link: 'http://www.example.com'
      })
    }
  },
}


```

The above code snippet is an example of how to apply a [Special link](content-dialog.md#special-links).

When the user clicks on **Add an Example Link**, the URL <mark style="color:blue;">http://www.example.com</mark> is applied to the selection (a button, an image or a text).

The waiting mode will not be perceived, and there is no cancel action.

### **Apply a link with a delay**

The following code snippet displays and example of applying a link with a delay.

```javascript


contentDialog: {
  specialLinks: {
    label: 'Add an Example Link after 2 seconds',
    handler: function(resolve, reject) {
      setTimeout(function() {
        resolve({
          type: 'custom',
          label: 'external special link',
          link: 'http://www.example.com'
        })
      }, 2000)
    }
  },
}


```

The `setTimeout` function in the above code sample is used to delay the execution of the enclosed code. It delays the call to the `resolve` function by 2000 milliseconds, or 2 seconds. This means that after initiating the special link dialog process, the application will wait for 2 seconds before adding and displaying the specified special link with the label 'external special link' and the URL 'http://www.example.com'.

### **Opening a dialog UI element**

The following code snippet displays and example of opening a dialog UI element.

```javascript

contentDialog: {
  specialLinks: {
    label: 'Custom text for links',
    handler: function(resolve, reject) {
      openMySpecialLinkDialog() // Replace this with your application function
        .then(specialLink => resolve(specialLink))
        .catch(() => reject())
    }
  },
},

```

In this example the `openMySpecialLinkDialog()` should be replaced with a function that opens a modal window (or other element) of the host application, where the user can select or build a link.

The selection is then returned as the value of `specialLink` to the `resolve()` function.

A cancel action will trigger the `reject()` function instead.

## Returned value syntax

Values must use the same pattern used in the `beeConfig` object.

The returned object is validated against the expected format.

If the validation fails, an error will be returned in the browser console:

E.g., `Error getting content rowDisplayConditions, the item is malformed.`

These errors will not trigger any visible notification in the UI.

## Merge Tags

Merge tags allow you to dynamically insert values into your content, such as user information or other variables. This section will guide you on how to configure merge tags in your host application. See the following section for sample code on setting up merge tags in your content dialog configuration.

### **Merge Tags Configuration**

Take the following steps to configure [merge tags](content-dialog.md#merge-tags) in your application:

1.  **Open your content dialog configuration file:**

    Locate the file where you configure your application's content dialog.
2.  **Add the `contentDialog` object:**

    If it doesn't already exist, add the `contentDialog` object into your configuration file.
3.  **Configure the `mergeTags` property:**

    Inside the `contentDialog` object, insert the `mergeTags` property as shown below:

    ```javascript
    contentDialog: {
        mergeTags: {
            label: 'Apply dynamic syntax',
            handler: function(resolve, reject) {
                //your function goes here
            }
        },
    },
    ```
4.  **Define the handler function:**

    Within the `handler` function, write your logic to dynamically insert values into the content.
5.  **Add a corresponding action in the text toolbar:**

    Ensure that the text toolbar includes an action for the merge tag element, allowing users to apply dynamic syntax easily.
6.  **Test your implementation:**

    Validate that the merge tags are working correctly within the UI, ensuring that the dynamic values are properly inserted.

<pre class="language-javascript"><code class="lang-javascript">
contentDialog: {
	mergeTags: {
		label: 'Apply dynamic syntax',
		handler: function(resolve, reject) {
			//your function goes here
		}
	},
},
<strong>
</strong></code></pre>

You can add a new action, available in the text toolbar, and associated with the merge tag element:

<figure><img src="../../.gitbook/assets/3Screen-Shot-2018-01-23-at-17.10.43-1024x247.png" alt=""><figcaption></figcaption></figure>

### **Most common use cases**

A few of the most common use case for [merge tags](content-dialog.md#merge-tags) are the following:

* Your application has a high number of placeholders and needs to provide a categorization or search form
* Placeholder availability depends on options that the user can select while building the message
* You want to display the same UI your users already know and use in your application
* You need to separate merge tags from other text placeholders

### **Value**

The following code snippet defines an object with `name` and `value` parameters meant for handling placeholders in an application. The `name` parameter, although not immediately displayed, is useful for later reference if the user selection is saved and reloaded. The `value` parameter contains a text string with specific syntax. This is for inserting dynamic content. This setup is important for applications to manage many placeholders or custom text fields efficiently.

```javascript
{
	name: 'Placeholder name', // Will not be shown
	value: '{{ syntax }}' // Text string that will be added
}
```

{% hint style="info" %}
**Important:** The name parameter may be later displayed if the user selection is saved and loaded in `beeConfig` on subsequent requests.
{% endhint %}

## Special Links <a href="#special-links" id="special-links"></a>

Special links are dynamic URLs embedded within emails to execute predefined actions, such as:

* **Unsubscribing a recipient:** Allowing users to easily opt-out from mailing lists.
* **Loading a Web version of an email:** Enabling recipients to view the email content in a browser.
* **Sending the email to a friend:** Facilitating users to share the email with others.

A few end user benefits of using special links are the following:

* **User Convenience:** Simplifies adding recurring URLs and actions to designs, which increases efficiency throughout the design creation process.
* **Consistent Implementation:** Ensures URLs and actions are consistent and accessible across various platforms.

{% hint style="info" %}
**Important:** Special links are inserted as code and treated as such during export, ensuring they populate in the HTML as-is. This prevents encoding issues and guarantees that the syntax is validated by the sending platform.&#x20;
{% endhint %}

By incorporating special links, end users benefit from the ease of managing various links efficiently across diverse platforms.

This section will explain how to configure special links with steps and provide a code sample to help get you started.

### **Special Links Configuration**

Take the following steps to configure special links in your application:

1. Define a `contentDialog` object within your configuration or settings file.
2. Add a `specialLinks` property to the `contentDialog` object.
3. Set the `label` property to the desired name for your link, for example, 'Search a post link'.
4. Create a `handler` function within the `specialLinks` object where you will define the custom logic for handling the link.
5. Ensure this `handler` function takes `resolve` and `reject` parameters to manage its behavior.

The following code snippet provides an example of how you can configure special links.

```javascript

contentDialog: {
	specialLinks: {
		label: 'Search a post link',
		handler: function(resolve, reject) {
			//your function goes here
		}
	},
},
```

Links can be applied to different [content types](../../dev-console-settings/server-side-options/content-options.md). When you define a link dialog action, it will be displayed in the text-toolbar, which is the same behavior for merge tags, as shown in the following image.

<figure><img src="../../.gitbook/assets/4Screen-Shot-2018-01-23-at-17.35.35-1024x245.png" alt=""><figcaption></figcaption></figure>

The following image shows an example action that applies to image or button content types.

<figure><img src="../../.gitbook/assets/5Screen-Shot-2018-01-23-at-17.37.40.png" alt=""><figcaption></figcaption></figure>

### **Most common use cases:**

A few of the most common use case for [special links](content-dialog.md#special-links) are the following:

* Apply links to products or news using a categories pattern, a search form, or a visual browser
* Apply special parameters or configuration to certain links with a wizard or form
* You want to display the same UI your users already know and use in your application

### **Value**

In the following code sample, the parameters serve the following purposes:

* **type**: Represents the type of link but will not be shown to the user directly.
* **label**: Provides default text for the link if no specific text is selected.
* **link**: Contains the URL that will be applied when creating the link, with the possibility of using placeholders.

```javascript
{
    type: 'A link type', // will not be shown
    label: 'Text', // Will be used as default text when text is not selected
	link: 'http://...' // The URL that will be applied. Placeholders can be used
}
```

{% hint style="info" %}
**Important:** The type parameter will be displayed later if the user selection is saved and loaded in `beeConfig` during subsequent requests.
{% endhint %}

## Merge Contents <a href="#merge-contents" id="merge-contents"></a>

Merge contents is a feature that allows you to consolidate multiple content sources into a unified display. This section will cover how to configure this feature and its most common use cases.

### **Merge Contents Configuration**

1. Access the configuration file of your application.
2. Locate the `contentDialog` object within the file.
3. Add a `mergeContents` property to the `contentDialog` object.
4. Inside the `mergeContents` property, set a `label` with the description you want to appear, such as 'Set up a new product recommendation'.
5. Implement a `handler` function that will process your custom logic. This function should accept two parameters: `resolve` and `reject`.
6. Insert your specific code inside the `handler` function where indicated.

Your configuration should look like the following:

<pre class="language-javascript"><code class="lang-javascript"><strong>
</strong><strong>contentDialog: {
</strong>	mergeContents: {
		label: 'Set up a new product recommendation',
		handler: function(resolve, reject) {
			//your function goes here
		}
	},
},

</code></pre>

The content dialog adds a button to the merge content list as shown in the following image.

<figure><img src="../../.gitbook/assets/6Screen-Shot-2018-01-24-at-10.39.07.png" alt=""><figcaption></figcaption></figure>

### **Most common use cases**

A few of the most common use case for merge contents are the following:

* Set up the content and/or layout for a product recommendation
* Set up the content and/or layout for a dynamic advertising
* Set up the content and/or layout for another type of targeted content

{% hint style="info" %}
**Important:** To display the Dynamic content tile in the contents panel, you must configure [mergeContents](smart-merge-tags.md) in [beeConfig](../../getting-started/readme/installation/configuration-parameters/) with at least one predefined item.
{% endhint %}

### **Value**

In the following code snippet, the properties perform the following tasks:

* **name**: This property specifies the display name of the content. It appears in the editor UI and helps users identify the content item within the messaging interface.
* **value**: This property represents the actual content that will be injected into the HTML output, shown in the preview. The `{{ syntax }}` is typically used for dynamic content insertion.

```javascript

{
	name: 'Content name', // Will be displayed in the editor UI and in the message
	value: '{{ syntax }}' // Text string that will be added to the HTML output (will be show in the preview)
}

```

## Display Conditions <a href="#display-conditions" id="display-conditions"></a>

Display conditions allow you to control when specific content is shown based on predefined criteria. This section will cover how to configure display conditions in your application and common use cases.

### **Display Conditions Configuration**

To configure display conditions in your host application, take the following steps:

1.  **Define the `contentDialog` Object**: Start by defining an object called `contentDialog` in your code. This object will hold the configuration for the display conditions.

    ```javascript
    contentDialog: {
        // Configuration properties go here
    },
    ```
2.  **Add the `rowDisplayConditions` Property**: Within the `contentDialog` object, add a property named `rowDisplayConditions`. This property will specify the conditions under which a particular row is displayed.

    ```javascript
    contentDialog: {
        rowDisplayConditions: {
            // Properties for display conditions go here
        },
    },
    ```
3.  **Set the `label` Property**: Inside the `rowDisplayConditions` object, define a `label` property. This property sets the text label for the display condition. For example, to set the label as "Open builder":

    ```javascript
    contentDialog: {
        rowDisplayConditions: {
            label: 'Open builder',
        },
    },
    ```
4.  **Define the `handler` Function**: Add a `handler` property inside the `rowDisplayConditions` object. This property is a function that determines the logic for your display conditions. It accepts two parameters: `resolve` and `reject`, which are typically used for promise handling.

    ```javascript
    contentDialog: {
        rowDisplayConditions: {
            label: 'Open builder',
            handler: function(resolve, reject) {
                // Your function goes here
            }
        },
    },
    ```
5.  **Implement the Display Logic**: Within the `handler` function, implement the logic to determine whether the row should be displayed. Use the `resolve` function to indicate the conditions are met, and the `reject` function to indicate they are not.

    ```javascript
    contentDialog: {
        rowDisplayConditions: {
            label: 'Open builder',
            handler: function(resolve, reject) {
                // Your custom logic to determine display conditions
                if (/* condition */) {
                    resolve();
                } else {
                    reject();
                }
            }
        },
    },
    ```
6.  **Complete the Configuration**: Make sure your configuration object is properly closed and integrated into your application. Ensure that all necessary conditions and logic are correctly defined within the `handler` function.

    ```javascript
    contentDialog: {
        rowDisplayConditions: {
            label: 'Open builder',
            handler: function(resolve, reject) {
                // Your custom logic to determine display conditions
                if (/* condition */) {
                    resolve();
                } else {
                    reject();
                }
            }
        },
    },
    ```

{% hint style="success" %}
Customize the logic within the `handler` function to meet your specific needs.
{% endhint %}

A new button will be available in the display condition widget. In this example, the button says “Open builder”, which is the `label` shown in the JSON configuration file shown above.

<figure><img src="../../.gitbook/assets/7Screen-Shot-2018-01-24-at-10.45.15 (1).png" alt=""><figcaption></figcaption></figure>

### **Most common use cases:**

A few of the most common use case for display conditions are the following:

* Display a condition builder or form to target a segment of recipients
* Display a form to create a loop with the row dynamic contents, as product recommendations

### **Value**

The following code snippet configures a display condition with a specific label, description, and delimiters that define the start and end of the condition block in the template. This will be shown in the editor UI and inserted around the selected row based on the specified conditions.

```javascript
{
	type: 'A category for this condition', // Will not be shown
	label: 'Condition', // Will be displayed as the condition name
	description: 'Small text describing what the condition does', // Will be displayed in the editor UI to identify the condition action
	before: '{% raw %}
{% if something == \'Condition\' %}', // Will be added before the selected row
	after: '{% endif %}
{% endraw %}', // Will be added after the selected row
}
```

{% hint style="info" %}
**Important:** The type parameter may be later displayed if the user selection is saved and loaded in `beeConfig` on subsequent requests.
{% endhint %}

### **An example**

In this example, a window is shown to users when they click on the button to open the builder.

<figure><img src="../../.gitbook/assets/8display.condition.dialog.jpg" alt=""><figcaption></figcaption></figure>

The UI is entirely up to the hosting application. Here, the developer decided to offer some fields at the top where the _Display Condition_ can be named and described, an area below it where parameters, values, and operators can be selected, and a preview on the right.

When users click on “Confirm”, the information is passed back to the editor and shown in the properties panel.

<figure><img src="../../.gitbook/assets/9after.confirm.jpg" alt=""><figcaption></figcaption></figure>

Of course, it can be edited in the editor like any other _Display condition_, if the user has the [rights to do so](roles-and-permissions.md).

<figure><img src="../../.gitbook/assets/10edit.view_.jpg" alt=""><figcaption></figcaption></figure>

Reference our [Advanced Permissions documentation](advanced-permissions.md#add-condition-and-edit-condition-buttons) to learn more about managing the visibility of the Add Condition and Edit Condition buttons.&#x20;

## Custom Rows <a href="#custom-rows" id="custom-rows"></a>

Custom rows allow you to import products or news using various patterns, set up predefined content layouts, and create dynamic sections for recommendations, codes, and advertisements. This section will discuss how to configure custom rows in your host application.

### **Custom Rows Configuration**

The following code snippet displays an example of how to configure custom row.

```javascript
contentDialog: {
    externalContentURLs: {
            label: 'Search products',
            handler: function(resolve, reject) {
                // Your function
        }
    }
}
```

The content dialog adds a new item, using your text label, in the Rows drop-down:

<figure><img src="../../.gitbook/assets/11CustomRows_ContentDialog_01.jpeg" alt=""><figcaption></figcaption></figure>

### **Most common use cases**

A few of the most common use case for custom rows are the following:

* Import a set of products or news, as custom rows, using a categories pattern, a search form, or a visual browser
* Set up the row layout for a set of predefined contents
* Set up rows with dynamic content to build dynamic sections that provide product recommendations, QR or bar codes, advertising content, etc.

### **Value**

The following code snippet configures a custom row with a specific name and value. This will be shown in the editor UI in reference to a specific custom row based on the specified conditions.&#x20;

```javascript
{
    "name":"Results name", // Will be added as a new choice in the rows drop-down
    "value":"https://..." // Will be used to get the list of rows
}
```

This response will:

1. Create a new drop-down choice with the provided name
2. Display the rows provided by the URL in the rows panel

<figure><img src="../../.gitbook/assets/12results.jpeg" alt=""><figcaption></figcaption></figure>

Notice that in the rows list, names returned by the content dialog display as highlighted elements to give them further visibility over starting choices.

The content dialog can be used as many times as the user needs and, depending on the response, the behavior may change:

#### **1. Returning the same name**

This overwrites the existing results, keeping the same name in the drop-down.\
This behavior perfectly matches our example above, where the host application returns “Your search results” every time the content dialog is resolved.

#### **2. Returning a new name**

This creates a new drop-down choice, keeping the previous results as selectable elements. Previous results are available directly in the drop-down.\
Usage example:

<figure><img src="../../.gitbook/assets/13Search_multiple.jpeg" alt=""><figcaption></figcaption></figure>

## Synced Rows

[Synced rows](../../rows/saved-rows/synced-rows.md) are rows that are used across multiple designs, ensuring consistency when updates to a row are made. This section will cover how to configure synced rows in your application.

### **Synced Rows Configuration**

The following code snippet displays an example of how to configure [synced rows](../../rows/saved-rows/synced-rows.md).

```javascript
contentDialog: {
    editSyncedRow: {
		label: 'Edit synced rows',
		description: `This row is used in other designs.
					  You can decide to update all the designs or transform this single row into a regular one`,
		notPermittedDescription: `This row is used in other designs.
                                  Your plan does not permit you to edit it. Please contact your account administrator`,
        handler: function (resolve, reject, args) => {
        	resolve(false) // the boolean will be the value of  'Label of the sidebar button that triggers the contentDialog'`synced`
                           // if false the row will be un-synced, if true nothing will happen.
    	}
    }
}
```

The `label`, `description` and `notPermittedDescription` fields handle the wording related to the “Edit synced row” call-to-action/button. Here’s how and where they are used:

* `label`: Label related to the sidebar button that triggers the content dialog
* `description`: Description of the action on top of the button
* `notPermittedDescription`: Description of the action when the button is hidden from the dedicated [advanced permission](advanced-permissions.md)&#x20;

Here’s an example of what `label` and `description` would look like:

<figure><img src="../../.gitbook/assets/14image-11-300x179.png" alt=""><figcaption></figcaption></figure>

And here’s an example of what `notPermittedDescription` would look like:

<figure><img src="../../.gitbook/assets/15image2-300x171.png" alt=""><figcaption></figcaption></figure>

## Save Rows <a href="#save-rows" id="save-rows"></a>

**Save rows** refer to the functionality that allows users to save changes made to specific rows in a data table. This section will discuss how to configure the **Save rows** feature in your host application.

### **Saved Rows Configuration**

The following code snippet displays an example of how to configure [save rows](../../rows/saved-rows/).

```javascript
contentDialog: {
    saveRow: {
        handler: function (resolve, reject, args) {
            // Your function
        }
    }
}
```

Unlike the rest of content dialog configurations, _Save rows_ doesn’t use the `label` parameter as the UI element is a save icon displayed on the selected row (and in the row’s properties panel):

<figure><img src="../../.gitbook/assets/16saveicon-1024x134.png" alt=""><figcaption></figcaption></figure>

The _Save rows_ content dialog is a mandatory step in the [Save rows](../../rows/saved-rows/) workflow.

The `resolve` function must return metadata for the selected row. The [_metadata_](../../rows/saved-rows/) section of the rows schema allows you to keep track of row-specific information.

The `args` object in the handler function returns to the host application metadata already applied to the selected row.

### **Value**

The following code snippet configures a save row with a specific name and category. This will be shown in the editor UI in reference to a specific saved row.

```javascript

{
    "name":"Row name", // Mandatory metadata
    "Category":"A row category" // If you provide category management for saved rows
    "...":"..." // You can add as metadata as your application needs
}

```

This response will provide metadata that is added to the row in the asset (email, page, popup) before it’s provided through the [Save Rows callback](../../rows/saved-rows/).

The row name is the only required metadata and it’s displayed as the row title in the _Rows_ panel:

* A string of plain text that identifies the row.
* Displayed in the row card when the row is shown in the _Rows_ panel.
* Used for text searches within the _Rows_ panel

&#x20;Check the [Saved rows metadata section](../../rows/saved-rows/save-rows-overview.md) for further details on recommended metadata.

## Forms <a href="#forms" id="forms"></a>

Forms are interactive elements that allow users to input and submit data. This section will discuss how to configure forms to meet specific requirements in your host application.

### **Forms Configuration**

The following code snippet displays an example of how to configure [forms](../../visual-builders/form-block/).

```javascript
manageForm: {
	label: 'Edit form',
	handler: async (resolve, reject, args) => { 
		// Your function
	} 
},
```

If you want to have total control on the forms that a Beefree SDK application displays and renders, you can use this _forms_ Content Dialog rather than passing a single form to the Beefree SDK application.

The [forms](../../visual-builders/form-block/) Content Dialog works the same way as the previous Content Dialog for [save rows](content-dialog.md#save-rows) **–** but in this case, the `resolve` function should return the structure for the desired form.

The `args` object in the handler function returns to the host application the form object already applied. With this information, the application can decide what to display to the user (e.g., edit the current form, suggest a similar form, etc.).

To understand how this data is structured, refer to the [form structure page](../../visual-builders/form-block/integrating-and-using-the-form-block/form-structure-and-parameters.md) on this website.

## Custom Attributes <a href="#custom-attributes" id="custom-attributes"></a>

Custom attributes are user-defined metadata that can be added to links and images within an editor. This section will discuss how to configure custom attributes in your host application.

### **Custom Attributes Configuration**

The following code snippet displays an example of how to configure [custom attributes](custom-attributes.md).

```javascript
        customAttribute: {
          label: 'Search Attributes',
          handler: (resolve, reject) => {
            resolve({
              key: '2783f0ea-f6af-44f3-856e-d7a01cd87714',
              name: '100% Custom',
              value: 'My custom value',
              target: 'link',
            })
          }
        },
```

If your end users need to apply custom attributes to the links and images in their content, you can completely customize the user experience and workflow for adding those attributes with a Content Dialog that will take over the editor’s UI. The dialog will need to return the attribute to apply.

## Custom Video <a href="#custom-video" id="custom-video"></a>

Custom video allows you to integrate and configure videos from custom sources other than standard platforms like YouTube and Vimeo. This section will discuss how to configure custom video for your host application.

### **Custom Video Configuration**

The following code snippet displays an example of how to configure custom video.

```javascript
addVideo: {
  label: 'Choose a video',
  handler: async (resolve, reject) => {
    resolve({
      videoSrc: 'https://link.to.your.custom.video', // mandatory
      thumbSrc: 'https://my.beautifulimages.com/thebest.jpg', // mandatory
      thumbAlt: 'The title of my custom video!', // optional
    })
  }
}
```

It is possible to leverage the Content Dialog method to add videos from custom sources – other than YouTube and Vimeo.

You can use the `addVideo` Content Dialog modal, which will take over the builder’s UI. The video will be added as a thumbnail in the content area.

The user must fill out the video URL from a custom source, the image used as a thumbnail, and an alt text/title by implementing a custom modal window (optional). When the user clicks on the video thumbnail, it will open `videoSrc` in a new tab/window.
