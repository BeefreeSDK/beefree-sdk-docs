---
description: Explore how to implement customization options for a form's layout.
---

# Form layout customization

{% hint style="info" %}
This feature is available on all [Beefree SDK plan types](https://developers.beefree.io/pricing-plans) and applies only to [Page](../../page-builder/) and [Popup](../../popup-builder/) builders.
{% endhint %}

## Overview

This document outlines how you can customize a form’s layout, and discusses the available layout customization options. These options allow you to adjust various elements of forms to improve your end's user experience creating them. Form layout options ensure your application's end users have more tools to create a more effective presentation of their forms.

Key form layout customization options include:

* **Multiple choice and radio button orientation**: You can adjust the orientation of multiple choice and radio button elements, choosing between horizontal or vertical alignment to suit your design preferences or space constraints.
* **New layout presets**: Three layout presets are available: horizontal, vertical, and grid. These presets define the overall structure of the form, allowing you to easily apply a consistent layout across fields.

The form field width includes the following customization option:

* **Form field width property**: A new boolean property, `fullWidth`, enables you to manage form field widths. When set to `true`, the field will expand to 100% width. When set to `false`, it the field width is set to 50%.

The following video provides a visual representation of these customization options and how they function within the user interface.

{% embed url="https://drive.google.com/file/d/1e8lpahPP0U3LN8nZR4ZIcjdvQWrkHEv3/view?usp=drive_link" %}

## Prerequisites

Prior to getting started, ensure you have the following:

* [Beefree SDK Plan](https://developers.beefree.io/accounts/signup/)
  * Page builder or Popup builder application within your [Dev Console](https://developers.beefree.io/accounts/login/?from=website\_menu)

## Implementing Multiple and Single Choice Orientation

For this implementation, there is a field called `orientation` in the JSON at the field object level. This field controls the layout orientation for multiple-choice and single-choice fields, which include radio buttons and checkboxes. The `orientation` field accepts the following two values:

* **horizontal**
* **vertical**

{% hint style="info" %}
**Default behavior:** If the `orientation` field is not included in the JSON, the form will default to horizontal orientation both on the backend and the frontend.
{% endhint %}

### JSON Structure Example

The following JSON display an example of the updated structure for a radio button field with the `orientation` field included:

```json
{
    "structure": {
        "fields": {
            "gender": {
                "type": "radio",
                "label": "Gender",
                "orientation": "vertical",  // Newly added field for layout orientation
                "attributes": {},
                "options": [
                    {
                        "type": "option",
                        "value": "M",
                        "label": "Male"
                    },
                    {
                        "type": "option",
                        "value": "F",
                        "label": "Female"
                    },
                    {
                        "type": "option",
                        "value": "-",
                        "label": "Not telling"
                    }
                ]
            }
        },
        "layout": [
            [
                "gender"
            ]
        ]
    },
    "attributes": {},
    "style": {
        "labels": {},
        "fields": {},
        "buttons": {}
    }
}
```

### Steps to Configure the Orientation Field in JSON

Take the following steps to configure the `orientation` field:

1. **Locate the form field object in the JSON**: Find the field you want to configure, such as a radio button or checkbox field. This will be under the `"fields"` key within the JSON structure.
2. **Add the `orientation` property**: Inside the field object, add a new property called `orientation`.
3.  **Set the value**: Assign the `orientation` field a value of either `"horizontal"` or `"vertical"`, depending on how you want the options displayed in the form.

    ```json
    "orientation": "vertical"
    ```
4. **Save the changes**: After making the necessary updates to the JSON structure, ensure that the changes are saved.
5. **Test the form**: Once the JSON is updated, test the form to ensure that the options are displayed in the correct orientation. If the field is missing, check if the default horizontal orientation is applied.

These steps will allow you to effectively control the layout orientation of multiple-choice fields in your forms.

### Implementing New Form Layout Presets

The layout of the form fields can be controlled using a new `layoutPreset` field. This field is located in the `structure` object of the JSON and supports four possible values:

* `vertical`
* `horizontal`
* `grid`

{% hint style="info" %}
**Note:** If the `layoutPreset` is not defined, it will use  the layout structure (default behavior).
{% endhint %}

**JSON Structure Example**

Here is an example of a form JSON structure utilizing layout presets:

```json
{
    "structure": {
        "layoutPreset": "grid",  // New field to define form layout
        "fields": {
            "email": {
                "type": "email",
                "label": "Email Address",
                "fullWidth": true,  // Only applicable for 'grid' preset
                "attributes": {}
            }
        }
    },
    "attributes": {},
    "style": {
        "labels": {},
        "fields": {},
        "buttons": {}
    }
}
```

### **Layout Presets**

The following list shows the available options for layout presets.

* **Vertical**: Fields will be stacked vertically, one on top of another.
* **Horizontal**: Fields will be aligned horizontally, side by side.
* **Grid**: Fields will be organized into a grid layout, allowing for more complex positioning.

### Steps to Configure Form Layout Presets in JSON

Take the following steps to configure the `layoutPreset` field:

1. **Locate the `structure` object in the JSON**: Find the `structure` key within the form’s JSON definition where the fields and layout are defined.
2. **Add or modify the `layoutPreset` field**: Inside the `structure` object, add a new property called `layoutPreset`.
3.  **Set the desired value**: Assign the `layoutPreset` field one of the following values to control the layout of the form:

    * `"vertical"`: Stack fields vertically.
    * `"horizontal"`: Align fields horizontally.
    * `"grid"`: Organize fields in a grid format.

    Example:

    ```json
    "layoutPreset": "horizontal"
    ```
4. **Configure field properties (if applicable)**: If you are using the `grid` layout, you may also need to adjust other field properties like `fullWidth` to control the width of individual fields. For example, set `"fullWidth": true` to make a field span the full width of the grid column.
5. **Save and test the form**: After setting the `layoutPreset`, save the updated JSON structure and test the form layout to ensure the fields are displayed according to the selected preset.

By following these steps, you can easily configure and control the layout of your form fields using the new `layoutPreset` field.

## Implementing the `fullWidth` Field

A new boolean field, `fullWidth`, has been introduced within each form field object. This field is applicable only when the layout preset is set to `grid`. If a layout other than `grid` is used, the `fullWidth` field will be ignored or removed from the JSON structure.

In a grid layout, setting `fullWidth` to `true` will cause the form field to span the entire width of the grid column, while setting it to `false` will restrict the field's width to a smaller portion of the grid.

### Steps to Configure the `fullWidth` Field in JSON

Take the following steps to configure the `fullWidth` field:

1. **Ensure the layout preset is set to `grid`**: The `fullWidth` field only functions when the form’s layout preset is set to `"grid"`. Verify that the `"layoutPreset"` field in the JSON is set to `"grid"`.
2. **Locate the desired form field**: In the JSON structure, find the field you want to configure, such as an email or text field.
3. **Add the `fullWidth` field**: Inside the form field object, add a new property called `fullWidth`.
4.  **Set the boolean value**:

    * Set `fullWidth` to `true` to make the form field span the entire width of the grid column.
    * Set `fullWidth` to `false` if you want the form field to occupy half or a portion of the grid column.

    Example:

    ```json
    "fullWidth": true
    ```
5. **Save the changes**: After adding or modifying the `fullWidth` field, save the updated JSON structure.
6. **Test the form in grid layout**: Ensure that the form’s layout is set to `grid` and that the field's width behaves as expected.

By following these steps, you can effectively configure the `fullWidth` property to control the width of form fields in grid layouts.

### **End User Interaction**

* **Layout Widget**: End users can change the layout preset using a layout widget available in the form sidebar.
* **Field Width Widget**: When the form is using the `grid` preset, the `fullWidth` field can be modified by users through a field width widget available in the **Manage Fields** section or the **Edit Form Modal**.

The **Submit** field will always have `fullWidth` set to `true`, and the corresponding widget will be disabled to ensure it spans the full width. For more details on the end user experience, reference the [Form Layout Customization end user documentation](https://docs.beefree.io/end-user-guide/forms/form-layout-customization).&#x20;
