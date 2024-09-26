# Icon and Social Widgets

## Overview

This page covers the classnames used for icon and social widgets in the sidebar. These widgets allow you to add, configure, and style icons (including social media icons) in your application. Below, you will find detailed information on each widget’s classnames, including deprecated versions (if applicable) and current classnames to ensure your application remains up-to-date.

### 1. Icon Organizer

**Description:** The icon organizer widget manages and displays icon collections, allowing for adding, organizing, and previewing icons in a structured manner.

**Deprecated Classnames:**

* icons-manager\_\_pop--cs
* icons-manager\_\_popcontent

**New Classnames:**

* button-small--cs
* add-social-icon--cs

**Sample CSS:**

```css
.button-small--cs {
    background-color: #f0f0f0;
    padding: 15px;
}

.add-social-icon--cs {
    list-style: none;
    padding: 0;
}
```

**Sample HTML:**

```html
<div class="button-small--cs">
  <ul class="add-social-icon--cs">
    <li class="icon-item">Icon 1</li>
    <li class="icon-item">Icon 2</li>
    <li class="icon-item">Icon 3</li>
  </ul>
</div>
```

### 2. Social Icon Manager

**Description:** The social icon manager widget allows users to add and configure social media icons within the sidebar. It provides a way to easily manage the appearance and behavior of social icons, as well as their associated links.

**Deprecated Classnames:**

* icons-manager\_\_pop--cs
* icons-manager\_\_popcontent

**New Classnames:**

* button-small--cs
* add-social-icon--cs

**Sample CSS:**

```css
.add-social-icon--cs {
    background-color: #007bff;
    color: white;
    border-radius: 4px;
    padding: 10px;
}

.button-small--cs {
    color: #333;
    margin: 5px 0;
}
```

**Sample HTML:**

```html
<button class="add-social-icon--cs">Add Social Icon</button>
<ul class="social-icon-collection">
  <li class="button-small--cs">Facebook</li>
  <li class="button-small--cs">Twitter</li>
  <li class="button-small--cs">Instagram</li>
</ul>
```

### 3. Add New Social Icon

**Description:** This widget allows the addition of new social media icons to your collection. Users can easily configure the icon type, link, and style.

**Deprecated Classnames:**

* icons-manager\_\_pop--cs
* icons-manager\_\_popcontent

**New Classnames:**

* button-small--cs
* add-social-icon--cs
* dropdown-menu--cs
* dropdown-menu-button--cs
* dropdown-menu-search--cs
* input-search--cs
* dropdown-menu-scrollable--cs
* dropdown-menu-item--cs

**Sample CSS:**

```css
.add-social-icon--cs {
    color: #fff;
    background-color: #28a745;
    padding: 8px;
}

.button-small--cs {
    font-size: 12px;
    padding: 5px 10px;
}
```

**Sample HTML:**

```html
<div class="dropdown-menu--cs">
  <button class="button-small--cs add-social-icon--cs dropdown-menu-button--cs">Add New Social Icon</button>
  <div class="dropdown-menu-search--cs">
    <input type="text" class="input-search--cs" placeholder="Search Icons">
  </div>
  <div class="dropdown-menu-scrollable--cs">
    <ul>
      <li class="dropdown-menu-item--cs">Facebook</li>
      <li class="dropdown-menu-item--cs">Twitter</li>
      <li class="dropdown-menu-item--cs">Instagram</li>
    </ul>
  </div>
</div>
```

### 4. Social Icon Tooltip

**Description:** The tooltip provides a hover effect for social icons, displaying additional information about the link or the social network. This enhances the user experience by offering contextual information.

**Deprecated Classnames:**

* popover\_\_tab

**New Classnames:**

* social-tooltip--cs
* tooltip-active--cs

**Sample CSS:**

```css
.social-tooltip--cs {
    background-color: #333;
    color: white;
    padding: 5px;
}

.tooltip-active--cs {
    color: #fff;
    background-color: #444;
    padding: 5px;
    border-radius: 4px;
}
```

**Sample HTML:**

```html
<div class="social-tooltip--cs">
  <span class="tooltip-active--cs">Follow us on Twitter</span>
</div>
```

### 5. Social Icon Alignment

**Description:** This widget allows users to align social icons horizontally or vertically within a container. It’s useful when customizing the layout of social icons in headers, footers, or sidebars.

**Deprecated Classnames:**

* widget\_\_label
* icon-organizer\_\_panel

**New Classnames:**

* social-align-horizontal--cs
* social-align-vertical--cs

**Sample CSS:**

```css
.social-align-horizontal--cs {
    display: flex;
    gap: 10px;
}

.social-align-vertical--cs {
    display: flex;
    flex-direction: column;
    gap: 15px;
}
```

**Sample HTML:**

```html
<div class="social-align-horizontal--cs">
  <i class="social-icon-item--cs">Facebook</i>
  <i class="social-icon-item--cs">Twitter</i>
  <i class="social-icon-item--cs">Instagram</i>
</div>
```

### 6. Icon Collection Panel

**Description:** The icon collection panel manages collections of icons that can be added to various parts of your application, including both general icons and social media icons.

**Deprecated Classnames:**

* icons-manager\_\_pop--cs

**New Classnames:**

* button-small--cs
* add-social-icon--cs

**Sample CSS:**

```css
.icon-collection-panel--cs {
    background-color: #f8f9fa;
    padding: 20px;
}

.panel__title--cs {
    font-weight: bold;
    font-size: 16px;
    margin-bottom: 10px;
}
```

**Sample HTML:**

```html
<div class="icon-collection-panel--cs">
  <div class="panel__title--cs">Icon Collection</div>
  <ul class="icons-collection-list--cs">
    <li class="icon-item">Icon 1</li>
    <li class="icon-item">Icon 2</li>
  </ul>
</div>
```

### 7. Social Icon URL

**Description:** This widget allows you to specify the URL associated with each social icon. The user can input a URL, which will be tied to the social media icon for easy navigation.

**Deprecated Classnames:**

* widget\_\_textbox

**New Classnames:**

* social-icon-url--cs
* input-url-social--cs

**Sample CSS:**

```css
.social-icon-url--cs {
    color: #333;
    border: 1px solid #ccc;
    padding: 10px;
}

.input-url-social--cs {
    background-color: #fff;
    padding: 10px;
}
```

**Sample HTML:**

```html
<input type="url" class="social-icon-url--cs input-url-social--cs" placeholder="Enter Social URL" />
```

### 8. Icon Preview

**Description:** This widget provides a preview of how an icon will appear once added to the interface. It is used in the icon configuration panel to give a real-time preview of icon styles.

**Deprecated Classnames:**

* panel\_\_icon-preview-wrapper

**New Classnames:**

* icon-preview--cs
* preview-icon-active--cs

**Sample CSS:**

```css
.icon-preview--cs {
    background-color: #f1f1f1;
    padding: 15px;
}

.preview-icon-active--cs {
    color: #007bff;
    font-size: 20px;
}
```

**Sample HTML:**

```html
<div class="icon-preview--cs">
  <i class="preview-icon-active--cs">Icon Preview</i>
</div>
```

This page consolidates all classnames related to icons and social media widgets. For deprecated classnames, make sure to transition to the new ones to maintain current styles and functionality.

For more detailed implementation on how to customize form and input widgets, refer to the [Customizing Sidebar Widgets](./#customizing-sidebar-widgets) section on the [Sidebar Widgets Classnames page](./).
