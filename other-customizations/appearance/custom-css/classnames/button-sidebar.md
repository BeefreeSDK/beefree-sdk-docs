# Button Sidebar

This page lists the classnames for different buttons within the sidebar, and is for those seeking to customize or understand the styling applied to these components. You can use this information to more easily modify or enhance the user interface of your web application.

This page will cover button classnames for the following sidebar areas:

* [Content](https://docs.beefree.io/beefree-sdk/other-customizations/appearance/custom-css#content)
* [Rows](https://docs.beefree.io/beefree-sdk/other-customizations/appearance/custom-css#rows)
* [Settings](https://docs.beefree.io/beefree-sdk/other-customizations/appearance/custom-css#settings)

## Content <a href="#content" id="content"></a>

The tables in this section list the classnames for buttons within the content area of the sidebar.

### Add-on <a href="#add-on" id="add-on"></a>

This section lists the Add-on sidebar widget sub-elements and classnames.

#### **Add-on CTA**

| Sub-Element | Deprecated                                                          | New Classnames              |
| ----------- | ------------------------------------------------------------------- | --------------------------- |
| NA          | <ul><li><code>btn</code></li><li><code>btn-primary</code></li></ul> | `add-on-sidebar-button--cs` |

### Button <a href="#button" id="button"></a>

This section lists the Button sidebar widgets and their respective deprecated and new classnames.

#### **Write with AI**

| Sub-element | Deprecated                                                                  | New Classnames        |
| ----------- | --------------------------------------------------------------------------- | --------------------- |
| NA          | <ul><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `ai-sidebar-icon--cs` |

#### **Link**

This section lists the Button sidebar widgets and their respective deprecated and new classnames.

| Sub-element             | Deprecated                                                                                                  | New Classnames                 |
| ----------------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------ |
| Special links           | <ul><li><code>href-container__link</code></li><li><code>href-container__link--special-link</code></li></ul> | `href-special-link--cs`        |
| Link file               | <ul><li><code>href-container__link</code></li><li><code>href-container__link--link-file</code></li></ul>    | `href-link-file--cs`           |
| Add custom special link | <ul><li><code>href-container__link</code></li><li><code>href-container__link--special-link</code></li></ul> | `href-custom-special-link--cs` |

#### **Attributes**

This section lists the Button sidebar widgets and their respective deprecated and new classnames.

| Sub-element       | Deprecated                                                                                                                                                                                       | New Classnames           |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------ |
| Add new attribute | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul> | `toggle-menu-button--cs` |
| Delete            | <ul><li><code>field-remove</code></li></ul>                                                                                                                                                      | `delete-attribute--cs`   |

### Carousel <a href="#carousel" id="carousel"></a>

This section lists the Carousel sidebar widgets, sub-elements, and classnames.

#### **Add New Slide**

| Sub-element | Deprecated                                                                                                                                       | New Classnames               |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------- |
| NA          | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>BeeButton_*</code></li></ul> | `icon-manager__add-icon--cs` |

#### **Draggable Item**

| Sub-element  | Deprecated | New Classnames                   |
| ------------ | ---------- | -------------------------------- |
| Change image | NA         | `carousel-item-change-image--cs` |
| Delete       | NA         | `carousel-item-delete-image--cs` |

### Dynamic Content <a href="#dynamic-content" id="dynamic-content"></a>

This section lists the Dynamic sidebar widgets, sub-elements, and classnames.

#### **Choose a Custom Merge Content**

| Sub-element | Deprecated                                                                                           | New Classnames             |
| ----------- | ---------------------------------------------------------------------------------------------------- | -------------------------- |
| NA          | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `select-merge-content--cs` |

### Form <a href="#form" id="form"></a>

This section lists the Form sidebar widgets, sub-elements, and classnames.

#### **Edit Form**

| Sub-element | Deprecated | New Classnames              |
| ----------- | ---------- | --------------------------- |
| NA          | NA         | `content-dialog-button--cs` |

#### **Manage Fields**

| Sub-element   | Deprecated                                                                                                                                                                                       | New Classnames           |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------ |
| Edit          | <ul><li><code>field-edit</code></li></ul>                                                                                                                                                        | `form-field-edit--cs`    |
| Delete        | <ul><li><code>field-remove</code></li></ul>                                                                                                                                                      | `form-field-delete--cs`  |
| Add new field | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul> | `toggle-menu-button--cs` |

### Heading <a href="#heading" id="heading"></a>

This section lists the Form sidebar widgets, sub-elements, and classnames.

#### **Write with AI**

| Sub-elemet | Deprecated                                                                  | New Classnames                                     |
| ---------- | --------------------------------------------------------------------------- | -------------------------------------------------- |
| NA         | <ul><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | <ul><li><code>ai-sidebar-icon--cs</code></li></ul> |

### Icons <a href="#icons" id="icons"></a>

This section lists the Icons sidebar widgets, sub-elements, and classnames.

#### **Add New Icon**

| Sub-element | Deprecated                                                                                                                                                                                       | New Classnames       |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------- |
| Button      | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul> | `icons-add-icon--cs` |

#### **Draggable Icon**

| Sub-element   | Deprecated                                                                                                  | New Classnames          |
| ------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------- |
| Change image  | <ul><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li><li><code>BeeIcons_*</code></li></ul> | `icons-change-icon--cs` |
| Apply effects | <ul><li><code>btn-default</code></li><li><code>BeeButton_*</code></li><li><code>BeeIcons_*</code></li></ul> | `icons-edit-icon--cs`   |
| Delete        | <ul><li><code>BeeButton_*</code></li><li><code>BeeIcons_*</code></li></ul>                                  | `icons-delete-icon--cs` |

### Image <a href="#image" id="image"></a>

This section lists the Image sidebar widgets, sub-elements, and classnames.

#### **Apply Effects**

| Sub-element | Deprecated                                                                                                                                 | New Classnames         |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------- |
| NA          | <ul><li><code>btn</code></li><li><code>btn-image-editor</code></li><li><code>btn-default</code></li><li><code>BeeButton_*</code></li></ul> | `btn-image-editor--cs` |

**Change Image**

| Sub-element | Deprecated                                                                                                                                  | New Classnames        |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| NA          | <ul><li><code>btn</code></li><li><code>btn-file-picker</code></li><li><code>btn-secondary</code></li><li><code>BeeButton_*</code></li></ul> | `btn-file-picker--cs` |

#### **Link**

| Sub-element             | Deprecated                                                                                                  | New Classnames                 |
| ----------------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------ |
| Special links           | <ul><li><code>href-container__link</code></li><li><code>href-container__link--special-link</code></li></ul> | `href-special-link--cs`        |
| Link file               | <ul><li><code>href-container__link</code></li><li><code>href-container__link--link-file</code></li></ul>    | `href-link-file--cs`           |
| Add custom special link | <ul><li><code>href-container__link</code></li><li><code>href-container__link--special-link</code></li></ul> | `href-custom-special-link--cs` |

#### **Attributes**

| Sub-element       | Deprecated                                                                                                                                                                                       | New Classnames                                        |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- |
| Add new attribute | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul> | <ul><li><code>toggle-menu-button--cs</code></li></ul> |
| Delete            | <ul><li><code>field-remove</code></li></ul>                                                                                                                                                      | <ul><li><code>delete-attribute--cs</code></li></ul>   |

### List <a href="#list" id="list"></a>

This section lists the List sidebar widgets, sub-elements, and classnames.

#### **Write with AI**

| Sub-element | Deprecated                                                                   | New Classnames                                     |
| ----------- | ---------------------------------------------------------------------------- | -------------------------------------------------- |
| NA          | <ul><li><code>btn</code></li><li><code>BeeButton_beeButton*</code></li></ul> | <ul><li><code>ai-sidebar-icon--cs</code></li></ul> |

### Menu <a href="#menu" id="menu"></a>

This section lists the Menu sidebar widgets, sub-elements, and classnames.

#### **Add New Item**

| Sub-element | Deprecated                                                                                                                                                                                       | New Classnames                                           |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| NA          | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul> | <ul><li><code>menu-items-add-button--cs</code></li></ul> |

#### **Menu Item**

| Sub-element | Deprecated                                                                                               | New Classnames                 |
| ----------- | -------------------------------------------------------------------------------------------------------- | ------------------------------ |
| Delete      | <ul><li><code>BeeButton_*</code></li><li><code>BeeMenuItems_*</code></li></ul>                           | `menu-items-delete-button--cs` |
| Link file   | <ul><li><code>href-container__link</code></li><li><code>href-container__link--link-file</code></li></ul> | `href-link-file--cs`           |

### Paragraph <a href="#paragraph" id="paragraph"></a>

This section lists the Paragraph sidebar widgets, sub-elements, and classnames.

#### **Write with AI**

| Sub-element | Deprecated                                                                           | New Classnames                                     |
| ----------- | ------------------------------------------------------------------------------------ | -------------------------------------------------- |
| NA          | <ul><li><code>btn-primary</code></li><li><code>BeeButton_beeButton*</code></li></ul> | <ul><li><code>ai-sidebar-icon--cs</code></li></ul> |

### Social <a href="#social" id="social"></a>

This section lists the Social sidebar widgets, sub-elements, and classnames.

#### **Add New Icon**

| Sub-element | Deprecated                                                                                                                                                                                       | New Classnames        |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------- |
| Button      | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul> | `social-add-icon--cs` |

#### **Social Icon Item**

| Sub-element   | Deprecated                                                                                                        | New Classnames           |
| ------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------------ |
| Delete        | <ul><li><code>icon-remove</code></li></ul>                                                                        | `icon-remove--cs`        |
| Change image  | <ul><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li><li><code>BeeSocialIcons_*</code></li></ul> | `social-change-icon--cs` |
| Apply effects | <ul><li><code>btn-default</code></li><li><code>BeeButton_*</code></li><li><code>BeeSocialIcons_*</code></li></ul> | `social-edit-icon--cs`   |

## Rows <a href="#rows" id="rows"></a>

The tables in this section list the classnames for buttons within the row area of the sidebar.

<figure><img src="../../../../.gitbook/assets/CleanShot 2024-09-16 at 17.56.46.png" alt=""><figcaption></figcaption></figure>

### **Row Background Image**

| Sub-element  | Deprecated                                                                                                                                                                   | New Classnames        |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| Choose image | <ul><li><code>btn</code></li><li><code>btn-file-picker</code></li><li><code>btn-secondary</code></li><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `btn-file-picker--cs` |

### **Row Background Video**

| Sub-element  | Deprecated                                                                                                                                | New Classnames        |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| Change video | <ul><li><code>btn</code></li><li><code>btn-file-picker</code></li><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `btn-file-picker--cs` |

### **Display Condition**

| Sub-element      | Deprecated                                                                                           | New Classnames                             |
| ---------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| Select condition | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `row-display-condition-select-button--cs`  |
| Add condition    | <ul><li><code>btn-default</code></li><li><code>BeeButton_*</code></li></ul>                          | `row-display-condition-add-button--cs`     |
| Edit condition   | <ul><li><code>btn-default</code></li><li><code>BeeButton_*</code></li></ul>                          | `row-display-condition-edit-button--cs`    |
| Open builder     | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `row-display-condition-builder-button--cs` |

**Column Structure**

| Sub-element | Deprecated                                                                             | New Classnames              |
| ----------- | -------------------------------------------------------------------------------------- | --------------------------- |
| Add new     | <ul><li><code>column-manager--add</code></li><li><code>BeeButton_*</code></li></ul>    | `column-manager-add--cs`    |
| Delete      | <ul><li><code>column-manager--delete</code></li><li><code>BeeButton_*</code></li></ul> | `column-manager-delete--cs` |

## Settings <a href="#settings" id="settings"></a>

The tables in this section list the classnames for buttons within the settings area of the sidebar.

<figure><img src="../../../../.gitbook/assets/CleanShot 2024-09-16 at 17.57.26.png" alt=""><figcaption></figcaption></figure>

### **Favicon**

| Sub-element | Deprecated                                                                                                                                                                                       | New Classnames                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------- |
| Add favicon | <ul><li><code>btn</code></li><li><code>btn-primary</code></li><li><code>icon-manager__add-icon</code></li><li><code>icon-manager__add-icon--cs</code></li><li><code>BeeButton_*</code></li></ul> | <ul><li><code>favicon-add-icon--cs</code></li></ul> |

### **Favicon item**

| Sub-element    | Deprecated                                                                  | New Classnames       |
| -------------- | --------------------------------------------------------------------------- | -------------------- |
| Change favicon | <ul><li><code>btn-primary</code></li><li><code>BeeButton_*</code></li></ul> | `favicon-change--cs` |
| Delete         | <ul><li><code>BeeButton_*</code></li></ul>                                  | `favicon-delete--cs` |
