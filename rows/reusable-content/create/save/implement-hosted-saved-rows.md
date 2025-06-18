# Implement Hosted Saved Rows

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above.
{% endhint %}

## **Overview**

With Hosted Saved Rows, you can provide your end users with the option to save and manage reusable content directly within the builder. Hosted Saved Rows can be activated through a toggle within the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu), which makes it an excellent option for those who are interested in a fast implementation of [Saved Rows](./). Once you toggle this feature on, your end users will be able to save the rows they create within the builder, and reuse them easily in the future. They can also perform actions to manage the rows that they save, such as renaming them, deleting them, categorizing, or recategorizing them. This page covers [the steps](implement-hosted-saved-rows.md#enable-hosted-saved-rows) you need to take to successfully implement [Hosted Saved Rows](../../../storage/hosted-saved-rows.md). &#x20;

The following video tutorial discusses what Saved Rows are, how reusable content can support your end users throughout their content creation journeys, and how you can implement Hosted Saved Rows in your application.

{% embed url="https://www.youtube.com/watch?v=5m80DgKW0x8" %}
Save Time with Hosted Rows Video Tutorial
{% endembed %}

## **Enable Hosted Saved Rows**

To enable Hosted Saved Rows for your application, follow these steps:

1. Log in to the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application you'd like to configure Hosted Saved Rows for.
3. Click on **Details.**
4. Navigate to **Application configuration** and click **View more.**
5. Scroll to the **Saved Rows** section.
   1.  Toggle on the **Hosted on the Beefree SDK Infrastructure** option.

       <figure><img src="../../../../.gitbook/assets/CleanShot 2024-11-20 at 20.28.15.png" alt="Beefree SDK Developer console user interface displaying the toggle options for hosted and self-hosted saved rows"><figcaption></figcaption></figure>
   2.  Read the pricing information in the popup closely, because additional fees may apply.\*&#x20;

       <figure><img src="../../../../.gitbook/assets/CleanShot 2024-11-20 at 20.28.37.png" alt="Beefree SDK Developer console user interface displaying the popup confirming usage based fees may apply"><figcaption></figcaption></figure>
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

## User Interface and End User Experience

Once you successfully enable Hosted Saved Rows within the Developer Console, your application's end users will have access to a new **Save** icon for each row, and other options for managing the rows they save.

The Hosted Saved Rows UI includes the following experience for end users:

*   End users can save a row using the **Save** icon.    &#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 14.00.04.png" alt="Beefree SDK user interface displaying the save icon on the builder stage end users see"><figcaption></figcaption></figure>
*   They have the ability to name and categorize rows.&#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 14.03.25.png" alt="Beefree SDK user interface displaying the save row modal with Row name and Category options"><figcaption></figcaption></figure>
*   They  can edit a row's name or category and save those changes. &#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 14.07.16.gif" alt="Beefree SDK user interface displaying the edit row options, which allows editing the name or category of a row"><figcaption></figcaption></figure>
*   End users can decide to reuse or delete rows through the **Rows** tab in the side panel.&#x20;

    <figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 14.08.29.gif" alt="Beefree SDK user interface displaying the delete row option, which allows deleting a row"><figcaption></figcaption></figure>
*   They can also use the vertical three dots to add and manage categories.

    <figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 14.09.34.gif" alt="Beefree SDK user interface displaying the add new category option, which allows adding more row categories in the builder"><figcaption></figcaption></figure>

Reference the [Hosted Saved Rows end user documentation](https://docs.beefree.io/end-user-guide/hosted-saved-rows) for more information on the end user steps and experience.

## Limit the Number of Hosted Saved Rows by UID

You can limit the number of Hosted Saved Rows an end user can save by their unique UID. The `maxHostedRowsLimit` parameter lets you define the maximum number of Hosted Saved Rows an end user can create in your Beefree SDK configuration. Use this parameter to establish predictable saving patterns for Hosted Saved Rows within your application.

**Why use `maxHostedRowsLimit`?**

* **Customize at the user level:** Set unique limits per user ID (UID), giving you flexibility to adapt quotas based on specific needs or plan tiers.
* **Control usage and make costs more predictable:** Prevent scenarios where users save large numbers of rows, leading to unexpected usage-based charges. By setting a clear upper limit, you can better forecast and manage your costs.
* **Differentiate your pricing plans:** Create customized experiences for different user segments. For example, offer 3 saved rows to free-tier users and unlock higher limits for premium users. This allows you to align features with your pricing model and incentivize upgrades.

**Code Snippet Example**

The following code snippet shows an example of how to use the `maxHostedRowsLimit` parameter in your `beeConfig` file.

```javascript
const beeConfig = {
  rowsConfiguration: {
    // Define custom row behavior or limitations here
    // e.g., maxColumnsPerRow: 2,
  },
  maxHostedRowsLimit: 10, // Maximum number of hosted saved rows the user can save
};
```

In this example, the user can save up to 10 Hosted Saved Rows. Beefree SDK will block attempts to save more than this limit. &#x20;

### **Custom the Toast Message**

When you limit the number Hosted Saved Rows for an end user, they will see a toast message on the lower right-hand side of the screen when their limit is reached. The default message for this toast message is the following:

> **Title:** Saved rows limit reached
>
> **Description:** You've saved 5 of 5 rows. To save a new row, please delete an existing one first.

The following image shows how this default toast message looks within the user interface.

<figure><img src="../../../../.gitbook/assets/CleanShot 2025-06-07 at 16.14.11.png" alt="Default toast message the end user sees when they&#x27;ve reached their saved rows limit"><figcaption></figcaption></figure>

You can use [Custom Languages](../../../../other-customizations/advanced-options/custom-languages.md) to customize both the title and description text within this message. For example, if you have more of playful brand tone within your application, and want to adjust the message accordingly, you can.&#x20;

In the following code snippet, the default text was changed to the following:&#x20;

> **Title:** Whoa there, design superstar!&#x20;
>
> **Description:** You’ve hit your 5-row max—time to let one go before saving another.

This was achieved by adding the `translations` object to the `beeConfig`, and then adding the strings within the object with the new text.

#### Code Snippet of Example Toast Message Customization

```javascript
var beeConfig = {
  uid: uid, // [mandatory]
  container: "bee-plugin-container", // [mandatory]
  language: "en-US",
  trackChanges: true,
  mergeTags: mergeTags,
  translations: {
    "hosted-content": {
      "save-row-max-limit-error-toast-title": "Whoa there, design superstar! ", // Title text
      "save-row-max-limit-error-toast-description": "You’ve hit your 5-row max—time to let one go before saving another.", // Message text
    },
  },
  saveRows: uid === "Admin" || uid === "Designer",
};
```

## **Configure Advanced Permissions**

Hosted Saved Rows includes [advanced permissions](../../../../other-customizations/advanced-options/advanced-permissions.md#hosted-saved-rows) to control how rows and categories are accessed and managed. These permissions allow you to define user capabilities, such as editing or deleting rows.

### **Available Permissions**

The permissions you can control for Hosted Saved Rows through Advanced Permissions are the following:

* **`canDeleteHostedRow`:** Allows or prevents deleting hosted rows.
* **`canEditHostedRow`:** Enables or disables editing of hosted rows.
* **`canManageHostedRowCategory`:** Controls whether end users can manage row categories.
* **`canAddHostedRowCategory`:** Determines if end users can add new categories.

### **Permission Behavior**

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

<figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 21.02.35.png" alt="User interface showing the save icon and default behavior of saveRows boolean"><figcaption></figcaption></figure>

### Hiding the Save Icon

The following image does not show the save icon when the end user clicks on the row. This behavior occurs after adding `saveRows` to your `beeConfig` and setting it to `false`.

<figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 21.02.03.png" alt="User interface not showing the save icon and the behavior of saveRows boolean when set to false"><figcaption></figcaption></figure>

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

In the following image, the **ROWS** tab is no longer available to the end user. In the following image, the **ROWS** tab is no longer available to the end user and the order of the tabs are **Content** first and **Settings** second.

<figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 15.04.18.png" alt="User interface not showing the rows tab based on the custom configuration"><figcaption></figcaption></figure>

The tab order represented in the snippet below with `settings` first and `content` second, results in the visualization displayed in the image after.

```javascript
defaultTabsOrder: ['settings', 'content']
```

In the following image, the **ROWS** tab is no longer available to the end user and the order of the tabs are **Settings** first and **Content** second.

<figure><img src="../../../../.gitbook/assets/CleanShot 2025-01-27 at 15.10.54.png" alt="User interface not showing the rows tab based on the custom configuration with the order of the tabs showing Settings first and Content second"><figcaption></figcaption></figure>

Reference the [Hosted Saved Rows Webinar](../../../storage/hosted-saved-rows.md#webinar-tutorial) to learn more about other customizations that are compatible with Hosted Saved Rows. The webinar discusses the following topics:

* How to enable Hosted Saved Rows
* How to use [Advanced Permissions](../../../../other-customizations/advanced-options/advanced-permissions.md#hosted-saved-rows) with Hosted Saved Rows
* How to restrict which end users can save rows
* How to customize the modals related to Hosted Saved Rows
* How to use Hosted Saved Rows with [Content Services API](../../../../apis/content-services-api/)

Reference the [sample code in this GitHub repository](https://github.com/mailupinc/beefree-sdk-hosted-saved-rows-demo) to follow along with the [webinar tutorial](../../../storage/hosted-saved-rows.md#webinar-tutorial).

Visit the [Hosted Saved Rows page](../../../storage/hosted-saved-rows.md) to also learn more about the following topics:

* [Troubleshooting and FAQs](../../../storage/hosted-saved-rows.md#troubleshooting-and-faqs)
* [Deactivating Hosted Saved Rows](../../../storage/hosted-saved-rows.md#deactivating-hosted-saved-rows)
* [What Happens When Deactivated](../../../storage/hosted-saved-rows.md#what-happens-when-deactivated)
