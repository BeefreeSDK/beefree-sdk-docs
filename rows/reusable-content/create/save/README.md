# Save Reusable Content

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. If you're on the Essentials plan, [upgrade a development application](../../../../getting-started/readme/development-applications.md) for free to try this and other Core-level features.
{% endhint %}

## Saved Rows Overview

This page provides an overview of Saved Rows and their key benefits.

### What Are Saved Rows?

Saved Rows in Beefree SDK optimize the content creation process by allowing users to save, categorize, and manage reusable rows for future use. When this feature is enabled, users can simply click the **Save** icon on a row within their design and store it for later. This ensures quick access to preferred layouts and design elements across multiple projects.

### Benefits of Saved Rows

#### For End Users

* **Reusable Rows:** Save rows once and reuse them across multiple designs.
* **Flexible Categorization:** Organize rows into intuitive categories for discoverability.
* **Easily Manage Rows:** Manage rows with intuitive editing options.

#### For Host Applications

* **Enhanced User Experience:** Enable users to save, categorize, and manage their rows efficiently.
* **Flexible Implementation and Management Options:** Activate, store, and manage Saved Rows using either hosted or self-hosted options.
* **Highly Customizable:** Enable or disable end user permissions to delete, edit, manage, or add Saved Rows.&#x20;

### How Saved Rows Work

#### Saving Rows

When enabled, Saved Rows allow end users to select a row in their design and save it. This process involves:

1. Selecting a row in the builder.
2. Clicking the **Save** icon in the toolbar or row properties panel.
3. Storing the row’s structure, content, and styles as a JSON document in your chosen storage solution.\*

{% hint style="info" %}
\*Beefree SDK offers [two paths](./#activation-paths-for-saved-rows) for this: [Hosted Saved Rows](implement-hosted-saved-rows.md) or [Self-hosted Saved Rows](implement-self-hosted-saved-rows.md).
{% endhint %}

#### Using Saved Rows

Saved Rows are displayed in the builder’s Rows panel. Users can:

* Browse saved rows by category.
* Search for rows using metadata like row names or descriptions.
* Drag and drop rows into their designs for immediate use.

#### Activation Paths for Saved Rows

There are two paths you can take to activate Saved Rows for your application:

* Hosted Saved Rows
* Self-Hosted Saved Rows

Both paths provide their own set of benefits. The following section discusses these activation paths at a high-level. For more detailed information on both activation routes, reference Implement Hosted Saved Rows and Implement Self-Hosted Saved Rows.

### Hosting Options for Saved Rows

Saved Rows can be hosted and configured using one of the following options:

#### **Beefree SDK Hosted Infrastructure:** Hosted Saved Rows

* Fully managed by Beefree SDK, and activated through a toggle in the Developer Console.
* Ideal for teams that want a quick setup without maintaining backend systems.
* Offers centralized storage, security, and reliability, while also providing a user interface to save and  reuse rows within your application.

#### **Self-Hosted Infrastructure:** Self-Hosted Saved Rows

* Allows full control over where and how rows are stored.
* Suitable for teams with specific compliance or integration needs.
* Requires development resources for managing row storage, and creating a user interface to manage and reuse rows.

Learn more about [Storage for Reusable Content](../../../storage/).

### Examples of Saved Rows in Action

#### Standardized Footers

Save a footer row with contact details, social media links, and copyright information. Use it across multiple email templates to ensure consistency.

#### E-Commerce Product Grids

Create reusable rows showcasing product images, descriptions, and call-to-action buttons. Pull these rows dynamically from an e-commerce catalog for up-to-date content.

#### Promotional Banners

Save promotional rows with pre-configured styles and messaging. Reuse them across campaigns to maintain branding and reduce setup time.
