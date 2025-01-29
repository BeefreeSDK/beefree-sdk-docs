# Content Area Padding

{% hint style="info" %}
This feature is available on all [Beefree SDK plans](https://beefree-sdk-testing.webflow.io/pricing-plans). It is available for Email, Page, and Popup builders.
{% endhint %}

## Overview

Content Area Padding allows end users to precisely adjust the padding around the content inside of any row. This provides them with greater design flexibility, precision, and control. By managing padding on all sides—top, bottom, left, and right—they can fine-tune the spacing within their layouts to achieve clean, professional, and visually appealing designs easily.

By using Content Area Padding, end users can:

*   Design outer areas with different colors.

    <div align="left"><figure><img src="../.gitbook/assets/CleanShot 2025-01-15 at 14.52.49.gif" alt="" width="563"><figcaption></figcaption></figure></div>
*   Add transparent borders.&#x20;

    <div align="left"><figure><img src="../.gitbook/assets/CleanShot 2025-01-15 at 15.20.59.gif" alt="" width="563"><figcaption></figcaption></figure></div>
* Gain precise control over padding, borders, and spacing.
* Use row-level padding to manage spacing without disrupting the row's content.

The following GIF displays how end users can apply padding around content within their rows.

<div align="left"><figure><img src="../.gitbook/assets/CleanShot 2025-01-10 at 16.08.29.gif" alt="" width="563"><figcaption></figcaption></figure></div>

Reference the [white label end user guide ](https://docs.beefree.io/end-user-guide)to learn more about the end user experience. You can clone the Markdown files in this [GitHub repository](https://github.com/mailupinc/beefreeSDKwhiteLabelDocs/blob/main/content-area-padding.md) and customize the instructions for your application's end users.&#x20;

## Prerequisites

Prior to activating Content Area Padding, ensure you have the following:

* A [Beefree SDK plan](https://beefree-sdk-testing.webflow.io/pricing-plans)
* An application in the [Developer Console with a Client ID and Client Secret](https://developers.beefree.io/accounts/login/?from=website_menu)

## Activation

To activate Content Area Padding, you'll need to complete the following:

* Enable the toggle in the [Developer Console](content-area-padding.md#developer-console).

{% hint style="info" %}
**Note:** Content Area Padding is on by default for new applications. For existing applications, it is off by default and will need to be toggled on in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
{% endhint %}

### Developer Console Steps

Take the following steps to activate the feature within the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu):

1. Log in to your [Developer Console account](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application you'd like to activate it for.
3. Click on **Details**.
4. Click **Application configuration**.
5. Navigate to the **Services** section.
   1. Toggle on the **Enable content area padding** option located in the second section.

<figure><img src="../.gitbook/assets/CleanShot 2025-01-14 at 13.05.39.gif" alt=""><figcaption><p>GIF displaying the <strong>Enable content area padding</strong> toggle</p></figcaption></figure>

Once you toggle on the feature, the **Content Area Padding** option will be available to your application's end users. In the builder, they can locate the option inside the **Layout** section under the **ROWS** tab.

<div align="center"><figure><img src="../.gitbook/assets/CleanShot 2025-01-14 at 13.08.22@2x.png" alt="" width="375"><figcaption><p>Image of the builder sidebar displaying Content Area Padding</p></figcaption></figure></div>

## Optional Functionality

This section lists optional functionality available for Content Area Padding, including the option to set restrictions and permissions for feature access.

### Content Defaults

Content defaults refer to the predefined settings for Content Area Padding that serve as the base configuration for all content within your application. By utilizing Content defaults, you can maintain uniformity across the user interface without needing to apply manual adjustments for each row.

```json
{
  "row": {
    "padding": "20px",
    "paddingLeft": "25px",
    "paddingRight": "20px",
    "paddingTop": "15px",
    "paddingBottom": "10px"
  }
}
```

Learn more about[ Content Area Padding for Content defaults](appearance/content-defaults.md#row).

### Advanced Permissions

Advanced Permissions in the context of Content Area Padding refer to the granular control settings that you can use to manage who can view and not view padding options within your application. These permissions ensure that only authorized users have access to adjust padding settings.

The following JSON displays an example of the `show` and `locked` boolean options with the `padding` configuration.

```json
{
  "padding": {
    "show": true,
    "locked": false
  }
}
```

Learn more about [Content Area Padding for Advanced Permissions](advanced-options/advanced-permissions.md#rows).

### Row AddOn | Simplified Rows Schema

With Row AddOns, you can create custom row structures that your users can gain inspiration from and design with. They give you greater control over the UI, enabling you to further personalize the experience you provide to your end users.

#### Simplified Rows Schema

The Simplified Rows Schema optimizes the definition of data structures, leading to consistent and reusable configurations. By implementing **Content Area Padding** within this schema, padding settings for Row AddOns are standardized, ensuring data uniformity. This uniformity simplifies custom API development and database integration by aligning data structures with application requirements.

Learn more about [Content Area Padding for Simplified Rows Schema.](../rows/reusable-content/create/#simplified-rows-schema)

## Additional Considerations

Consider the following when using Content Area Padding:

* Content Area Padding is  compatible with the [Brand Management API](../apis/content-services-api/brand-style-management.md). However, note that the Brand Management API is not compatible with the `mobileStyles` property.
