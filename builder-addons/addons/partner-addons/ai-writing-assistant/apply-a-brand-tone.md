---
description: >-
  Learn how to provide your end users with the option to tailor the AI Writing
  Assistant's responses by adding a brand tone.
---

# Apply a Brand Tone

{% hint style="info" %}
The AI Writing Assistant AddOn and Brand Tone feature are only available for [Superpowers](https://developers.beefree.io/pricing-plans) and [Enterprise](https://developers.beefree.io/pricing-plans) plans.
{% endhint %}

## Introduction to Brand Tone <a href="#simple-guide-for-integrating-brand-tone" id="simple-guide-for-integrating-brand-tone"></a>

The **Apply a Brand Tone** feature is an optional enhancement to the [AI Writing Assistant AddOn](./). This feature allows your application's end users to define which brand tone they want the AI Writing Assistant to use when generating text. This definition provides OpenAI with additional brand tone context it considers when generating text to return to your end user. The result is more precise, accurate, and useable copy for your application's end users.

By configuring the [AI Writing Assistant](./) to reflect a specific brand tone, you empower end users to create designs that consistently align with their brand identity, reducing the need for manual adjustments to the AI's responses. This feature can improve workflows through organic and beneficial adoption of the [AI Writing Assistant](./), positioning your application as a powerful tool.

To learn more about the end user experience and what it looks like to utilize this feature on the frontend, visit the [Apply a Brand Tone](https://docs.beefree.io/end-user-guide/ai-tools-for-content-creation/apply-a-brand-tone) white label end user documentation. The markdown file is also available in our [white label docs repository.](https://github.com/BeefreeSDK/beefree-sdk-whitelabel-docs)

{% hint style="info" %}
**Note:** OpenAI is currently the only compatible provider with this feature.
{% endhint %}

## Prerequisites <a href="#simple-guide-for-integrating-brand-tone" id="simple-guide-for-integrating-brand-tone"></a>

Prior to getting started, ensure you have the following:

* A [Superpowers or Enterprise Beefree SDK plan](https://developers.beefree.io/pricing-plans)
* The AI Writing Assistant AddOn enabled in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
* OpenAI API Key

## Integrating Brand Tone <a href="#simple-guide-for-integrating-brand-tone" id="simple-guide-for-integrating-brand-tone"></a>

This section will walk you through how to add the **Apply** **brand tone** option to the [AI Writing Assistant](./) integrated within your host application.

At a high-level, this section will cover how to take the following steps and successfully integrate Brand Tone:

1. [Add `isBrandTonesEnabled` setting to `ai-integration`](apply-a-brand-tone.md#how-to-integrate-the-ai-writing-assistant-add-on-and-configure-it-with-the-brand-tone-settings)
2. [Add hooks to `BeeConfig` for data storage and management](apply-a-brand-tone.md#id-2.-hooks-for-data-storage)

{% hint style="info" %}
**Note:** Ensure you have the [AI Writing Assistant AddOn](./) configured and implemented prior to integrating the Brand Tone option. For details steps on how to configure this AddOn, visit the [AI Writing Assistant documentation](./).
{% endhint %}

### Configure the AI Writing Assistant with the Brand Tone Settings <a href="#how-to-integrate-the-ai-writing-assistant-add-on-and-configure-it-with-the-brand-tone-settings" id="how-to-integrate-the-ai-writing-assistant-add-on-and-configure-it-with-the-brand-tone-settings"></a>

Take the following steps to configure the AI Writing Assistant to include Brand Tone:

1. Add the `ai-integration` AddOn to your `beeConfig` object under the `addOns` array.
2. Add the `isBrandTonesEnabled` setting and set the boolean to `true`. This is the only required setting to enable this feature.
3. (Optional) Customize the settings for the **Brand Tones** feature to allow users to add, edit, delete, or select tones based on your application’s needs.

#### Sample Code for Brand Tones Settings <a href="#sample-code-snippet-for-integration" id="sample-code-snippet-for-integration"></a>

The following code snippet provides an example configuration for integrating the [AI Writing Assistant](./) AddOn with the settings for managing **Brand Tones**:

```javascript
const beeConfig = {
  uid: 'unique_user_id', // Unique identifier for the user
  addOns: [
    {
      id: "ai-integration", // Identifier for the AI integration add-on
      settings: {
        isBrandTonesEnabled: true, // Mandatory to enable the Brand Tones feature
        canAddBrandTones: true, // Optional: Allow the user to add new Brand Tones
        canDeleteBrandTones: false, // Optional: Prevent the user from deleting existing Brand Tones
        canEditBrandTones: true, // Optional: Allow the user to edit existing Brand Tones
        canSelectBrandTones: true // Optional: Allow the user to select Brand Tones for use
      }
    }
  ],
  // Other configurations
};
```

#### Available Settings for Brand Tone <a href="#available-settings-for-brand-tone" id="available-settings-for-brand-tone"></a>

You can control the different settings for the **Brand Tone** using the following booleans. You can use these boolean flags to allow or restrict user actions.

For example:

* Set `isBrandTonesEnabled: true` if you want to enable the **Brand Tones** feature.
* Set `canDeleteBrandTones: false` to prevent end users from deleting existing tones.

The following table provides details about each setting and how you can customize them.

| Setting               | Data Type | Example Value | Description                                                                 |
| --------------------- | --------- | ------------- | --------------------------------------------------------------------------- |
| `isBrandTonesEnabled` | Boolean   | `true`        | Determines if the **Brand Tones** feature is enabled for the user.          |
| `canAddBrandTones`    | Boolean   | `true`        | Allows users to add new Brand Tones to their account.                       |
| `canDeleteBrandTones` | Boolean   | `false`       | Allows users to delete existing Brand Tones.                                |
| `canEditBrandTones`   | Boolean   | `true`        | Allows users to edit existing Brand Tones.                                  |
| `canSelectBrandTones` | Boolean   | `true`        | Allows users to select from available Brand Tones for use in their session. |

### Add Hooks for Data Storage

This section explains how to add hooks for data storage and management.

#### **Introduction to Hooks**

Hooks allow your application to store and manage Brand Tone data. By defining the `brandTone` hook, you ensure communication between your system and Beefree SDK, enabling users to create and manage Brand Tones effectively.

#### **Step-by-Step Instructions**

**1. Define the Hook**

Add the `brandTone` hook to your `beeConfig` object. This hook handles all Brand Tone-related actions like retrieving, saving, and deleting tones.

Sample Code:

```javascript
const beeConfig = {
    uid: 'unique_user_id',  // Unique identifier for the user
    addOns: [
        // ...
    ],
    hooks: {
      // ... ,
      brandTone: {
        handler: async (resolve, reject, { action, data }) => {
          switch (action) {
            case 'get':
              const brandVoiceList = await getBrandTones() // Your own implementation to retrieve saved brand tones
              resolve(brandVoiceList)
              break
            case 'save':
              await saveBrandTone(data) // Store brand tone to your own system
              resolve()
              break
            case 'saveSelected':
              await saveSelectedBrandTone(data) // Store the selected brand tone to your own system
              resolve()
              break
            case 'getSelected':
              const selectedBrandTone = await getSelectedBrandTone() // Get the stored selected brand (this will be autoselect when the users open the AI side panel)
              resolve(selectedBrandTone)
              break
            case 'delete':
              await deleteBrandTone(data) // Delete the brand tone from your system
              resolve()
              break
            case 'edit':
              await editBrandTone(data) // Update the just edited brand tone on your system 
              resolve()
              break
            default:
              break
          }
        }
      }
    }
};
```

**2. Implement the Handler Logic**

The `brandTone` hook supports various actions.&#x20;

The handler receives the `resolve` and `reject` methods to fulfill the Promise for the requested data or action. Use `reject` only for issues encountered on your application's side, such as errors in data retrieval. Always call `resolve` after processing the data within your system.

Alongside `resolve` and `reject`, the handler also receives an object containing `action` and `data` properties. The `action` determines the specific scenario in the Brand Tones flow, while the `data` is used to store any necessary changes.

Refer to the table below for details on when and how each action will be triggered.

| Action name    | Description                                                                                                                                                                                                             | Data received                                                | Expected resolved value                                                                             |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| `get`          | Will be requested as soon as the AI Side Panel opens and after successful operations (e.g. edit, delete, save). It asks for a saved Brand Tones list that you’ll likely retrieve from your system.                      | `none`                                                       | Array of Brand Tone (in the exact form you received that in `save` action)                          |
| `save`         | Will be requested when the user clicks on “Save” in the Modal to create a Brand Tone. This is where you store data in your system.                                                                                      | `brandTone` object                                           | <p><code>none</code><br>(just a <code>resolve()</code> to confirm save action succeded)</p>         |
| `edit`         | Will be requested when the user clicks on “Save” in the Modal to edit an existing Brand Tone. This is where you update data in your system.                                                                             | `brandTone` object                                           | <p><code>none</code><br>(just a <code>resolve()</code> to confirm edit action succeded)</p>         |
| `delete`       | Will be requested when the user clicks on “Delete” in the Modal to manage existing Brand Tones. This is where you remove the brand tone data from your system.                                                          | `brandTone` object                                           | <p><code>none</code><br>(just a <code>resolve()</code> to confirm delete action succeded)</p>       |
| `getSelected`  | <p>Will be requested as soon as the AI Side Panel opens and after successful operations (e.g. edit, delete, save).</p><p>It asks for the <code>id</code> of the Brand Tone to pre-select on the Brand Tones select.</p> | `none`                                                       | `string` (the `id` of the Brand Tone)                                                               |
| `saveSelected` | <p>Will be requested when the user selects the Brand Tone from the select and after successful operations (e.g. edit, delete, save).</p><p>This is to preserve the user selection between different sessions.</p>       | `string` (the `id` of the Brand Tone the user just selected) | <p><code>none</code><br>(just a <code>resolve()</code> to confirm saveSelected action succeded)</p> |

## Additional Considerations

* The Brand Tone feature is available only through the AI Writing Assistant AddOn with OpenAI as the provider.
* Configuring hooks for data storage is required to enable this feature successfully.
* Thoroughly test your implementation to ensure smooth communication between the SDK and your system.
