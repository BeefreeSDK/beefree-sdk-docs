---
description: >-
  This page provides a comprehensive list of HTML form field types, detailing
  their unique attributes and options, along with global attributes that apply
  to all fields.
---

# Allowed form fields

## Global Attributes

The following global attributes are applicable across all field types. They define essential properties related to accessibility, content structure, behavior, and presentation. Reference the **Global attributes** and **Attributes** sub-sections of the [HTML reference in mdn web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference) to try out the attributes and learn more about their specifications.

List of Global Attributes and their corresponding explanations:

* **`accesskey`**: Defines a shortcut key to activate or focus an element.&#x20;
* **`class`**: Assigns one or more class names to an element, used for styling and script interaction.
* **`contenteditable`**: Indicates whether the content of the element is editable.
* **`dir`**: Specifies the text direction (`ltr`, `rtl`, or `auto`).
* **`disabled`**: Disables an element, making it not selectable.
* **`readonly`**: Prevents modification of the element’s content while still allowing interaction.
* **`draggable`**: Allows the element to be dragged.
* **`hidden`**: Hides the element.
* **`id`**: Assigns a unique identifier to an element.
* **`name`**: Specifies the name of the form control. Reference the mdn web docs on the name attribute to try it and learn more about its specifications.
* **`itemid`**: Provides a unique identifier for items when using microdata.
* **`itemprop`**: Specifies properties for microdata.
* **`itemref`**: References other items related to the current item for microdata.
* **`itemscope`**: Defines the scope of an item for microdata.
* **`itemtype`**: Defines the type of an item for microdata.
* **`lang`**: Declares the language of the element’s content.
* **`tabindex`**: Defines the tab order for focusable elements.
* **`title`**: Provides additional information about an element, often used as a tooltip.
* **`value`**: Specifies the value of the input element.

## Unique Attributes

The following sections list the unique attributes for each field type. Reference the [\<input> types sub-section of the HTML Reference section of the mdn web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button) to try out and learn more about unique attributes outlined in the subsequent sections.

{% hint style="info" %}
**Note:** [Global Attributes](allowed-form-fields.md#global-attributes) apply to each of the field types listed in the following sections.
{% endhint %}

### Checkbox Field

The `checkbox` field allows users to select multiple options from a list. It is often used to toggle between two states, like "checked" or "unchecked."

#### Unique Attributes:

* **`checked`** (boolean): Specifies whether the checkbox is selected by default.&#x20;

#### Available Options:

* **`options`**: An array of options, each with:
  * **`value`** (string)
  * **`label`** (string)

### Color Field

The `color` field allows users to select a color from a color picker.

#### Unique Attributes:

* **`autocomplete`** (string): Specifies if the browser should provide autocomplete suggestions.
* **`list`** (string): Refers to a `<datalist>` that provides predefined color options.
* **`required`** (boolean): Specifies that the field must be filled before form submission.

### Datalist Field

The `datalist` field provides a list of predefined options for other input fields, enhancing usability by offering suggestions.

#### Unique Attributes:

No unique attributes.

#### Available Options:

* **`options`**: An array of options, each with:
  * **`value`** (string)

### Date Field

The `date` field allows users to select a date, displayed as a date picker.

#### Unique Attributes:

* **`autocomplete`** (string): Specifies if the browser should suggest previously entered dates.&#x20;
* **`max`** (string): Sets the maximum date allowed.
* **`min`** (string): Sets the minimum date allowed.
* **`required`** (boolean): Specifies that a date must be selected before submission.&#x20;
* **`step`** (string): Specifies the granularity of selectable dates (e.g., steps in days).&#x20;

### Datetime-Local Field

The `datetime-local` field allows users to input both a date and a time.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`max`** (string): Sets the maximum allowed date and time.
* **`min`** (string): Sets the minimum allowed date and time.
* **`required`** (boolean): Requires a date and time before form submission.
* **`step`** (string): Specifies the granularity of selectable times (e.g., steps in minutes).&#x20;

### Email Field

The `email` field is used for inputting one or more email addresses.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`maxlength`** (string): Specifies the maximum number of characters allowed.
* **`minlength`** (string): Specifies the minimum number of characters required.
* **`multiple`** (boolean): Allows multiple email addresses.&#x20;
* **`placeholder`** (string): Displays a hint to the user.
* **`required`** (boolean): Requires an email address before form submission.
* **`size`** (string): Sets the visible width of the input.

### File Field

The `file` field allows users to upload one or more files from their device.

#### Unique Attributes:

* **`accept`** (string): Specifies the types of files accepted by the server (e.g., `image/png`).&#x20;
* **`capture`** (string): Allows capturing images/audio from the camera/microphone if supported.&#x20;
* **`multiple`** (boolean): Allows selecting multiple files.&#x20;
* **`required`** (boolean): Specifies that at least one file must be uploaded.&#x20;

### Hidden Field

The `hidden` field stores data that the user cannot see or interact with but is submitted with the form.

#### Unique Attributes:

* **`autocomplete`** (string)

### Image Field

The `image` field creates a graphical submit button using an image.

#### Unique Attributes:

* **`alt`** (string): Provides alternate text if the image cannot be displayed.&#x20;
* **`height`** (string): Specifies the image URL.&#x20;
* **`src`** (string): Defines the height of the image (in pixels).
* **`width`** (string): Defines the width of the image (in pixels).&#x20;

### Label Field

The `label` field associates a text label with a form control, improving accessibility.

#### Unique Attributes:

No unique attributes.

### Month Field

The `month` field allows users to select a month and year without choosing a specific day.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`max`** (string): Specifies the latest allowed month.
* **`min`** (string): Specifies the earliest allowed month.
* **`required`** (boolean): Ensures a selection is made before form submission.&#x20;
* **`step`** (string): Defines the interval for month selection.&#x20;

### Number Field

The `number` field allows users to input numeric values.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`max`** (number): Sets the maximum allowed value.
* **`min`** (number): Sets the minimum allowed value.
* **`required`** (boolean): Requires a numeric value before submission.
* **`step`** (number): Specifies the allowed increment for numbers.&#x20;

### Password Field

The `password` field allows users to input masked text (e.g., passwords).

#### Unique Attributes:

* **`autocomplete`** (string)
* **`maxlength`** (string): Limits the number of characters allowed.
* **`minlength`** (string): Sets the minimum number of characters required.&#x20;
* **`pattern`** (string): Specifies a regular expression for validation.
* **`placeholder`** (string): Provides a hint to the user.&#x20;
* **`required`** (boolean): Specifies that the field must be filled.
* **`size`** (string): Defines the visible width of the input.

### Radio Field

The `radio` field allows users to select one option from a group.

#### Unique Attributes:

* **`checked`** (boolean): Indicates whether the radio button is selected by default.&#x20;
* **`required`** (boolean): Specifies that one option must be selected before form submission.&#x20;

#### Available Options:

* **`options`**: An array of options, each with:
  * **`value`** (string)
  * **`label`** (string)

### Range Field

The `range` field allows users to select a numeric value within a range, often displayed as a slider.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`max`** (number): Sets the maximum allowed value.&#x20;
* **`min`** (number): Sets the minimum allowed value.&#x20;
* **`step`** (number):Defines the granularity of the range (e.g., steps in increments of 1 or 10).&#x20;

### Select Field

The `select` field creates a dropdown list that allows users to choose one or more options.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`multiple`** (boolean): Allows multiple selections if set to true.&#x20;
* **`required`** (boolean): Specifies that the user must select at least one option.
* **`size`** (string): Defines the number of visible options in the dropdown.&#x20;

#### Available Options:

* **`options`**: An array of options, either:
  * **`option`** elements, with:
    * **`value`** (string)
    * **`label`** (string)
  * **`optgroup`** elements, containing groups of options.

### Search Field

The `search` field allows users to enter search queries with specialized input handling.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`dirname`** (string): Submits the text directionality of the search field with the form.&#x20;
* **`maxlength`** (string): Limits the number of characters allowed in the input.&#x20;
* **`minlength`** (string): Specifies the minimum number of characters.&#x20;
* **`placeholder`** (string): Provides a hint about the expected input.
* **`required`** (boolean): Ensures that a search term is entered before submission.

### Submit Field

The `submit` field creates a button that submits the form data.

#### Unique Attributes:

* **`data-sitekey`** (string): Used in conjunction with reCAPTCHA to verify form submissions.&#x20;
* **`data-callback`** (string): Defines a JavaScript function to be executed after submission.&#x20;
* **`data-action`** (string): Defines an action to be associated with the submit button.&#x20;
* **`width`** (string): Defines the width of the submit button.

### Tel Field

The `tel` field allows users to enter telephone numbers.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`maxlength`** (string): Limits the number of characters allowed.&#x20;
* **`minlength`** (string): Sets the minimum number of characters required.&#x20;
* **`pattern`** (string): Provides a pattern for validation (e.g., for formatting telephone numbers).
* **`placeholder`** (string): Displays a hint about the expected input.&#x20;
* **`required`** (boolean): Specifies that a telephone number must be entered before submission.&#x20;
* **`size`** (string): Defines the visible width of the input.&#x20;

### Text Field

The `text` field allows users to input text.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`maxlength`** (string): Limits the number of characters allowed.&#x20;
* **`minlength`** (string): Specifies the minimum number of characters.&#x20;
* **`pattern`** (string): Provides a regular expression for validation.&#x20;
* **`placeholder`** (string): Displays a hint for the expected input.&#x20;
* **`required`** (boolean): Ensures that a value is entered before form submission.
* **`size`** (string): Specifies the visible width of the text input.&#x20;

### Textarea Field

The `textarea` field allows for multi-line text input, offering more space than the `text` field.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`cols`** (number): Defines the visible width of the textarea in characters.
* **`rows`** (number): Defines the visible height of the textarea in lines.&#x20;
* **`maxlength`** (string): Limits the number of characters allowed.&#x20;
* **`minlength`** (string): Sets the minimum number of characters required.&#x20;
* **`placeholder`** (string): Provides a hint about the expected input.&#x20;
* **`spellcheck`** (string): Enables or disables spell checking.
* **`wrap`** (string): Controls text wrapping behavior (e.g., `"hard"` or `"soft"`).
* **`required`** (boolean): Specifies that input is mandatory before form submission.&#x20;

### Time Field

The `time` field allows users to input a time (hours, minutes, and optionally seconds).

#### Unique Attributes:

* **`autocomplete`** (string)
* **`max`** (string): Sets the latest allowable time.
* **`min`** (string): Sets the earliest allowable time.&#x20;
* **`required`** (boolean): Requires a time to be entered before form submission. &#x20;
* **`step`** (string): Specifies the time granularity (e.g., steps in seconds).&#x20;

### URL Field

The `url` field is used for inputting valid URLs.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`maxlength`** (string): Sets the maximum number of characters allowed.
* **`minlength`** (string): Specifies the minimum number of characters required.
* **`placeholder`** (string): Provides a hint for the expected input.&#x20;
* **`required`** (boolean): Ensures that a valid URL is entered before form submission.&#x20;

### Week Field

The `week` field allows users to select a specific week within a year.

#### Unique Attributes:

* **`autocomplete`** (string)
* **`max`** (string): Specifies the latest week that can be selected. &#x20;
* **`min`** (string): Specifies the earliest week that can be selected.&#x20;
* **`required`** (boolean): Requires a week to be selected before form submission.&#x20;
* **`step`** (string): Specifies the granularity of week selection.&#x20;

***
