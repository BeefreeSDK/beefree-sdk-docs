---
description: >-
  Learn more about Custom AddOns, and how to develop and implement your own
  custom built AddOn.
---

# Custom AddOns

{% hint style="info" %}
This feature is available on Beefree SDK [Superpowers plan](https://developers.beefree.io/pricing-plans) and above. Upgrade a [development application](https://docs.beefree.io/beefree-sdk/~/changes/463/getting-started/readme/development-applications) at no extra charge to explore features from higher plan tiers. **Note:** Usage on a development application still counts toward [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) and limits.
{% endhint %}

### Introduction <a href="#introduction" id="introduction"></a>

Custom AddOns are useful when there is a feature you'd like to offer within your application that is not available in our AddOn Marketplace within the Developer Console. In these instances, you can develop your own Custom AddOns for your application's end users.

Custom AddOns extend the functionality of the Beefree email builder by allowing you to create custom content tiles that integrate with your own services, data sources, and workflows. Whether you're building an image generator, product catalog integration, or custom HTML component, Custom AddOns give you the flexibility to tailor the editor to your specific needs.

#### Common Use Cases

The following list outlines a few of the most common use cases for building Custom AddOns.

* **E-commerce Integration:** Build AddOns that pull product data from your catalog and insert product images, descriptions, and pricing.
* **Image Libraries:** Connect to stock photo services, user-uploaded assets, or AI image generators.
* **Dynamic Content:** Create AddOns for countdown timers, live social media feeds, weather widgets, or personalized recommendations.
* **Third-Party Services:** Integrate with CRMs, marketing platforms, analytics services, or any external API.

#### Example of a Custom AddOn <a href="#example-of-a-custom-addon" id="example-of-a-custom-addon"></a>

Let's say you embedded our email editor in your event engagement platform, which has a feature that allows event marketers to insert an event ticket's QR code in marketing campaigns sent to create more engagement around an event.

* You want those marketers, users of your platform, to be able to easily include a QR code in the emails they send to remind people about the event. That way ticket holders can use the QR code to quickly get into the event venue.
* So you decide to create a "QR Code" addon: "QR Code" becomes a new [tile](https://docs.beefree.io/beefree-sdk/~/changes/463/other-customizations/appearance/content-tile-sorting#full-list-of-content-tiles) in the **Content** tab in the editor.
* Marketers drag and drop the tile, click on **Select event** to indicate which event the QR is for, and use the editor to style that section of the message (e.g. size, padding, etc.).
* The QR code is created dynamically by your platform, at the time the email is sent to a ticket buyer.
* The feature is specific to your application.

<figure><img src="https://806400411-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F8c7XIQHfAtM23Dp3ozIC%2Fuploads%2FvgjD293CRfdtPEfK0pcL%2FQRcode_add2-1024x527.jpg?alt=media&#x26;token=6e20bd17-062e-4b31-a6c8-3a2345c40ec5" alt=""><figcaption></figcaption></figure>

### Getting started <a href="#getting-started" id="getting-started"></a>

Log into the [Beefree SDK Console](https://developers.beefree.io/) and locate any application that is on the Superpowers or Enterprise plans. Click on **Details** to navigate to the application details page. In the lower part of the page, locate the **Application configuration** section and click on **AddOns**.

<figure><img src="https://806400411-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F8c7XIQHfAtM23Dp3ozIC%2Fuploads%2F0JM48xYioBHJPJtjjXEQ%2FCleanShot%202025-03-13%20at%2015.01.17.png?alt=media&#x26;token=44959c8e-12f7-4a8d-aaab-d03369d76248" alt=""><figcaption></figcaption></figure>

You will be taken to a page that lists the AddOns that have been installed for this application. Since you are just getting started, the list is likely empty. Click on **Create a custom addon** to start the process of creating a Custom AddOn.

<figure><img src="https://806400411-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F8c7XIQHfAtM23Dp3ozIC%2Fuploads%2FpxiEcHUIst1RvU7tGflw%2FCleanShot%202025-03-13%20at%2015.01.53.png?alt=media&#x26;token=e55b45e2-7e4a-4e7a-860e-3af410179885" alt=""><figcaption></figcaption></figure>

Refer to the [How to Build AddOns with Content Dialog](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/build-addons-with-content-dialog) and [Build AddOns with External Iframe](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/build-addons-with-external-iframe) for more details on how to build your AddOn.

#### Prerequisites

Before you start building Custom AddOns, ensure you have:

1. **A Beefree SDK account** at [developers.beefree.io](https://developers.beefree.io/)
2. **Superpowers plan or above** — Custom AddOns are only available on the Superpowers and Enterprise plans. If you're not on one of these plans:
   * Create a development application
   * Request an upgrade from your account dashboard
3. **A development application** — Always test your AddOns in a development environment before deploying to production. Development applications inherit the plan of the production application they're connected to.

#### Development Methods

There are two methods for building Custom AddOns. They are:

* [Content Dialog Method](build-addons-with-content-dialog.md)
* [External Iframe Method](build-addons-with-external-iframe/)

#### Available AddOn Types

Custom AddOns can return different types of content. Each type displays different properties in the editor's sidebar:

| Type              | Description                                           | Documentation                                                                                                                              |
| ----------------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **Image**         | Inserts an image module with image properties         | [Image AddOn Guide](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/image-addon)         |
| **HTML**          | Inserts an HTML module with custom markup             | [HTML AddOn Guide](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/html-addon)           |
| **Mixed**         | Inserts multiple content modules at once              | [Mixed AddOn Guide](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/mixed-content-addon) |
| **Row**           | Inserts a pre-built row structure                     | [Row AddOn Guide](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/row-addon)             |
| **Paragraph**     | Inserts a paragraph module                            | [Paragraph AddOn Guide](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/paragraph-addon) |
| **Button**        | Inserts a button module                               | [Button AddOn Guide](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/button-addon)       |
| **Title/Heading** | Inserts a title/heading module (type: `'heading'`)    | [Title AddOn Guide](https://docs.beefree.io/beefree-sdk/~/changes/463/data-structures/simple-schema/title-schema)                          |
| **List**          | Inserts a list module (ordered or unordered)          | [List AddOn Guide](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/list-addon)           |
| **Menu**          | Inserts a menu module with multiple linked items      | [Menu AddOn Guide](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/menu-addon)           |
| **Icon**          | Inserts an icon module with images, labels, and links | [Icon AddOn Guide](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types/icon-addon)           |

{% hint style="info" %}
**Title/Heading Schema Note:** When creating a Title AddOn in the Beefree Console, you select "Title" as the type. However, when resolving content in your code, you must use `type: 'heading'` in the content object, along with these required properties:

* `title`: The heading level ('h1', 'h2', 'h3', 'h4')
* `text`: The actual heading text content
{% endhint %}

#### Quick Start Guide

Here's a high-level overview of the process to create a Custom AddOn:

**Step 1: Create AddOn in Beefree SDK Console**

1. Log into [developers.beefree.io](https://developers.beefree.io/)
2. Navigate to your application's **AddOns** section
3. Click **Create a custom addon**
4. Fill in the form:
   * **Name**: Display name shown to users
   * **Type**: The content type your AddOn will insert (Image, HTML, Button, etc.)
   * **Handle**: Unique identifier for your code (e.g., `my-custom-addon`)
   * **Method**: Content Dialog or External Iframe
   * **Icon**: Optional custom icon for your AddOn tile
   * **Description**: User-facing explanation
5. Click **Create**
6. Copy your **AddOn Handle** — you'll need it in your code

**Step 2: Register AddOn in Your Code**

Add the AddOn to your `beeConfig`:

```javascript
const beeConfig = {
  // ... other config options
  addOns: [
    {
      id: 'my-custom-addon',  // Must match the handle from Console
      openOnDrop: true        // Optional: Auto-open when dropped
    }
  ],
  contentDialog: {
    addOn: {
      handle: 'my-custom-addon',  // Must match the handle from Console
      handler: (resolve, reject, args) => {
        // Your AddOn logic goes here
      }
    }
  }
};
```

**Step 3: Implement Handler Logic**

Your handler must resolve with a properly formatted content object matching your AddOn's type.

**Content Object Structure:**

```javascript
// Image AddOn Example
resolve({
  type: 'image',
  value: {
    src: 'https://example.com/image.jpg',
    alt: 'Description'
  }
});

// Button AddOn Example
resolve({
  type: 'button',
  value: {
    label: 'Click Me',
    href: 'https://example.com',
    'background-color': '#7747FF',
    color: '#FFFFFF',
    'border-radius': 4,
    'padding-top': 12,
    'padding-right': 24,
    'padding-bottom': 12,
    'padding-left': 24
  }
});

// Heading AddOn Example
resolve({
  type: 'heading',
  value: {
    title: 'h2',
    text: 'Welcome!',
    align: 'center',
    size: 28,
    color: '#333333',
    bold: true
  }
});

// HTML AddOn Example
resolve({
  type: 'html',
  value: {
    html: '<div>Custom HTML</div>'
  }
});
```

**Step 4: Test Your AddOn**

1. Initialize Beefree SDK with your config
2. Look for your AddOn tile in the Content tab
3. Drag and drop the tile onto the stage
4. Verify that:
   * Your handler is called
   * The module appears on the stage
   * Sidebar properties display correctly
   * Clicking the module works as expected

#### Content Object Schema

All AddOns must resolve with a content object that follows this structure:

```javascript
{
  type: string,        // Must match your AddOn type
  value: object,       // Type-specific properties
  mergeTags: array     // Optional: For dynamic content
}
```

The `value` object varies by type. See the [AddOn Types documentation](https://docs.beefree.io/beefree-sdk/~/changes/463/builder-addons/custom-addons/custom-addon-types) for complete schemas for each type.

#### Direct Open Feature (openOnDrop)

The `openOnDrop` property controls whether your AddOn handler is triggered immediately when a user drops the tile onto the stage:

```javascript
addOns: [
  {
    id: 'my-custom-addon',
    openOnDrop: true  // Handler opens automatically on drop
  }
]
```

**When to use `openOnDrop: true`:**

* User needs to configure the module before insertion (e.g., select an image, enter button text)
* Your AddOn requires user input

**When to use `openOnDrop: false` or omit:**

* Your AddOn inserts pre-defined content
* No user interaction is needed
* Users can configure the module after insertion via the sidebar

You can detect if your handler was triggered by a drop action:

```javascript
handler: (resolve, reject, args) => {
  if (args.hasOpenOnDrop) {
    // Handler was triggered by a drop action
  }
  // Your logic
}
```

#### Troubleshooting

**Module Not Appearing on Stage**

* Check that your `resolve()` content object matches your AddOn's type
* Verify the `type` property in your content object matches the Console type
* Open the browser console for validation errors
* **For Title AddOns specifically:** Ensure you're using `type: 'heading'` (not `type: 'title'`), and that you've included the required `title` property (e.g., `'h1'`, `'h2'`, `'h3'`, `'h4'`)

**Handler Not Firing**

* Confirm the `handle` in `contentDialog.addOn.handle` matches the handle from Console
* Check that the AddOn is registered in the `addOns` array with the correct `id`
* Verify your AddOn is enabled in the Console

**Sidebar Not Showing Expected Properties**

* Ensure the `type` in your content object is correct
* Check that you're using the correct property names (e.g., `label` for buttons, not `text`)
* Review the [Simple Schema documentation](https://docs.beefree.io/beefree-sdk/data-structures/simple-schema) for your type

**Content Not Editable**

* HTML and Mixed types are only editable by reopening your AddOn
* Other types should be editable via sidebar — check your content object structure
