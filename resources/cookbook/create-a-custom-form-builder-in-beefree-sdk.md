---
description: >-
  Learn how to build a custom form builder interface that integrates with
  Beefree SDK, allowing end users to create forms dynamically and add them to
  their email designs.
---

# Create a Custom Form Builder in Beefree SDK

## Why Build a Custom Form Builder?

While [pre-defined default forms](create-a-form-library-in-beefree-sdk.md) are great for common use cases, sometimes your end users need complete flexibility to create custom forms from scratch. A form builder interface lets users:

1. Dynamically add form fields of different types (text, email, select, etc.)
2. Preview forms as they build them
3. Customize field properties like labels and options
4. Save and integrate forms directly into their page and popup designs
5. Reuse form structures across multiple campaigns

With Beefree SDK's `contentDialog.manageForm` handler, you can create a modal-based form builder that seamlessly integrates with the editor workflow.

#### Project Map: Where to Look in the Sample Project

This recipe is based on the [beefree-sdk-form-block-demo](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo) GitHub project. Clone it, then explore these key files:

| File                                                                                                                         | Purpose                              | What You'll Learn                                          |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | ---------------------------------------------------------- |
| [`form-builder-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-builder-example.html) | Complete form builder implementation | How to create a modal-based form builder with live preview |
| [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/proxy-server.js)                     | Authentication proxy server          | How to handle secure Beefree SDK authentication            |
| [`template.json`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/template.json)                         | Base email template                  | How forms integrate with email designs                     |
| [`README.md`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/README.md)                                 | Project documentation                | Understanding the complete form block ecosystem            |

{% hint style="info" %}
**Note:** This form builder uses a modal interface that opens when users click "Edit Form" in the Beefree SDK editor.
{% endhint %}

#### Data Flow Diagram

Here's how the custom form builder integrates with Beefree SDK:

```
+-------------------+        +-------------------+        +-------------------+
|                   |        |                   |        |                   |
| Beefree SDK       | -----> | contentDialog     | -----> | Form Builder      |
| Editor            |        | manageForm        |        | Modal             |
|                   |        |                   |        |                   |
+-------------------+        +-------------------+        +-------------------+
         ^                            |                            |
         |                            |                            |
         |                            v                            v
+-------------------+        +-------------------+        +-------------------+
|                   |        |                   |        |                   |
| Form Integration  | <----- | Form Structure    | <----- | Live Preview      |
| (Drag & Drop)     |        | (JSON)            |        | (Real-time)       |
|                   |        |                   |        |                   |
+-------------------+        +-------------------+        +-------------------+
```

**Why this flow?** The SDK triggers the form builder via `contentDialog`, users build forms with live preview, the structure is saved as JSON, and then integrated back into the email design.

#### Step 1: Clone and Setup

Clone the repository and install dependencies:

```bash
git clone https://github.com/BeefreeSDK/beefree-sdk-form-block-demo.git
cd beefree-sdk-form-block-demo
npm install
```

Create your `.env` file with Beefree SDK credentials:

```env
BEE_CLIENT_ID=your-client-id-here
BEE_CLIENT_SECRET=your-client-secret-here
uid=demo-user
```

#### Step 2: The Form Builder Modal Structure

**File to reference**: [`form-builder-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-builder-example.html) (lines 146-169)

The form builder uses a modal interface with two main sections:

```html
<!-- Custom Modal for Form Builder -->
<div id="form-modal" class="modal-overlay" style="display: none;">
  <div class="modal">
    <h2>Form Builder</h2>
    <div class="form-builder">
      <!-- Field Type Buttons -->
      <div class="field-list">
        <button onclick="addField('text')">Text</button>
        <button onclick="addField('number')">Number</button>
        <button onclick="addField('email')">Email</button>
        <button onclick="addField('date')">Date</button>
        <button onclick="addField('checkbox')">Checkbox</button>
        <button onclick="addField('select')">Select</button>
        <button onclick="addField('textarea')">Textarea</button>
        <button onclick="addField('password')">Password</button>
        <button onclick="addField('file')">File</button>
        <button onclick="addField('submit')">Submit</button>
      </div>
      <!-- Live Preview Area -->
      <div class="form-preview" id="form-preview">
        <!-- Form fields will be added here dynamically -->
      </div>
    </div>
    <button class="save-button" onclick="saveForm()">Save Form</button>
  </div>
</div>
```

#### Step 3: Form Structure Management

**File to reference**: [`form-builder-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-builder-example.html) (lines 213-229)

The form structure is managed as a JavaScript object that gets populated as users add fields:

```js
var formStructure = {
  structure: {
    title: 'Custom Form',
    description: 'This is a custom form built by the user.',
    fields: {},           // Dynamic fields added by user
    layout: [],          // Dynamic layout based on field order
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

#### Step 4: Content Dialog Integration

**File to reference**: [`form-builder-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-builder-example.html) (lines 271-282)

The key integration point is the `contentDialog.manageForm` handler:

```js
beeConfig = {
  // ... other config options
  contentDialog: {
    manageForm: {
      label: 'Edit Form',
      handler: async (resolve, reject, args) => {
        // Open the form builder modal
        openModal();
        
        // Wait for user to build and save form
        await new Promise((res) => {
          window.saveForm = () => {
            resolve(formStructure);  // Return built form structure
            closeModal();            // Close the modal
          };
        });
      }
    }
  },
  defaultForm: formStructure,  // Use the dynamic form structure
  // ... other handlers
};
```

#### Step 5: Dynamic Field Addition

**File to reference**: [`form-builder-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-builder-example.html) (lines 383-417)

The `addField()` function handles dynamic field creation with live preview:

```js
function addField(type) {
  const fieldId = `field-${Date.now()}`;  // Unique field ID
  const fieldLabel = prompt(`Enter label for ${type} field:`, `${type} Field`);

  if (fieldLabel) {
    // Create field definition
    const field = {
      type: type,
      label: fieldLabel,
      canBeRemovedFromLayout: true,
      removeFromLayout: false,
      attributes: {
        required: true,
      },
    };

    // Add options for select fields
    if (type === 'select') {
      field.options = [
        { type: 'option', label: 'Option 1', value: 'option1' },
        { type: 'option', label: 'Option 2', value: 'option2' },
      ];
    }

    // Add to form structure
    formStructure.structure.fields[fieldId] = field;
    formStructure.structure.layout.push([fieldId]);

    // Update live preview
    const formPreview = document.getElementById('form-preview');
    const fieldElement = document.createElement('div');
    fieldElement.className = 'form-field';
    fieldElement.innerHTML = `
      <label>${fieldLabel}</label>
      <input type="${type}" placeholder="${fieldLabel}" />
    `;
    formPreview.appendChild(fieldElement);
  }
}
```

#### Step 6: Field Type Configuration

The form builder supports multiple field types with automatic configuration:

```js
// Text-based fields (text, email, password, etc.)
const textField = {
  type: 'text',
  label: 'Full Name',
  attributes: {
    required: true,
    placeholder: 'Enter your name',
    maxlength: 100
  }
};

// Number fields with validation
const numberField = {
  type: 'number',
  label: 'Age',
  attributes: {
    required: true,
    min: 18,
    max: 100,
    placeholder: 'Enter your age'
  }
};

// Select dropdowns with options
const selectField = {
  type: 'select',
  label: 'Country',
  attributes: { required: true },
  options: [
    { type: 'option', label: 'United States', value: 'us' },
    { type: 'option', label: 'Canada', value: 'ca' },
    { type: 'option', label: 'United Kingdom', value: 'uk' }
  ]
};

// File upload fields
const fileField = {
  type: 'file',
  label: 'Upload Document',
  attributes: {
    accept: '.pdf,.doc,.docx',
    required: false
  }
};
```

#### Step 7: Live Preview System

The form builder includes a real-time preview system that shows users exactly how their form will look:

```js
function updatePreview(fieldId, field) {
  const formPreview = document.getElementById('form-preview');
  const fieldElement = document.createElement('div');
  fieldElement.className = 'form-field';
  fieldElement.id = `preview-${fieldId}`;
  
  let inputHTML = '';
  switch (field.type) {
    case 'select':
      inputHTML = `
        <select>
          ${field.options.map(opt => 
            `<option value="${opt.value}">${opt.label}</option>`
          ).join('')}
        </select>
      `;
      break;
    case 'textarea':
      inputHTML = `<textarea placeholder="${field.label}"></textarea>`;
      break;
    case 'checkbox':
      inputHTML = `<input type="checkbox" /> ${field.label}`;
      break;
    default:
      inputHTML = `<input type="${field.type}" placeholder="${field.label}" />`;
  }
  
  fieldElement.innerHTML = `
    <label>${field.label}</label>
    ${inputHTML}
  `;
  
  formPreview.appendChild(fieldElement);
}
```

#### Step 8: Modal Management

**File to reference**: [`form-builder-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-builder-example.html) (lines 374-381)

Simple modal controls for opening and closing the form builder:

```js
// Modal Functions
function openModal() {
  document.getElementById('form-modal').style.display = 'flex';
  // Clear previous form data
  document.getElementById('form-preview').innerHTML = '';
  formStructure.structure.fields = {};
  formStructure.structure.layout = [];
}

function closeModal() {
  document.getElementById('form-modal').style.display = 'none';
}
```

#### Step 9: Form Validation and Schema

Before saving, you can add validation to ensure the form structure is valid:

```js
function validateFormStructure(structure) {
  // Check required properties
  if (!structure.title || !structure.fields) {
    throw new Error('Form must have a title and fields');
  }
  
  // Validate field types
  const validTypes = ['text', 'email', 'number', 'select', 'checkbox', 'textarea', 'password', 'file', 'submit'];
  for (const [fieldId, field] of Object.entries(structure.fields)) {
    if (!validTypes.includes(field.type)) {
      throw new Error(`Invalid field type: ${field.type}`);
    }
    
    // Validate select fields have options
    if (field.type === 'select' && (!field.options || field.options.length === 0)) {
      throw new Error(`Select field ${fieldId} must have options`);
    }
  }
  
  return true;
}

// Enhanced save function
window.saveForm = () => {
  try {
    validateFormStructure(formStructure.structure);
    resolve(formStructure);
    closeModal();
  } catch (error) {
    alert('Form validation error: ' + error.message);
  }
};
```

#### Step 10: Advanced Field Configuration

For more sophisticated forms, you can enhance the field addition process:

```js
function addAdvancedField(type) {
  const fieldId = `field-${Date.now()}`;
  
  // Show configuration modal for field
  const config = showFieldConfigModal(type);
  
  if (config) {
    const field = {
      type: type,
      label: config.label,
      canBeRemovedFromLayout: config.removable !== false,
      removeFromLayout: false,
      canBeModified: config.modifiable !== false,
      attributes: {
        required: config.required || false,
        placeholder: config.placeholder || '',
        ...config.customAttributes
      }
    };
    
    // Add field-specific configurations
    switch (type) {
      case 'select':
      case 'radio':
        field.options = config.options || [];
        break;
      case 'number':
        if (config.min) field.attributes.min = config.min;
        if (config.max) field.attributes.max = config.max;
        break;
      case 'text':
        if (config.maxlength) field.attributes.maxlength = config.maxlength;
        if (config.pattern) field.attributes.pattern = config.pattern;
        break;
    }
    
    formStructure.structure.fields[fieldId] = field;
    formStructure.structure.layout.push([fieldId]);
    updatePreview(fieldId, field);
  }
}
```

#### Step 11: Running the Form Builder

Start the proxy server:

```bash
node proxy-server.js
```

Open `form-builder-example.html` in your browser:

1. **SDK loads** with authentication via the proxy
2. **Drag a form block** onto the design stage
3. **Click "Edit Form"** to open the form builder modal
4. **Add fields** using the field type buttons
5. **Preview in real-time** as you build your form
6. **Save the form** to integrate it into your page or popup design

#### Step 12: CSS Styling

**File to reference**: [`form-builder-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-builder-example.html) (lines 38-132)

The form builder includes responsive CSS for a custom interface:

```css
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.form-builder {
  display: flex;
  gap: 20px;
}

.field-list {
  width: 200px;
  border: 1px solid #ddd;
  padding: 10px;
  border-radius: 4px;
}

.form-preview {
  flex: 1;
  border: 1px solid #ddd;
  padding: 10px;
  border-radius: 4px;
  min-height: 300px;
}
```

#### Advanced Features

Customize the form builder further with your additions and styling. A few customization examples include:&#x20;

* **Form Templates:** Save commonly used form structures as templates:
* **Field Reordering:** Add drag-and-drop reordering for form fields:

#### Learn More

* Full example project: [beefree-sdk-form-block-demo](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo)
* Form reference documentation: [Form Block Integration](https://docs.beefree.io/beefree-sdk/forms/form-block)
* Content Dialogs: [Custom Dialog Handlers](https://docs.beefree.io/beefree-sdk/getting-started/configuration-object#contentdialog)
* Validation: [Form Schema Validation](https://github.com/BeefreeSDK/beefree-sdk-sample-forms/blob/master/validation%20schema/form_validation_schema.json)

#### Implementation Checklist

* **Set up modal interface** with field buttons and preview area
* **Configure `contentDialog.manageForm`** handler for SDK integration
* **Implement dynamic field addition** with live preview updates
* **Add form validation** for structure integrity
* **Style the interface** for professional appearance
* **Test the complete workflow** from form building to design integration
* **Customize the form builder by adding your own advanced features** like templates and field reordering

Clone the example project, explore the `form-builder-example.html` file, and customize the form builder interface to match your application's needs. Your users will then have a powerful tool for creating custom forms directly within their page and popup designs.
