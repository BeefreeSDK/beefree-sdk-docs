# Custom CSS

{% hint style="info" %}
This feature is available on Beefree SDK [Superpowers plan](https://dam.beefree.io/pluginpricing) and above. If you're on the Core or Essentials plan, [upgrade a development application](../../getting-started/readme/development-applications.md) for free to try this and other Superpowers-level features.
{% endhint %}

## Defining a custom look & feel through a CSS stylesheet <a href="#defining-a-custom-look-feel-through-a-css-stylesheet" id="defining-a-custom-look-feel-through-a-css-stylesheet"></a>

To define a custom look and feel through a CSS stylesheet, assign the URL of your CSS file to the `customCss` property in your JavaScript code, as shown in the following example.

```javascript

customCss: 'https://yourdomain.com/stylesheet.css'

```

## Using different values for different users of the builder <a href="#using-different-values-for-different-users-of-the-editor" id="using-different-values-for-different-users-of-the-editor"></a>

You can customize the builder's CSS for different users by dynamically setting the `customCss` property with a unique CSS file URL for each user. Simply concatenate the user-specific identifier to the base URL as shown in the example code.

```javascript

customCss: 'https://yourdomain.com/' + users[config.user].id + '.css'

```

## Best practices and risk management <a href="#best-practices-and-risk-management" id="best-practices-and-risk-management"></a>

Custom CSS is an advanced feature, which gives the host application great flexibility to customize the UI/UX of the builder.

Please use this feature with caution.

When used properly, it is a powerful tool that can be leveraged to accomplish anything from applying custom styles with fine granularity to changing icons.

When misused, however, it may harm the user experience and the rendering capability of the builder’s stage. For example, styles applied to the stage via CSS will _not_ be reflected in the preview or exported HTML.

{% hint style="info" %}
If you're looking to hide certain UI elements, we recommend you first check if that can be accomplished with [Advanced Permissions](../advanced-options/advanced-permissions.md), as it may be easier to implement.
{% endhint %}

For the best possible results, please follow these best practices:

* Avoid using generic global styles. (e.g. \*, p, input, etc.) that could propagate to the editing stage.
* Use CSS selectors to select specific elements and groups (e.g. body.bee–cs h3).
* Do not attempt to pass JavaScript or any other scripts via CSS.
* Ensure the custom CSS URL is hosted over HTTPS.
* Do not link to CSS files hosted on GitHub, or by any 3rd party.
* Never style elements on the stage, since those styles will not appear in the final HTML, and therefore lead to a confusing user experience.

Please note that classnames with the `--cs` suffix are reliable selectors for customCSS.\
Other selectors such as the following should be avoided as much as possible:

* Nested tag structure (e.g. `div > div > div` )
* Siblings (`input + label`)
* Classnames without –cs (e.g. `.icons__item)`
* Prefixed classname selectors (e.g. `div[class^="StageModuleIcons_itemRow"]`)

## Sample Custom CSS Theme <a href="#sample-custom-css-theme" id="sample-custom-css-theme"></a>

Reference the following Sample Custom CSS Theme to see an example of how you can use custom CSS in your web application.

```url

https://gist.github.com/44daee53546a9f48ecad7f52784efa55.git

```

## Classnames <a href="#sample-custom-css-theme" id="sample-custom-css-theme"></a>

Classnames in CSS are identifiers used to define and apply specific styles to HTML elements. They enable developers to target elements more efficiently and apply styles across multiple elements consistently. Classnames make it easier to manage and control the appearance of web pages through styling.

Reference classnames for custom CSS.

{% tabs %}
{% tab title="Button Sidebar" %}
This article lists the classnames for different buttons within the sidebar, aimed at developers seeking to customize or understand the styling applied to these components. You can use this information to more easily modify or enhance the user interface of your web application.

This section will cover button classnames for the following sidebar areas:

* [Content](custom-css.md#content)
* [Rows](custom-css.md#rows)
* [Settings](custom-css.md#settings)

## Content

This section lists the classnames for buttons within the content area of the sidebar.

### Add-on

This section lists the Add-on sidebar widget sub-elements and classnames.

#### Add-on CTA

<table><thead><tr><th width="153">Sub-Element</th><th width="199">Deprecated</th><th>New Classnames</th></tr></thead><tbody><tr><td>NA</td><td><ul><li><code>btn</code></li><li><code>btn-primary</code></li></ul></td><td><code>add-on-sidebar-button--cs</code></td></tr></tbody></table>

### Button

This section lists the Button sidebar widgets and their respective deprecated and new classnames.

#### Write with AI

| Sub-element | Deprecated                                                                  | New Classnames        |
| ----------- | --------------------------------------------------------------------------- | --------------------- |
| NA          | <ul><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `ai-sidebar-icon--cs` |

#### Link

This section lists the Button sidebar widgets and their respective deprecated and new classnames.

<table><thead><tr><th width="215">Sub-element</th><th>Deprecated</th><th>New Classnames</th></tr></thead><tbody><tr><td>Special links</td><td><ul><li><code>href-container__link</code></li><li><code>href-container__link--special-link</code></li></ul></td><td><code>href-special-link--cs</code></td></tr><tr><td>Link file</td><td><ul><li><code>href-container__link</code></li><li><code>href-container__link--link-file</code></li></ul></td><td><code>href-link-file--cs</code></td></tr><tr><td>Add custom special link</td><td><ul><li><code>href-container__link</code></li><li><code>href-container__link--special-link</code></li></ul></td><td><code>href-custom-special-link--cs</code></td></tr></tbody></table>

#### Attributes

This section lists the Button sidebar widgets and their respective deprecated and new classnames.

| Sub-element       | Deprecated                                                                                                                                                                                          | New Classnames           |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| Add new attribute | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li> <code>icon-manager__add-icon</code> </li><li><code>icon-manager__add-icon--cs</code></li><li> <code>BeeButton_*</code></li></ul> | `toggle-menu-button--cs` |
| Delete            | <ul><li><code>field-remove</code></li></ul>                                                                                                                                                         | `delete-attribute--cs`   |

### Carousel

This section lists the Carousel sidebar widgets, sub-elements, and classnames.

#### Add New Slide

| Sub-element | Deprecated                                                                                                                                          | New Classnames               |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| NA          | <ul><li><code>btn</code> </li><li><code>btn-primary</code></li><li> <code>icon-manager__add-icon</code> </li><li><code>BeeButton_*</code></li></ul> | `icon-manager__add-icon--cs` |

#### Draggable Item

<table><thead><tr><th width="182">Sub-element</th><th width="143">Deprecated</th><th>New Classnames</th></tr></thead><tbody><tr><td>Change image</td><td>NA</td><td><code>carousel-item-change-image--cs</code></td></tr><tr><td>Delete</td><td>NA</td><td><code>carousel-item-delete-image--cs</code></td></tr></tbody></table>

### Dynamic Content

This section lists the Dynamic sidebar widgets, sub-elements, and classnames.

#### Choose a Custom Merge Content

| Sub-element | Deprecated                                                                                            | New Classnames             |
| ----------- | ----------------------------------------------------------------------------------------------------- | -------------------------- |
| NA          | <ul><li><code>btn</code> </li><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `select-merge-content--cs` |

### Form

This section lists the Form sidebar widgets, sub-elements, and classnames.

#### Edit Form

| Sub-element | Deprecated | New Classnames              |
| ----------- | ---------- | --------------------------- |
| NA          | NA         | `content-dialog-button--cs` |

#### Manage Fields

| Sub-element   | Deprecated                                                                                                                                                                                         | New Classnames           |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| Edit          | <ul><li><code>field-edit</code></li></ul>                                                                                                                                                          | `form-field-edit--cs`    |
| Delete        | <ul><li><code>field-remove</code></li></ul>                                                                                                                                                        | `form-field-delete--cs`  |
| Add new field | <ul><li><code>btn</code> </li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code> </li><li><code>BeeButton_*</code></li></ul> | `toggle-menu-button--cs` |

### Heading

This section lists the Form sidebar widgets, sub-elements, and classnames.

#### Write with AI

| Sub-elemet | Deprecated                                                                  | New Classnames                                     |
| ---------- | --------------------------------------------------------------------------- | -------------------------------------------------- |
| NA         | <ul><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | <ul><li><code>ai-sidebar-icon--cs</code></li></ul> |

### Icons

This section lists the Icons sidebar widgets, sub-elements, and classnames.

#### Add New Icon

| Sub-element | Deprecated                                                                                                                                                                                           | New Classnames       |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| Button      | <ul><li><code>btn</code> </li><li><code>btn-primary</code> </li><li><code>icon-manager__add-icon</code> </li><li><code>icon-manager__add-icon--cs</code> </li><li><code>BeeButton_*</code></li></ul> | `icons-add-icon--cs` |

#### Draggable Icon

| Sub-element   | Deprecated                                                                                                  | New Classnames          |
| ------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------- |
| Change image  | <ul><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li><li><code>BeeIcons_*</code></li></ul> | `icons-change-icon--cs` |
| Apply effects | <ul><li><code>btn-default</code></li><li><code>BeeButton_*</code></li><li><code>BeeIcons_*</code></li></ul> | `icons-edit-icon--cs`   |
| Delete        | <ul><li><code>BeeButton_*</code></li><li><code>BeeIcons_*</code></li></ul>                                  | `icons-delete-icon--cs` |

### Image

This section lists the Image sidebar widgets, sub-elements, and classnames.

#### Apply Effects

| Sub-element | Deprecated                                                                                                                                 | New Classnames         |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------- |
| NA          | <ul><li><code>btn</code></li><li><code>btn-image-editor</code></li><li><code>btn-default</code></li><li><code>BeeButton_*</code></li></ul> | `btn-image-editor--cs` |

#### Change Image

| Sub-element | Deprecated                                                                                                                                  | New Classnames        |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| NA          | <ul><li><code>btn</code></li><li><code>btn-file-picker</code></li><li><code>btn-secondary</code></li><li><code>BeeButton_*</code></li></ul> | `btn-file-picker--cs` |

#### Link

| Sub-element             | Deprecated                                                                                                  | New Classnames                 |
| ----------------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------ |
| Special links           | <ul><li><code>href-container__link</code></li><li><code>href-container__link--special-link</code></li></ul> | `href-special-link--cs`        |
| Link file               | <ul><li><code>href-container__link</code></li><li><code>href-container__link--link-file</code></li></ul>    | `href-link-file--cs`           |
| Add custom special link | <ul><li><code>href-container__link</code></li><li><code>href-container__link--special-link</code></li></ul> | `href-custom-special-link--cs` |

#### Attributes

| Sub-element       | Deprecated                                                                                                                                                                                       | New Classnames                                        |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- |
| Add new attribute | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul> | <ul><li><code>toggle-menu-button--cs</code></li></ul> |
| Delete            | <ul><li><code>field-remove</code></li></ul>                                                                                                                                                      | <ul><li><code>delete-attribute--cs</code></li></ul>   |

### List

This section lists the List sidebar widgets, sub-elements, and classnames.

#### Write with AI

| Sub-element | Deprecated                                                                   | New Classnames                                     |
| ----------- | ---------------------------------------------------------------------------- | -------------------------------------------------- |
| NA          | <ul><li><code>btn</code></li><li><code>BeeButton_beeButton*</code></li></ul> | <ul><li><code>ai-sidebar-icon--cs</code></li></ul> |

### Menu

This section lists the Menu sidebar widgets, sub-elements, and classnames.

#### Add New Item

<table><thead><tr><th width="193">Sub-element</th><th width="286">Deprecated</th><th>New Classnames</th></tr></thead><tbody><tr><td>NA</td><td><ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul></td><td><ul><li><code>menu-items-add-button--cs</code></li></ul></td></tr></tbody></table>

#### Menu Item

| Sub-element | Deprecated                                                                                               | New Classnames                 |
| ----------- | -------------------------------------------------------------------------------------------------------- | ------------------------------ |
| Delete      | <ul><li><code>BeeButton_*</code></li><li><code>BeeMenuItems_*</code></li></ul>                           | `menu-items-delete-button--cs` |
| Link file   | <ul><li><code>href-container__link</code></li><li><code>href-container__link--link-file</code></li></ul> | `href-link-file--cs`           |

### Paragraph

This section lists the Paragraph sidebar widgets, sub-elements, and classnames.

#### Write with AI

| Sub-element | Deprecated                                                                           | New Classnames                                     |
| ----------- | ------------------------------------------------------------------------------------ | -------------------------------------------------- |
| NA          | <ul><li><code>btn-primary</code></li><li><code>BeeButton_beeButton*</code></li></ul> | <ul><li><code>ai-sidebar-icon--cs</code></li></ul> |

### Social

This section lists the Social sidebar widgets, sub-elements, and classnames.

#### Add New Icon

<table><thead><tr><th width="168">Sub-element</th><th width="302">Deprecated</th><th>New Classnames</th></tr></thead><tbody><tr><td>Button</td><td><ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul></td><td><code>social-add-icon--cs</code></td></tr></tbody></table>

**Social Icon Item**

| Sub-element   | Deprecated                                                                                                        | New Classnames           |
| ------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------------ |
| Delete        | <ul><li><code>icon-remove</code></li></ul>                                                                        | `icon-remove--cs`        |
| Change image  | <ul><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li><li><code>BeeSocialIcons_*</code></li></ul> | `social-change-icon--cs` |
| Apply effects | <ul><li><code>btn-default</code></li><li><code>BeeButton_*</code></li><li><code>BeeSocialIcons_*</code></li></ul> | `social-edit-icon--cs`   |

## Rows

This section lists the classnames for buttons within the row area of the sidebar.

#### Row Background Image

| Sub-element  | Deprecated                                                                                                                                                                   | New Classnames        |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| Choose image | <ul><li><code>btn</code></li><li><code>btn-file-picker</code></li><li><code>btn-secondary</code></li><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `btn-file-picker--cs` |

#### Row Background Video

| Sub-element  | Deprecated                                                                                                                                | New Classnames        |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| Change video | <ul><li><code>btn</code></li><li><code>btn-file-picker</code></li><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `btn-file-picker--cs` |

#### Display Condition

| Sub-element      | Deprecated                                                                                           | New Classnames                             |
| ---------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| Select condition | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `row-display-condition-select-button--cs`  |
| Add condition    | <ul><li><code>btn-default</code></li><li><code>BeeButton_*</code></li></ul>                          | `row-display-condition-add-button--cs`     |
| Edit condition   | <ul><li><code>btn-default</code></li><li><code>BeeButton_*</code></li></ul>                          | `row-display-condition-edit-button--cs`    |
| Open builder     | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `row-display-condition-builder-button--cs` |

#### Column Structure

| Sub-element | Deprecated                                                                             | New Classnames              |
| ----------- | -------------------------------------------------------------------------------------- | --------------------------- |
| Add new     | <ul><li><code>column-manager--add</code></li><li><code>BeeButton_*</code></li></ul>    | `column-manager-add--cs`    |
| Delete      | <ul><li><code>column-manager--delete</code></li><li><code>BeeButton_*</code></li></ul> | `column-manager-delete--cs` |

## Settings

This table lists the classnames for buttons within the settings area of the sidebar.

#### Favicon

| Sub-element | Deprecated                                                                                                                                                                                       | New Classnames                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------- |
| Add favicon | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul> | <ul><li><code>favicon-add-icon--cs</code></li></ul> |

**Favicon item**

| Sub-element    | Deprecated                                                                  | New Classnames       |
| -------------- | --------------------------------------------------------------------------- | -------------------- |
| Change favicon | <ul><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `favicon-change--cs` |
| Delete         | <ul><li><code>BeeButton_*</code></li></ul>                                  | `favicon-delete--cs` |
{% endtab %}

{% tab title="RadioGroup" %}
Radiogroups in the context of our web application refer to a UI component that groups together a set of radio buttons, allowing users to select one option from multiple choices. Each radiogroup is associated with specific classnames that define the appearance and behavior of the grouped buttons within the sidebar's layout. These classnames, such as `radiogroup--cs` and `radiogroup-button--cs`, are crucial for ensuring consistent and functional navigation in your application's user interface.

This section will cover widget classnames for content in the sidebar. This section will list the classnames for the following sidebar tabs:

* [Rows](custom-css.md#rows)
* [Rows & Content](custom-css.md#rows-and-content)
* [Content](custom-css.md#content)
* [Settings](custom-css.md#settings)

### Rows

This section lists the classnames for widgets and content within the row area of the sidebar.

#### Vertical Align

| Content | Deprecated | New Classnames                                                                                                           |
| ------- | ---------- | ------------------------------------------------------------------------------------------------------------------------ |
| NA      | NA         | <ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li></ul> |

#### Row Background Image - Apply Image To

<table><thead><tr><th width="123">Content</th><th width="304">Deprecated</th><th>New Classnames</th></tr></thead><tbody><tr><td>NA</td><td><ul><li><code>tgl-container</code></li><li><code>tgl-container--cs</code> </li><li><code>btn-group</code> </li><li><code>number-selector</code></li><li><code>number-selector--cs</code></li><li><code>tgl_bgd</code></li><li><code>active</code> </li><li><code>btn</code></li><li><code>multiToggle_option_background-toggle-content-area</code></li><li><code>multiToggle_option_background-toggle-row</code></li><li><code>btn-primary</code></li><li><code>tgl-label</code></li></ul></td><td><ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li></ul></td></tr></tbody></table>

### Rows & Content

This section lists the classnames for widgets and content within the Row & Content area of the sidebar.

#### Hide On (Mobile/Desktop) + Confirmation Modal

<table><thead><tr><th width="176">Content</th><th width="230">Deprecated</th><th>New Classnames</th></tr></thead><tbody><tr><td><ul><li>Button</li><li>Carousel</li><li>Divider</li><li>Form</li><li>Heading</li><li>Html</li><li>Icons</li><li>Image</li><li>List</li><li>Menu</li><li>Dynamic</li><li>Content</li><li>Paragraph</li><li>Social</li><li>Spacer</li><li>Text</li><li>Video</li></ul></td><td><ul><li><code>hide-on-mobile__desktop</code></li><li><code>hide-on-mobile__mobile</code></li><li><code>btn-primary</code></li><li><code>hideOn-confirm-modal-icon--cs</code></li></ul></td><td><ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li><li><code>confirm-modal-icon--cs</code></li></ul></td></tr></tbody></table>

### Content

This section lists the classnames for widgets and content within the Content area of the sidebar.

#### Hide on (amp/html)

| Content                                                                                                                                                                                                                                | Deprecated                                                                                                      | New Classnames                                                                                                           |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| <ul><li>Button</li><li>Divider</li><li>Form</li><li>Heading</li><li>Html</li><li>Icons</li><li>Image</li><li>List</li><li>Dynamic</li><li>Content</li><li>Paragraph</li><li>Social</li><li>Spacer</li><li>Text</li><li>Video</li></ul> | <ul><li><code>hide-on-amp__amp</code></li><li><code>hide-on-amp__html</code></li><li><code>btn</code></li></ul> | <ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li></ul> |

#### Align

| Content                                                                                                                                                                                                | Deprecated                                                                                                                                                                                                                                                                                                                                             | New Classnames                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| <ul><li>Button</li><li>Form</li><li>Form Label Options</li><li>Form Button Options</li><li>Heading</li><li>Icons</li><li>Image</li><li>Menu</li><li>Paragraph</li><li>Social</li><li>Divider</li></ul> | <ul><li><code>item_1-2</code></li><li><code>widget__label</code></li><li><code>btn</code></li><li><code>btn-default</code></li><li><code>align-left</code></li><li><code>active</code></li><li><code>btn-align-left</code></li><li><code>btn-align-right</code></li><li><code>btn-align-center</code></li><li><code>btn-align-justify</code></li></ul> | <ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li></ul> |

#### Line Height

| Content                                                                                                         | Deprecated                                                                                                                                                                                                                                                                     | New Classnames                                                                                                           |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| <ul><li>Button</li><li>Form Label Options</li><li>Heading</li><li>Paragraph</li><li>List</li><li>Text</li></ul> | <ul><li><code>item_1-2</code></li><li><code>widget__label</code></li><li><code>active</code></li><li><code>btn-line-height--120</code></li><li><code>btn-line-height--150</code></li><li><code>btn-line-height--180</code></li><li><code>btn-line-height--200</code></li></ul> | <ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li></ul> |

#### List Type

| Content | Deprecated                                                                                                                                                                                                    | New Classnames                                                                                                           |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| List    | <ul><li><code>icon-toggle</code></li><li><code>icon-toggle--cs</code></li><li><code>icon-toggle-item</code></li><li><code>icon-toggle-item--cs</code></li><li><code>icon-toggle-item--active</code></li></ul> | <ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li></ul> |

#### Label Position

| Content            | Deprecated                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | New Classnames                                                                                                           |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Form Label Options | <ul><li><code>tgl-container</code></li><li><code>tgl-container--cs</code></li><li><code>item_1-2</code></li><li><code>widget__label</code></li><li><code>btn-group</code></li><li><code>number-selector</code></li><li><code>number-selector--cs</code></li><li><code>tgl_bgd</code></li><li><code>active</code></li><li><code>btn</code></li><li><code>multiToggle_option_descriptor_form_style_labels_label-position_0</code></li><li><code>multiToggle_option_descriptor_form_style_labels_label-position_1</code></li><li><code>btn-primary</code></li><li><code>static-label</code></li><li><code>tgl-label</code></li></ul> | <ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li></ul> |

#### Text Directon

| Content                                                                 | Deprecated                                                                                | New Classnames                                                                                                           |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| <ul><li>Button</li><li>Heading</li><li>List</li><li>Paragraph</li></ul> | <ul><li><code>paragraph-item</code></li><li><code>paragraph-item--active</code></li></ul> | <ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li></ul> |

#### Select the Content to Use

<table><thead><tr><th>Content</th><th width="232">Deprecated</th><th>New Classnames</th></tr></thead><tbody><tr><td>Dynamic Content</td><td><ul><li><code>item_1-2</code></li><li><code>widget__label</code></li><li><code>radio-button</code></li><li><code>radio-button__radio</code></li></ul></td><td><ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li></ul></td></tr></tbody></table>

### Settings

This section lists the classnames for widgets and content within the Settings area of the sidebar.

Content Area Alight

| Content | Deprecated                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | New Classnames                                                                                                                  |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| NA      | <ul><li><code>tgl-container</code></li><li><code>tgl-container--cs</code></li><li><code>item_1-2</code></li><li><code>widget__label</code></li><li><code>btn-group</code></li><li><code>number-selector</code></li><li><code>number-selector--cs</code></li><li><code>tgl_bgd</code></li><li><code>active</code></li><li><code>btn</code></li><li><code>multiToggle_option_content_computedStyle_align_0</code></li><li><code>multiToggle_option_content_computedStyle_align_1</code></li><li><code>btn-primary static-label</code></li><li><code>tgl-label</code></li></ul> | <p></p><ul><li><code>radiogroup--cs</code></li><li><code>radiogroup-button--cs</code></li><li><code>active--cs</code></li></ul> |
{% endtab %}

{% tab title="Columns" %}
This section covers classnames for the column structure widget.

| Sidebar Tab | Deprecated Classnames | New Classnames                                                                                                                                                                            |
| ----------- | --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Rows        | `PanelGroup_handle*`  | <ul><li><code>panel-group-dragging--cs</code></li><li><code>column-manager-delete--cs</code></li><li><code>column-manager-add--cs</code></li><li><code>panel-divider--cs</code></li></ul> |
{% endtab %}

{% tab title="Font Style" %}
This section covers widget classnames for content in the sidebar, and lists the classnames for the following widgets:

* Font Style
* Configure Icon Collection

#### Font Style

| Content       | Deprecated                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | New Classnames                                                                                                                         |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Form - Label  | <ul><li><code>tgl-container</code></li><li><code>tgl-container--cs</code></li><li><code>item_1-2</code></li><li><code>widget__label</code></li><li><code>btn-group</code></li><li><code>number-selector</code></li><li><code>number-selector--cs</code></li><li><code>tgl_bgd</code></li><li><code>multiToggle_option_descriptor_form_style_labels_font-weight_0</code></li><li><code>multiToggle_option_descriptor_form_style_labels_font-weight_1</code></li><li><code>button-default--cs</code></li><li><code>button-medium--cs</code></li><li><code>button--cs"</code></li><li><code>active</code></li></ul> | <ul><li><code>multi-toggle--cs</code></li><li><code>multi-toggle-btns--cs</code></li><li><code>toggle-btn-pressed--cs</code></li></ul> |
| Form - Button | <ul><li><code>title_icon</code></li><li><code>icon-organizer__panel</code></li><li><code>panel__icon-preview-wrapper</code></li><li><code>panel__title</code></li><li><code>comp-tree-placeholder</code></li></ul>                                                                                                                                                                                                                                                                                                                                                                                               | <ul><li><code>multi-toggle--cs</code></li><li><code>multi-toggle-btns--cs</code></li><li><code>toggle-btn-pressed--cs</code></li></ul> |

#### Configure Icon Collection

| Content | Deprecated                                                                                                                                                                                                                                                                          | New Classnames                                                                                        |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Social  | <ul><li><code>item_1-2</code></li><li><code>widget__label</code></li><li><code>title_icon</code></li><li><code>icon-organizer__panel</code></li><li><code>panel__icon-preview-wrapper</code></li><li><code>panel__title</code></li><li><code>comp-tree-placeholder</code></li></ul> | <ul><li><code>social-collection-list--cs</code></li><li><code>panel__title--cs</code></li></ul>       |
| Icons   | <ul><li><code>item_1-2</code></li><li><code>widget__label</code></li><li><code>icon-organizer__panel</code></li><li><code>panel__icon-preview-wrapper</code></li><li><code>panel__title</code></li><li><code>comp-tree-placeholder</code></li></ul>                                 | <p></p><ul><li><code>icons-collection-list--cs</code></li><li><code>panel__title--cs</code></li></ul> |
{% endtab %}

{% tab title="Input Text" %}
This section discusses and lists the various CSS classnames relevant to the application's sidebar widgets where textual input is required. These classnames facilitate the styling and functional integration of widgets such as URLs, images, alt texts, and more, providing a comprehensive guide for developers to enhance the user interface effectively.

This section will cover button classnames for the following sidebar areas:

* [Content](custom-css.md#content)
* [Rows](custom-css.md#rows)
* [Settings](custom-css.md#settings)

## Content

This section lists the classnames for widgets within the Content tab.

### Image

| Widget | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                          |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| URL    | <ul><li><code>number-selector--cs</code></li><li><code>input-image-url</code></li><li><code>item_1-2</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Image, GIF, and Sticker

| Widget                      | Deprecated                                                                                                                                                                                                                                                                                           | New Classnames                                                                                                                                              |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Alt Text                    | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul>                                                                        | <ul><li><code>input-text--cs</code> </li><li><code>input-text-boxed--cs</code></li></ul>                                                                    |
| Dynamic Image > Dynamic URL | <p></p><ul><li><code>number-selector--cs</code></li></ul><ul><li><code>alternate-text--cs</code></li></ul><ul><li><code>item_1-2</code></li></ul><ul><li><code>widget__textbox</code></li></ul><ul><li><code>widget__label</code></li></ul><ul><li><code>widget__label--textbox btn</code></li></ul> | <p></p><ul><li><code>input-text--cs input</code></li></ul><ul><li><code>text-boxed--cs</code></li></ul><ul><li><code>dynamic-image-url--cs</code></li></ul> |

### Image, Button, Icons, Menu, GIF, and Sticker

| Widget               | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                                 |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Web page > URL       | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul>        |
| Send email > Mail to | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Send email > Subject | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Send email > Body    | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Tel > Tel            | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Send SMS> Tel        | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Send SMS > Message   | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Image, Button, GIF, Sticker, and Video

| Widget     | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                                 |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Attributes | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Video

| Widget | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                                 |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| URL    | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Title  | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Social

| Widget          | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                                 |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Item > Title    | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Item > Alt text | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Item > URL      | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Icons

| Widget           | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                                 |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Item > Image URL | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Item > Alt text  | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Item > Icon Text | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Item > Title     | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Form

| Widget      | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                                 |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Field label | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### All Modules

| Widget           | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                                 |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Block identifier | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

## Rows

This section lists the classnames for widgets within the Rows tab.

| Widget               | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                                 |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Row background image | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Row background video | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

## Settings

This section lists the classnames for widgets within the Settings tab.

| Widget               | Deprecated                                                                                                                                                                                                                                                           | New Classnames                                                                                                                                    |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| Row background image | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul>                                        | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul>                                                    |
| Title                | <ul><li><code>number-selector--cs</code></li><li><code>alternate-txt--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li><li><code>page-metadata-title--cs</code></li></ul>       |
| Description          | <ul><li><code>number-selector--cs</code></li><li><code>alternate-txt--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li><li><code>page-metadata-description--cs</code></li></ul> |
| Subject              | <ul><li><code>number-selector--cs</code></li><li><code>alternate-text--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textboxbtn</code></li></ul>                      | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li><li><code>page-metadata-subject--cs</code></li></ul>     |
| Preheader            | <ul><li><code>number-selector--cs</code></li><li><code>alternate-txt-cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul>  | <p></p><ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li><li><code>page-metadata-preheader-cs</code></li></ul>    |
{% endtab %}

{% tab title="Slider" %}
The various classnames and `data-qa` attributes associated with entities within the application that feature sliders. These identifiers are crucial for styling and testing purposes, tailored to different areas like Add-On, Button, Form, and Image entities where sliders are a key component.

This section will cover button classnames for the following sidebar areas:

* [Content](custom-css.md#content)
* [Settings](custom-css.md#settings)

## Content

This section lists the classnames for sliders within the Content tab.

<table><thead><tr><th width="89">Entity</th><th width="72">Sidebar Widget</th><th>Deprecated</th><th>New Classnames</th><th>Data-QA</th><th>Notes</th></tr></thead><tbody><tr><td>Add-On (Image)</td><td><ul><li>Width</li></ul></td><td><ul><li><code>BeeImageWidth_*</code></li><li><code>BeeWidthSlider_*</code></li><li><code>rc-slider*</code></li></ul></td><td><ul><li><code>slider--cs</code></li><li><code>slider-wrapper--cs</code></li></ul></td><td><ul><li><code>slider-btn</code></li></ul></td><td>data-qa was moved from a div to the actual input element</td></tr><tr><td>Button</td><td><ul><li>Width</li></ul></td><td><ul><li><code>BeeImageWidth_*</code></li><li><code>BeeWidthSlider_*</code></li><li><code>rc-slider*</code></li></ul></td><td><ul><li><code>slider--cs</code></li><li><code>slider-wrapper--cs</code></li></ul></td><td><ul><li><code>slider-btn</code></li></ul></td><td>data-qa was moved from a div to the actual input element</td></tr><tr><td>Form</td><td><ul><li>Width</li><li>Button Width</li></ul></td><td><ul><li><code>BeeWidthSlider_*</code></li><li><code>rc-slider*</code></li><li><code>widget-BeeImageWidth</code></li></ul></td><td><ul><li><code>slider--cs</code></li><li><code>slider-wrapper--cs</code></li></ul></td><td><ul><li><code>slider-btn</code></li></ul></td><td>data-qa was moved from a div to the actual input element</td></tr><tr><td>Image</td><td><ul><li>Width</li></ul></td><td><ul><li><code>BeeImageWidth_*</code></li><li><code>BeeWidthSlider_*</code></li><li><code>rc-slider*</code></li></ul></td><td><ul><li><code>slider--cs</code></li><li><code>slider-wrapper--cs</code></li></ul></td><td><ul><li><code>slider-btn</code></li></ul></td><td>data-qa was moved from a div to the actual input element</td></tr></tbody></table>

## Settings

This section lists the classnames for sliders within the Settings tab.

| Entity             | Deprecated                                                                      | New Classnames                                                                    | Data-QA                                   | Notes                                                    |
| ------------------ | ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | ----------------------------------------- | -------------------------------------------------------- |
| Content Area Width | <ul><li><code>BeeWidthSlider_*</code></li><li><code>rc-slider*</code></li></ul> | <ul><li><code>slider--cs</code></li><li><code>slider-wrapper--cs</code></li></ul> | <ul><li><code>slider-btn</code></li></ul> | data-qa was moved from a div to the actual input element |
{% endtab %}
{% endtabs %}
