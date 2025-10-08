---
description: >-
  This page discusses how to use the Direct Open parameter for AddOns within
  Beefree SDK. It includes instructions for both Custom and Partner AddOns.
---

# Direct Open

### Overview

With the Direct Open feature, you can immediately trigger your AddOn's content dialog or insert content as soon as the user drops the tile onto the editor stage. This eliminates the extra click step, creating a more efficient end user experience. With the `openOnDrop` parameter, you can determine whether or not your end user needs to perform an extra click before triggering the content dialog. The parameter can be set to `true` or `false` in your addon configuration within your `beeConfig`. It is available for Custom and Partner AddOns, and can be used for addons using content dialog or iframe method.

A few of the end user benefits include the following:

* **Immediate engagement** — Users start interacting right away
* **Better UX** — More intuitive interaction
* **Fewer clicks** — Reduces friction in workflow

**Without Direct Open:**

1. User drops tile → Placeholder appears
2. User clicks button → Dialog opens
3. User selects content → Content inserted

The following GIF displays an example of how a Custom AddOn without Direct Open is added to the builder stage.

<figure><img src="../.gitbook/assets/CleanShot 2025-10-01 at 09.07.41.gif" alt=""><figcaption></figcaption></figure>

**With Direct Open:**

1. User drops tile → Dialog opens immediately
2. User selects content → Content inserted

The following GIF displays an example of how a Custom AddOn with Direct Open is added to the builder stage.

<figure><img src="../.gitbook/assets/CleanShot 2025-10-01 at 09.13.49.gif" alt=""><figcaption></figcaption></figure>

### Configuration

This section discusses how to configure the `openOnDrop` parameter.&#x20;

#### Step 1: Enable in beeConfig

Add the `addOns` array with `openOnDrop: true`:

```javascript
const beeConfig = {
  container: 'bee-editor',
  addOns: [
    {
      id: 'my-html-addon',    // Your AddOn handle
      openOnDrop: true        // Enable Direct Open
    },
    {
      id: 'my-image-addon',
      openOnDrop: true
    }
  ],
  
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        // Your handler logic
      }
    }
  }
};
```

#### Step 2: Handle the Flag

Check `args.hasOpenOnDrop` to know if Direct Open triggered:

```javascript
contentDialog: {
  addOn: {
    handler: (resolve, reject, args) => {
      const { contentDialogId, hasOpenOnDrop } = args;
      
      console.log(`${contentDialogId} opened via Direct Open:`, hasOpenOnDrop);
      
      // Your logic here
    }
  }
}
```

### Configuration Reference

```javascript
const beeConfig = {
  container: 'bee-editor',
  addOns: [
    {
      id: string,           // Required: AddOn handle or UUID
      openOnDrop: boolean,  // true = enable, false/undefined = disable
      editable: boolean     // Optional: allow re-editing (default: true)
    }
  ]
};
```

### Implementation Patterns

This section outlines common implementation patterns by scenario.&#x20;

#### Pattern 1: Immediate Auto-Insert

Skip the dialog entirely and insert content immediately:

```javascript
handler: (resolve, reject, args) => {
  if (args.hasOpenOnDrop) {
    // Auto-insert default content
    resolve({
      type: 'html',
      value: {
        html: `<div>Auto-inserted content</div>`
      }
    });
  } else {
    // Show dialog when manually triggered
    yourDialog.open({
      ok: (content) => resolve(content),
      cancel: () => reject()
    });
  }
}
```

**Use when:** Content doesn't require user input.

#### Pattern 2: Pre-load Data

Fetch and insert data without showing a dialog:

```javascript
handler: async (resolve, reject, args) => {
  if (args.hasOpenOnDrop) {
    // Pre-load and auto-insert
    const data = await fetchDefaultContent();
    resolve({
      type: 'image',
      value: {
        src: data.imageUrl,
        alt: data.description
      }
    });
  } else {
    // Show full selection dialog
    yourImageSelector.open({
      ok: (img) => resolve(img),
      cancel: () => reject()
    });
  }
}
```

**Use when:** You have default or recommended content to insert.

#### Pattern 3: Different UI Based on Trigger

Show simplified vs. full UI:

```javascript
handler: (resolve, reject, args) => {
  if (args.hasOpenOnDrop) {
    // Show quick-select dialog
    yourQuickSelector.open({
      ok: (selection) => resolve(selection),
      cancel: () => reject()
    });
  } else {
    // Show full customization dialog
    yourAdvancedEditor.open({
      ok: (customContent) => resolve(customContent),
      cancel: () => reject()
    });
  }
}
```

**Use when:** You want different experiences for drop compared to edit.

#### Pattern 4: Multiple AddOns

Enable for specific AddOns only:

```javascript
const beeConfig = {
  addOns: [
    {
      id: 'simple-html',
      openOnDrop: true   // Enable
    },
    {
      id: 'complex-product',
      openOnDrop: false  // Disable (default behavior)
    }
  ],
  
  contentDialog: {
    addOn: {
      handler: (resolve, reject, args) => {
        switch (args.contentDialogId) {
          case 'simple-html':
            // hasOpenOnDrop will be true when dropped
            if (args.hasOpenOnDrop) {
              resolve({ type: 'html', value: { html: '<div>Quick</div>' } });
            } else {
              yourDialog.open(...);
            }
            break;
            
          case 'complex-product':
            // hasOpenOnDrop will always be false
            yourProductSelector.open(...);
            break;
        }
      }
    }
  }
};
```

### Sample Code

The following code snippet displays a simple example of Direct Open for various addon types.

```javascript
const ID_TYPES = {
  "cool-image-addon": "image",
  "cool-html-addon": "html",
  "cool-iframe-addon": "html",
  "cool-mixed-addon": "mixed",
  "cool-row-addon": "row",
  "cool-paragraph-addon": "paragraph",

  "cool-button-addon": "button",
  "cool-title-addon": "heading",
  "cool-list-addon": "list",
  "cool-menu-addon": "menu",
  "cool-icon-addon": "icon",
}

const beeConfig = {
  addOns: [
    {
      // partner add-on uuid
      id: 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
      openOnDrop: true
    },
    {
      id: 'cool-iframe-addon', // your handle id
      openOnDrop: true
    },
    {
      id: 'cool-mixed-addon', // your handle id
      openOnDrop: true
    },
    {
      id: 'cool-paragraph-addon', // your handle id
      openOnDrop: true
    },
    {
      id: 'cool-image-addon', // your handle id
      openOnDrop: true
    },
    {
      id: 'cool-row-addon', // your handle id
      openOnDrop: true
    },
  ],
  contentDialog: {
   	addOns: {
  		handler: function(resolve, reject, args) {
          const hasOpenedOnDrop = args.hasOpenOnDrop
          const addOnId = args?.contentDialogId
          console.log(`addon ${addOnId} opended automatically ${hasOpenedOnDrop}`)

          if (addOnId === 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx') {
            return 
          }

          let attributes = undefined 
          if (hasOpenedOnDrop) {
            const { attributes, mergeTags } = fetchStyles(addOnId) // preload content 
            resolve({
              type: ID_TYPES[addOnId],
              value: attributes,
              mergeTags,
            })
          }

          if (!attributes) {
            attributes = prompt('Please enter your attributes')
          }

          resolve({
            type: ID_TYPES[addOnId],
            value: { ...JSON.stringify(attributes) }
         })
  		}
   	}
  }
}
```

### Partner AddOns (UUID)

Direct Open works with Partner AddOns from the directory:

```javascript
addOns: [
  {
    id: 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',  // Partner AddOn UUID
    openOnDrop: true
  },
  {
    id: 'my-custom-addon',  // Your custom handle
    openOnDrop: true
  }
]
```

{% hint style="info" %}
**Note:** Partner AddOns manage their own dialogs, you don't handle them in your `contentDialog.addOn.handler`.
{% endhint %}

### Troubleshooting

| Issue                        | Solution                                          |
| ---------------------------- | ------------------------------------------------- |
| Dialog not opening on drop   | Verify `openOnDrop: true` and correct `id`        |
| `hasOpenOnDrop` is undefined | Update to latest Beefree SDK version              |
| Dialog opens twice           | Don't manually trigger in response to Direct Open |
| Still requires button click  | Check `addOns` array configuration                |
