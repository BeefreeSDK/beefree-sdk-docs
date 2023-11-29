# Save Rows Overview

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above.\
If you're on the Essentials plan, [upgrade a development application](../getting-started/development-applications.md) for free to try this and other Core-level features.
{% endhint %}

## Overview <a href="#overview" id="overview"></a>

Save Rows allows users to select a row in a message and save it for later use. More specifically, it allows users to submit a request to the host application to save a piece of content and turn it into a reusable element. The host application, using the [Custom Rows](../custom-rows/) feature, can feed these saved elements back to the builder as rows that can be dragged into other messages.

## How it works <a href="#how-it-works" id="how-it-works"></a>

### **The new Save icon**

When the feature is enabled, a new _Save_ icon is added to the action icons when a row is selected:

![](https://docs.beefree.io/wp-content/uploads/2018/11/saveicon-1024x134.png)

The same action is also available in the row properties panel when a row is selected:

![](https://docs.beefree.io/wp-content/uploads/2018/11/saveicon\_properties-300x210.png)

By clicking on this icon, users trigger a request to the host application to store the row’s JSON document, which includes:

* row structure and settings;
* contents and their settings;
* all style settings.

It is entirely up to the host application:

* where to store the JSON documents that describe these saved rows;
* if and how to display them to users of the application;
* whether to allow users to edit them individually
* when and how to feed them back to the builder, using the [Custom Rows](../custom-rows/) feature.

## **Enabling Save Rows in the Beefree SDK Console**

_Save Rows_ – as most Beefree SDK features – is made available to users in an off state and must be activated in the [Beefree SDK Console](https://developers.beefree.io/).

To do so:

1. Login into the [Beefree SDK Console](https://developers.beefree.io/).
2. Click _Details_ next to the application you want to configure.
3. Click the _view more_ link under the _Application configuration_ heading.
4. Toggle _Enable saving rows_ on and click the _Save_ button to save the new setting.

<figure><img src="https://docs.beefree.io/wp-content/uploads/2018/11/setup.png" alt="" width="563"><figcaption></figcaption></figure>

## **Making Save Rows available only to select users**

Once the feature has been turned on at the global level, in [Beefree SDK Console](https://developers.beefree.io/), you may want to disable _Save Rows_ on a per-user basis.  This can be accomplished via the client-side configuration document that you feed to an application when initializing the builder for a certain user.

Why? Because you may decide to make the feature available to different users of your application:

* depending on the subscription plan that they are on (you could push users to a higher plan based on the ability to save a row for later);
* depending on the purchase of an optional feature (same);
* to allow “beta” users to see it while keeping it hidden from the rest of your users;
* etc.

Here’s how to do so:

* Enable _Saved Rows_ in the [Beefree SDK Console](https://developers.beefree.io/). as mentioned above.
* Add the configuration parameter _saveRows_ to the _beeConfig_ document:
  * Set it to _false_ for all users that cannot save rows.

Here is a simple example:

## **Save Row Configuration**

```javascript

const beeConfig = {
    uid: 'dev-user',
    language: 'en-US',
    ...
    saveRows: false // boolean
    ...
}

```

## **Understanding the end-user experience**

How does _Save Rows_ work from the end-user point of view? It’s in part based on the changes to the builder mentioned above, and in part affected by how you decide to implement the feature within your application.

Let’s review the various steps in the workflow to better understand what we mean.

Saving a row:

1. Activate the feature as described above.
2. Load a [Beefree SDK template](https://dam.beefree.io/githhubtemplates).
3. Select the row you want to save.
4. Click on the _Save_ icon.
5. Your application will need to open some sort of a dialog that allows for some user input.
6. Users will enter various metadata, such as the name of the row, a category, tags, etc.
7. The user closes the dialog

Using a previously saved row:

1. Users click on the _Rows_ tab.
2. Users select a category of rows from the _Rows_ tab’s drop-down menu. For example:
   1. A user created a “Footers” category when saving a row
   2. You saved the row and that category name
   3. You fed an array of custom rows called “Footers” back to the builder
   4. The same user finds “Footers” in the _Rows_ drop-down menu.
3. The user drags the row into the editing stage.

Here is a visual example using our demo application:

![](https://docs.beefree.io/wp-content/uploads/2018/11/saveRows.gif)

## **Saving rows workflow for developers**

When the _save row_ action is triggered by the user, the builder starts the following sequence:

1. **Metadata Content dialog**\
   Used to collect data from the host application and add it to the row object.\
   Metadata helps your application to identify a row, overwrite a previously saved version, etc.
2. **Save Rows Callback.**\
   Function that returns the row to the host application.

The following describes the recommended workflow to implement saved rows in a host SaaS application.

1. Enable _Save Rows_ in the [Beefree SDK Console](https://developers.beefree.io/) as described above.
2. Load a [Beefree SDK template](https://dam.beefree.io/githhubtemplates).
3. Select the row you want to save and make note of the new save icon.
4. Click the save icon to trigger a Metadata Content Dialog.  To successfully handle this step, you must complete these tasks:
   * Add a Metadata Content Dialog object to your _beeConfig_. This configures your handler.
   * Implement the handler method to open a dialog (e.g., modal window) to collect any metadata you wish your users to input when saving a row.
5. The dialog should contain a form and complete the following specs:
   1. Save the row returned in the Metadata Content Dialog’s _args_ object.
   2. Collect metadata from the end-user, such as row name.
   3. Merge the metadata with the row, so it can be immediately returned to the application.
   4. Return a metadata object to the application so the stage can immediately use the data.
6. The application will update the selected row on the stage with the returned metadata.
7. The application will trigger the _onSaveRow_ callback with the following details:
   * JSON of the selected row
   * HTML preview of the selected row
   * Page Partial of the selected row contained in a page. Use this JSON document to allow users to edit a saved row independently of any message or landing page that might use it.
8. The application will refresh the Rows panel to reload the selected rows data feed.
9. Host app will listen for _onSaveRows_ callback and update the previously saved records with the HTML preview.

## Displaying rows <a href="#displaying-rows" id="displaying-rows"></a>

To display saved rows in the _Rows_ tab, add them to the list of rows available to users by leveraging the [Custom Rows feature](../custom-rows/).

The rows are organized in lists that are displayed based on your rows configuration. Use the metadata submitted by your users to categorize them, creating multiple lists of rows: this can significantly improve the user experience.

Here is an example of a rows configuration that displays saved rows organized by category:

```json

rowsConfiguration: {
            emptyRows: true,
            defaultRows: true,         
            externalContentURLs: [{
                name: "Headers",
                value: "https://URL-01"
                },{
                name: "Footers",
                value: "https://URL-02"
                },{
                name: "Product grids",
                value: "https://URL-03"
                },{
                name: "Main article",
                value: "https://URL-04"
            }]         
        },

```

In this example, the _Rows_ tab will show:

* _Empty rows_
* _Default rows_
* _Headers_
* _Footers_
* _Product grids_
* _Main article_

_…_ retrieving the arrays of JSON documents for custom rows (_externalContentURLs_) from the URLs specified.

These _custom rows_ names (_Headers, Footers, Product grids, etc._) could be the result of a “Category” metadata entered by the user at the time the row was saved. The input could be the result of:

1. The user writing a new category name for the selected row.
2. The user selecting from a list of existing categories, previously created by the user, or set up by you.

Here is another example that shows _saved rows_ organized in the _Rows_ tab based on the campaign type:

```javascript

rowsConfiguration: {
            emptyRows: true,
            defaultRows: true,         
            externalContentURLs: [{
                name: "Acquisition series",
                value: "https://URL-01"
                },{
                name: "Newsletter",
                value: "https://URL-02"
                },{
                name: "Transactional",
                value: "https://URL-03"
                },{
                name: "Post-Purchase Drip",
                value: "https://URL-04"
            }]         
        },

```

## Saved Rows Management <a href="#saved-rows-management" id="saved-rows-management"></a>

Accessing, and organizing saved rows is now easier than ever with Saved Rows Management. With this feature, we’ve introduced a new action in the list of saved rows that your application can intercept to handle changes in this list itself. This means you can now delete, rename, or re-organize your saved rows, right inside the builder.

![](https://docs.beefree.io/wp-content/uploads/2021/11/savedrowsmanagement.gif)

## How to implement

Implementing this new feature requires some development effort from the host application.

Here is what you need to know for each action.

## Saved Row Management Actions

In the section below you can learn how to configure the Saved Rows Management categories, and allow users to perform such actions straight from the builder.

## **Configure Delete Rows**

To get started, you will need to create a content dialog in your application configuration parameters. The content dialog method should be named `onDeleteRow` and be nested under the `contentDialog` object, as follows:

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  contentDialog: {
    onDeleteRow: {
      handler: async (resolve, reject, args) => {
 
      }
    }
  },
}

```

Following that, amend your `rowsConfiguration` object with the additional parameters:

* The `handle` parameter to utilize in your `onDeleteRow` handler from the previous step
* The optional `behaviors` parameter to set management permissions

Here’s an example:

```javascript

rowsConfiguration: {
  externalContentURLs: [
    {
      name: "Saved Rows",
      value: "category-value",
      handle: "category-handle",
      behaviors: {
        canEdit: true,
        canDelete: false,
        canEditSyncedRows: false,
        canDeleteSyncedRows: false,
      },
    }
  ]
}

```

When the `onDeleteRow` method is called, utilize the 3rd parameter to obtain an argument containing the handle value of the row being requested, as well as the row metadata. Use the handle and the row’s metadata to determine which row should be deleted.

## **Example** **args:**

```json

{
  value: "category-value",
  handle: "category-handle",
  row: {
    name: "My row name",
    metadata: {
      name: "My row name",
      guid: "key-for-deletion"
    }
    ... // more row data
  }
}

```

Finally, we can call the `resolve` method, passing the value `true` if you want to refresh the rows, or `false` if you want to keep the side panel’s current listing.

## **Example onDeleteRow with args:**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  contentDialog: {
    onDeleteRow: {
      handler: async (resolve, reject, args) => {
        // get the unique row id from metadata
        const row_id = args?.row?.metadata?.guid 
        // pseudo code to delete a row and refresh the panel...
        const result = await fakeRowDeleteService(row_id)
        if (result === 'success') resolve(true) 
        reject(result) 
      }
    }
  },
}

```

## **Configure Edit Row Metadata**

To get started, much like with deleting rows, you will need to create a content dialog in your application configuration parameters. The content dialog method should be named `onEditRow` and be nested under the `contentDialog` object, as follows:

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  contentDialog: {
    onEditRow: {
      handler: async (resolve, reject, args) => {
 
      }
    }
  },
}

```

Following that, amend your `rowsConfiguration` object with the additional parameters:

* The `handle` parameter to utilize in your `onEditRow` handler from the previous step
* The optional `behaviors` parameter to set management permissions

Here’s an example:

```javascript

rowsConfiguration: {
  externalContentURLs: [
    {
      name: "Saved Rows",
      value: "category-value",
      handle: "category-handle",
      behaviors: {
        canEdit: true,
        canDelete: false,
        canEditSyncedRows: false,
        canDeleteSyncedRows: false,
      },
    }
  ]
}

```

When the `onEditRow` method is called, utilize the 3rd parameter to obtain an argument containing the handle value of the row being requested, as well as the row metadata. Use the handle and the row’s metadata to determine which row should be edited.

## **Example** **args:**

```javascript

{
  value: "category-value",
  handle: "category-handle",
  row: {
    name: "My row name",
    metadata: {
      name: "My row name",
      guid: "key-for-deletion"
    }
    ... // more row data
  }
}

```

Finally, we can call the `resolve` method, passing the value `true` if you want to refresh the rows, or `false` if you want to keep the side panel’s current listing.

## **Example onEditRow with args:**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  contentDialog: {
    onEditRow: {
      handler: async (resolve, reject, args) => {
        // get the unique row id from metadata
        const row_id = args?.row?.metadata?.guid 
        // pseudo code to edit a row and refresh the panel...
        const result = await openFakeDialogToEditRow(row_id)
        if (result === 'success') resolve(true) 
        reject(result) 
      }
    }
  },
}

```

## **Errors and Warnings**

Saved Rows Management also provides errors and warnings for your application, so you can handle all cases gracefully.

**Sample warning:**

```json

{
  warn: {
    message: "This is a warning",
    detail: "You don't have management permissions."
  }
}

```

## **Sample error:**

```json

{
  error: {
    message: "This is an error",
    detail: "You don't have management permissions."
  }
}

```

You can call the `reject` method, passing the message you want to display.

## **Example:**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  contentDialog: {
    onEditRow: {
      handler: async (resolve, reject, args) => {
        const warn = {
          message: 'This is a warning.',
          detail: 'You don't have management permissions.'
        }
        return reject({ warn }) 
      }
    }
  },
}

```

## Loading External Rows with an Instance Method <a href="#loading-external-rows-with-an-instance-method" id="loading-external-rows-with-an-instance-method"></a>

Saved Rows Management also comes with the ability to load any external rows via an instance method instead of an external URL. In addition, since you can now access rows through your application, you don’t need to perform authentication.

To start, define a hook in your application configuration. The hook method should be named `getRows` and will be nested under the `hooks` object, as follows:

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  hooks: {
    getRows: {
      handler: async (resolve, reject, args) => {

      }
    }
  },
}

```

Following that, amend your `rowsConfiguration` object with the additional parameters:

* The `handle` parameter to utilize in your `getRows` handler from the previous step
* The `isLocal` parameter to let the application know to use the hook handler

### Here’s an example:

```json

rowsConfiguration: {
  externalContentURLs: [
    {
      name: "Saved Rows via Hooks",
      value: "category-value",
      handle: "category-handle",
      isLocal: true,
    }
  ]
}

```

When the getRows method is invoked, utilize the 3rd parameter to obtain an argument containing the handle value of the row being requested. Use the handle to determine which set of rows should be returned.

### **Example** **args:**

```json

{
  value: "category-value",
  handle: "category-handle",
}

```

Finally, we can call the resolve method, passing in an array of savedRows.

### **Example hook with args:**

```javascript

beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  hooks: {
    getRows: {
      handler: async (resolve, reject, args) => {
        // get the handle
        const handle = args.handle
        // pseudo code to get the rows with the handle...
        const rows = await fakeRowsService(handle)
        resolve([ ...rows ]) 
      }
    }
  },
}

```

{% hint style="info" %}
If you are using a React application, be sure to pass a new rows array and not a reference to a row state. Otherwise, the rows state may be “stale” and won’t update in the side panel.
{% endhint %}

## Saved rows schema <a href="#saved-rows-schema" id="saved-rows-schema"></a>

The following is the basic structure of the row’s JSON schema. Simply put, the schema is the structure of your saved rows data feed.

```javascript

[
    {
        metadata: {
            name: 'My row name' // Identifies the row, required.
        }
        columns: { ... }
        ...
    }, // The row that was previously saved. - (*)
    ...
]

```

{% hint style="info" %}
**NOTE**: The row schema is complex and we do not recommend creating rows programmatically. Therefore, there is no schema reference of the row itself. However, you can add your own parameters to the row’s metadata or use our [Simplified Row Schema](../custom-rows/generating-custom-rows-from-existing-content.md) to generate them programmatically from existing content.
{% endhint %}

The _metadata_ section of the rows schema allows you to keep track of row-specific information.

```javascript

metadata: {
    "name": "My Saved Row", // The row's title displayed in the "Rows" panel.
    "tags": "product, two columns, blue",
    ... additional custom parameters
}

```

### **Required metadata**

#### **name** The saved row’s title displayed in the _Rows_ panel.

* A string of plain text that identifies the row.
* Displayed in the row card when the row is shown in the _Rows_ panel.
* Used for text searches within the _Rows_ panel

#### **Recommended metadata**

**category**\
A category can be useful for organizing your feeds on the Rows tab.

**id**\
A handle that identifies the row in the host application’s data storage.

**idParent**\
Useful to track rows that were saved from previously saved rows. Keeping track of where a row came from allows you to implement additional editing features.

**dateCreated**\
The date the row was created: useful for filtering/sorting rows for content management purposes in your application. It can also help with technical support tasks.

**dateModified**\
The date a saved row was updated: useful for filtering/sorting rows for content management purposes in your application. It can also help with technical support tasks.

**userId**\
To let your application decide whom can edit or save rows.

**tags**\
Useful to create filters, management, search, and in general to organize the content in your application.

## Metadata Content Dialog <a href="#metadata-content-dialog" id="metadata-content-dialog"></a>

The metadata content dialog is triggered by the save icon in Beefree SDK. This step is required to provide Beefree SDK with information about the row, such as its name and/or id.  The Metadata Content Dialog is added in the same manner as other Content Dialogs, such as Merge Tags.  Please review the [Content Dialog](../advanced-options/content-dialog.md) section for more details about how to use Beefree SDK’s Content Dialog feature.

An example Metadata Content Dialog configuration can be found below.

```javascript

contentDialog: {
    saveRow: {
        handler: function (resolve, reject, args) {
            return window.bee.onHandleMetadata(args)
               .then((metadata) => {
                 resolve(metadata, { synced: true }) //  {
                reject()
              })
       }
    },
externalContentURLs: {
   handler: function (resolve, reject, args) {
       return window.bee.onSearchSavedRows(args)
           .then((rows) => {
             resolve(rows)
           })
           .catch(() => {
             reject()
           })
     }
   },
},

```

The metadata resolve function now accepts an `options` object in which you can pass the property `synced` to determine if the row needs to be saved and treated by the builder as synced.

```json

{ synced: true }

```

## Save Rows callback <a href="#save-rows-callback" id="save-rows-callback"></a>

When the _Metadata Content Dialog_ is completed, the application triggers the _Save Rows callback_.  The callback returns the following details:

**rowJSON**\
JSON of the selected row.

**rowHTML**\
HTML preview of the selected row

**pageJSON**\
Page Partial of the selected row contained in a page (for editing a row as an independent piece of content).

```javascript

onSaveRow: function (rowJSON, rowHTML, pageJSON) {
    // Do something with the returned values...
},

```

## Edit Saved Rows <a href="#edit-saved-rows" id="edit-saved-rows"></a>

With [Edit Single Row](edit-single-row-mode.md) mode you can offer an easy way for your users to edit saved rows individually, using a tailored UI built to modify the row structure, content, and style settings without worrying about messing up with the overall design of the email campaign, landing page, or pop-up.

<figure><img src="https://docs.beefree.io/wp-content/uploads/2022/03/image1.png" alt=""><figcaption></figcaption></figure>

Enabling a more modular approach to saved rows simplifies how users can design and act on content: updating small details in a saved row, saving it, then deploying it to existing templates becomes a matter of minutes. If you want to learn more about how to leverage Edit Single Row mode to safely modify a Saved Row, take a look at the dedicated technical documentation.
