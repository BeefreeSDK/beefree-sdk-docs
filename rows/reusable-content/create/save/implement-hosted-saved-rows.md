# Implement Hosted Saved Rows

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above.
{% endhint %}

## **How to Set Up Hosted Saved Rows**

Hosted Saved Rows simplifies row management by allowing you to store and retrieve saved rows using Beefree SDK's secure infrastructure. This fully managed solution eliminates the need for custom backend systems and UI development, enabling faster implementation and reduced maintenance.

This guide explains how to enable Hosted Saved Rows and configure advanced permissions to control row access and management.

### **Step 1: Enable Hosted Saved Rows**

To enable Hosted Saved Rows for your application, follow these steps:

1. Log in to the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application you'd like to configure Hosted Saved Rows for.
3. Click on **Details.**
4. Navigate to **Application configuration** and click **View more.**
5. Scroll to the **Saved Rows** section.
   1.  Toggle on the **Hosted on the Beefree SDK Infrastructure** option.

       <figure><img src="../../../../.gitbook/assets/CleanShot 2024-11-20 at 20.28.15.png" alt=""><figcaption></figcaption></figure>
   2.  Read the pricing information in the popup closely, because additional fees may apply.\*&#x20;

       <figure><img src="../../../../.gitbook/assets/CleanShot 2024-11-20 at 20.28.37.png" alt=""><figcaption></figcaption></figure>
   3. If you'd like to proceed, confirm you read and understand the pricing to activate the feature.

{% hint style="info" %}
**Important:** Keep in mind that charges apply for saved rows that are hosted not only in your production applications, but also for your development applications.
{% endhint %}

\*Hosted Saved Rows have the following pricing structure:

| Pricing Considerations | Free          | Essential     | Core              | Superpowers      | Enterprise       |
| ---------------------- | ------------- | ------------- | ----------------- | ---------------- | ---------------- |
| Allotment              | Not available | Not available | 100 Hosted Rows   | 250 Hosted Rows  | 1000 Hosted Rows |
| Price for extra unit   |               |               | $0.35/Hosted Rows | $0.25/Hosted Row | $0.20/Hosted Row |

**Note:** Visit our [Usage-based fees article](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees#h_01JE4K84YM3M040X7JBQR7GVW1) to learn more about Hosted Saved Rows pricing.

Once you've successfully enabled Hosted Saved Rows in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu), you'll access the following:

* Rows saved by your application's end users will be stored and hosted in the Beefree SDK storage option.
* End users can save rows directly to the hosted infrastructure and retrieve them as needed.

### **Step 2: Configure Advanced Permissions**

Hosted Saved Rows includes [advanced permissions](../../../../other-customizations/advanced-options/advanced-permissions.md#hosted-saved-rows) to control how rows and categories are accessed and managed. These permissions allow you to define user capabilities, such as editing or deleting rows.

#### **Available Permissions**

1. **`canDeleteHostedRow`:** Allows or prevents deleting hosted rows.
2. **`canEditHostedRow`:** Enables or disables editing of hosted rows.
3. **`canManageHostedRowCategory`:** Controls whether end users can manage row categories.
4. **`canAddHostedRowCategory`:** Determines if end users can add new categories.

#### **Permission Behavior**

* If both `canDeleteHostedRow` and `canEditHostedRow` are set to `false`, the row menu will be hidden.
* If both `canManageHostedRowCategory` and `canAddHostedRowCategory` are set to `false`, the category management menu will be hidden.

#### **Example Configuration**

The following configuration displays an example of the `rows` object inside of `advancedPermissions`:

```javascript
{
...
advancedPermissions:{
  ...
  rows:{
    behaviors: {
        canDeleteHostedRow: false,
        canEditHostedRow: false,
        canManageHostedRowCategory: false,
        canAddHostedRowCategory: false,
      },
    ...
  },
  ...
  }
...
}
```

### **Step 3: Managing Hosted Saved Rows**

Once Hosted Saved Rows is activated, end users can:

*   Save rows directly from the builder using the **Save** icon.  &#x20;

    &#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2024-11-21 at 16.15.36.png" alt="" width="563"><figcaption></figcaption></figure>
*   Name and categorize rows into categories for better discoverability.&#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2024-11-21 at 16.17.34.png" alt="" width="375"><figcaption></figcaption></figure>
*   Access, reuse, edit and delete rows through the **Rows** tab in the side panel.&#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2024-11-21 at 16.19.03.png" alt="" width="267"><figcaption></figcaption></figure>

Visit the [Hosted Saved Rows page](../../../storage/hosted-saved-rows.md) to learn more about the following topics:

* [Troubleshooting and FAQs](../../../storage/hosted-saved-rows.md#troubleshooting-and-faqs)
* [Deactivating Hosted Saved Rows](../../../storage/hosted-saved-rows.md#deactivating-hosted-saved-rows)
* [What Happens When Deactivated](../../../storage/hosted-saved-rows.md#what-happens-when-deactivated)
