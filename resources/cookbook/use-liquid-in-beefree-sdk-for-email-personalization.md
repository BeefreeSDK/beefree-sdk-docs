---
description: >-
  This recipe explains how you can use Liquid in Beefree SDK to support advanced
  email personalization options for your end users.
---

# Use Liquid in Beefree SDK for Email Personalization

## Overview

This project showcases how to configure [Beefree SDK's](https://docs.beefree.io/beefree-sdk) email editor with [Liquid](https://shopify.github.io/liquid/) templating for dynamic and personalized email content. Built with React and the `@beefree.io/sdk` [npm package](https://www.npmjs.com/package/@beefree.io/sdk), it's designed for developers and teams who need to customize Beefree SDK's email builder for end users who need to create sophisticated and highly personalized email campaigns that include conditional content and product loops.

This project is designed for:

* **Email Developers** who need advanced personalization features
* **Marketing Teams** creating dynamic, data-driven campaigns
* **Developers** integrating advanced email functionality into their applications
* **Agencies** building advanced custom email solutions for clients

Reference the project code in the [beefree-liquid-email-personalization](use-liquid-in-beefree-sdk-for-email-personalization.md) GitHub repository.&#x20;

{% embed url="https://github.com/BeefreeSDK/beefree-liquid-email-personalization" %}

## Getting Started

This section includes what you need to get started with the project.

### Prerequisites

* Node.js (v16 or higher)
* npm or yarn
* Beefree SDK credentials

### Installation

1. Clone the repository:

```bash
git clone https://github.com/BeefreeSDK/beefree-liquid-email-personalization.git
cd Liquid
```

2. Install dependencies:

```bash
npm install
```

3. Set up environment variables:

```bash
# Create .env file with your Beefree credentials
BEE_CLIENT_ID=your_client_id
BEE_CLIENT_SECRET=your_client_secret
BEE_API_KEY=your_api_key # Optional for Importing HTML if wanted
```

4. Start the development servers:

```bash
# Start both the proxy server and React dev server
npm start

# Or start them separately:
npm run server  # Starts proxy server on port 3001
npm run dev     # Starts React dev server on port 3000
```

5. Open your browser to `http://localhost:3000`

#### Development

The application uses:

* **Vite**: Fast React development server
* **React**: Modern UI framework
* **@beefree.io/sdk**: Official Beefree SDK npm package
* **Proxy Server**: Backend for authentication and API calls

The React app runs on port 3000 and proxies API calls to the backend server on port 3001.

#### Configuration

The main configuration is in `src/App.jsx`. Key areas you can customize:

* **Merge Tags**: Add your custom data fields in the `MERGE_TAGS` array
* **Display Conditions**: Create conditional logic for your use cases in `getDisplayUseCases()`
* **Custom Rows**: Define your pre-built [rows](../../rows/reusable-content/create/pre-build/implement-custom-rows.md) in the `rowsConfiguration`
* **Content Dialogs**: Build custom user interfaces in `makeContentDialog()`

### Additional Resources

For questions and support:

* Check the [Beefree SDK documentation](https://docs.beefree.io/)
* Review the [Liquid documentation](https://shopify.github.io/liquid/)

### What's Included

This section list what's included within this project.

* [**React Application**](use-liquid-in-beefree-sdk-for-email-personalization.md): Modern React-based email editor
* [**Beefree SDK Integration**](https://www.npmjs.com/package/@beefree.io/sdk): Using the official `@beefree.io/sdk` npm package
* [**Liquid Templating**](https://shopify.github.io/liquid/): Support for dynamic content and personalization
* [**Display Conditions**](../../other-customizations/advanced-options/display-conditions.md): Conditional content based on customer data
* [**Custom Rows**](../../rows/reusable-content/create/pre-build/implement-custom-rows.md): Pre-built email templates with Liquid integration
* [**Content Dialogs**](../../other-customizations/advanced-options/content-dialog.md): Custom modals for enhanced user experience
* [**Merge Tags**](../../other-customizations/advanced-options/special-links-and-merge-tags.md): Drag-and-drop personalization fields
* [**Product Loops**](https://support.beefree.io/hc/en-us/articles/20739290016914-Adding-Dynamic-Content-in-Beefree-for-Klaviyo): Dynamic product recommendations and abandoned cart items

#### File Structure

This project has the following file structure.

```
Liquid/
├── src/
│   ├── App.jsx              # Main React component with Beefree SDK integration
│   ├── main.jsx             # React entry point
│   └── index.css            # Application styles
├── public/
│   └── template.json        # Default email template
├── index.html               # HTML entry point for React app
├── vite.config.js           # Vite configuration
├── proxy-server.js          # Backend server for authentication and API calls
├── package.json             # Node.js dependencies
└── README.md                # This file
```

## Liquid Overview

[Liquid](https://shopify.github.io/liquid/) is a template language created by Shopify that allows you to create dynamic content by embedding simple logic and variables into your templates. It's widely used in email marketing for personalization and conditional content.

#### Key Liquid Features in this Project

The following list shows a few examples of Liquid used in this project.

* **Variables**: `{{ customer.first_name }}`
* **Conditionals**: `{% if customer.is_vip %}...{% endif %}`
* **Loops**: `{% for product in products %}...{% endfor %}`
* **Filters**: `{{ product.price | money }}`
* **Comments**: `{% comment %}...{% endcomment %}`

#### Why Liquid for Email?

Liquid is particularly well-suited for email personalization because it:

* Supports complex conditional logic
* Handles loops for dynamic content (products, recommendations)
* Provides built-in filters for formatting
* Is language-agnostic and widely supported
* Integrates well with CRM and e-commerce platforms

### Beefree SDK

Beefree SDK is a JavaScript library that provides a complete email editor experience. It's designed to be embedded into web applications, offering a visual drag-and-drop interface for creating professional email campaigns. This project uses the official `@beefree.io/sdk` [npm package](https://www.npmjs.com/package/@beefree.io/sdk) for modern React integration.

#### Key Capabilities

* **Visual Editor**: Intuitive drag-and-drop interface
* **Responsive Design**: Mobile-first email creation
* **Template Library**: Pre-built templates and components
* **Custom Content**: Support for custom rows and modules
* **API Integration**: Suite of different APIs for extending the builder's functionality
* **Multi-language**: Language-agnostic implementation

## Beefree SDK and Liquid

The combination of Beefree SDK and Liquid creates a powerful email personalization platform:

1. **Visual Editing**: Users can design emails visually while incorporating dynamic content
2. **Real-time Preview**: See how personalization will look with sample data
3. **Flexible Logic**: Complex conditional content and loops
4. **Scalable**: Handle complex personalization rules
5. **Developer-Friendly**: Easy to integrate and customize

## Project Implementation

This section outlines and describes the Beefree SDK and Liquid integration.

### Beefree SDK Configuration

The `beeConfig` includes [merge tags](../../other-customizations/advanced-options/smart-merge-tags.md), [display conditions](../../other-customizations/advanced-options/display-conditions.md), [content dialogs](../../other-customizations/advanced-options/content-dialog.md), and custom modals. The following code snippet shows an example of how these features come together in the React implementation:

```javascript
import BeefreeSDK from '@beefree.io/sdk';

// Beefree SDK configuration
const beeConfig = {
  container: 'beefree-sdk-container',
  language: 'en-US',
  enabledAdvancedPreview: true,
  trackChanges: true,
  
  // Merge tags for personalization
  mergeTags: MERGE_TAGS,
  
  // Content dialog for custom functionality
  contentDialog: {
    rowDisplayConditions: {
      label: 'Display Conditions',
      handler: async function(resolve, reject) {
        // Custom modal implementation
      }
    },
    externalContentURLs: {
      label: 'Load Custom Rows',
      handler: function(resolve, reject) {
        // Custom rows loading
      }
    }
  },
  
  // Rows configuration
  rowsConfiguration: {
    emptyRows: true,
    defaultRows: true,
    selectedRowType: 'Personalization Rows',
    externalContentURLs: [
      {
        name: 'Beefree SDK Demo Custom Rows',
        value: 'https://qa-bee-playground-backend.getbee.io/api/customrows/?ids=1,2,3,4'
      }
    ]
  }
};

// Initialize the editor using the constructor and start method
const BeefreeSDKInstance = new BeefreeSDK(v2Token);
const instance = await BeefreeSDKInstance.start(beeConfig, templateJson, '', { shared: false });
```

### Merge Tags Integration

[Merge tags](../../other-customizations/advanced-options/smart-merge-tags.md) provide personalization fields that can easily be added to email designs by end users on the frontend:

```javascript
const MERGE_TAGS = [
  // Customer data
  { name: "{{ customer.first_name }}", value: "{{ customer.first_name }}" },
  { name: "{{ customer.email }}", value: "{{ customer.email }}" },
  { name: "{{ customer.favorite_color }}", value: "{{ customer.favorite_color }}" },
  
  // Order data
  { name: "{{ last_order.total_price | money }}", value: "{{ last_order.total_price | money }}" },
  
  // Product data (for loops)
  { name: "{{ item.product_name }}", value: "{{ item.product_name }}" },
  { name: "{{ item.price | money }}", value: "{{ item.price | money }}" },
  
  // Shop data
  { name: "{{ shop.name }}", value: "{{ shop.name }}" }
];
```

### Display Conditions

[Display conditions](../../other-customizations/advanced-options/display-conditions.md) allow for conditional rules to be wrapped around [rows](../../rows/reusable-content/) within designs inside of the email builder. The following code snippet displays an example of conditional rules implemented within this project.&#x20;

```javascript
function getDisplayUseCases() {
  return [
    {
      type: 'Personalization',
      name: 'Display if favorite color = green',
      description: 'Show row only to customers who prefer green',
      before: "{% if customer.favorite_color == 'green' %}",
      after: '{% endif %}'
    },
    {
      type: 'Personalization',
      name: 'Loop — Abandoned cart items',
      description: 'Repeat row for each item in abandoned cart',
      before: '{% for item in customer.abandoned_cart %}',
      after: '{% endfor %}'
    },
    {
      type: 'Personalization',
      name: 'Display if VIP',
      description: 'Show row only for VIP customers',
      before: '{% if customer.is_vip %}',
      after: '{% endif %}'
    }
  ];
}
```

### Custom Content Dialog

The [content dialog](../../other-customizations/advanced-options/content-dialog.md) provides a custom modal for selecting display conditions:

```javascript
function makeContentDialog() {
  return {
    rowDisplayConditions: {
      label: 'Display Conditions',
      handler: async function(resolve, reject) {
        try {
          const result = await openUseCaseModal(getDisplayUseCases());
          resolve(result);
        } catch (e) {
          reject(e);
        }
      }
    }
  };
}
```

## Customization Guide

This section discusses how you can customize the code within this project to experiement with adding your own dynamic content use cases.

### Creating Custom Modals

The following code shows an example custom modal that integrates the Beefree SDK [content dialog](../../other-customizations/advanced-options/content-dialog.md):

```javascript
function openUseCaseModal(items) {
  return new Promise((resolve, reject) => {
    const modal = document.createElement('div');
    modal.className = 'modal';
    
    const list = items.map((it, idx) => `
      <label style="display:block;border:1px solid var(--border);border-radius:10px;padding:10px;margin-bottom:8px;background:#0a122e">
        <div style="display:flex;gap:10px;align-items:flex-start">
          <input type="radio" name="ucase" value="${idx}" style="margin-top:4px" />
          <div>
            <div style="font-weight:800">${it.name}</div>
            <div style="color:#94a3b8;margin:4px 0">${it.description}</div>
            <pre style="white-space:pre-wrap;background:#0b1230;border:1px dashed #233159;border-radius:8px;padding:8px;">before: ${it.before}\nafter:  ${it.after}</pre>
          </div>
        </div>
      </label>`).join('');
    
    modal.innerHTML = `
      <div class="modal-content">
        <h3 style="margin-bottom:8px">Select a display condition</h3>
        <div style="max-height:420px;overflow:auto">${list}</div>
        <div class="modal-actions">
          <button id="uc-cancel" class="btn">Cancel</button>
          <button id="uc-select" class="btn primary">Select</button>
        </div>
      </div>`;
    
    document.body.appendChild(modal);
    modal.style.display = 'block';
    
    // Event handlers
    modal.querySelector('#uc-cancel').onclick = () => {
      modal.remove();
      reject(new Error('cancelled'));
    };
    
    modal.querySelector('#uc-select').onclick = () => {
      const checked = modal.querySelector('input[name="ucase"]:checked');
      if (!checked) {
        modal.remove();
        reject(new Error('no_selection'));
        return;
      }
      const idx = Number(checked.value);
      const it = items[idx];
      modal.remove();
      resolve({
        type: it.type,
        label: it.name,
        description: it.description,
        before: it.before,
        after: it.after
      });
    };
  });
}
```

### Adding New Merge Tags

To add new merge tags for different data sources:

```javascript
// Add to MERGE_TAGS array
const MERGE_TAGS = [
  // Existing tags...
  
  // New custom tags
  { name: "{{ customer.loyalty_points }}", value: "{{ customer.loyalty_points }}" },
  { name: "{{ customer.last_purchase_date }}", value: "{{ customer.last_purchase_date | date: '%B %d, %Y' }}" },
  { name: "{{ campaign.name }}", value: "{{ campaign.name }}" },
  { name: "{{ store.location }}", value: "{{ store.location }}" }
];
```

### Custom Display Conditions

Create new display conditions for different use cases:

```javascript
function getCustomDisplayUseCases() {
  return [
    {
      type: 'Loyalty',
      name: 'High-value customers',
      description: 'Show content only to customers with 1000+ loyalty points',
      before: '{% if customer.loyalty_points >= 1000 %}',
      after: '{% endif %}'
    },
    {
      type: 'Geography',
      name: 'Local store promotion',
      description: 'Show store-specific content based on location',
      before: "{% if customer.default_address.city == 'New York' %}",
      after: '{% endif %}'
    },
    {
      type: 'Behavior',
      name: 'Recent purchasers',
      description: 'Target customers who bought in the last 30 days',
      before: "{% if customer.last_purchase_date >= 'now' | date: '%s' | minus: 2592000 %}",
      after: '{% endif %}'
    }
  ];
}
```

## Frontend Personalization Examples

Reference the following resources to see advanced personalization examples and tutorials for end users of your application.

* [Product loops](https://support.beefree.io/hc/en-us/articles/20739290016914-Adding-Dynamic-Content-in-Beefree-for-Klaviyo) using merge tags and display conditions.
* [Hide or show](https://support.beefree.io/hc/en-us/articles/20739290016914-Adding-Dynamic-Content-in-Beefree-for-Klaviyo) content using display conditions.
* [Dynamic content](https://support.beefree.io/hc/en-us/articles/20740522282258-Adding-Dynamic-Content-in-Beefree-for-HubSpot-Product-Loops) using for loops. &#x20;
