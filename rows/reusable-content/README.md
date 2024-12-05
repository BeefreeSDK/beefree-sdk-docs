# Reusable Content

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. If you're on the Essentials plan, [upgrade a development application](https://docs.beefree.io/beefree-sdk/getting-started/readme/development-applications) for free to try this and other Core-level features.
{% endhint %}

Beefree SDK offers a comprehensive suite of features that enable your application's end users to save and manage reusable content. Rows are a core feature of the visual builders within Beefree SDK that provide end users with an intuitive avenue for saving and reusing content throughout their design creation workflows. They provide a structured method to house various types of content such as headers, paragraphs, images, and buttons.

Rows are also a fundamental part of how designs are built and structured within the visual builders. In the following GIF, you can see how each row functions as a component of a continuous design.&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-03 at 17.29.14.gif" alt=""><figcaption></figcaption></figure>

Rows allow end users to add multiples types of content to a section of a design. End users can either create their own rows from scratch (and save them for reuse on a later day), or they can use pre-designed rows that are  pre-loaded into the host application and ready for use. Pre-loaded rows are helpful when providing a template structure that end users can customize as they build their designs.&#x20;

Providing end users with the option to easily reuse content comes with a host of benefits, including:

* **Pre-designed and customizable content**: End users can select from rows that already contain content, which they can then customize for their specific needs.
* **Flexible structure**: Rows help organize different content types in a structured layout, which promotes a clean and efficient design.
* **Drag-and-drop functionality**: Rows can easily be dragged and dropped onto the stage.
* **Continuity with current user experience**: End users can add empty structures, which preserves creativity and allows them to build and design from scratch.
* **Option to disable empty rows**: If preferred, end users can opt to work solely with pre-made rows, focusing on content customization without the need to build layouts from the ground up.

In addition to rows offering a variety of benefits for end users, there are also clear benefits for the host application, including:&#x20;

* **Ready-to-go content delivery**: The host application can pass pre-built, ready-to-go rows directly into the builder, reducing the need for end users to create content from scratch.
* **Customization control**: Host applications can offer a variety of customizable rows, ensuring users follow design guidelines while still providing creative freedom.
* **Improved user experience**: Pre-designed rows simplify the user interface, making the builder more intuitive and less complex for users.
* **Optional removal of empty structures**: Host applications can disable empty row options if desired, encouraging users to focus on modifying pre-existing content.
* **Efficient content management**: Rows enable the host to provide consistent, reusable content blocks that can be updated globally, streamlining content management and maintaining design consistency across the platform.

### Understanding the Different Types of Rows in Beefree SDK

This section outlines the different row-related features available within Beefree SDK. Throughout the following pages of the Rows section, we will discuss each of these different row-related features in depth, including what they are, how they look, and how to implement them if they are a good fit for your application and end users.&#x20;

#### Custom Rows

The purpose of Custom Rows is to provide pre-configured rows that your end users can drag-and-drop into the builder and start customizing.

The following GIF provides a visual of how Custom Rows look to end users:

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-03 at 17.53.35.gif" alt=""><figcaption></figcaption></figure>

Custom Rows are integrated by adding the `rowsConfiguration` parameter to your [`beeConfig`](../../getting-started/readme/installation/configuration-parameters/). The following code snippet is the one used to configure the row in the GIF above.

```json
rowsConfiguration : {
 "externalContentURLs": [
  {
   "name": "External resource",
   "value": "https://bee-playground-backend.getbee.io/api/customrows?ids=1,2,3,4"
  }
 ]
}
```

Visit the [Beefree SDK playground](https://developers.beefree.io/playground) to experiment more with the Custom Rows configuration, and visit the [Implement Custom Rows page](create/pre-build/implement-custom-rows.md) to learn more about integrating this feature within your application.

#### Hosted Saved Rows

Hosted Saved Rows allow your end users to save and manage their own rows to be used later–a powerful way to help them streamline their workflows!

Also, Hosted Saved Rows simultaneously provides both a storage solution and user interface your application's end users can engage with to save and manage their rows.

In the following GIF, with Hosted Saved Rows, Beefree SDK provides the user interface and infrastructure to power Saved Rows so you can bring this feature to your end users instantly.  &#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-03 at 18.22.16.gif" alt=""><figcaption></figcaption></figure>

[Implementing Hosted Saved Rows](create/save/implement-hosted-saved-rows.md) takes only a few seconds, because it activated through a toggle in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu). The following image shows how the toggle looks like in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu). &#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-03 at 18.26.16.png" alt=""><figcaption></figcaption></figure>

Visit the [Implement Hosted Saved Rows](create/save/implement-hosted-saved-rows.md) page to learn more about customization options and integration details.

#### Self-hosted Saved Rows

[Self-hosted Saved Rows](create/save/implement-self-hosted-saved-rows.md) are similar to Hosted Saved Rows on the frontend, but require you to connect your own database on the backend. This feature also provides you with more customization options on the frontend if you'd more granular control over customizing your end user's experience saving and managing rows.

&#x20;The following GIF shows an example of a customized modal for saving a row within an application. This modal uses both [saved rows](./#hosted-saved-rows) and [content dialog](../../other-customizations/advanced-options/content-dialog.md) for the customized experience.

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-03 at 18.45.20.gif" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note:** Unlike Hosted Saved Rows, Self-hosted Saved Rows does require development.
{% endhint %}

#### Synced Rows

The purpose of [Synced Rows](sync/implement-synced-rows.md) is to maintain consistency by synchronizing row updates across multiple designs. A synced row can be reused across multiple designs and each design is updated whenever a synced row is updated. When you edit a synced row, you a redirected to [Edit Single Row Mode](sync/initialize-edit-single-row-mode.md).

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-03 at 18.57.13.gif" alt=""><figcaption></figcaption></figure>

#### Edit Single Row Mode

The purpose of Edit Single Row Mode is to allow precise editing of rows inside of a dedicated row builder. The GIF above displays an example of Edit Single Row Mode. Visit [Initialize Edit Single Row Mode](sync/initialize-edit-single-row-mode.md) to learn more about how to implement this feature.
