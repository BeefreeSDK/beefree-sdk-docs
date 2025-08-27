---
description: >-
  This recipe explains how you can use Liquid in Beefree SDK to support advanced
  email personalization options for your end users.
---

# Use Liquid in Beefree SDK for Email Personalization

{% hint style="info" %}
This tutorial uses Display Conditions, Content Dialog, and Merge Tags. Display Conditions requires a [Core plan or above](https://developers.beefree.io/pricing-plans). &#x20;
{% endhint %}

<details>

<summary>Copy this pre-built prompt to get started faster with AI</summary>

````
# **Beefree SDK + Liquid Templating Integration Guide**

**Purpose:** Demonstrate how to integrate **Liquid templating** with **Beefree SDK** to create advanced email personalization features in React applications.

**Scope:** This guide covers merge tags, display conditions, custom content dialogs, and dynamic content loading for personalized email campaigns.

---

## **1. Project Overview**

This project showcases a complete integration of Beefree SDK with Liquid templating for email personalization, featuring:

- **React-based Beefree SDK integration** using `@beefree.io/sdk`
- **Liquid templating** for dynamic content and personalization
- **Custom content dialogs** for managing display conditions and external content
- **Merge tags** for drag-and-drop personalization fields
- **External content loading** for pre-built row templates
- **Secure proxy server** for authentication

---

## **2. Core Components**

### **2.1 Beefree SDK Configuration with Liquid Features**

```javascript
const beeConfig = {
  container: 'beefree-sdk-container',
  language: 'en-US',
  enabledAdvancedPreview: true,
  trackChanges: true,
  
  // Liquid personalization features
  mergeTags: [
    { name: 'Customer Name', value: '{{ customer.name }}' },
    { name: 'Customer Email', value: '{{ customer.email }}' },
    { name: 'Order Total', value: '{{ order.total }}' },
    { name: 'Product Name', value: '{{ product.name }}' },
    { name: 'Product Price', value: '{{ product.price }}' },
    { name: 'Store Name', value: '{{ shop.name }}' }
  ],
  
  // Custom content dialog for Liquid features
  contentDialog: {
    rowDisplayConditions: {
      title: 'Display Conditions',
      description: 'Set conditions for when this row should be displayed',
      handler: (data, callback) => {
        // Custom modal for Liquid conditional logic
        showDisplayConditionsModal(data, callback);
      }
    },
    externalContentURLs: {
      title: 'Pre-built Rows',
      description: 'Load pre-built row templates with Liquid personalization',
      handler: (data, callback) => {
        // Custom modal for external content selection
        showExternalContentModal(data, callback);
      }
    }
  },
  
  // Rows configuration for Liquid templates
  rowsConfiguration: {
    emptyRows: true,
    defaultRows: true,
    selectedRowType: 'default',
    externalContentURLs: 'https://qa-bee-playground-backend.getbee.io/api/customrows/?ids=1,2,3,4'
  },
  
  // Event handlers
  onChange: (pageJson) => {
    console.log('Content changed:', pageJson);
  },
  onRemoteChange: (pageJson) => {
    console.log('Remote change:', pageJson);
  },
  onViewChange: (view) => {
    console.log('View changed:', view);
  },
  onError: (error) => {
    console.error('Beefree SDK error:', error);
  }
};
```

### **2.2 Liquid Templating Examples**

#### **Basic Merge Tags**
```liquid
Hello {{ customer.name }},

Thank you for your order of {{ order.total }}. 
Your items will be shipped from {{ shop.name }}.
```

#### **Conditional Display Logic**
```liquid
{% if customer.total_spent > 100 %}
  <div class="vip-section">
    <h2>VIP Customer Benefits</h2>
    <p>You've earned {{ customer.reward_points }} reward points!</p>
  </div>
{% endif %}
```

#### **Product Loops**
```liquid
{% for product in products %}
  <div class="product-item">
    <img src="{{ product.image }}" alt="{{ product.name }}">
    <h3>{{ product.name }}</h3>
    <p class="price">{{ product.price }}</p>
    {% if product.on_sale %}
      <span class="sale-badge">SALE!</span>
    {% endif %}
  </div>
{% endfor %}
```

---

## **3. Custom Content Dialogs**

### **3.1 Display Conditions Modal**

```javascript
const showDisplayConditionsModal = (data, callback) => {
  const modal = document.createElement('div');
  modal.className = 'liquid-modal';
  modal.innerHTML = `
    <div class="modal-content">
      <div class="modal-header">
        <h3>Display Conditions</h3>
        <button class="close-btn" onclick="this.parentElement.parentElement.parentElement.remove()">×</button>
      </div>
      <div class="modal-body">
        <p>Set Liquid conditions for when this row should be displayed:</p>
        <textarea 
          id="liquid-condition" 
          placeholder="{% if customer.total_spent > 100 %}...{% endif %}"
          style="width: 100%; height: 100px; font-family: monospace;"
        >${data.condition || ''}</textarea>
        <div class="button-group">
          <button class="btn btn-primary" onclick="applyCondition()">Apply Condition</button>
          <button class="btn btn-secondary" onclick="this.parentElement.parentElement.parentElement.remove()">Cancel</button>
        </div>
      </div>
    </div>
  `;
  
  document.body.appendChild(modal);
  
  window.applyCondition = () => {
    const condition = document.getElementById('liquid-condition').value;
    callback({ condition });
    modal.remove();
  };
};
```

### **3.2 External Content Modal**

```javascript
const showExternalContentModal = (data, callback) => {
  const modal = document.createElement('div');
  modal.className = 'liquid-modal';
  modal.innerHTML = `
    <div class="modal-content">
      <div class="modal-header">
        <h3>Pre-built Rows</h3>
        <button class="close-btn" onclick="this.parentElement.parentElement.parentElement.remove()">×</button>
      </div>
      <div class="modal-body">
        <p>Select pre-built row templates with Liquid personalization:</p>
        <div class="row-grid">
          <div class="row-item" onclick="selectRow('product-showcase')">
            <h4>Product Showcase</h4>
            <p>Dynamic product display with Liquid loops</p>
          </div>
          <div class="row-item" onclick="selectRow('customer-greeting')">
            <h4>Customer Greeting</h4>
            <p>Personalized welcome message</p>
          </div>
          <div class="row-item" onclick="selectRow('order-summary')">
            <h4>Order Summary</h4>
            <p>Order details with conditional logic</p>
          </div>
        </div>
      </div>
    </div>
  `;
  
  document.body.appendChild(modal);
  
  window.selectRow = (rowType) => {
    callback({ rowType });
    modal.remove();
  };
};
```

---

## **4. Advanced Liquid Features**

### **4.1 Dynamic Content Loading**

```javascript
// Load external content with Liquid variables
const loadExternalContent = async (contentId) => {
  try {
    const response = await fetch(`/api/content/${contentId}`);
    const content = await response.json();
    
    // Process Liquid variables in the content
    const processedContent = processLiquidVariables(content, {
      customer: { name: 'John Doe', email: 'john@example.com' },
      shop: { name: 'My Store' },
      products: [
        { name: 'Product 1', price: '$29.99', on_sale: true },
        { name: 'Product 2', price: '$49.99', on_sale: false }
      ]
    });
    
    return processedContent;
  } catch (error) {
    console.error('Error loading external content:', error);
  }
};
```

### **4.2 Liquid Variable Processing**

```javascript
const processLiquidVariables = (content, variables) => {
  let processed = content;
  
  // Replace simple variables
  Object.keys(variables).forEach(key => {
    if (typeof variables[key] === 'string' || typeof variables[key] === 'number') {
      processed = processed.replace(new RegExp(`{{ ${key} }}`, 'g'), variables[key]);
    }
  });
  
  // Handle nested objects
  Object.keys(variables).forEach(key => {
    if (typeof variables[key] === 'object' && !Array.isArray(variables[key])) {
      Object.keys(variables[key]).forEach(subKey => {
        processed = processed.replace(
          new RegExp(`{{ ${key}.${subKey} }}`, 'g'), 
          variables[key][subKey]
        );
      });
    }
  });
  
  return processed;
};
```

---

## **5. Implementation Steps**

### **5.1 Setup Requirements**

1. **Install dependencies:**
   ```bash
   npm install @beefree.io/sdk react react-dom
   ```

2. **Create `.env` file:**
   ```
   BEE_CLIENT_ID=your_client_id
   BEE_CLIENT_SECRET=your_client_secret
   ```

3. **Setup proxy server** for secure authentication

### **5.2 React Component Structure**

```javascript
import { useEffect, useRef, useState } from 'react';
import BeefreeSDK from '@beefree.io/sdk';

export default function BeefreeLiquidEditor() {
  const containerRef = useRef(null);
  const [beeInstance, setBeeInstance] = useState(null);
  const [sdkLoaded, setSdkLoaded] = useState(false);

  useEffect(() => {
    initializeEditor();
  }, []);

  const initializeEditor = async () => {
    try {
      // Get authentication token
      const response = await fetch('/proxy/bee-auth', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ uid: 'demo-user' })
      });
      const { token } = await response.json();

      // Initialize Beefree SDK
      const bee = new BeefreeSDK(token);
      const instance = await bee.start(beeConfig, {});
      
      setBeeInstance(instance);
      setSdkLoaded(true);
    } catch (error) {
      console.error('Initialization error:', error);
    }
  };

  return (
    <div>
      <div 
        id="beefree-sdk-container" 
        ref={containerRef}
        style={{ 
          width: '90%', 
          height: '700px',
          margin: '0 auto',
          background: '#ffffff'
        }}
      >
        <div style={{ padding: '20px', color: '#000' }}>
          {sdkLoaded ? 'Beefree SDK loaded!' : 'Loading Beefree SDK...'}
        </div>
      </div>
      
      <button onClick={() => beeInstance?.loadRows()}>
        Load External Rows
      </button>
    </div>
  );
}
```

---

## **6. Best Practices**

### **6.1 Liquid Syntax Guidelines**

- **Use descriptive variable names:** `{{ customer.first_name }}` instead of `{{ name }}`
- **Implement proper conditionals:** Always include `{% endif %}` and `{% endfor %}`
- **Handle edge cases:** Use `{% if customer.name %}` to check for existence
- **Optimize loops:** Limit product loops to reasonable numbers

### **6.2 Security Considerations**

- **Never expose sensitive data** in Liquid variables
- **Validate user input** before processing Liquid templates
- **Use secure proxy server** for authentication
- **Sanitize dynamic content** to prevent XSS attacks

### **6.3 Performance Optimization**

- **Cache processed templates** for frequently used content
- **Lazy load external content** to improve initial load times
- **Minimize API calls** by batching content requests
- **Use efficient Liquid filters** for data transformation

---

## **7. Troubleshooting**

### **7.1 Common Issues**

- **SDK not loading:** Check authentication token and network connectivity
- **Liquid variables not rendering:** Verify variable names and syntax
- **External content not loading:** Check API endpoints and CORS settings
- **Modal not displaying:** Ensure CSS styles are properly loaded

### **7.2 Debug Tips**

- **Enable console logging** for detailed error messages
- **Test Liquid syntax** in a separate environment first
- **Validate JSON structure** of external content
- **Check browser network tab** for failed requests

---

This integration provides a powerful foundation for creating personalized email campaigns with dynamic content, conditional logic, and a smooth user experience through Beefree SDK's intuitive interface combined with Liquid's templating capabilities.
````

</details>

## Overview

This project showcases how to configure [Beefree SDK's](https://docs.beefree.io/beefree-sdk) email editor with [Liquid](https://shopify.github.io/liquid/) templating for dynamic and personalized email content. Built with React and the `@beefree.io/sdk` [npm package](https://www.npmjs.com/package/@beefree.io/sdk), it's designed for developers and teams who need to customize Beefree SDK's email builder for end users who need to create sophisticated and highly personalized email campaigns that include conditional content and product loops.

This project is designed for:

* **Email Developers** who need advanced personalization features
* **Marketing Teams** creating dynamic, data-driven campaigns
* **Developers** integrating advanced email functionality into their applications
* **Agencies** building advanced custom email solutions for clients

Reference the project code in the [beefree-liquid-email-personalization](use-liquid-in-beefree-sdk-for-email-personalization.md) GitHub repository.&#x20;

{% embed url="https://github.com/BeefreeSDK/beefree-liquid-email-personalization" %}

The video provides a visual example of the demo and how Display Conditions, Content Dialog, and Merge Tags are integrated on the frontend.

{% embed url="https://drive.google.com/file/d/1YkJ9S2JGzdpKJ7qy9I6WRhD3jbbcra8O/view?usp=sharing" %}

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

This section lists what's included within this project.

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
