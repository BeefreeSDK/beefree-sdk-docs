---
description: >-
  A classnames change log where you can reference current and past changes to
  CSS classes.
---

# Change Log

## Release Scheduled for March 2025

This section includes a reference of the new classnames scheduled for release in March 2025. The new classnames will be related to [Mobile Badge](change-log.md#mobile-badge-or-scheduled-for-march-2025) and [Confirmation Dialogs](change-log.md#confirmation-dialogs-or-scheduled-for-march-2025). For more details, click the **>** symbol to expand the expandable content sections containing additional information.&#x20;

### Mobile Badge | Scheduled for March 2025

This section includes a reference for new classnames related to Mobile Badge.

#### Content

Reference the classname changes related to Content for Mobile Badge in the following expandable section.

<details>

<summary>Mobile Badge Content </summary>

This section shows the classname updates for the Mobile Badge Content. The following Markup variations apply to each of the **Content types** outlined in this section.

* Converted the badge into a button
* Removed a `<span>`
* Moved it out of the widget's label tag

#### <mark style="background-color:purple;">Button</mark>

**Affected Sub-element:** Width Slider

**Classnames Removed:** Not applicable

**Classnames Added**

* `widget-mobile-badge-enabled--cs`

#### <mark style="background-color:purple;">Carousel, Text, Video</mark>

**Affected Sub-element:** Block options - Padding

**Classnames Removed:** Not applicable

**Classnames Added**

* `widget-mobile-badge-enabled--cs`

#### <mark style="background-color:purple;">Divider, Image, Social</mark>

**Affected Sub-element:** Align, Block options - Padding

**Classnames Removed:** Not applicable

**Classnames Adde**

* `widget-mobile-badge-enabled--cs`

#### <mark style="background-color:purple;">Form</mark>

**Affected Sub-element:** Font size, Block options - Padding

**CClassnames Removed:** Not applicable

**Classnames Added**

* `widget-mobile-badge-enabled--cs`

#### <mark style="background-color:purple;">Button, Title, Icons, Image, List, Menu, Paragraph</mark>

**Affected Sub-element:** Font size, Align, Block options - Padding

**Classnames Removed:** Not applicable

**Classnames Added**

* `widget-mobile-badge-enabled--cs`

#### <mark style="background-color:purple;">Spacer</mark>

**Affected Sub-element:** Height

**Classnames Removed:** Not applicable

**Classnames Added**

* `widget-mobile-badge-enabled--cs`

</details>

#### Rows

Reference the classname changes related to Rows for Mobile Badge in the following expandable section.

<details>

<summary>Mobile Badge Row</summary>

The following sections show the classname updates for the Mobile Badge Row.

**Affected Sub-element:** Columns Structure - Padding

**Markup Variations**

The following Markup variations apply for Mobile badge row.&#x20;

* Converted the badge into a button
* Removed a `<span>`

**Classnames Removed:** Not applicable

**Classnames Added**

* `widget-mobile-badge-enabled--cs`

</details>

### Confirmation Dialogs | Scheduled for March 2025

This section includes a reference for new classnames related to Confirmation Dialogs.

#### Rows

Reference the classname changes related to Rows for Confirmation Dialogs in the following expandable section.

<details>

<summary>Delete Row Confirmation Dialog</summary>

**Affected Sub-element:** Delete Row Confirmation Dialog

**Markup Variations:**

* Removed SVG icon

**Classnames Added**

* `confirmation-title--cs`

</details>

Reference the corresponding [Custom Translations for Delete Row](../../advanced-options/custom-languages.md#sample-language-file-4). &#x20;

#### Column

Reference the classname changes related to Columns for Confirmation Dialogs in the following expandable section.

<details>

<summary>Delete Column Confirmation Dialog</summary>

**Affected Sub-element:** Delete Column Confirmation Dialog

**Markup Variations:**

* Removed SVG icon

**Classnames Added**

* `confirmation-title--cs`

</details>

Reference the corresponding [Custom Translations for Delete Column](../../advanced-options/custom-languages.md#sample-language-file-5).

#### Module

Reference the classname changes related to Modules for Confirmation Dialogs in the following expandable section.

<details>

<summary>Delete Module Confirmation Dialog</summary>

**Affected Sub-element:** Delete Module Confirmation Dialog

**Markup Variations:**

* Removed SVG icon

**Classnames Added**

* `confirmation-title--cs`

</details>

Reference the corresponding [Custom Translations for Delete Module](../../advanced-options/custom-languages.md#sample-language-file-6).

#### Rows

Reference the classname changes related to Rows for Confirmation Dialogs in the following expandable section.

<details>

<summary>Hide Row on Mobile with Module Already Hidden on Desktop</summary>

**Affected Sub-element:** Hide Row Confirmation Dialog

**Markup Variations:**

* Removed SVG icon

**Classnames Added**

* `confirmation-title--cs`

</details>

Reference the corresponding [Custom Translations for Hide Row on Mobile with Module Already Hidden on Desktop](../../advanced-options/custom-languages.md#hide-row-on-mobile-with-module-already-hidden-on-desktop).

#### Rows

Reference the classname changes related to Rows for Confirmation Dialogs in the following expandable section.

<details>

<summary>Remove Custom Display Condition</summary>

**Affected Sub-element:** Remove Custom Display Condition Confirmation Dialog

**Classnames Added**

* `confirmation-title--cs`

</details>

Reference the corresponding [Custom Translations for Remove Custom Display Condition](../../advanced-options/custom-languages.md#sample-language-file-7).

#### File manager

Reference the classname changes related to File Manager for Confirmation Dialogs in the following expandable section.

<details>

<summary>Confirm Delete Single File</summary>

**Affected Sub-element:** File Manager - Confirm Delete Single File

**Classnames Added**

* `confirmation-title--cs`

</details>

Reference the corresponding [Custom Translations for Confirm Delete Single File](../../advanced-options/custom-languages.md#sample-language-file-8).

#### File manager

Reference the classnames added in the following expandable section.

<details>

<summary>Confirm Delete Multiple Files</summary>

**Affected Sub-element:** File Manager - Confirm Delete Multiple Files

**Classnames Addded**

* `confirmation-title--cs`

</details>

Reference the corresponding [Custom Translations for Confirm Delete Multiple Files](../../advanced-options/custom-languages.md#confirm-delete-multiple-files).

#### File manager

Reference the classnames added in the following expandable section.

<details>

<summary>Confirm Upload Existing File</summary>

**Affected Sub-element:** File Manager - Confirm Upload Existing File (Custom FSP and ConfirmOverwriteModalEnabled)

**Classnames Added**

* `confirmation-title--cs`

</details>

Reference the corresponding [Custom Translations for Confirm Upload Existing File](../../advanced-options/custom-languages.md#sample-language-file-9).

## January 30, 2025 Releases

### Display Conditions Widget and Modal | Release on January 30, 2025

#### Display Conditions Widget

<details>

<summary>New Classnames Display Conditions Widget</summary>

### Display Condition Widget

*   **Display Conditions Widget**\
    Affected Sub-element: Display Conditions Widgets

    **Changes:**

    * Markup Variations:
      * `contentDialog` button is now "secondary", not "primary".

    **Classnames Comparison:**

    | Classnames Removed | Classnames Added                        |
    | ------------------ | --------------------------------------- |
    | `item_1-2`         | `display-condition-card--cs`            |
    | `panel__actions`   | `display-condition-card_custom--cs`     |
    |                    | `display-condition-label--cs`           |
    |                    | `display-condition-description--cs`     |
    |                    | `display-condition-label_before--cs`    |
    |                    | `display-condition-before--cs`          |
    |                    | `display-condition-label_after--cs`     |
    |                    | `display-condition-after--cs`           |
    |                    | `display-condition-buttons--cs`         |
    |                    | `row-display-condition-edit-button--cs` |

</details>

#### Select Display Condition Modal

<details>

<summary>New Classnames Select Display Condition Modal</summary>

### Select Display Condition Modal

*   **Select Display Condition Modal**\
    Affected Sub-element: Select Display Condition Modal&#x20;



    **Classnames Comparison:**

    | Classnames Removed  | Classnames Added                  |
    | ------------------- | --------------------------------- |
    | `category-selected` | `selectable-modal-search--cs`     |
    | `back-action`       | `selectable-modal-breadcrumb--cs` |
    |                     | `selectable-modal-items-list--cs` |

</details>

## December 5, 2024 Releases

### Add New Social and Form | Released on December 5th

#### Form&#x20;

<details>

<summary>New Classnames Form </summary>

### Form

*   **Form**\
    Affected Sub-element: Manage fields - Add new field

    **Changes:**

    * Markup Variations:
      * Removed some wrapper divs
      * Replaced all the list HTML

    **Classnames Comparison:**

    | Classnames Removed       | Classnames Added               |
    | ------------------------ | ------------------------------ |
    | `toggle-menu-button--cs` | `button-small--cs`             |
    | `button-large--cs`       | `button-solid--cs`             |
    | `widget__textbox`        | `button-primary--cs`           |
    | `widget__searchbox`      | `button--cs`                   |
    | `scrollable__panel--cs`  | `add-form-field--cs`           |
    |                          | `dropdown-menu--cs`            |
    |                          | `dropdown-menu-button--cs`     |
    |                          | `dropdown-menu-search--cs`     |
    |                          | `input-search--cs`             |
    |                          | `dropdown-menu-scrollable--cs` |
    |                          | `dropdown-menu-item--cs`       |

</details>

#### Social&#x20;

<details>

<summary>New Classnames Social </summary>

### Social

*   **Social**\
    Affected Sub-element: Configure icon collection - Add social icon

    **Changes:**

    * Markup Variations:
      * Removed some wrapper divs
      * Replaced all the popover HTML

    **Classnames Comparison:**

    | Classnames Removed          | Classnames Added               |
    | --------------------------- | ------------------------------ |
    | `icons-manager__pop--cs`    | `button-small--cs`             |
    | `icons-manager__popcontent` | `button-solid--cs`             |
    | `popver__tab`               | `button-primary--cs`           |
    | `social-add-icon--cs`       | `button--cs`                   |
    |                             | `add-social-icon--cs`          |
    |                             | `dropdown-menu--cs`            |
    |                             | `dropdown-menu-button--cs`     |
    |                             | `dropdown-menu-search--cs`     |
    |                             | `input-search--cs`             |
    |                             | `dropdown-menu-scrollable--cs` |
    |                             | `dropdown-menu-item--cs`       |

</details>

### Add New Attributes and Title Bar | Release on December 5th&#x20;

#### 1. Button, Image, Video&#x20;

<details>

<summary>New Classnames Button, Image, Video </summary>

*   **Button, Image, Video**\
    Affected Sub-element: Configure attributes - Add new attribute

    **Changes:**

    * Markup Variations:
      * Removed some wrapper divs
      * Replaced all the list HTML

    **Classnames Comparison:**

    | Classnames Removed       | Classnames Added               |
    | ------------------------ | ------------------------------ |
    | `toggle-menu-button--cs` | `button-small--cs`             |
    | `button-large--cs`       | `button-solid--cs`             |
    | `scrollable__panel--cs`  | `button-primary--cs`           |
    |                          | `button--cs`                   |
    |                          | `add-attribute--cs`            |
    |                          | `dropdown-menu--cs`            |
    |                          | `dropdown-menu-button--cs`     |
    |                          | `dropdown-menu-search--cs`     |
    |                          | `input-search--cs`             |
    |                          | `dropdown-menu-scrollable--cs` |
    |                          | `dropdown-menu-item--cs`       |

</details>

#### 2. Sidebar Title

<details>

<summary>New Classnames All</summary>

### Sidebar Title

*   Sidebar Title\
    Affected Sub-element: Sidebar Title

    **Changes:**

    * Markup Variations:
      * Added `<div role="toolbar">`
      * `<a>` elements are now `<button>`

    **Classnames Comparison:**

    | Classnames Removed         | Classnames Added                             |
    | -------------------------- | -------------------------------------------- |
    | `widgets-section__heading` | `widgets-section__heading--cs`               |
    | `icon`                     | `sidebar-panel-title-icon--cs`               |
    | `icon-*`                   | `sidebar-panel-title-icon-comment--cs`       |
    |                            | `sidebar-panel-title-icon-delete--cs`        |
    |                            | `sidebar-panel-title-icon-duplicate--cs`     |
    |                            | `sidebar-panel-title-icon-closepanel--cs`    |
    |                            | `sidebar-panel-title-icon-save--cs`          |
    |                            | `sidebar-panel-title-icon-editSyncedRow--cs` |

</details>

#### 3. Rows

<details>

<summary>New Classnames Rows </summary>

**Rows**\
Affected Sub-element: Sidebar Title

**Changes:**

Markup Variations:

* Added `<div role="toolbar">`
* `<a>` elements are now `<button>`

**Classnames Comparison:**

* **Classnames Removed:**
  * `widgets-section__heading`
  * `icon`
  * `icon-*`
* **Classnames Added:**
  * `widgets-section__heading--cs`
  * `sidebar-panel-title-icon--cs`
  * `sidebar-panel-title-icon-comment--cs`
  * `sidebar-panel-title-icon-delete--cs`
  * `sidebar-panel-title-icon-duplicate--cs`
  * `sidebar-panel-title-icon-closepanel--cs`
  * `sidebar-panel-title-icon-save--cs`
  * `sidebar-panel-title-icon-editSyncedRow--cs`

</details>

## November 7, 2024 Releases

### Mobile Stage Mode, History, and Empty States | Released on November 7th

<details>

<summary>Mobile Stage Mode, History, and Empty States </summary>

### Mobile Stage Mode, History, and Empty States

*   **Mobile Stage Mode**\
    Affected Sub-element: Wrapper

    **Classnames Added:**

    * `stagemode__buttonswrapper--cs`

    **Mobile Stage Mode Buttons:**

    * Desktop button: `stagemode__button__desktop--cs`
    * Mobile button: `stagemode__button__mobile--cs`
    * Display toggle button: `stagemode__button__display--cs`
*   **Undo/Redo**\
    Affected Sub-elements: Undo/Redo Buttons and History Panel

    **Classnames Added:**

    * Toggle button: `undo-redo__toggleButton--cs`
    * Undo button: `undo-redo__undoButton--cs`
    * Redo button: `undo-redo__redoButton--cs`
    * History panel: `undo-redo__history--cs`
    * History panel item: `history__step--cs`
*   **Empty States (Various Modules)**\
    Affected Modules: Image, Icons, Video, Menu, Social, Form, AddOn, Dynamic Content

    **Classnames Added:**

    * Image module: `stage-module_image_placeholder--cs`
    * Icons module: `stage-module_icons_placeholder--cs`
    * Video module: `stage-module_video_placeholder--cs`
    * Menu module: `stage-module_menu_placeholder--cs`
    * Social module: `stage-module_social_placeholder--cs`
    * Form module: `stage-module_form_placeholder--cs`
    * AddOn module: stage`-module_addon_placeholder--cs`
    * DynamicContent module: `stage-module_merge-content_placeholder--cs`

</details>

### Changes Font Stye and Drag-and-Drop Widgets | Released on November 7th&#x20;

#### **1. Form Components**

<details>

<summary>New Classnames for Form Components </summary>

### Form Components

* **Affected Widgets**: Font style
*   **Changes**:

    * **Markup Variations**: Removed some wrapper `div` and `span` elements.
    * **Classnames Comparison**:

    | Classnames Removed                                              | Classnames Added         |
    | --------------------------------------------------------------- | ------------------------ |
    | `tgl-container`                                                 | `multi-toggle--cs`       |
    | `tgl-container--cs`                                             | `multi-toggle-btns--cs`  |
    | `item_1-2`                                                      | `toggle-btn-pressed--cs` |
    | `widget__label`                                                 |                          |
    | `btn-group`                                                     |                          |
    | `number-selector`                                               |                          |
    | `number-selector--cs`                                           |                          |
    | `tgl_bgd`                                                       |                          |
    | `multiToggle_option_descriptor_form_style_labels_font-weight_0` |                          |
    | `multiToggle_option_descriptor_form_style_labels_font-weight_1` |                          |
    | `button-default--cs`                                            |                          |
    | `button-medium--cs`                                             |                          |
    | `button--cs`                                                    |                          |
    | `active`                                                        |                          |

</details>

#### **2. Social Widget**

<details>

<summary>New Classnames for Social Widget </summary>

### Social Widget

* **Affected Widget**: Configure Icon Collection
*   **Changes**:

    * **Markup Variations**:
      * Removed wrapper `div`.
      * Replaced the drag handle `div` with a `button`.
    * **Classnames Comparison**:

    | Classnames Removed            | Classnames Added             |
    | ----------------------------- | ---------------------------- |
    | `item_1-2`                    | `social-collection-list--cs` |
    | `widget__label`               | `panel__title--cs`           |
    | `icons-manager__pop`          |                              |
    | `title_icon`                  |                              |
    | `icon-organizer__panel`       |                              |
    | `panel__icon-preview-wrapper` |                              |
    | `panel__title`                |                              |
    | `comp-tree-placeholder`       |                              |

</details>

#### **3. Icons Widget**

<details>

<summary>New Classnames for Icons Widget </summary>

### Icons Widget

* **Affected Widget**: Configure Icon Collection
*   **Changes**:

    * **Markup Variations**:
      * Removed wrapper `div`.
      * Replaced the drag handle `div` with a `button`.
    * **Classnames Comparison**:

    | Classnames Removed            | Classnames Added            |
    | ----------------------------- | --------------------------- |
    | `item_1-2`                    | `icons-collection-list--cs` |
    | `widget__label`               | `panel__title--cs`          |
    | `icon-organizer__panel`       |                             |
    | `panel__icon-preview-wrapper` |                             |
    | `panel__title`                |                             |
    | `comp-tree-placeholder`       |                             |

</details>

#### **4. Menu Widget**

<details>

<summary>New Classnames for Menu Widget </summary>

### Menu Widget

* **Affected Widget**: Configure Menu Items
*   **Changes**:

    * **Markup Variations**:
      * Removed wrapper `div`.
      * Replaced the drag handle `div` with a `button`.
    * **Classnames Comparison**:

    | Classnames Removed            | Classnames Added            |
    | ----------------------------- | --------------------------- |
    | `item_1-2`                    | `items-collection-list--cs` |
    | `widget__label`               | `item-organizer__panel--cs` |
    | `icon-organizer__panel`       | `panel__title--cs`          |
    | `icon-organizer__panel--cs`   |                             |
    | `panel__icon-preview-wrapper` |                             |
    | `panel__title`                |                             |
    | `title__icon`                 |                             |
    | `comp-tree-placeholder`       |                             |

</details>

#### **5. Form Widget**

<details>

<summary>New Classnames for Form Widget</summary>

### Form Widget

* **Affected Widget**: Manage Fields
*   **Changes**:

    * **Markup Variations**:
      * Removed wrapper `div` and `span` elements.
      * Replaced the drag handle `div` with a `button`.
    * **Classnames Comparison**:

    | Classnames Removed            | Classnames Added         |
    | ----------------------------- | ------------------------ |
    | `item_1-2`                    | `form-items-list--cs`    |
    | `widget__label`               | `form-item__panel--cs`   |
    | `icon-organizer__panel`       | `form-field-item-id--cs` |
    | `icon-organizer__panel--cs`   |                          |
    | `panel__icon-preview-wrapper` |                          |
    | `panel__title`                |                          |
    | `title__icon`                 |                          |
    | `comp-tree-placeholder`       |                          |

</details>

#### **6. Carousel Widget**

<details>

<summary>New Classnames for Carousel Widget </summary>

### Carousel Widget

* **Affected Widget**: Configure Carousel
*   **Changes**:

    * **Markup Variations**:
      * Removed wrapper `div` and `span` elements.
      * Added a `label` tag.
      * Replaced `div` elements with `ul` and `li` for better semantic structure.
      * Replaced the drag handle `div` with a `button`.
    * **Classnames Comparison**:

    | Classnames Removed           | Classnames Added             |
    | ---------------------------- | ---------------------------- |
    | `icon-manager__add-icon--cs` | `widget__label--cs`          |
    | `icon-organizer__panel--cs`  | `carousel-slides-list--cs`   |
    | `comp-tree-placeholder`      | `carousel-add-slide-btn--cs` |
    |                              | `slide-organizer__panel--cs` |

</details>

## October 10, 2024 Releases

### Form Edit Modal | Released on October 10th

#### **1. Form Edit Modal - Text Inputs**

<details>

<summary>List of New Classnames for the Form Edit Modal Text Inputs</summary>

### Form Edit Modal - Text Inputs

* **Affected Sub-element**: All text inputs
*   **Changes**:

    * **Markup Variations**:
      * Updated to the new input text component.
      * The label is now positioned on top instead of to the left.
    * **Classnames Comparison**:

    | Classnames Removed       | Classnames Added       |
    | ------------------------ | ---------------------- |
    | `number-selector--cs`    | `input-text--cs`       |
    | `item_1-2`               | `input-text-boxed--cs` |
    | `widget__textbox`        |                        |
    | `widget__label`          |                        |
    | `widget__label--textbox` |                        |
    | `btn`                    |                        |

</details>

#### **2. Form Edit Modal - Required and Read Only Toggles**

<details>

<summary>List of New Classnames for the Form Edit Modal Required and Read Only Toggles  </summary>

### **Form Edit Modal - Required and Read Only Toggles**

* **Affected Sub-element**: Required and Read Only Toggles
*   **Changes**:

    * **Markup Variations**:
      * Changed from toggles to checkboxes for Required and Read Only fields.
    * **Classnames Comparison**:

    | Classnames Removed   | Classnames Added       |
    | -------------------- | ---------------------- |
    | `toggle-wrapper--cs` | `checkbox-wrapper--cs` |
    | `toggle-input--cs`   | `widget__label--cs`    |
    | `toggle-slider--cs`  |                        |

</details>
