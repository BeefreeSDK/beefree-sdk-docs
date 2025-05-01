# Implement Synced Rows

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. Upgrade a [development application](../../../getting-started/readme/development-applications.md) at no extra charge to explore features from higher plan tiers. **Note:** Usage on a development application still counts toward [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) and limits.
{% endhint %}

## Overview <a href="#overview" id="overview"></a>

Synced Rows expands on the foundational capabilities of [Save Rows](../create/save/) and [Edit Single Row Mode](implement-synced-rows.md#edit-single-row-mode), helping users manage rows more effectively. Using the `merge-rows` and `synced-rows` methods in the [Content Services API (CSAPI)](../../api-endpoints.md), you can create an efficient row management workflow. This ensures that when users update content in one row marked as “synced,” those updates are reflected across all connected designs using that synced row.

### Key features

* **Cross-design synchronization**: Sync saved row contents across multiple linked designs.
* **Design consistency**: Lock rows in linked designs to keep designs uniform.
* **Editing flexibility**: Convert rows from synced to unsynced, making individual changes as needed.
* **Intuitive edit indicator**: Look for the pencil icon at the top-right of synced rows, which provides access to editing options

### Example use cases

* **Auto-updating contacts**: Change a contact in one email, and it updates across multiple campaigns.
* **Effortless re-branding**: Edit your logo once and watch it reflect across all designs.
* **Unified transactional footers**: Update details like copyright or social links, and it automatically updates in all relevant email templates.

### Elements that can be synchronized

* **Row details**: This includes structure, settings, and styles.
* **Content details**: Settings and styles of individual content blocks.
* **Metadata**: Any metadata tied to the saved row.

## Prerequisites <a href="#prerequisites" id="prerequisites"></a>

Prior to implementing Synced Rows, review the following prerequisites:

1. [Save Rows](../../storage/self-hosted-saved-rows.md): Implement [Self-hosted Saved Rows](../create/save/implement-self-hosted-saved-rows/) first, because it establishes the foundation for a row management workflow.
2. [Edit Single Row Mode](initialize-edit-single-row-mode.md) & [Content Services API (CSAPI)](../../api-endpoints.md): Familiarizing yourself with Edit Single Rows Mode and CSAPI will provide you with a mechanism to edit and manage synced rows, which will support your implementation workflow. However, they are not strictly necessary to implement Synced Rows.

## How it works <a href="#how-it-works" id="how-it-works"></a>

When a row is saved with the `synced` property, it becomes a “synced row.” To maintain consistency, synced rows cannot be edited within a design. Instead, they function as reference points, ensuring uniformity across all linked designs. The host app must load the row’s JSON using Single Row Edit Mode to edit synced rows. Any modifications to synced rows can be propagated to all linked designs with the help of the CSAPI’s `merge-rows` and `synced-rows` methods.

Unsynced saved rows, in contrast, allow for edits that don’t impact other designs. They’re ideal for making design-specific changes without influencing other designs that might share the same base row.

## Designating a row as "synced" <a href="#designating-a-row-as-synced" id="designating-a-row-as-synced"></a>

As previously mentioned, a synced row is a saved row designated `synced` when saved. To set a row’s synced property, adjust the JSON response from the `saveRow` Content Dialog.

You might need to modify the `saveRow` handler from the Metadata Content Dialog step in your app’s Save Rows workflow.

If you need a refresher, check out:

* [Save Rows workflow for developers](../create/save/implement-self-hosted-saved-rows/)
* [Metadata Content Dialog response format](../create/save/implement-self-hosted-saved-rows/)

Here’s a **sample implementation for the Metadata Content Dialog**, offering the synced row option:

<figure><img src="../../../.gitbook/assets/CleanShot 2024-12-04 at 20.56.10.png" alt=""><figcaption></figcaption></figure>

The JSON returned to the builder includes the user’s input and selections from the UI. The configuration below shows the new synced row setting applied to the options argument of the resolve method.

### **Example** <a href="#example" id="example"></a>

```json

contentDialog: {
  saveRow: {
    handler: async (resolve, reject, args) => {
      // The following is psuedo code: You need to create "openMetaDataContentDialogModal".
      const metadata = await openMetaDataContentDialogModal(args)
      // Metadata object format:
      // Example: https://docs.beefree.io/save-rows/#saved-rows-metadata
      // {
      //   "guid": "Globally unique id to track this row",
      //   "name": "string",
      //   "category": "string",
      // }
      resolve(metadata, { synced: true })
    }
  },
},
```

## Identifying synced rows <a href="#identifying-synced-rows" id="identifying-synced-rows"></a>

Look for the pencil icon at the top-right of synced rows. Rows without this icon are standard saved rows. The icon provides a clear visual cue for quickly identifying and editing synced rows.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-12-04 at 20.56.35.png" alt=""><figcaption></figcaption></figure>

## Editing synced rows <a href="#editing-synced-rows" id="editing-synced-rows"></a>

To edit a synced row, click the pencil icon. Editing options appear in the sidebar panel. Inside, you’ll find a CTA button and optional text.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-12-04 at 20.56.53.png" alt=""><figcaption></figcaption></figure>

The CTA button opens the `editSyncedRow` Content Dialog, allowing the host application to interact with the end-user and receive their selection.

The host application has complete control over the content dialog and UX. However, the content dialog must always return a boolean value of `true` or `false` to trigger one of the following outcomes:

1. If `true`, the row remains synced to disable content editing in the design before closing the dialog.
2. If `false`, the row updates to enable editing and remove the synced property before closing the dialog.

**For example**, a content dialog might **present users with two options**:

1. Edit the row across all designs.
2. Unsync the row, turning it into a standard saved row.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-12-04 at 20.57.12.png" alt=""><figcaption></figcaption></figure>

The first option, to edit the row across all designs, allows users to make changes to the synced row that will be reflected in all designs that use it.

The second option, to unsync the row, converts the synced row into a standard saved row. This means that any changes made to the row will only affect the design in which it is being edited. This option is useful when the user needs to make specific changes to a single design without affecting other designs that may use the same saved row.

The user’s selection from the above example `editSyncedRow` content dialog UI is returned to the builder as a boolean value. Below is an example of the `editSyncedRow` configuration for the UI above. Note the boolean value `false` in the resolve method unlocks the row:

### **Example** <a href="#example-1" id="example-1"></a>

```json

contentDialog: {
    editSyncedRow: {
		label: 'Edit synced rows',
		description: `This row is used in other designs.
					  You can decide to update all the designs or transform this single row into a regular one`,
		notPermittedDescription: `This row is used in other designs.
                                  Your plan does not permit you to edit it. Please contact your account administrator`,
        handler: function (resolve, reject, args) => {
        	resolve(false) // the boolean will be the value of 'Label of the sidebar button that triggers the contentDialog' `synced`
                           // if false the row will be un-synced, if true nothing will happen.
    	}
    }
}
```

A comprehensive reference of the `editSyncedRow` Content Dialog settings, such as the CTA button label and optional text, can be found in our [Content Dialog docs](../../../other-customizations/advanced-options/content-dialog.md#synced-rows).

The following animation shows this **example of edit synced rows workflow** in action. We’ll dive into this process in the following sections.

<figure><img src="../../../.gitbook/assets/CleanShot 2024-12-04 at 20.57.50.gif" alt=""><figcaption></figcaption></figure>

## Example synced rows workflow <a href="#example-synced-rows-workflow" id="example-synced-rows-workflow"></a>

Suppose a user selects “Edit and update everywhere” from the content dialog. How does the host app ensure seamless editing and synchronization of the row?

Here’s a breakdown of the typical workflow the host app adopts:

1. **Initialization**: The host app launches the Edit Single Row Mode in a new builder instance to enable editing of the synchronized row. Our [Edit Single Row Mode documentation](initialize-edit-single-row-mode.md) is available for reference for a deeper understanding.
2. **User edits**: Users generally hit ‘Save’ to confirm their edits once they modify the synchronized row. Simultaneously, the host app can proactively track these edits using the `onChange` method.
3. **Synchronization timing**: The decision on when to synchronize changes across all designs rests with the host application. Given the potential need to propagate edits to multiple designs, holding off until the user indicates their wish to exit is customary.
4. **Initiation of synchronization**: The synchronization is initiated as soon as the user signifies their satisfaction with the edits, either through the ‘Save’ or ‘Save & Exit’ options.
5. **Redirection & Synchronizing changes**: After editing a row, the host app usually performs a synchronous [merge rows using the CSAPI](../../api-endpoints.md). The user will then be redirected to their ongoing design, where they can see their edits reflected in the synced row.
6. **Background syncing**: Given the possible existence of numerous linked designs, a background process is usually set in motion to update all other templates.

## Synchronizing row changes <a href="#synchronizing-row-changes" id="synchronizing-row-changes"></a>

In the fifth step of the sample workflow, the goal is to bring the user back to their ongoing design with the updated content. This is achieved using the CSAPI’s `merge-rows` method.

The `merge-rows` method functions as a sophisticated “find and replace.”

* i.e., To synchronize content, the host app forwards a request comprising the outdated template, the newly edited row, and a succinct query detailing which row(s) the API should target for replacement. The “query” is a standards-based JSON Path query typically referencing a globally unique identifier that was added to the saved row during the Metadata Content Dialog step.

For an example on how to use the `merge-rows` method, visit our [API Reference on Merge Rows](../../api-endpoints.md).

## Efficient template updates <a href="#efficient-template-updates" id="efficient-template-updates"></a>

To update rows across all designs, keeping track of the templates where rows have been dropped is crucial. There are two principal methods to associate rows with templates:

**Using the `onChange` method**

Upon adding a synced row into a design, the `onChange` callback method supplies the row’s metadata. The metadata will contain the row’s `guid`, which can be used to link the synced row to the `guid` assigned to the template by the host app. Commonly, this is achieved by establishing an index record within the app’s database linking the template’s `guid` with the row’s `guid`.

**Leverage the `synced-rows` method**

For those rows incorporated into designs before the implementation of the `onChange` tracking method, CSAPI’s `synced-rows` method is available. Use the `synced-rows` method get a list of all the synced rows inside a template with their corresponding `rowIdentifier` values. To learn more about how to use this endpoint, visit our[ API Reference on Synced Rows](../../api-endpoints.md).

The specific objectives of the host application steer the choice between these methods. Whatever the choice, the primary focus is meticulously tracking the row across all linked templates, ensuring accurate and efficient updates.

## Advanced Permissions for the Edit Synced Row Button

{% hint style="info" %}
Adding [Advanced Permissions](../../../other-customizations/advanced-options/advanced-permissions.md) to Synced Rows is available for Superpowers and Enterprise plans. Upgrade a [development application](../../../getting-started/readme/development-applications.md) at no extra charge to explore features from higher plan tiers. **Note:** Usage on a development application still counts toward [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) and limits. In your development application, you'll be able to try Advanced Permissions with Synced Rows. This is available for Email, Page, and Popup builders.
{% endhint %}

By configuring advanced permissions for Synced Rows, you can manage the visibility of and access to the **Edit Synced Row** toolbar button. These customization options enable you to define whether end users can:

* View the **Edit Synced Row** button.
* Click the **Edit Synced Row** button.
* Edit Synced Rows using one of the following options:
  * Redirecting to the [Edit Single Row Mode](initialize-edit-single-row-mode.md) builder to edit the Synced Row, and save changes applied globally.
  * Converting a Synced Row to a Saved Row.

A few of the benefits of applying advanced permissions to Synced Rows are the following:

* Limit who can modify synced rows to ensure centralized control.
* Hide unnecessary editing actions for users who only need to reuse existing content.
* Prevent accidental edits to shared content, maintaining consistency across templates.

Sure! Here's a clearer and more user-friendly version of your configuration steps, based on the code you shared:

### Configuration Steps

Follow these steps to enable or customize the `editSyncedRow` option in your Beefree SDK configuration:

1. Open your codebase and locate where you configure the Beefree SDK.
2. If it doesn’t already exist, add the `advancedPermissions` object to your configuration.
3.  Inside `advancedPermissions`, add the following nested structure:

    ```js
    advancedPermissions: {
      rows: {
        toolbar: {
          editSyncedRow: {
            show: true,     // or false
            locked: true,   // or false
          }
        }
      }
    }
    ```
4. Set the Properties:
   * `show`: Set to `true` to display the edit button for Synced Rows, or `false` to hide it.
   * `locked`: Set to `true` to make the edit button read-only, or `false` to make it clickable.
5. Save your changes and test your implementation to confirm the desired behavior.

### Available Settings

The following table outlines the configurable parameters for Synced Rows.

| Parameter | Type    | Description                                                     | Additional info           |
| --------- | ------- | --------------------------------------------------------------- | ------------------------- |
| `show`    | boolean | Controls the visibility of the **Edit Synced Row** button.      | Default value is `true`.  |
| `locked`  | boolean | Determines whether the **Edit Synced Row** button is clickable. | Default value is `false`. |

### Examples

The following code snippet shows an example configuration where `show` is set to `true` and `locked` is set to `false`. In the subsequent image, you can see this configuration results in a clickable **Edit Synced Row** button that is visible in the toolbar.&#x20;

```javascript
advancedPermissions: {
        rows: {
          toolbar: {
            editSyncedRow: {
              show: true,
              locked: false,
            },
          },
        },
      },
```

The following image shows a clickable **Edit Synced Row** button in the toolbar.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-03-28 at 11.26.39.png" alt=""><figcaption></figcaption></figure>

The following code snippet shows an example configuration where `show` is set to `true` and `locked` is set to `true`. In the subsequent image, you can see the configuration result, which is a visible **Edit Synced Row** button that can't be clicked in the toolbar.

```javascript
advancedPermissions: {
        rows: {
          toolbar: {
            editSyncedRow: {
              show: true,
              locked: true,
            },
          },
        },
      },
```

The following image shows a visible **Edit Synced Row** button in the toolbar, but it is not clickable.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-03-28 at 11.29.08.png" alt=""><figcaption></figcaption></figure>

The following code snippet shows an example configuration where `show` is set to `false` and `locked` is set to `true`. In the subsequent image, you can see this configuration results in a toolbar without the button.

```javascript
advancedPermissions: {
        rows: {
          toolbar: {
            editSyncedRow: {
              show: false,
              locked: true,
            },
          },
        },
      },
```

The following image shows a toolbar without the **Edit Synced Row** button.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-03-28 at 11.30.35.png" alt=""><figcaption></figcaption></figure>
