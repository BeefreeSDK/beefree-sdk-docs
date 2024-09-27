# Button and Action Widgets

## Overview

This page covers the classnames used for buttons, sliders, and interactive widgets like toggles in the sidebar. Below, you will find detailed information on each widget’s classnames, including deprecated versions (if applicable) and current classnames to ensure your application remains up-to-date.

### 1. Button

**Description:** Buttons are widely used for user interactions such as submitting forms, toggling features, or performing actions. Different types of buttons include primary, secondary, and action buttons.

**Deprecated Classnames:**

* btn
* btn-primary

**New Classnames:**

* add-on-sidebar-button--cs
* ai-sidebar-icon--cs

**Sample CSS:**

```css
.add-on-sidebar-button--cs {
    background-color: #007bff;
    padding: 10px 20px;
}

.ai-sidebar-icon--cs {
    background-color: #6c757d;
    padding: 10px 20px;
}
```

**Sample HTML:**

```html
<button class="add-on-sidebar-button--cs">Submit</button>
<button class="ai-sidebar-icon--cs">Cancel</button>
```

### 2. Toggle Button

**Description:** Toggle buttons are used to switch between two states, such as enabling or disabling features. They can be styled to look like switches or buttons with an active/inactive state.

**Deprecated Classnames:**

* multiToggle\_option\_descriptor\_form\_style\_labels\_font-weight\_0

**New Classnames:**

* slider--cs
* slider-wrapper--cs

**Sample CSS:**

```css
.slider--cs {
    background-color: #e7e7e7;
    padding: 5px 10px;
}

.slider-wrapper--cs {
    background-color: #28a745;
}
```

**Sample HTML:**

```html
<button class="slider--cs">Enable</button>
<button class="slider-wrapper--cs">Disable</button>
```

### 3. Action Button Group

**Description:** Action button groups are used when multiple buttons are grouped together to perform related actions. These button groups are often seen in toolbars or for setting configurations.

**Deprecated Classnames:**

* href-container\_\_link
* href-container\_\_link--special

**New Classnames:**

* href-special-link--cs
* href-link-file--cs

**Sample CSS:**

```css
.href-special-link--cs {
    padding: 5px 15px;
    margin-right: 5px;
}

.href-link-file--cs {
    background-color: #007bff;
    color: white;
}
```

**Sample HTML:**

```html
<div class="btn-group">
  <button class="href-special-link--cs">Option 1</button>
  <button class="href-link-file--cs">Option 2</button>
  <button class="href-special-link--cs">Option 3</button>
</div>
```

### 4. Slider

**Description:** Sliders are used to adjust values within a range. They are commonly used for settings like volume, brightness, or numerical values. Sliders are interactive and can have custom styling for the track and handle.

**Deprecated Classnames:**

* BeeWidthSlider\_\*
* rc-slider

**New Classnames:**

* slider--cs
* slider-wrapper--cs

**Sample CSS:**

```css
.slider-wrapper--cs {
    background-color: #ddd;
    height: 5px;
}

.slider--cs {
    background-color: #007bff;
    width: 20px;
    height: 20px;
    border-radius: 50%;
}
```

**Sample HTML:**

```html
<div class="slider--cs">
  <div class="slider-wrapper--cs">
    <div class="slider--cs"></div>
  </div>
</div>
```

### 5. Button with Icon

**Description:** Buttons with icons are commonly used to perform actions while also providing a visual representation (an icon) to make the function clearer. These buttons are useful for toolbars, navigation, or forms.

**Deprecated Classnames:**

* href-container\_\_link

**New Classnames:**

* href-custom-special-link--cs

**Sample CSS:**

```css
.href-custom-special-link--cs {
    display: flex;
    align-items: center;
}

.href-custom-special-link--cs i {
    margin-right: 5px;
}
```

**Sample HTML:**

```html
<button class="href-custom-special-link--cs">
  <i class="icon-left"></i> Save
</button>
<button class="href-custom-special-link--cs">
  Delete <i class="icon-right"></i>
</button>
```

### 6. Button Dropdown

**Description:** Button dropdowns allow users to select an option from a list of choices, typically used in toolbars or forms. The button dropdown can display a list of actions when clicked, providing an expandable option set.

**Deprecated Classnames:**

* dropdown-menu--cs
* dropdown-menu-button--cs

**New Classnames:**

* href-special-link--cs

**Sample CSS:**

```css
.href-special-link--cs {
    background-color: #007bff;
    color: white;
    padding: 10px 20px;
}

.href-link-file--cs {
    background-color: white;
    color: #333;
    padding: 10px;
    border-bottom: 1px solid #ddd;
}
```

**Sample HTML:**

```html
<div class="href-special-link--cs">
  <button class="btn">Actions</button>
  <div class="dropdown-menu--cs">
    <a class="href-link-file--cs" href="#">Action 1</a>
    <a class="href-link-file--cs" href="#">Action 2</a>
    <a class="href-link-file--cs" href="#">Action 3</a>
  </div>
</div>
```

### 7. Icon Toggle Button

**Description:** An icon toggle button is a button that toggles between two states (like active/inactive) and includes an icon to visually indicate the current state. This is often used for settings, favorites, or switches.

**Deprecated Classnames:**

* icon-toggle--cs
* icon-toggle-item--cs

**New Classnames:**

* icon-toggle-btn--cs
* icon-toggle-active--cs

**Sample CSS:**

```css
.icon-toggle-btn--cs {
    background-color: #e7e7e7;
    padding: 10px;
}

.icon-toggle-active--cs {
    background-color: #28a745;
    color: white;
}
```

**Sample HTML:**

```html
<button class="icon-toggle-btn--cs">
  <i class="icon"></i> Off
</button>
<button class="icon-toggle-btn--cs icon-toggle-active--cs">
  <i class="icon-active"></i> On
</button>
```

### 8. Toggle Switch

**Description:** Toggle switches are used for binary options, typically for settings or features that can be turned on or off. These switches offer a visual and functional representation of an active/inactive state.

**Deprecated Classnames:**

* toggle-wrapper--cs
* toggle-input--cs

**New Classnames:**

* toggle-switch--cs
* toggle-switch-active--cs

**Sample CSS:**

```css
.toggle-switch--cs {
    background-color: #ccc;
    padding: 5px;
}

.toggle-switch-active--cs {
    background-color: #28a745;
    color: white;
}
```

**Sample HTML:**

```html
<div class="toggle-switch--cs">
  <span class="switch-label">Off</span>
  <div class="switch"></div>
</div>
<div class="toggle-switch--cs toggle-switch-active--cs">
  <span class="switch-label">On</span>
  <div class="switch"></div>
</div>
```

This page consolidates all classnames related to buttons, sliders, and interactive widgets. For deprecated classnames, make sure to transition to the new ones.

For more detailed implementation on how to customize form and input widgets, refer to the [Customizing Sidebar Widgets](./#customizing-sidebar-widgets) section on the [Sidebar Widgets Classnames page](./).
