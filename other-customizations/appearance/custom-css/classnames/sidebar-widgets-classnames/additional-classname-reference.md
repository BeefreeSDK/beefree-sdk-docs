# Additional Classname Reference

## Additional Classname Reference

This page covers additional updates made to various content types within the sidebar. It outlines the changes to classnames for dynamic content areas, image URLs, background settings, sliders, and more.

### 1. Image URL

**Description:** The image URL widget handles image sources, allowing users to input or configure the URLs of images. This widget has been updated to streamline unnecessary wrappers.

**Deprecated Classnames:**

* number-selector--cs
* input-image-url
* item\_1-2

**New Classnames:**

* input-text--cs
* input-text-boxed--cs
* input-text-detached--cs

**Sample CSS:**

```css
.input-text--cs {
    border: 1px solid #ccc;
}

.input-text-boxed--cs {
    padding: 10px;
}

.input-text-detached--cs {
    display: block;
    margin: 10px 0;
}
```

**Sample HTML:**

```html
<div class="input-text--cs input-text-boxed--cs input-text-detached--cs">
  <label class="widget__label--cs">Image URL</label>
  <input type="text" class="widget__textbox" placeholder="Enter image URL">
</div>
```

### 2. Row Background Image

**Description:** This widget allows users to apply background images to rows, including the ability to configure image properties and add/remove background elements.

**Deprecated Classnames:**

* number-selector--cs
* tgl\_bgd

**New Classnames:**

* row-bg-image--cs

**Sample CSS:**

```css
.row-bg-image--cs {
    background-image: url('background.jpg');
    padding: 15px;
}
```

**Sample HTML:**

```html
<div class="row-bg-image--cs" style="background-image: url('background.jpg')"></div>
```

### 3. Row Background Video

**Description:** This widget is used to add videos as background elements for rows, improving dynamic content presentation and design aesthetics.

**Deprecated Classnames:**

* tgl-container
* number-selector--cs

**New Classnames:**

* row-bg-video--cs

**Sample CSS:**

```css
.row-bg-video--cs {
    padding: 15px;
}
```

**Sample HTML:**

```html
<div class="row-bg-video--cs">
  <video src="background.mp4" autoplay muted loop></video>
</div>
```

### 4. Add-on Width Slider

**Description:** This widget allows users to adjust the width of certain add-ons like images or forms. The width slider was completely rewritten for better functionality and accessibility.

**Deprecated Classnames:**

* BeeWidthSlider\_\*
* rc-slider

**New Classnames:**

* slider--cs
* slider-wrapper--cs

**Sample CSS:**

```css
.slider-wrapper--cs {
    padding: 10px;
}

.slider--cs {
    width: 100%;
}
```

**Sample HTML:**

```html
<div class="slider-wrapper--cs">
  <div class="slider--cs">
    <input type="range" min="0" max="100" value="50">
  </div>
</div>
```

### 5. Dynamic Image > Dynamic URL

**Description:** This widget manages dynamic images, allowing the configuration of image URLs that can change dynamically based on user interaction or external data sources. Unnecessary wrappers were removed.

**Deprecated Classnames:**

* number-selector--cs
* widget\_\_textbox

**New Classnames:**

* dynamic-image-url--cs
* input-text-boxed--cs

**Sample CSS:**

```css
.dynamic-image-url--cs {
    color: #333;
    padding: 8px;
}
```

**Sample HTML:**

```html
<div class="input-text-boxed--cs dynamic-image-url--cs">
  <label class="widget__label--cs">Dynamic Image URL</label>
  <input type="text" class="widget__textbox" placeholder="Enter dynamic image URL">
</div>
```

### 6. Send Email > Mail To

**Description:** The widget allows users to configure the "mail to" field in forms or buttons, streamlining email interactions from within the application.

**Deprecated Classnames:**

* number-selector--cs
* widget\_\_textbox

**New Classnames:**

* input-text--cs
* input-text-boxed--cs

**Sample CSS:**

```css
.input-text--cs {
    padding: 10px;
}
```

**Sample HTML:**

```html
<div class="input-text--cs input-text-boxed--cs">
  <label class="widget__label--cs">Email Address</label>
  <input type="email" class="widget__textbox" placeholder="Enter email address">
</div>
```

### 7. Row Background Image - Apply to Content Area

**Description:** Allows users to apply background images to content areas of rows. This widget has been optimized by removing unnecessary wrapper elements.

**Deprecated Classnames:**

* tgl-container
* btn-group

**New Classnames:**

* radiogroup--cs
* radiogroup-button--cs

**Sample CSS:**

```css
.radiogroup-button--cs {
    background-color: #eaeaea;
    padding: 10px;
}
```

**Sample HTML:**

```html
<div class="radiogroup--cs">
  <button class="radiogroup-button--cs">Apply Background to Content Area</button>
</div>
```

### 8. Panel Group & Column Management

**Description:** This section deals with managing rows and columns, including features for adding, deleting, and dragging panels.

**New Classnames:**

* panel-group-dragging--cs
* column-manager-add--cs
* column-manager-delete--cs
* panel-divider--cs

**Sample CSS:**

```css
.panel-group-dragging--cs {
    background-color: #f5f5f5;
}

.column-manager-add--cs {
    color: #28a745;
}

.column-manager-delete--cs {
    color: #dc3545;
}

.panel-divider--cs {
    border-bottom: 1px solid #ccc;
}
```

**Sample HTML:**

```html
<div class="panel-group-dragging--cs">
  <button class="column-manager-add--cs">Add Column</button>
  <button class="column-manager-delete--cs">Delete Column</button>
  <div class="panel-divider--cs"></div>
</div>
```

### 9. Carousel Management

**Description:** This section includes managing carousel components, including slides and related elements.

**New Classnames:**

* carousel-slides-list--cs
* carousel-add-slide-btn--cs
* slide-organizer\_\_panel--cs

**Sample CSS:**

```css
.carousel-slides-list--cs {
    padding: 15px;
}

.carousel-add-slide-btn--cs {
    background-color: #007bff;
    color: white;
}

.slide-organizer__panel--cs {
    border: 1px solid #ddd;
    padding: 10px;
}
```

**Sample HTML:**

```html
<div class="carousel-slides-list--cs">
  <div class="slide-organizer__panel--cs">Slide 1</div>
  <button class="carousel-add-slide-btn--cs">Add Slide</button>
</div>
```

### 10. Page Metadata

**Description:** Manage metadata like page titles, descriptions, and preheaders.

**New Classnames:**

* page-metadata-title--cs
* page-metadata-description--cs
* page-metadata-subject--cs
* page-metadata-preheader--cs

**Sample CSS:**

```css
.page-metadata-title--cs {
    font-size: 24px;
    font-weight: bold;
}

.page-metadata-description--cs {
    font-size: 14px;
}

.page-metadata-preheader--cs {
    color: #888;
}
```

**Sample HTML:**

```html
<div class="page-metadata-title--cs">Page Title</div>
<div class="page-metadata-description--cs">This is the description for the page.</div>
<div class="page-metadata-preheader--cs">Preheader text for email previews.</div>
```

For more detailed implementation on how to customize form and input widgets, refer to the [Customizing Sidebar Widgets](./#customizing-sidebar-widgets) section on the [Sidebar Widgets Classnames page](./).
