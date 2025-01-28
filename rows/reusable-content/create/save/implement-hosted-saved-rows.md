# Implement Hosted Saved Rows

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above.
{% endhint %}

## **How to Set Up Hosted Saved Rows**

Hosted Saved Rows simplifies row management by allowing you to store and retrieve saved rows using Beefree SDK's secure infrastructure. This fully managed solution eliminates the need for custom backend systems and UI development, enabling faster implementation and reduced maintenance.

This page covers how to:

* [Enable Hosted Saved Rows](implement-hosted-saved-rows.md#enable-hosted-saved-rows)
* [User Interface and End User Experience](implement-hosted-saved-rows.md#user-interface-and-end-user-experience)
* [Configure Advanced Permissions](implement-hosted-saved-rows.md#configure-advanced-permissions)
* [Making Saved Rows Available to Select Users](implement-hosted-saved-rows.md#making-saved-rows-available-to-select-users)
* [Removing the Rows Tab for Select Users](implement-hosted-saved-rows.md#removing-the-rows-tab-for-select-users)

### **Enable Hosted Saved Rows**

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

### User Interface and End User Experience

Once you successfully enable Hosted Saved Rows within the Developer Console, your application's end users will have access to a new **Save** icon for each row, and other options for managing the rows they save.

The Hosted Saved Rows UI includes the following experience for end users:

*   End users can save a row using the **Save** icon.    &#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 14.00.04.png" alt=""><figcaption></figcaption></figure>
*   They have the ability to name and categorize rows.&#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 14.03.25.png" alt=""><figcaption></figcaption></figure>
*   They  can edit a row's name or category and save those changes. &#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 14.07.16.gif" alt=""><figcaption></figcaption></figure>
*   End users can decide to reuse or delete rows through the **Rows** tab in the side panel.&#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 14.08.29.gif" alt=""><figcaption></figcaption></figure>
*   They can also use the vertical three dots to add and manage categories.

    <figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 14.09.34.gif" alt=""><figcaption></figcaption></figure>

Reference the [Hosted Saved Rows end user documentation](https://docs.beefree.io/end-user-guide/hosted-saved-rows) for more information on the end user steps and experience.

### **Configure Advanced Permissions**

Hosted Saved Rows includes [advanced permissions](../../../../other-customizations/advanced-options/advanced-permissions.md#hosted-saved-rows) to control how rows and categories are accessed and managed. These permissions allow you to define user capabilities, such as editing or deleting rows.

#### **Available Permissions**

The permissions you can control for Hosted Saved Rows through Advanced Permissions are the following:

* **`canDeleteHostedRow`:** Allows or prevents deleting hosted rows.
* **`canEditHostedRow`:** Enables or disables editing of hosted rows.
* **`canManageHostedRowCategory`:** Controls whether end users can manage row categories.
* **`canAddHostedRowCategory`:** Determines if end users can add new categories.

#### **Permission Behavior**

Keep the following behaviors in mind when setting advanced permissions:

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

## **Making Saved Rows Available to Select Users**

Once Saved Rows is enabled globally in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu), you can disable it for specific users using the `saveRows` parameter in the `beeConfig` document. This lets you control access based on subscription plans, feature purchases, or beta testing.

Take the following step to disable access for specific users:

* Set `saveRows` to `false` for users who shouldn’t have access.

The following code provides a simple example of how to add the `saveRows` configuration parameter and set it to `false` to make the feature unavailable to select users.

```javascript

const beeConfig = {
    uid: 'dev-user',
    language: 'en-US',
    ...
    saveRows: false // boolean
    ...
}

```

### Default Behavior

The following image shows the save icon when the end user clicks on the row.

<figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 21.02.35.png" alt=""><figcaption></figcaption></figure>

### Hiding the Save Icon

The following image does not show the save icon when the end user clicks on the row. This behavior occurs after adding `saveRows` to your `beeConfig` and setting it to `false`.

<figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 21.02.03.png" alt=""><figcaption></figcaption></figure>

## Removing the Rows Tab for Select Users

Similar to how you may want to restrict which end users can save rows based on subscription type, plan type, and so on, you can also control which users have access to the **ROWS** tab within the builder altogether. By default, the **ROWS** tab is available within the builder.

You can remove the **ROWS** tab by:

* Add the `defaultTabsOrder` parameter to your `beeConfig` and set it to: `['content', 'settings']` or `['settings', 'content']`.

{% hint style="info" %}
**Note:** The only difference between these two options is the order in which they will appear in the builder.
{% endhint %}

Keep in mind the `defaultTabsOrder` is a string array (`string[]`).

The tab order represented in the snippet below with `content` first and `settings` second, results in the visualization displayed in the image after.

```javascript
defaultTabsOrder: ['content', 'settings']
```

In the following image, the **ROWS** tab is no longer available to the end user.

<figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 15.04.18.png" alt=""><figcaption></figcaption></figure>

The tab order represented in the snippet below with `settings` first and `content` second, results in the visualization displayed in the image after.

```javascript
defaultTabsOrder: ['settings', 'content']
```

In the following image, the **ROWS** tab is no longer available to the end user.

<figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 15.10.54.png" alt=""><figcaption></figcaption></figure>

Visit the [Hosted Saved Rows page](../../../storage/hosted-saved-rows.md) to learn more about the following topics:

* [Troubleshooting and FAQs](../../../storage/hosted-saved-rows.md#troubleshooting-and-faqs)
* [Deactivating Hosted Saved Rows](../../../storage/hosted-saved-rows.md#deactivating-hosted-saved-rows)
* [What Happens When Deactivated](../../../storage/hosted-saved-rows.md#what-happens-when-deactivated)
