---
description: >-
  A classnames change log where you can reference current and past changes to
  CSS classes.
---

# Change Log

## Add New Social and Form | Release Coming Soon

1.  **Form**\
    Affected Sub-element: Manage fields - Add new field

    **Changes:**

    * Markup Variations:
      * Removed some wrapper divs
      * Replaced all the list HTML

    **Classnames Comparison:**

    | Classnames Removed      | Classnames Added             |
    | ----------------------- | ---------------------------- |
    | toggle-menu-button--cs  | button-small--cs             |
    | button-large--cs        | button-solid--cs             |
    | widget\_\_textbox       | button-primary--cs           |
    | widget\_\_searchbox     | button--cs                   |
    | scrollable\_\_panel--cs | add-form-field--cs           |
    |                         | dropdown-menu--cs            |
    |                         | dropdown-menu-button--cs     |
    |                         | dropdown-menu-search--cs     |
    |                         | input-search--cs             |
    |                         | dropdown-menu-scrollable--cs |
    |                         | dropdown-menu-item--cs       |
2.  **Social**\
    Affected Sub-element: Configure icon collection - Add social icon

    **Changes:**

    * Markup Variations:
      * Removed some wrapper divs
      * Replaced all the popover HTML

    **Classnames Comparison:**

    | Classnames Removed          | Classnames Added             |
    | --------------------------- | ---------------------------- |
    | icons-manager\_\_pop--cs    | button-small--cs             |
    | icons-manager\_\_popcontent | button-solid--cs             |
    | popver\_\_tab               | button-primary--cs           |
    | social-add-icon--cs         | button--cs                   |
    |                             | add-social-icon--cs          |
    |                             | dropdown-menu--cs            |
    |                             | dropdown-menu-button--cs     |
    |                             | dropdown-menu-search--cs     |
    |                             | input-search--cs             |
    |                             | dropdown-menu-scrollable--cs |
    |                             | dropdown-menu-item--cs       |

***

## Add New Attributes and Title Bar | Release Coming Soon

1.  **Button, Image, Video**\
    Affected Sub-element: Configure attributes - Add new attribute

    **Changes:**

    * Markup Variations:
      * Removed some wrapper divs
      * Replaced all the list HTML

    **Classnames Comparison:**

    | Classnames Removed      | Classnames Added             |
    | ----------------------- | ---------------------------- |
    | toggle-menu-button--cs  | button-small--cs             |
    | button-large--cs        | button-solid--cs             |
    | scrollable\_\_panel--cs | button-primary--cs           |
    |                         | button--cs                   |
    |                         | add-attribute--cs            |
    |                         | dropdown-menu--cs            |
    |                         | dropdown-menu-button--cs     |
    |                         | dropdown-menu-search--cs     |
    |                         | input-search--cs             |
    |                         | dropdown-menu-scrollable--cs |
    |                         | dropdown-menu-item--cs       |
2.  **All**\
    Affected Sub-element: Sidebar Title

    **Changes:**

    * Markup Variations:
      * Added `<div role="toolbar">`
      * `<a>` elements are now `<button>`

    **Classnames Comparison:**

    | Classnames Removed         | Classnames Added                           |
    | -------------------------- | ------------------------------------------ |
    | widgets-section\_\_heading | widgets-section\_\_heading--cs             |
    | icon                       | sidebar-panel-title-icon--cs               |
    | icon-\*                    | sidebar-panel-title-icon-comment--cs       |
    |                            | sidebar-panel-title-icon-delete--cs        |
    |                            | sidebar-panel-title-icon-duplicate--cs     |
    |                            | sidebar-panel-title-icon-closepanel--cs    |
    |                            | sidebar-panel-title-icon-save--cs          |
    |                            | sidebar-panel-title-icon-editSyncedRow--cs |
3.  **Rows**\
    Affected Sub-element: Sidebar Title

    **Changes:**

    * Markup Variations:
      * Added `<div role="toolbar">`
      * `<a>` elements are now `<button>`

    **Classnames Comparison:**

    | Classnames Removed         | Classnames Added                           |
    | -------------------------- | ------------------------------------------ |
    | widgets-section\_\_heading | widgets-section\_\_heading--cs             |
    | icon                       | sidebar-panel-title-icon--cs               |
    | icon-\*                    | sidebar-panel-title-icon-comment--cs       |
    |                            | sidebar-panel-title-icon-delete--cs        |
    |                            | sidebar-panel-title-icon-duplicate--cs     |
    |                            | sidebar-panel-title-icon-closepanel--cs    |
    |                            | sidebar-panel-title-icon-save--cs          |
    |                            | sidebar-panel-title-icon-editSyncedRow--cs |

## Mobile Stage Mode, History, and Empty States | Release Coming Soon

1.  **Mobile Stage Mode**\
    Affected Sub-element: Wrapper

    **Classnames Added:**

    * stagemode\_\_buttonswrapper--cs

    **Mobile Stage Mode Buttons:**

    * Desktop button: stagemode\_\_button\_\_desktop--cs
    * Mobile button: stagemode\_\_button\_\_mobile--cs
    * Display toggle button: stagemode\_\_button\_\_display--cs
2.  **Undo/Redo**\
    Affected Sub-elements: Undo/Redo Buttons and History Panel

    **Classnames Added:**

    * Toggle button: undo-redo\_\_toggleButton--cs
    * Undo button: undo-redo\_\_undoButton--cs
    * Redo button: undo-redo\_\_redoButton--cs
    * History panel: undo-redo\_\_history--cs
    * History panel item: history\_\_step--cs
3.  **Empty States (Various Modules)**\
    Affected Modules: Image, Icons, Video, Menu, Social, Form, AddOn, Dynamic Content

    **Classnames Added:**

    * Image module: stage-module\_image\_placeholder--cs
    * Icons module: stage-module\_icons\_placeholder--cs
    * Video module: stage-module\_video\_placeholder--cs
    * Menu module: stage-module\_menu\_placeholder--cs
    * Social module: stage-module\_social\_placeholder--cs
    * Form module: stage-module\_form\_placeholder--cs
    * AddOn module: stage-module\_addon\_placeholder--cs
    * DynamicContent module: stage-module\_merge-content\_placeholder--cs

## Changes Font Stye and Drag-and-Drop Widgets | Release Coming Soon

### **1. Form Components**

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

### **2. Social Widget**

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

### **3. Icons Widget**

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

### **4. Menu Widget**

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

### **5. Form Widget**

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

### **6. Carousel Widget**

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

## Changes Form Edit Modal Update | Released October 10, 2024

### **1. Form Edit Modal - Text Inputs**

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

### **2. Form Edit Modal - Required and Read Only Toggles**

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
