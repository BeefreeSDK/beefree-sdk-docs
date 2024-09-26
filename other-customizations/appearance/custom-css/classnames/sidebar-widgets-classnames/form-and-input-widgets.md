# Form and Input Widgets

## Overview

This page covers the classnames used for form and input widgets in the sidebar. These widgets allow you to create and customize form fields, text areas, and manage field configurations. Below, you will find detailed information on each widget’s classnames, including deprecated versions (if applicable) and current classnames to ensure your application remains up-to-date.

### 1. Form Label

**Description:** The form label widget provides clear, concise labels for input fields, ensuring accessibility and ease of use.

**Deprecated Classnames:**

* toggle-menu-button--cs
* button-large--cs
* widget\_\_textbox
* scrollable\_\_panel--cs

**New Classnames:**

* button-small--cs
* add-form-field--cs
* dropdown-menu--cs

**Sample CSS:**

```css
.widget__label {
    color: #333;
    padding: 10px;
}

.input-text-boxed--cs {
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
}
```

**Sample HTML:**

```html
<label class="widget__label" for="input1">Name</label>
<input type="text" class="input-text-boxed--cs" placeholder="Enter your text" />
```

### 2. Input Text

**Description:** This widget styles textual input fields, such as URLs, email addresses, and general text inputs. These fields are essential for gathering user information.

**Deprecated Classnames:**

* number-selector--cs
* widget\_\_textbox
* item\_1-2

**New Classnames:**

* input-text--cs
* input-text-boxed--cs

**Sample CSS:**

```css
.input-text--cs {
    background-color: #fff;
    padding: 8px;
}

.input-text-boxed--cs {
    border: 1px solid #ddd;
    padding: 10px;
}
```

**Sample HTML:**

```html
<input type="text" class="input-text--cs input-text-boxed--cs" placeholder="Enter your text" />
```

### 3. Input Text - Email

**Description:** This widget is for email input fields, typically used with a form label to indicate that a valid email address is required.

**Deprecated Classnames:**

* number-selector--cs
* widget\_\_textbox
* item\_1-2

**New Classnames:**

* input-text--cs

**Sample CSS:**

```css
.input-text--cs {
    color: #333;
    background-color: #f9f9f9;
    border-radius: 4px;
}
```

**Sample HTML:**

```html
<input type="email" class="input-text--cs" placeholder="Enter your email" />
```

### 4. Input Text - URL

**Description:** This widget handles URL inputs, often used in forms that require website links or external resources.

**Deprecated Classnames:**

* number-selector--cs
* input-image-url
* widget\_\_textbox

**New Classnames:**

* input-text--cs

**Sample CSS:**

```css
.input-text--cs {
    color: #444;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
}
```

**Sample HTML:**

```html
<input type="url" class="input-text--cs" placeholder="Enter URL" />
```

### 5. Input Text - Tel

**Description:** This widget is used for telephone number input fields, typically included in contact forms.

**Deprecated Classnames:**

* number-selector--cs
* widget\_\_textbox
* item\_1-2

**New Classnames:**

* input-text--cs

**Sample CSS:**

```css
.input-text--cs {
    background-color: #e7f1ff;
    border: 1px solid #007bff;
}
```

**Sample HTML:**

```html
<input type="tel" class="input-text--cs" placeholder="Enter phone number" />
```

### 6. Manage Fields - Add New Field

**Description:** The "Add New Field" widget allows users to dynamically add new fields to forms. This is particularly useful for managing custom forms in the sidebar.

**Deprecated Classnames:**

* toggle-menu-button--cs
* button-large--cs
* widget\_\_textbox

**New Classnames:**

* button-small--cs
* add-form-field--cs
* dropdown-menu--cs
* dropdown-menu-button--cs
* dropdown-menu-search--cs
* input-search--cs
* dropdown-menu-scrollable--cs
* dropdown-menu-item--cs

**Sample CSS:**

```css
.add-form-field--cs {
    background-color: #28a745;
    color: white;
}

.button-small--cs {
    padding: 5px 10px;
    font-size: 12px;
}
```

**Sample HTML:**

```html
<button class="add-form-field--cs button-small--cs">Add New Field</button>
```

### 7. Textarea

**Description:** The textarea widget is used for multiline text inputs such as comments or descriptions. It is a flexible input area that allows users to enter longer text.

**Deprecated Classnames:**

* widget\_\_textbox
* textarea-box-old

**New Classnames:**

* input-text--cs
* textarea-boxed--cs

**Sample CSS:**

```css
.textarea-boxed--cs {
    border: 1px solid #ccc;
    padding: 10px;
    border-radius: 4px;
}
```

**Sample HTML:**

```html
<textarea class="input-text--cs textarea-boxed--cs" placeholder="Enter your message"></textarea>
```

### 8. Select Dropdown

**Description:** The select dropdown widget allows users to choose from predefined options, often used for categorical inputs.

**Deprecated Classnames:**

* item\_1-2
* widget\_\_textbox

**New Classnames:**

* dropdown-menu--cs
* dropdown-menu-item--cs

**Sample CSS:**

```css
.dropdown-menu--cs {
    background-color: #fff;
    border-radius: 4px;
}

.dropdown-menu-item--cs {
    padding: 10px;
    border-bottom: 1px solid #ddd;
}
```

**Sample HTML:**

```html
<select class="dropdown-menu--cs dropdown-menu-item--cs">
  <option value="1">Option 1</option>
  <option value="2">Option 2</option>
  <option value="3">Option 3</option>
</select>
```

### 9. Checkbox and Radio Button

**Description:** Checkboxes and radio buttons are common input elements used for binary or multiple-choice options.

**Deprecated Classnames:**

* toggle-wrapper--cs
* toggle-input--cs
* toggle-slider--cs

**New Classnames:**

* radiogroup--cs
* radiogroup-button--cs

**Sample CSS:**

```css
.radiogroup-button--cs {
    margin-right: 10px;
}

.checkbox-wrapper--cs {
    margin-right: 10px;
}
```

**Sample HTML:**

```html
<!-- Checkbox -->
<input type="checkbox" class="checkbox-wrapper--cs" id="check1">
<label for="check1">I agree</label>

<!-- Radio Button -->
<input type="radio" class="radiogroup-button--cs" name="choice" id="radio1" value="1">
<label for="radio1">Option 1</label>
<input type="radio" class="radiogroup-button--cs" name="choice" id="radio2" value="2">
<label for="radio2">Option 2</label>
```

This page consolidates all form and input-related classnames. For deprecated classnames, ensure you're transitioning to the new classnames.

For more detailed implementation on how to customize form and input widgets, refer to the [Customizing Sidebar Widgets](./#customizing-sidebar-widgets) section on the [Sidebar Widgets Classnames page](./).
