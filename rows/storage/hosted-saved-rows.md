# Hosted Saved Rows

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above.
{% endhint %}

## **Overview**

Hosted Saved Rows offers a fully managed solution, eliminating the need to set up and maintain backend systems. With this option, Beefree SDK handles storage, security, scaling, and updates, allowing your team to focus on delivering a great user experience. In addition to managing storage, this option also provides you with a [ready-to-go user interface](hosted-saved-rows.md#ready-to-go-user-interface) made available to your application's end users through a toggle in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).&#x20;

This [ready-to-go UI](hosted-saved-rows.md#ready-to-go-user-interface) enables application end users to:

* Save a row and make it available for reuse in the future.
* Add new saved row categories to organize the rows they save.
* Edit a saved row's existing name and category.
* Delete a saved row.
* Update existing saved rows with the option to save them as new saved rows.&#x20;

### **Key Benefits**

* Fully managed by Beefree SDK, and activated through a toggle in the Developer Console.
* Ideal for teams that want a quick setup without maintaining backend systems.
* Offers centralized storage, security, and reliability, while also providing a user interface to save and  reuse rows within your application.
* Allows for advanced controls through configuring [Advanced Permissions for Hosted Saved Rows](../../other-customizations/advanced-options/advanced-permissions.md#hosted-saved-rows).

### Webinar Tutorial

Learn more about how to enable and customize Hosted Saved Rows in the following video. The webinar discusses:

* How to enable Hosted Saved Rows
* How to use [Advanced Permissions](../../other-customizations/advanced-options/advanced-permissions.md#hosted-saved-rows) with Hosted Saved Rows
* How to restrict which end users can save rows
* How to customize the modals related to Hosted Saved Rows
* How to use Hosted Saved Rows with [Content Services API](../../apis/content-services-api/)

Reference the [sample code in this GitHub repository](https://github.com/BeefreeSDK/beefree-sdk-hosted-saved-rows-demo) to follow along with the webinar tutorial.

{% embed url="https://www.youtube.com/watch?v=BSqWRusx2fg" %}
Webinar on Hosted Saved Rows
{% endembed %}

## **Enable Hosted Saved Rows**

To enable Hosted Saved Rows for your application, follow these steps:

1. Log in to the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application you'd like to configure Hosted Saved Rows for.
3. Click on **Details.**
4. Navigate to **Application configuration** and click **View more.**
5. Scroll to the **Saved Rows** section.
   1.  Toggle on the **Hosted on the Beefree SDK Infrastructure** option.

       <figure><img src="../../.gitbook/assets/CleanShot 2024-11-20 at 20.28.15.png" alt=""><figcaption></figcaption></figure>
   2.  Read the pricing information in the popup closely, because additional fees may apply.\*&#x20;

       <figure><img src="../../.gitbook/assets/CleanShot 2024-11-20 at 20.28.37.png" alt=""><figcaption></figcaption></figure>
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

## **Deactivating Hosted Saved Rows**

If you decide to deactivate Hosted Saved Rows:

1. Return to the **Beefree SDK Console**.
2. Toggle the **Hosted on the Beefree SDK Infrastructure** option to **off**.
3. Save your changes.

### **What Happens When Deactivated**

* Hosted Saved Rows are removed from visibility in the builder.
* After 90 days, all Hosted Saved Rows data is permanently deleted unless the feature is reactivated.

## **Troubleshooting and FAQs**

#### **Can I reactivate Hosted Saved Rows after disabling it?**

Yes, if reactivated within 90 days, previously Hosted Saved Rows will be restored. To fully restore rows across all applications, re-enable Hosted Saved Rows for each application.

#### What is a Hosted Saved Row? <a href="#what-is-a-hosted-row" id="what-is-a-hosted-row"></a>

Beefree SDK has introduced an updated version of the popular Saved Rows feature called Hosted Saved Rows. With this feature, Beefree SDK is responsible for storing Saved Rows in its own S3 Bucket and handling all the necessary steps for allowing your users to save and reuse rows.

#### What are the biggest benefits of this feature for your end users? <a href="#what-are-the-biggest-benefits-of-this-feature-for-your-end-users" id="what-are-the-biggest-benefits-of-this-feature-for-your-end-users"></a>

End users can now easily save and reuse rows across multiple designs, including emails, pages, and popups. They can quickly find and manage Hosted Saved Rows by category.

#### What is the difference between Hosted Saved Rows and Self-Hosted Saved Rows? <a href="#what-is-the-difference-between-hosted-rows-and-saved-rows" id="what-is-the-difference-between-hosted-rows-and-saved-rows"></a>

The benefit for your users remains the same—they can save and reuse rows instead of rebuilding them every time. The only difference is that with Hosted Saved Rows, you don't have to develop all the necessary steps within your application on your own. All you need to do is activate the feature through a toggle in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).

#### Where are the Hosted Saved Rows stored? <a href="#where-are-the-hosted-rows-stored" id="where-are-the-hosted-rows-stored"></a>

We will store your end users' Hosted Saved Rows in a Beefree S3 Bucket. Each row will be exclusively used for the given UID belonging to the subscription.
