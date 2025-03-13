---
description: Learn more about client-side configuration for Custom and Partner AddOns.
---

# AddOns Configuration

## Adding client-side configurations for AddOns <a href="#adding-client-side-configurations-for-addons" id="adding-client-side-configurations-for-addons"></a>

Once you have initialized Beefree SDK, you can pass a series of [configuration parameters](../../getting-started/readme/installation/configuration-parameters/) to it.

The **AddOn section** of the configuration allows you to override the parameters you configured in the [Beefree SDK Console](https://dam.beefree.io/devmain), on a per-user basis.

For example:

* You can have an AddOn enabled at the application level, but disabled for users on a lower plan (so they have to upgrade to a higher plan in your app to get it).
* You could change the language used for the AddOn text labels depending on the language used for the builder, for that user.
* Etc.

### **Example**

The following code displays an AddOn configuration example.

```javascript

addOns: [
  {
    enabled: true,
    id: "", 
    label: 'Default title label override',
    ctaLabel: 'Default CTA label override',
    placeholder: 'Default stage placeholder override',       
  },
  {
    enabled: false,
    id: "",
  }
]

```

## AddOns Configuration in the Client Config

The `editable` parameter is a boolean that controls whether the content associated with a specific content AddOn can be modified by users. By default, this boolean is set to `false`, meaning the content is locked and cannot be edited. When set to `true`, the content becomes editable, allowing users to make changes as needed. However, it’s important to note that this parameter only applies to content AddOns and has no effect on row or mixed content AddOns. This feature provides flexibility in managing user permissions and ensuring that only intended content can be modified, enhancing control over the editing experience.

The following code snippet shows an example of how to configure an AddOn of type Paragraph.

```javascript
      
      addOns: [
        {
          id: "paragraph",
          editable: true,
        },
      ],
      
```

In the following code snippet, you can see additional examples of AddOn configurations for other content types.

```javascript

      addOns: [
        {
          editable: true,
          id: "html",
        },
        {
          editable: true,
          id: "button",
        },
      ],

```

{% hint style="info" %}
**Note:** The `editable` boolean has a default value of **false**. If this boolean is set to **true**, the content related to that content AddOn will become editable.
{% endhint %}

### Supported AddOn IDs for Configuration

When configuring your code for AddOns, it's important to note that each AddOn has a specific type that is identified by its `id`. Below are the supported content types that can be used as AddOn IDs:

* `Image`: For adding and configuring images.
* `HTML`: For embedding custom HTML code.
* `Mixed`: For a combination of various content types.
* `Row`: To structure content in rows.
* `Paragraph`: For text paragraphs.
* `Button`: To add call-to-action buttons.
* `Title`: For headings and subheadings. Set the `id` to `heading` in your configuration.
* `List`: For ordered and unordered lists.
* `Menu`: For navigation menus.
* `Icon`: To include icons.

Using these IDs correctly when defining your AddOn configurations ensures that the correct content type is implemented within your application.

## Parameters

This section provides an overview of what each parameter does.

#### Understanding the Parameters

* **enabled**: Determines if the AddOn is available within your application. Set to `false` to disable the AddOn.
* **id**: A unique identifier for the AddOn. This is important for distinguishing between different AddOns.
* **label**: A brief text that represents the AddOn’s purpose or content. It is displayed within the user interface.
* **ctaLabel**: Call-to-Action text encouraging the user to interact with the AddOn.
* **placeholder**: A short guide or prompt displayed before the AddOn content is initialized or added.
* **editable**: Controls whether the AddOn's content can be edited by the end user. When set to `true`, editing features are enabled.

| Parameter     | Type        | Description                                                                                                                                                                                                              |
| ------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `enabled`     | Boolean     | When false, the AddOn content is not displayed in the _Content_ tab.                                                                                                                                                     |
| `id`          | Number      | Identifies the AddOn by using the _handle_ provided in the configuration form.                                                                                                                                           |
| `label`       | Text String | The text string displayed for the AddOn tile in the _Content_ tab.                                                                                                                                                       |
| `ctaLabel`    | Text String | <p>The text string displayed in the button that triggers the AddOn action.</p><p></p><p>It’s displayed in:</p><ul><li>The content placeholder (before any content is applied)</li><li>The content properties</li></ul>   |
| `placeholder` | Text        | Text displayed in the content placeholder to provide further information about the content.                                                                                                                              |
| `editable`    | Boolean     | A boolean with a default value of **false**. If this boolean is set to **true**, the content related to that content AddOn will become editable. **Note:** This parameter has no effect for row or mixed content AddOns. |
