# Form Validation Schema

## Introduction

Schemas are structured definitions that describe the format, rules, and relationships of data within a system. They ensure consistency and validate inputs. The Form Schema defines the structure and properties of form elements, including fields, layouts, and attributes. This documentation breaks down the schema’s properties, usage examples, and key considerations for implementation.

### Schema Overview

This section summarizes the purpose and key characteristics of the Form Schema.

**Schema Name:** Form Schema\
**Purpose:** Defines the structure of forms, including fields, layouts, and form-level attributes.\
**Mandatory Fields:** `fields`\
**Related Schemas:**

* Used alongside field-specific schemas to define input types and their properties.

### Structure Definition

Reference the [Beefree SDK validation schema in GitHub](https://github.com/BeefreeSDK/beefree-sdk-sample-forms/tree/master/validation%20schema) for the full list of properties.

### Field Descriptions

The following table lists the field descriptions along with their corresponding data type, whether or not they are mandatory, and their description.

| Property      | Type   | Required | Description                                                  |
| ------------- | ------ | -------- | ------------------------------------------------------------ |
| `title`       | string | No       | The title of the form.                                       |
| `description` | string | No       | A description of the form.                                   |
| `fields`      | object | **Yes**  | Defines the form fields and their properties.                |
| `layout`      | array  | No       | Specifies the arrangement of fields in the form.             |
| `attributes`  | object | No       | Form-level attributes (e.g., `action`, `method`, `enctype`). |

**`fields` Property**

* **Type:** Object with dynamic keys matching the pattern `^[a-zA-Z0-9_-]+$`.
* Each field must include:
  * `type` (string, required): The input type (e.g., `text`, `email`, `checkbox`).
  * `label` (string, optional): The display label for the field.
  * `canBeRemovedFromLayout` (boolean, optional): Whether the field can be removed from the layout.
  * `removeFromLayout` (boolean, optional): Whether the field is excluded from the layout.
  * `attributes` (object, optional): Field-specific HTML attributes.
  * `options` (object/array, optional): Used for fields like `select`, `radio`, etc.

**`layout` Property**

* **Type:** Array of arrays or objects.
* Defines the visual arrangement of fields.
* Can include:
  * Simple arrays of field names (e.g., `["field1", "field2"]`).
  * Objects with `legend` (string) and `fields` (array of arrays) for grouped sections.

**`attributes` Property**

* **Type:** Object.
* Defines form-level HTML attributes.
* **Required:** `action` (string).
* Other optional properties include `method`, `enctype`, `target`, etc.

### Usage Example

This section demonstrates a comprehensive auto loan pre-approval form definition that showcases the full capabilities of the form specification. The example includes various field types, layout configurations, and form attributes to illustrate a real-world implementation.

#### **Auto Loan Pre-Approval Form Example**

The following example represents a complete auto loan application form, featuring:

* Multiple field types (text, select, radio, number, submit)
* Required field validation
* Conditional layout controls
* Comprehensive form attributes
* Demonstration of all supported HTML input types (even those hidden from the main layout)

```javascript
var autoLoanForm = {
  structure: {
    title: 'Auto Loan Pre-Approval',
    description: 'Check if you\'re pre-approved for an auto loan with Modern Bank.',
    fields: {
      full_name: {
        type: 'text',
        label: 'Full Name *',
        canBeRemovedFromLayout: true,
        removeFromLayout: false,
        canBeModified: true,
        attributes: {
          required: true,
          placeholder: 'Enter your full name',
        },
      },
      credit_score_range: {
        type: 'select',
        label: 'Credit Score Range *',
        canBeRemovedFromLayout: false,
        removeFromLayout: false,
        attributes: {
          required: true,
        },
        options: [
          { type: 'option', label: '300-579', value: '300-579' },
          { type: 'option', label: '580-669', value: '580-669' },
          { type: 'option', label: '670-739', value: '670-739' },
          { type: 'option', label: '740-799', value: '740-799' },
          { type: 'option', label: '800-850', value: '800-850' },
        ],
      },
      car_make_model: {
        type: 'text',
        label: 'Car Make and Model *',
        canBeRemovedFromLayout: false,
        removeFromLayout: false,
        attributes: {
          required: true,
          placeholder: 'Enter car make and model',
        },
      },
      loan_amount: {
        type: 'number',
        label: 'Loan Amount Requested *',
        canBeRemovedFromLayout: false,
        removeFromLayout: false,
        attributes: {
          required: true,
          min: 0,
          placeholder: 'Enter loan amount',
        },
      },
      car_type: {
        type: 'radio',
        label: 'New or Used Car *',
        canBeRemovedFromLayout: false,
        removeFromLayout: false,
        attributes: {
          required: true,
        },
        options: [
          { type: 'option', label: 'New', value: 'new' },
          { type: 'option', label: 'Used', value: 'used' },
        ],
      },
      // ... [rest of the form definition]
    },
    layout: [
      ['full_name'],
      ['credit_score_range'],
      ['car_make_model'],
      ['loan_amount'],
      ['car_type'],
      ['submit_button'],
      // Hidden fields demonstration
      ['number'],
      ['longtext'],
      ['datalist'],
      // ... [other hidden fields]
    ],
    attributes: {
      'accept-charset': 'UTF-8',
      action: 'http://example.com/read-form-script',
      autocomplete: 'on',
      enctype: 'multipart/form-data',
      method: 'post',
      novalidate: false,
      target: '_self',
    },
  },
};
```

**Structure Object Breakdown**

The `structure` object contains all form configuration elements:

1. **Metadata**:
   * `title`: Form header displayed to users
   * `description`: Explanatory text about the form's purpose
2. **Fields Configuration**:
   * Each field has type-specific properties and attributes
   * Includes layout control flags (`canBeRemovedFromLayout`, `removeFromLayout`)
   * Supports all HTML input types (demonstrated in hidden fields)
   * Required field validation through attributes
3. **Layout Management**:
   * The `layout` array defines the visual organization of fields
   * Supports multi-column layouts through nested arrays
   * Hidden fields are included in definition but removed from display
4. **Form Attributes**:
   * Comprehensive HTML form attributes
   * Supports modern features like charset declaration and autocomplete
   * Configurable submission handling (method, enctype, target)

### Additional Considerations

Consider the following when using the Form Schema:

* **Dynamic Fields:** Use `patternProperties` to validate field names.
* **Extensibility:** Custom attributes can be added under `data-*` patterns.
* **Layout Flexibility:** Use arrays or objects in `layout` for simple or grouped arrangements.
