# Layout and Structure Widgets

## Overview

This page covers the classnames used for managing the layout and structure of your web application, including rows, columns, carousels, and menus. Below, you will find detailed information on each widget’s classnames, including deprecated versions (if applicable) and current classnames to ensure your application remains up-to-date.

### 1. Row Structure

**Description:** Row structure widgets define the layout of rows in your application. You can customize background images, videos, alignment, and other properties related to row display.

**Deprecated Classnames:**

* PanelGroup\_handle\*

**New Classnames:**

* panel-group-dragging--cs
* column-manager-delete--cs

**Sample CSS:**

```css
.panel-group-dragging--cs {
    background-image: url('image.jpg');
    padding: 20px;
}

.column-manager-delete--cs {
    width: 100%;
    height: auto;
}
```

**Sample HTML:**

```html
<div class="panel-group-dragging--cs">
  <div class="column-manager-delete--cs" style="background-image: url('image.jpg')"></div>
</div>
```

### 2. Column Structure

**Description:** Column structure widgets define the layout and behavior of columns within a row. They control how content is divided into multiple columns and can include functionality for adding or deleting columns.

**Deprecated Classnames:**

* PanelGroup\_handle\*

**New Classnames:**

* column-manager-delete--cs

**Sample CSS:**

```css
.column-manager-delete--cs {
    color: #28a745;
    padding: 10px;
}
```

**Sample HTML:**

```html
<div class="column-manager-delete--cs">
  <button class="column-manager-add--cs">Add Column</button>
</div>
```

### 3. Carousel

**Description:** The carousel widget allows you to display content in a slider format, typically with multiple slides that users can navigate through. Carousels can contain images, text, or custom content.

**Deprecated Classnames:**

* PanelGroup\_handle\*

**New Classnames:**

* carousel--cs
* carousel-slide--cs

**Sample CSS:**

```css
.carousel--cs {
    background-color: #f9f9f9;
    padding: 20px;
}

.carousel-slide--cs {
    padding: 20px;
    background-color: #ddd;
    margin-bottom: 10px;
}
```

**Sample HTML:**

```html
<div class="carousel--cs">
  <div class="carousel-slide--cs">Slide 1</div>
  <div class="carousel-slide--cs">Slide 2</div>
  <div class="carousel-slide--cs">Slide 3</div>
</div>
```

### 4. Menu Structure

**Description:** Menus are used to create navigation within your application. The menu structure widget provides a customizable way to organize links and buttons, allowing for horizontal and vertical layouts.

**Deprecated Classnames:**

* PanelGroup\_handle\*

**New Classnames:**

* menu--cs
* menu-item--cs

**Sample CSS:**

```css
.menu--cs {
    background-color: #333;
    padding: 10px;
}

.menu-item--cs {
    color: #fff;
    padding: 10px 20px;
    text-decoration: none;
}
```

**Sample HTML:**

```html
<nav class="menu--cs">
  <a class="menu-item--cs" href="#">Home</a>
  <a class="menu-item--cs" href="#">About</a>
</nav>
```

### 5. Column Alignment

**Description:** The column alignment widget allows you to control how content within a column is aligned—left, right, center, or justified.

**Deprecated Classnames:**

* PanelGroup\_handle\*

**New Classnames:**

* column-align-left--cs
* column-align-right--cs

**Sample CSS:**

```css
.column-align-left--cs {
    text-align: left;
    padding: 10px;
}

.column-align-right--cs {
    text-align: right;
    padding: 10px;
}
```

**Sample HTML:**

```html
<div class="column-align-left--cs">Left Aligned Content</div>
<div class="column-align-right--cs">Right Aligned Content</div>
```

### 6. Row and Column Divider

**Description:** Dividers are used to visually separate rows and columns, providing a cleaner and more organized layout.

**Deprecated Classnames:**

* PanelGroup\_handle\*

**New Classnames:**

* row-divider--cs
* column-divider--cs

**Sample CSS:**

```css
.row-divider--cs {
    border-bottom: 2px solid #e0e0e0;
}

.column-divider--cs {
    border-right: 2px solid #e0e0e0;
}
```

**Sample HTML:**

```html
<div class="row-divider--cs"></div>
<div class="column-divider--cs"></div>
```

### 7. Dynamic Content Area

**Description:** The dynamic content area widget allows you to configure dynamic content for columns or rows, such as pulling in data from external sources.

**Deprecated Classnames:**

* PanelGroup\_handle\*

**New Classnames:**

* dynamic-content-area--cs
* content-area-active--cs

**Sample CSS:**

```css
.dynamic-content-area--cs {
    background-color: #f0f0f0;
    padding: 15px;
}

.content-area-active--cs {
    background-color: #007bff;
    color: white;
}
```

**Sample HTML:**

```html
<div class="dynamic-content-area--cs">
  <p>Dynamic content goes here...</p>
</div>
```

This page consolidates all classnames related to layout and structure widgets. For deprecated classnames, ensure you are transitioning to the new ones.

For more detailed implementation on how to customize form and input widgets, refer to the [Customizing Sidebar Widgets](./#customizing-sidebar-widgets) section on the [Sidebar Widgets Classnames page](./).
