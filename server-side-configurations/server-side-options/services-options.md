# Services Options

{% hint style="info" %}
Please note that server-side configurations are only available on [paid plans](https://dam.beefree.io/pluginpricing).
{% endhint %}

This page explains Service Options within the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu). You can enable these optional services to extend the functionality of the builder and add features visible in UI.

## Navigate to Services

Service Options are available for applications within the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu). Take the following steps to locate and enable them:

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu)
2. Navigate to the application you'd like to enable them for
3. Click **Details**
4. Click **Configure Application** under **Application Configurations**
5. Scroll down to the **Services** section
6. Check the checkboxes corresponding with the features you'd like to enable
7. Click **Save** **changes** in the upper right-hand corner&#x20;

Your Service Options settings have been enabled and will be reflected in the UI of your application.

The following image shows what the Services section looks like within the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu) and the available options.

<figure><img src="../../.gitbook/assets/CleanShot 2025-08-11 at 13.53.03.png" alt="Service options available within the Beefree SDK Developer Console" width="563"><figcaption></figcaption></figure>

## Service Options

This section lists and describes each of the options available in the **Services** section of the **Application Configurations**.&#x20;

### Media & File

**Move files between folders in the file manager**\
When enabled, users can reorganize assets by moving files across folders (via drag-and-drop or “Move to…”), keeping the library tidy without re-uploading.

[Learn more about moving files](https://docs.beefree.io/end-user-guide/manage-files/file-manager/how-to-move-files)

**Free stock image gallery in the file manager**\
Enable the free stock image gallery. Your end users will be able to add stock images to their designs using this gallery. The images are free to use under the Creative Commons Zero (CC0) license.

**Import from external source in file manager**\
When enabled, adds an option in the file manager to import images from different social networks and storage services. We use [Filestack](https://www.filestack.com/) for this feature. [Filestack](https://www.filestack.com/) may log the user’s IP address. If this is in conflict with your privacy policy, turn the feature off.

**Apply image effects**\
When enabled, an editor to apply image effects and transformations is available in the image module and for row background images.

### Design & Layout

**Row background image**\
When this is active, advanced users of the builder can set an image as the background of a row or [content area](../../other-customizations/content-area-padding.md).

**Row vertical align**\
Adds a row option to vertically align column content (top, middle, bottom). Helpful for layouts with mixed image/text heights.

**Cards style (Spacing and Cards rounded corners)**\
Applies a [card preset](../../other-customizations/cards-style-and-image-round-corners.md) to rows and columns, with balanced internal spacing and rounded corners for a modern, card-based look.

**Content area rounded corners**\
Exposes a global setting to round the main content [container’s corners](../../other-customizations/cards-style-and-image-round-corners.md) across the design.

**Content area padding**\
Lets you set default inner [padding for the main content area](../../other-customizations/content-area-padding.md), ensuring consistent spacing without per-row tweaks.

**Image rounded corners**\
Adds a property to round image corners directly in the image block.

**Button hover**\
Enables [hover state](../../other-customizations/hover-effect-for-buttons.md) controls on buttons (e.g., background, border, and text changes on hover) for clearer interactivity.

Learn more about [Hover Effect for Buttons](https://docs.beefree.io/end-user-guide/design-tools/hover-effect-for-buttons).

**Custom social icon**\
When enabled in the Social module, users can upload their own social media icons. A new “Add a custom icon” feature will appear in the Social content block’s property panel.

### Content Personalization

**Dynamic image**\
When this setting is enabled, users of the builder can specify both a static placeholder image and a dynamic image URL when adding an image content block. This allows for scenarios such as personalized birthday cards, countdown timers, dynamic ads, and other cases in which an image is built dynamically at the time it is served.

Learn more about [Dynamic Images](https://devportal.beefree.io/hc/en-us/articles/4403101966610-Using-dynamic-images-for-countdown-timers-and-personalized-content).

**Display conditions**\
When enabled, the display conditions widget will show as a row option. The widget can be used to apply the conditions created by the host applications or to add new syntax manually.

Learn more about [Display Conditions](../../other-customizations/advanced-options/display-conditions.md).

**Smart Merge Tags**\
Surfaces context-aware suggestions for [merge fields](../../other-customizations/advanced-options/smart-merge-tags.md) while editing, helping users pick the right data placeholders faster.

**Merge Tags preview in toolbar**\
Adds a toolbar control to preview[ merge tags](../../other-customizations/advanced-options/smart-merge-tags.md) with sample data from the host app, so users can validate personalization before sending.

**Multi-language template**\
Lets users [manage language variants](../../other-customizations/multi-language-templates.md) of the same design inside a single template and switch between them while editing.

Learn more about [Multi-language Templates](../../other-customizations/multi-language-templates.md)

### Editing & Collaboration

**Undo and changes history**\
When enabled, it will give users the ability to undo or redo any changes that have been made to the email, including the ability to rewind and fast-forward to any point in their recent [edit history](undo-and-changes-history.md).

**Commenting**\
Allows users to leave [comments](../../other-customizations/advanced-options/commenting.md) and start discussion threads inside an email or page, to collaborate asynchronously.

**Dark mode preview**\
When active, adds a toggle to the toolbar that allows a user to simulate the current design in [dark mode](https://docs.beefree.io/end-user-guide/preview-options/dark-mode-preview).

### Responsive Layout

**Do not stack on mobile**\
When enabled, adds a new row option to keep the horizontal layout on mobile devices. Useful when working with nav bars, icons, and other horizontal design elements.

[Learn more about Do not stack on mobile](../../other-customizations/mobile-design-mode.md)

**Stack order on mobile**\
Adds a row option to explicitly set the order of columns on mobile, so you can control which column appears first in small viewports.

[Learn more about Stack order on mobile](../../other-customizations/mobile-design-mode.md)

**Hide content on mobile or desktop**\
When enabled, adds a new property in the “Content properties” section of any content block that supports it. This widget allows users to hide a content block either on mobile or on desktop devices.

[Learn more about Hide content on mobile or desktop](../../other-customizations/mobile-design-mode.md)

**Mobile design mode**\
Enables a focused mobile editing canvas and tools tailored for small screens, making it easier to fine-tune spacing, text size, and layout for mobile.

[Learn more about Mobile design mode](../../other-customizations/mobile-design-mode.md)

### Additional Configuration & Restrictions

**Reverse stacking on mobile**\
When enabled, adds a new row option to revert the stacking order of columns on mobile. Useful for layouts with alternating visual and text: applying it will ensure that, on mobile, images are consistently on top of their accompanying copy.

[Learn more about Reverse stacking on mobile](../../other-customizations/mobile-design-mode.md)

**Disable anonymous usage tracking**\
We use third-party tools to aggregate anonymous usage data. It helps us develop a better product by assessing locations, devices, browsers, etc. This can be turned off if necessary.

**Disable the HTML sanitize service in the HTML content block**

* When you disable the HTML sanitization service, you’re removing all restrictions on what users of the builder can add inside the Custom HTML content block.
* The sanitize service checks and cleans up custom HTML, which can prevent the introduction of unsafe content or tags that might impact deliverability. However, disabling it can be useful if the host application needs custom HTML tags or attributes.
* If disabled, you should implement an alternative code review process, such as using the `onChange` or `onSave` [events](../../getting-started/readme/installation/methods-and-events.md) to review content.
* The [client-side configuration](../../getting-started/readme/installation/configuration-parameters/) allows enabling (`forceSanitizeHTML: true`) per user, but cannot disable sanitization for security reasons.

Learn more about [Custom HTML](https://docs.beefree.io/end-user-guide/content-blocks/custom-html#html-tag-restrictions-in-emails) and [Custom Head HTML](https://docs.beefree.io/end-user-guide/design-tools/add-custom-head-html).

**Activate custom limitations on File Manager**\
In this section, you can activate restrictions for the [file manager](broken-reference):

* Specify which file formats your users can upload.
* Set a maximum allowed size (default: 20MB).

Instead of file extensions, categories such as image, video, or text are shown, mapped to [MIME types.](../../file-manager/file-manager-application-overview/file-extensions-and-groups.md)
