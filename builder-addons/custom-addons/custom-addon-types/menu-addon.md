# Menu AddOn

### Overview

The Menu AddOn type allows you to insert navigation menus with multiple linked items. This is ideal for email headers, footer navigation, quick links, or any horizontal/vertical menu structure.

#### Prerequisites

Before implementing a Menu AddOn in your code, you must first create the addon in the [Beefree SDK Developer Console](https://developers.beefree.io/):

1. Log into the Developer Console and navigate to your application
2. Create a new Custom AddOn and select "Menu" as the type
3. Configure the addon with a unique **handle** (e.g., `my-menu-addon`)
4. Choose your implementation method (Content Dialog or External iframe)
5. Save the addon configuration

{% hint style="info" %}
**Important:** The handle you create in the Developer Console must match exactly with the addon ID you reference in your code's `beeConfig`. This handle serves as the unique identifier that connects your code implementation to the addon configuration in the console.
{% endhint %}

#### Content Object Schema

**Required Structure**

The Menu AddOn schema defines a collection of linked text items organized in an `items` array. Each menu item contains text displayed to users and a nested `link` object with URL, title, and target properties. This structure creates clickable navigation elements perfect for email headers, footers, or any organized set of links within your email campaigns.

```javascript
{
  type: 'menu',
  value: {
    items: [                  // Required: Array of menu items
      {
        text: string,         // Menu item text
        link: {
          title: string,      // Link title attribute
          href: string,       // Link URL
          target: string      // '_self', '_blank', etc.
          }
      }
    ]
  }
}
```

**Basic Example**

This simple example creates a basic navigation menu with three common links. Each item has text displayed to users and a link object containing the destination URL and target behavior. This minimal structure is perfect for straightforward navigation needs like header menus or footer links.

```javascript
resolve({
  type: 'menu',
  value: {
    items: [
      {
        text: 'Home',
        link: {
          title: 'Home',
          href: 'https://example.com',
          target: '_self'
        }
      },
      {
        text: 'About',
        link: {
          title: 'About Us',
          href: 'https://example.com/about',
          target: '_self'
        }
      },
      {
        text: 'Contact',
        link: {
          title: 'Contact Us',
          href: 'https://example.com/contact',
          target: '_self'
        }
      }
    ]
  }
});
```

**Complete Navigation Example**

This comprehensive example demonstrates a full navigation menu with proper link targeting and descriptive titles. Using `target: '_blank'` opens links in new tabs, which is common for email navigation to keep the email client open. The descriptive `title` attributes improve accessibility and provide additional context when users hover over links.

```javascript
resolve({
  type: 'menu',
  value: {
    items: [
      {
        text: 'Shop',
        link: {
          title: 'Browse Our Products',
          href: 'https://example.com/shop',
          target: '_blank'
        }
      },
      {
        text: 'New Arrivals',
        link: {
          title: 'See What\'s New',
          href: 'https://example.com/new',
          target: '_blank'
        }
      },
      {
        text: 'Sale',
        link: {
          title: 'View Sale Items',
          href: 'https://example.com/sale',
          target: '_blank'
        }
      },
      {
        text: 'Blog',
        link: {
          title: 'Read Our Blog',
          href: 'https://example.com/blog',
          target: '_blank'
        }
      }
    ]
  }
});
```

#### Content Dialog Implementation

**Basic Handler**

The Content Dialog method enables programmatic menu insertion through a JavaScript handler. When users drag your menu addon onto the stage, this handler is immediately invoked and resolves with a predefined menu structure. This pattern works perfectly for static navigation menus that don't require user configuration, providing instant insertion of consistently formatted link sets.

```javascript
const beeConfig = {
  container: 'bee-editor',
  
  // Enable the addon with Direct Open feature
  addOns: [
    {
      id: 'my-menu-addon',  // Must match handle from Console
      openOnDrop: true
    }
  ],
  
  // Define the handler for menu insertion
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Check which addon triggered this handler
        if (args.contentDialogId === 'my-menu-addon') {
          // Immediately insert a navigation menu
          resolve({
            type: 'menu',
            value: {
              items: [
                {
                  text: 'Products',
                  link: {
                    title: 'Products',
                    href: 'https://example.com/products',
                    target: '_blank'
                  }
                },
                {
                  text: 'Services',
                  link: {
                    title: 'Services',
                    href: 'https://example.com/services',
                    target: '_blank'
                  }
                },
                {
                  text: 'Support',
                  link: {
                    title: 'Support',
                    href: 'https://example.com/support',
                    target: '_blank'
                  }
                }
              ]
            }
          });
        }
      }
    }
  }
};
```

**Pattern: Dynamic Menu Generation**

This pattern demonstrates programmatic menu generation from a structured data array, making it easy to maintain navigation links in a centralized configuration. By mapping through your navigation data, you can transform a simple structure into the proper menu schema format. This approach is particularly useful when menu items are managed in configuration files, databases, or need to be updated frequently across multiple templates.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Define navigation structure (could come from config, API, etc.)
      const navigationLinks = [
        { label: 'Home', url: 'https://example.com' },
        { label: 'Shop', url: 'https://example.com/shop' },
        { label: 'About', url: 'https://example.com/about' },
        { label: 'Contact', url: 'https://example.com/contact' }
      ];
      
      // Transform data into menu items
      const menuItems = navigationLinks.map(link => ({
        text: link.label,
        link: {
          title: link.label,
          href: link.url,
          target: '_blank'
        }
      }));
      
      // Resolve with generated menu
      resolve({
        type: 'menu',
        value: {
          items: menuItems
        }
      });
    }
  }
}
```

**Pattern: User-Configurable Menu**

This advanced pattern shows how to let users customize menu items through an interface before insertion. By opening a dialog where users can add, edit, or remove menu items and configure their URLs, you provide maximum flexibility while maintaining proper menu structure. The handler filters out invalid items (missing text or URL) before resolving, ensuring clean menu insertion with user-defined content and links.

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      // Open your custom UI for menu configuration
      // Replace 'yourMenuEditor' with your actual UI component
      yourMenuEditor.open({
        onSave: (menuConfig) => {
          // Filter out invalid items and transform to menu schema
          const items = menuConfig
            .filter(item => item.text && item.url)
            .map(item => ({
              text: item.text,
              link: {
                title: item.text,
                href: item.url,
                target: item.openInNewTab ? '_blank' : '_self'
              }
            }));
          
          // Resolve with user-configured menu
          resolve({
            type: 'menu',
            value: { items }
          });
        },
        onCancel: () => {
          // User canceled - reject to abort insertion
          reject();
        }
      });
    }
  }
}
```

#### Iframe Implementation

**Conceptual Flow**

The Iframe method allows you to create a fully custom interface for menu configuration using any web technology. Your iframe application communicates with Beefree through `postMessage` events, following a specific protocol. This approach is ideal when you need a rich UI for menu management, including features like drag-and-drop reordering, link validation, or menu templates before inserting the navigation into the email template.

**Required postMessage Communication**

Implement the standard postMessage protocol to integrate your iframe with Beefree. First, notify Beefree when your iframe is loaded and specify the dialog dimensions. Listen for the "init" message to receive editor context. When the user finishes creating their menu, send "onSave" with your menu object. If the user cancels, send "onCancel" to close the dialog without inserting content.

**1. Send "loaded" when your iframe is ready:**

```javascript
window.parent.postMessage({
  action: 'loaded',
  data: {
    width: '650px',
    height: '550px',
    isRounded: true,
    hasTitleBar: true,
    showTitle: true
  }
}, '*');
```

**2. Listen for "init" and "load" messages from Beefree:**

```javascript
window.addEventListener('message', (event) => {
  const { action, data } = event.data;
  
  if (action === 'init') {
    console.log('Editor locale:', data.locale);
    // Initialize your menu creation UI
  }
  
  if (action === 'load') {
    // Pre-populate when editing existing menu
    if (data && data.value && data.value.items) {
      const menuText = data.value.items
        .map(item => `${item.text} | ${item.link.href}`)
        .join('\n');
      document.getElementById('menuItems').value = menuText;
    }
  }
});
```

**3. Send "onSave" with menu data:**

```javascript
// When user clicks save/insert button
window.parent.postMessage({
  action: 'onSave',
  data: {
    type: 'menu',
    value: {
      items: [
        {
          text: 'Link 1',
          link: {
            title: 'Link 1',
            href: 'https://example.com/1',
            target: '_blank'
          }
        }
        // ... more items
      ]
    }
  }
}, '*');
```

**4. Send "onCancel" if user cancels:**

```javascript
// When user clicks cancel or closes dialog
window.parent.postMessage({
  action: 'onCancel'
}, '*');
```

**Simple Iframe Example**

This complete HTML example provides a functional menu creation interface. It demonstrates the full postMessage protocol and includes a dynamic item input system where users can add multiple menu links with text and URLs. The interface builds proper menu structure and sends it to Beefree. You can expand this basic example with link validation, reordering capabilities, or pre-built menu templates for common navigation patterns.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Menu Creator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }
    .menu-item {
      margin: 15px 0;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 4px;
    }
    input {
      width: 100%;
      padding: 8px;
      margin: 5px 0;
    }
    button {
      padding: 10px 20px;
      margin: 5px;
    }
  </style>
</head>
<body>
  <h2>Create Navigation Menu</h2>
  
  <div id="menuItems">
    <div class="menu-item">
      <input type="text" placeholder="Link text" value="Home" data-field="text">
      <input type="url" placeholder="URL" value="https://example.com" data-field="url">
    </div>
    <div class="menu-item">
      <input type="text" placeholder="Link text" value="About" data-field="text">
      <input type="url" placeholder="URL" value="https://example.com/about" data-field="url">
    </div>
    <div class="menu-item">
      <input type="text" placeholder="Link text" value="Contact" data-field="text">
      <input type="url" placeholder="URL" value="https://example.com/contact" data-field="url">
    </div>
  </div>
  
  <button onclick="addMenuItem()">Add Menu Item</button><br>
  <button onclick="insertMenu()">Insert Menu</button>
  <button onclick="cancel()">Cancel</button>

  <script>
    // Notify Beefree that iframe is loaded and ready
    window.parent.postMessage({
      action: 'loaded',
      data: { 
        width: '650px', 
        height: '550px',
        isRounded: true,
        hasTitleBar: true,
        showTitle: true
      }
    }, '*');

    // Listen for messages from Beefree
    window.addEventListener('message', (event) => {
      const { action, data } = event.data;
      
      if (action === 'init') {
        console.log('Editor locale:', data?.locale);
      }
      
      if (action === 'load' && data?.value?.items) {
        // Pre-populate when editing existing menu
        const menuText = data.value.items
          .map(item => `${item.text} | ${item.link.href}`)
          .join('\n');
        document.getElementById('menuItems').value = menuText;
      }
    });

    function addMenuItem() {
      const container = document.getElementById('menuItems');
      const div = document.createElement('div');
      div.className = 'menu-item';
      div.innerHTML = `
        <input type="text" placeholder="Link text" data-field="text">
        <input type="url" placeholder="URL" data-field="url">
      `;
      container.appendChild(div);
    }

    function insertMenu() {
      const menuItemDivs = document.querySelectorAll('.menu-item');
      const items = [];
      
      // Build menu items from inputs
      menuItemDivs.forEach(div => {
        const text = div.querySelector('[data-field="text"]').value;
        const url = div.querySelector('[data-field="url"]').value;
        
        if (text.trim() && url.trim()) {
          items.push({
            text: text,
            link: {
              title: text,
              href: url,
              target: '_blank'
            }
          });
        }
      });
      
      // Validate that at least one menu item exists
      if (items.length === 0) {
        alert('Please enter at least one menu item');
        return;
      }
      
      // Send menu data to Beefree
      window.parent.postMessage({
        action: 'onSave',
        data: {
          type: 'menu',
          value: { items }
        }
      }, '*');
    }

    function cancel() {
      window.parent.postMessage({ action: 'onCancel' }, '*');
    }
  </script>
</body>
</html>
```

#### Link Target Options

* **`_self`** - Opens in same tab/window (default for email)
* **`_blank`** - Opens in new tab/window (common for email links)
* **`_parent`** - Opens in parent frame
* **`_top`** - Opens in full window
