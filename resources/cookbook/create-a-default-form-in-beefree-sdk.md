---
description: >-
  Learn how to configure a default form in Beefree SDK that users can drag and
  drop onto the design stage, complete with pre-defined fields and validation.
---

# Create a Default Form in Beefree SDK

## Why Use Default Forms?

When building email campaigns, forms are essential for collecting user data like newsletter signups, survey responses, or contact information. Email recipients are typically led to these forms by clicking on a CTA (call-to-action) within the email that redirects to a landing page with the form within it. In Beefree SDK, forms can be built in both the page and popup builders. Instead of making your end users build forms from scratch every time they want to embed one within their page or popup design, you can pre-configure a default form with common field types and layouts. This default form will appear each time your end users drag and drop the Form block onto the stage for their page or popup design. Having a default form saves your end users time, and ensures consistency across content assets for their email campaigns.

With Beefree SDK's `defaultForm` configuration, you can:

1. **Pre-define common form structures** (contact forms, surveys, registrations)
2. **Set up field validation rules** (required fields, input types, placeholders)
3. **Enable drag-and-drop functionality** so users can easily add forms to their designs
4. **Configure form behavior** with custom handlers for save, submit, and change events

#### Project Map: Where to Look in the Sample Project

This recipe is based on the [beefree-sdk-form-block-demo](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo) GitHub project. Clone it, then explore these key files:

| File                                                                                                                         | Purpose                            | What You'll Learn                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- | ----------------------------------------------------------------------- |
| [`default-form-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/default-form-example.html) | Single default form implementation | How to configure `beeConfig.defaultForm` with a complete form structure |
| [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/proxy-server.js)                     | Node.js authentication proxy       | How to securely authenticate with Beefree SDK using LoginV2             |
| [`template.json`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/template.json)                         | Email template structure           | How forms integrate with existing email designs                         |
| [`form-library-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-library-example.html) | Multiple form library              | How to implement form selection via content dialogs                     |

{% hint style="info" %}
**Note:** Use this working project and its core concepts to implement default forms in your host application.
{% endhint %}

#### Data Flow Diagram

Here's how the default form system works:

```
+-------------------+        +-------------------+        +-------------------+
|                   |        |                   |        |                   |
| beeConfig Setup   | -----> |   Beefree SDK     | -----> |  Form Block.      |
| (defaultForm)     |        |   (Editor)        |        |  (Drag & Drop)    |
|                   |        |                   |        |                   |
+-------------------+        +-------------------+        +-------------------+
         |                            |                            |
         |                            |                            |
         v                            v                            v
+-------------------+        +-------------------+        +-------------------+
|                   |        |                   |        |                   |
| Form Structure    |        | User Interaction  |        | Event Handlers    |
| (fields, layout,  |        | (edit, validate,  |        | (onChange, onSave)|
|  attributes)      |        |  submit)          |        |                   |
+-------------------+        +-------------------+        +-------------------+
```

**Why this flow?** The `defaultForm` configuration provides the initial form structure, and Beefree SDK handles user interactions and form editing. The event handlers track form changes, and saves the Form as part of the design's JSON.

#### Step 1: Clone the Project

Clone the repository and install dependencies:

```bash
git clone https://github.com/BeefreeSDK/beefree-sdk-form-block-demo.git
cd beefree-sdk-form-block-demo
npm install
```

Create a `.env` file with your Beefree SDK credentials:

```env
BEE_CLIENT_ID=your-client-id-here
BEE_CLIENT_SECRET=your-client-secret-here
uid=demo-user
```

#### Step 2: The Proxy Server Setup

**File to reference**: [`proxy-server.js`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/proxy-server.js)

The proxy server handles secure authentication with Beefree SDK:

```js
// proxy-server.js
app.post('/proxy/bee-auth', async (req, res) => {
  try {
    const { uid } = req.body;
    const response = await axios.post(
      'https://auth.getbee.io/loginV2',
      {
        client_id: process.env.BEE_CLIENT_ID,
        client_secret: process.env.BEE_CLIENT_SECRET,
        uid: uid || 'demo-user'
      },
      { headers: { 'Content-Type': 'application/json' } }
    );
    res.json(response.data);
  } catch (error) {
    res.status(500).json({ error: 'Failed to authenticate' });
  }
});
```

{% hint style="info" %}
**Security Note:** Keep your credentials server-side—never expose your Client Secret to the browser.
{% endhint %}

#### Step 3: Default Form Configuration

**File to reference**: [`default-form-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/default-form-example.html)

The heart of the default form setup is the `beeConfig.defaultForm` object:

```js
var beeConfig = {
  container: 'bee-plugin-container',
  language: 'en-US',
  trackChanges: true,
  defaultForm: {
    structure: {
      title: "Auto Loan Pre-Approval",
      description: "Check if you're pre-approved for an auto loan with Modern Bank.",
      fields: {
        full_name: {
          type: "text",
          label: "Full Name *",
          canBeRemovedFromLayout: true,
          removeFromLayout: false,
          canBeModified: true,
          attributes: {
            required: true,
            placeholder: "Enter your full name",
          },
        },
        credit_score_range: {
          type: "select",
          label: "Credit Score Range *",
          canBeRemovedFromLayout: false,
          removeFromLayout: false,
          canBeModified: true,
          attributes: {
            required: true,
          },
          options: [
            { type: "option", label: "300-579", value: "300-579" },
            { type: "option", label: "580-669", value: "580-669" },
            { type: "option", label: "670-739", value: "670-739" },
            { type: "option", label: "740-799", value: "740-799" },
            { type: "option", label: "800-850", value: "800-850" },
          ],
        },
        // ... more fields
      },
      layout: [
        ["full_name"],
        ["credit_score_range"],
        ["car_make_model"],
        ["loan_amount"],
        ["car_type"],
        ["submit_button"],
      ],
      attributes: {
        "accept-charset": "UTF-8",
        action: "http://example.com/read-form-script",
        autocomplete: "on",
        enctype: "multipart/form-data",
        method: "post",
        novalidate: false,
        target: "_self",
      },
    },
    // Event handlers...
  }
};
```

#### Step 4: Form Structure Breakdown

The `defaultForm.structure` object contains three main components:

**Fields Definition**

Each field is defined with:

* **`type`**: Input type (text, select, radio, checkbox, etc.)
* **`label`**: Display label for the field
* **`attributes`**: HTML attributes (required, placeholder, min, max, etc.)
* **`options`**: For select/radio/checkbox fields
* **`canBeRemovedFromLayout`**: Whether users can remove this field
* **`canBeModified`**: Whether users can edit field properties

**Layout Array**

A 2D array that defines field arrangement:

```js
layout: [
  ["full_name"],           // Single field per row
  ["first_name", "last_name"], // Multiple fields per row
  ["submit_button"]
]
```

**Form Attributes**

Standard HTML form attributes:

```js
attributes: {
  action: "http://example.com/submit-form",
  method: "post",
  enctype: "multipart/form-data",
  autocomplete: "on"
}
```

Reference the full [Form Validation Schema in GitHub](https://github.com/BeefreeSDK/beefree-sdk-sample-forms/blob/master/validation%20schema/form_validation_schema.json).

#### Step 5: Event Handlers

**File to reference**: [`default-form-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/default-form-example.html) (lines 307-329)

Configure event handlers to manage form interactions:

```js
defaultForm: {
  structure: { /* ... */ },
  onChange: function (jsonFile, response) {
    console.log('Form changed:', jsonFile);
    console.log('Response:', response);
  },
  onSave: function (jsonFile, htmlFile) {
    // Save the form as HTML
    save('newsletter.html', htmlFile);
  },
  onSaveAsTemplate: function (jsonFile) {
    // Save as JSON template
    save('newsletter-template.json', jsonFile);
  },
  onAutoSave: function (jsonFile) {
    // Auto-save functionality
    console.log(new Date().toISOString() + ' autosaving...');
    window.localStorage.setItem('newsletter.autosave', jsonFile);
  },
  onSend: function (htmlFile) {
    // Handle test email sending
    const email = document.getElementById('integrator-test-emails').value;
    if (email) alert(`Would send test email to: ${email}`);
    else alert("Please enter an email address");
  },
  onError: function (errorMessage) {
    // Handle errors
    console.error('Form Error:', errorMessage);
  }
}
```

#### Step 6: Field Types and Validation

The default form supports various field types with built-in validation:

```js
// Text input with validation
full_name: {
  type: "text",
  label: "Full Name *",
  attributes: {
    required: true,
    placeholder: "Enter your full name",
    maxlength: 100
  }
},

// Number input with range
loan_amount: {
  type: "number",
  label: "Loan Amount *",
  attributes: {
    required: true,
    min: 1000,
    max: 100000,
    placeholder: "Enter amount"
  }
},

// Select dropdown
credit_score: {
  type: "select",
  label: "Credit Score Range *",
  attributes: { required: true },
  options: [
    { type: "option", label: "Excellent (750+)", value: "excellent" },
    { type: "option", label: "Good (650-749)", value: "good" },
    { type: "option", label: "Fair (550-649)", value: "fair" }
  ]
},

// Radio buttons
car_type: {
  type: "radio",
  label: "Vehicle Type *",
  attributes: { required: true },
  options: [
    { type: "option", label: "New", value: "new" },
    { type: "option", label: "Used", value: "used" }
  ]
}
```

#### Step 7: Making the Form Draggable

Once configured, the default form automatically becomes available in the Beefree SDK editor:

1. **Form Block**: Users can drag a Form block from the content panel
2. **Pre-populated**: The form appears with your default structure
3. **Editable**: Users can modify fields, layout, and styling
4. **Validation**: Built-in validation based on your field definitions

#### Step 8: Running the Example

1. Start the proxy server:

```bash
node proxy-server.js
```

2. Open `default-form-example.html` in your browser. You'll see:
   1. The Beefree SDK editor loads with authentication
   2. A pre-configured form is available in the form block
   3. Users can drag the form block onto the design stage
   4. The form includes all your predefined fields and validation

#### Advanced Configuration: Multiple Forms

If you are interested in providing your end users with a Form library of pre-existing forms they can choose from, reference the [Create a Form Library in Beefree SDK documentation](create-a-form-library-in-beefree-sdk.md).

You can also reference the GitHub sample project's code to see how it is implemented: [`form-library-example.html`](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo/blob/main/form-library-example.html)

#### Learn More

* Full example project: [beefree-sdk-form-block-demo](https://github.com/BeefreeSDK/beefree-sdk-form-block-demo)
* Form documentation: [Form Block Configuration](https://docs.beefree.io/beefree-sdk/forms/form-block)
* Authentication: [Authorization Guide](../../getting-started/readme/installation/authorization-process-in-detail.md)

#### Implementation Checklist

* **Set up proxy server** for secure authentication
* **Configure `defaultForm.structure`** with fields and layout
* **Add event handlers** for form interactions
* **Define field validation** with HTML5 attributes
* **Test drag-and-drop** functionality in the editor
* **Handle form submissions** in your application

Clone the example project, explore the `default-form-example.html` file, and adapt the `defaultForm` configuration to match your specific form requirements. The pre-configured form will then be available as a draggable block in your Beefree SDK editor.
