# Save Reusable Content

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. Upgrade a [development application](../../../../getting-started/readme/development-applications.md) at no extra charge to explore features from higher plan tiers. **Note:** Usage on a development application still counts toward [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) and limits.
{% endhint %}

## Saved Rows Overview

This page provides an overview of Saved Rows and their key benefits.

### What Are Saved Rows?

Saved Rows in Beefree SDK optimize the content creation process by allowing users to save, categorize, and manage reusable rows for future use. When this feature is enabled, users can simply click the **Save** icon on a row within their design and store it for later. This ensures quick access to preferred layouts and design elements across multiple projects.

Save Rows are particularly helpful in the following scenarios:&#x20;

* **Standardizing Footers:** Save a footer row with contact details, social media links, and copyright information. Use it across multiple email templates to ensure consistency.
* **Designing E-Commerce Product Grids:** Create reusable rows showcasing product images, descriptions, and call-to-action buttons. Pull these rows dynamically from an e-commerce catalog for up-to-date content.
* **Creating Promotional Banners:** Save promotional rows with pre-configured styles and messaging. Reuse them across campaigns to maintain branding and reduce setup time.

### Benefits of Saved Rows

There are several benefits to utilizing saved rows. This section outlines benefits for both end users and the host applications.

Saved Rows enable end users to:

* **Save and reuse content:** Create emails, landing pages, and popups, apply their own style and brand guidelines, and save all of that hard work inside of a row and reuse it at a later date. After saving a row, they can still edit the row and make any adjustments to the content blocks inside of it.
* **Flexible Categorization:** Organize rows into intuitive categories to easily find and reuse them later on.
* **Easily Manage Rows:** Edit the name and category of a saved row easily. Or, delete rows if they are no longer needed.

Saved Rows enable host applications to:

* **Enhance the User Experience:** Enable users to save, categorize, and manage rows efficiently.
* **Multiple Storage Options:** Activate, store, and manage Saved Rows using either [hosted](../../../storage/hosted-saved-rows.md) or [self-hosted](../../../storage/self-hosted-saved-rows.md) options.
* **Customize Permissions:** Enable or disable end user permissions to delete, edit, manage, or add Saved Rows.
* M**ake Saved Rows Available to Select Users:** Control which users can and cannot save rows.

### How Saved Rows Work

When enabled, Saved Rows allow end users to select a row in their design and save it. This process involves:

1. Selecting a row in the builder.
2. Clicking the **Save** icon in the toolbar or row properties panel.
3. Storing the row’s structure, content, and styles as a JSON document in your chosen storage solution.\*

{% hint style="info" %}
\*Beefree SDK offers [two paths](./#activation-paths-for-saved-rows) for this: [Hosted Saved Rows](implement-hosted-saved-rows.md) or [Self-hosted Saved Rows](implement-self-hosted-saved-rows/).
{% endhint %}

#### Using Saved Rows

Once created and saved, end users can reuse saved rows through the builder’s **ROWS** tab.&#x20;

There, users can:

* Browse saved rows by category.
* Search for rows using metadata like row names or descriptions.
* Drag and drop rows into their designs for immediate use.

#### Activation and Storage Paths for Saved Rows

There are two paths you can take to activate and store Saved Rows for your application:

* [Hosted Saved Rows](implement-hosted-saved-rows.md): Enabled by default. Provides a storage solution and user interface.
* [Self-Hosted Saved Rows](../../../storage/self-hosted-saved-rows.md): Requires activation in the Beefree SDK console, along with creating your own endpoints to connect a database.

Both paths provide their own set of benefits and limitations. It is important to familiarize yourself with the benefits and limitations of each option to choose the storage and activation solution that is best for you and your application's needs. For more detailed information on both activation routes, reference [Implement Hosted Saved Rows](implement-hosted-saved-rows.md) and Implement [Self-Hosted Saved Rows](implement-self-hosted-saved-rows/).

Learn more about [Storage for Reusable Content](../../../storage/) to discover the best option for you.
