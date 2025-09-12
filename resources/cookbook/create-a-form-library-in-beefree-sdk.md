---
description: >-
  Learn how to create a form library with multiple pre-built forms that users
  can select and drag into their Beefree SDK email designs through a modal
  interface.
---

# Create a Form Library in Beefree SDK

## Why Create a Form Library?

Instead of limiting users to a [single default form](create-a-default-form-in-beefree-sdk.md), a form library provides the best of both worlds. Users can choose from a curated collection of pre-built, industry-specific forms that are ready to use and fully customizable.

A form library is perfect when you want to:

1. **Offer multiple form templates** for different use cases (contact, survey, application, etc.)
2. **Provide industry-specific forms** (auto loans, mortgages, credit cards, etc.)
3. **Maintain consistent branding** across form types
4. **Speed up form creation** with pre-configured field validation and layouts

With Beefree SDK's `contentDialog.manageForm` handler, you can create a modal selection interface that integrates with Beefree SDK's editor.

#### Project Map: Where to Look in the Sample Project

This recipe is based on the [beefree-sdk-form-block-demo](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo) GitHub project. Clone it, then explore these key files:

| File                                                                                                                         | Purpose                              | What You'll Learn                                               |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | --------------------------------------------------------------- |
| [`form-library-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-library-example.html) | Complete form library implementation | How to create multiple pre-defined forms with a selection modal |
| [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/proxy-server.js)                     | Authentication proxy server          | How to handle secure Beefree SDK authentication with LoginV2    |
| [`template.json`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/template.json)                         | Base email template                  | How forms integrate with existing email designs                 |
| [`README.md`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/README.md)                                 | Project documentation                | Understanding the complete form block ecosystem                 |

{% hint style="info" %}
**Note:** This example includes three pre-built forms: Auto Loan Pre-Approval, Mortgage Pre-Approval, and Credit Card Application.
{% endhint %}

#### Data Flow Diagram

Here's how the form library integrates with Beefree SDK:

```
+-------------------+        +-------------------+        +-------------------+
|                   |        |                   |        |                   |
| Beefree SDK       | -----> | contentDialog     | -----> | Form Library      |
| Editor            |        | manageForm        |        | Modal             |
|                   |        |                   |        |                   |
+-------------------+        +-------------------+        +-------------------+
         ^                            |                            |
         |                            |                            |
         |                            v                            v
+-------------------+        +-------------------+        +-------------------+
|                   |        |                   |        |                   |
| Form Integration  | <----- | Selected Form     | <----- | Form Selection    |
| (Drag & Drop)     |        | Structure         |        | (Auto/Mortgage/CC)|
|                   |        |                   |        |                   |
+-------------------+        +-------------------+        +-------------------+
```

**Why this flow?** Beefree SDK triggers the form library through the `contentDialog`, and end users select a pre-built form from the list of available forms within the custom modal. The chosen structure is returned as JSON, and then integrated into the page or popup design.

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

#### Step 2: Form Library Modal Structure

**File to reference**: [`form-library-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-library-example.html) (lines 144-152)

The form library uses a simple modal interface with buttons for each available form:

```html
<!-- Custom Modal for Form Selection -->
<div id="form-modal" class="modal-overlay" style="display: none;">
  <div class="modal">
    <h2>Select Form Type</h2>
    <button onclick="selectForm('autoLoan')">Auto Loan Pre-Approval</button>
    <button onclick="selectForm('mortgage')">Mortgage Pre-Approval</button>
    <button onclick="selectForm('creditCard')">Credit Card Application</button>
  </div>
</div>
```

#### Step 3: Pre-Built Form Definitions

**File to reference**: [`form-library-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-library-example.html) (lines 233-810)

Each form in the library is a complete form structure object. Here's the Auto Loan form example:

```js
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
      submit_button: {
        type: 'submit',
        label: '',
        canBeRemovedFromLayout: false,
        removeFromLayout: false,
        attributes: {
          value: 'CHECK PRE-APPROVAL',
          name: 'submit_button',
        },
      },
    },
    layout: [
      ['full_name'],
      ['credit_score_range'],
      ['car_make_model'],
      ['loan_amount'],
      ['car_type'],
      ['submit_button'],
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

#### Step 4: Content Dialog Integration

**File to reference**: [`form-library-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-library-example.html) (lines 852-878)

The key integration point is the `contentDialog.manageForm` handler with form selection logic:

```js
beeConfig = {
  // ... other config options
  contentDialog: {
    manageForm: {
      label: 'Edit Form',
      handler: async (resolve, reject, args) => {
        // Open the form selection modal
        openModal();
        
        // Wait for user to select a form
        await new Promise((res) => {
          window.selectForm = (formType) => {
            let formStructure;
            
            // Switch between available forms
            switch (formType) {
              case 'autoLoan':
                formStructure = autoLoanForm;
                break;
              case 'mortgage':
                formStructure = mortgageForm;
                break;
              case 'creditCard':
                formStructure = creditCardForm;
                break;
              default:
                reject();  // Cancel if no valid form selected
                return;
            }
            
            resolve(formStructure);  // Return selected form
            closeModal();           // Close the modal
          };
        });
      }
    }
  },
  defaultForm: autoLoanForm,  // Set default form for initial load
  // ... other handlers
};
```

#### Step 5: Form Selection Logic

**File to reference**: [`form-library-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-library-example.html) (lines 857-875)

The `selectForm()` function handles user selection and returns the appropriate form structure:

```js
window.selectForm = (formType) => {
  let formStructure;
  
  switch (formType) {
    case 'autoLoan':
      formStructure = autoLoanForm;
      break;
    case 'mortgage':
      formStructure = mortgageForm;
      break;
    case 'creditCard':
      formStructure = creditCardForm;
      break;
    default:
      reject();  // Invalid selection
      return;
  }
  
  resolve(formStructure);  // Return the selected form structure
  closeModal();           // Close the selection modal
};
```

#### Step 6: Multiple Form Definitions

The library includes three complete form examples, each tailored for different use cases:

**Auto Loan Pre-Approval Form**

* Full name (text input)
* Credit score range (select dropdown)
* Car make and model (text input)
* Loan amount (number input)
* New or used car (radio buttons)
* Submit button

**Mortgage Pre-Approval Form**

```js
var mortgageForm = {
  structure: {
    title: 'Mortgage Pre-Approval',
    description: 'Check if you\'re pre-approved for a mortgage with Modern Bank.',
    fields: {
      full_name: {
        type: 'text',
        label: 'Full Name *',
        attributes: { required: true, placeholder: 'Enter your full name' }
      },
      annual_income: {
        type: 'number',
        label: 'Annual Income *',
        attributes: { required: true, min: 0, placeholder: 'Enter annual income' }
      },
      loan_amount: {
        type: 'number',
        label: 'Loan Amount Requested *',
        attributes: { required: true, min: 0, placeholder: 'Enter loan amount' }
      },
      loan_term: {
        type: 'select',
        label: 'Loan Term *',
        attributes: { required: true },
        options: [
          { type: 'option', label: '15 Years', value: '15' },
          { type: 'option', label: '30 Years', value: '30' }
        ]
      },
      property_type: {
        type: 'text',
        label: 'Property Type *',
        attributes: { required: true, placeholder: 'Enter property type' }
      },
      submit_button: {
        type: 'submit',
        attributes: { value: 'CHECK MORTGAGE PRE-APPROVAL', name: 'submit_button' }
      }
    },
    layout: [
      ['full_name'],
      ['annual_income'],
      ['loan_amount'],
      ['loan_term'],
      ['property_type'],
      ['submit_button']
    ]
  }
};
```

**Credit Card Application Form**

* Full name (text input)
* Credit score range (select dropdown)
* Credit card product (select dropdown)
* Credit limit requested (number input)
* Submit button

#### Step 7: Modal Management

**File to reference**: [`form-library-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-library-example.html) (lines 957-964)

Simple modal controls for the form selection interface:

```js
// Modal Functions
function openModal() {
  document.getElementById('form-modal').style.display = 'flex';
}

function closeModal() {
  document.getElementById('form-modal').style.display = 'none';
}
```

#### Step 8: Default Form Configuration

**File to reference**: [`form-library-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-library-example.html) (line 880)

Set which form appears by default when users first drag a form block:

```js
beeConfig = {
  // ... other config
  defaultForm: autoLoanForm,  // This form appears initially
  // ... other handlers
};
```

#### Step 9: Enhanced Form Library Structure

For a more robust form library, you can organize forms by category:

```js
const formLibrary = {
  financial: {
    autoLoan: {
      name: 'Auto Loan Pre-Approval',
      description: 'Quick pre-approval for vehicle financing',
      structure: autoLoanForm.structure
    },
    mortgage: {
      name: 'Mortgage Pre-Approval', 
      description: 'Home loan pre-qualification form',
      structure: mortgageForm.structure
    },
    creditCard: {
      name: 'Credit Card Application',
      description: 'Apply for a new credit card',
      structure: creditCardForm.structure
    }
  },
  contact: {
    general: {
      name: 'General Contact Form',
      description: 'Basic contact information form',
      structure: contactForm.structure
    },
    support: {
      name: 'Customer Support',
      description: 'Technical support request form',
      structure: supportForm.structure
    }
  },
  marketing: {
    newsletter: {
      name: 'Newsletter Signup',
      description: 'Email newsletter subscription',
      structure: newsletterForm.structure
    },
    survey: {
      name: 'Customer Survey',
      description: 'Feedback and satisfaction survey',
      structure: surveyForm.structure
    }
  }
};
```

#### Step 10: Advanced Modal Interface

Create a more sophisticated selection interface with categories and previews:

```html
<div id="form-modal" class="modal-overlay" style="display: none;">
  <div class="modal large-modal">
    <h2>Select Form Template</h2>
    
    <div class="form-categories">
      <div class="category">
        <h3>Financial Forms</h3>
        <div class="form-options">
          <div class="form-option" onclick="selectForm('autoLoan')">
            <h4>Auto Loan Pre-Approval</h4>
            <p>Quick pre-approval for vehicle financing</p>
            <div class="form-preview">
              <!-- Mini preview of form fields -->
            </div>
          </div>
          <div class="form-option" onclick="selectForm('mortgage')">
            <h4>Mortgage Pre-Approval</h4>
            <p>Home loan pre-qualification form</p>
          </div>
          <div class="form-option" onclick="selectForm('creditCard')">
            <h4>Credit Card Application</h4>
            <p>Apply for a new credit card</p>
          </div>
        </div>
      </div>
      
      <div class="category">
        <h3>Contact Forms</h3>
        <div class="form-options">
          <!-- Additional form options -->
        </div>
      </div>
    </div>
  </div>
</div>
```

#### Step 11: Form Validation and Customization

Add validation to ensure form integrity before selection:

```js
function validateFormStructure(formStructure) {
  if (!formStructure || !formStructure.structure) {
    throw new Error('Invalid form structure');
  }
  
  const { title, fields, layout } = formStructure.structure;
  
  if (!title || !fields || !layout) {
    throw new Error('Form must have title, fields, and layout');
  }
  
  // Validate that all layout fields exist in fields definition
  const layoutFields = layout.flat();
  const fieldKeys = Object.keys(fields);
  
  for (const layoutField of layoutFields) {
    if (!fieldKeys.includes(layoutField)) {
      throw new Error(`Layout references undefined field: ${layoutField}`);
    }
  }
  
  return true;
}

// Enhanced selection with validation
window.selectForm = (formType) => {
  let formStructure;
  
  try {
    switch (formType) {
      case 'autoLoan':
        formStructure = autoLoanForm;
        break;
      case 'mortgage':
        formStructure = mortgageForm;
        break;
      case 'creditCard':
        formStructure = creditCardForm;
        break;
      default:
        throw new Error('Invalid form type selected');
    }
    
    validateFormStructure(formStructure);
    resolve(formStructure);
    closeModal();
  } catch (error) {
    alert('Form selection error: ' + error.message);
  }
};
```

#### Step 12: Running the Form Library

1. Start the proxy server:

```bash
node proxy-server.js
```

2. Open `form-library-example.html` in your browser:
   1. **SDK loads** with authentication via the proxy
   2. **Drag a form block** onto the design stage
   3. **Click "Edit Form"** to open the form library modal
   4. **Select a form type** from the available options
   5. **Form integrates** automatically into your email design
   6. **Customize as needed** using Beefree SDK's form editing tools

#### Step 13: CSS Styling for Professional Appearance

**File to reference**: [`form-library-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-library-example.html) (lines 38-130)

The form library includes professional styling for the modal interface:

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

.modal {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  width: 300px;
  text-align: center;
}

.modal button {
  background: #d32f2f;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
  margin: 5px;
  font-size: 14px;
  width: 100%;
}

.modal button:hover {
  background: #b71c1c;
}
```

#### Advanced Features

You can build upon your integration and also add the following and more to further customize your end user's experience:&#x20;

* **Dynamic Form Loading:** Load forms from an external API or database:
* **Form Search and Filtering:** Add search functionality to large form libraries:
* **Form Analytics:** Track which forms are most popular:

#### Learn More

* Full example project: [beefree-sdk-form-block-demo](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo)
* API docs: [Form Block Integration](https://docs.beefree.io/beefree-sdk/forms/form-block)
* Content Dialogs: [Custom Dialog Handlers](https://docs.beefree.io/beefree-sdk/getting-started/configuration-object#contentdialog)

#### Implementation Checklist

* **Define multiple form structures** with complete field definitions
* **Create modal selection interface** with form options
* **Configure `contentDialog.manageForm`** handler for SDK integration
* **Implement form selection logic** with proper validation
* **Set default form** for initial drag-and-drop experience
* **Style the interface** for professional appearance
* **Test complete workflow** from selection to email integration
* **Consider advanced features** like categories, search, and analytics

Clone the example project, explore the `form-library-example.html` file, and customize the form library to match your specific industry needs. Your users will have quick access to professional, pre-built forms that can be easily integrated into their email campaigns.
