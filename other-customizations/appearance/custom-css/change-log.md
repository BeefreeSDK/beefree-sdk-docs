---
description: >-
  A classnames change log where you can reference current and past changes to
  CSS classes.
---

# Change Log

## Classname Changes Released October 10, 2024

### Changes Form Edit Modal Update

#### **1. Form Edit Modal - Text Inputs**

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

#### **2. Form Edit Modal - Required and Read Only Toggles**

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

### Changes Font Stye and Drag-and-Drop Widgets

#### **1. Form Components**

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

#### **2. Social Widget**

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

#### **3. Icons Widget**

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

#### **4. Menu Widget**

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

#### **5. Form Widget**

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

#### **6. Carousel Widget**

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
