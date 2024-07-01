---
description: >-
  Learn more about how to activate cards style widgets and image rounded
  corners.
---

# Cards Style and Image Round Corners

{% hint style="info" %}
This feature is available for all [Beefree SDK plan types](https://developers.beefree.io/pricing-plans). Available for Email Builder, Page Builder, and Popup Builder.
{% endhint %}

## Implementing Image Rounded Corners and Card Style Features

This guide explains how to enable the Image Rounded Corners and Cards Style features in your host application. It provides instructions for making these features available to your application's end users while they are designing emails, pages, and popups.

### Cards Style

Cards Style is a Row Property that enables you to create space between columns and round the corners of columns within a row.

The Cards Style feature allows users to transform ordinary messages into visually appealing layouts that grab their audience’s attention effortlessly. By incorporating stylish cards, users can effectively highlight product features, display customer testimonials, promote special offers, and present news updates in a structured and eye-catching manner. This not only enhances the readability and engagement of emails, pages, and popups but also ensures that important information stands out and resonates with viewers, providing significant value to the end-users and enriching their design experience within your application.

{% embed url="https://beefree.screencasthost.com/watch/cZ1uqcV803R" %}

Reference the [Column Management article in the White label end user guide](https://docs.beefree.io/end-user-guide/column-management#cards-style) to learn more about how your application's end users can use this feature.

### Image Round Corners

The Image Round Corners feature allows your application's end users to easily add rounded corners to images from the side panel, enhancing the visuals of emails, pages, and popups. This built-in tool offers a sleek and professional design option, ensuring a modern look.

Together, these features empower your application’s end-users to create more compelling and attractive designs effortlessly. Users can employ these stylistic options to make their content more engaging and easier to scan.

{% embed url="https://beefree.screencasthost.com/watch/cZ1uqiV800C" %}

Reference the [Images article in the White label end user guide](https://docs.beefree.io/end-user-guide/images#image-rounded-corners) to learn more about how your application's end users can use this feature.

## Prerequisites

Ensure you have the following prior to activating Cards Style and Image Round Corners:

* Beefree SDK account (any plan type)
* An application in the developer console
* Client ID and Client Secret

## How to Activate

Take the steps outlined in this section to enable Image Rounded Corners and Cards Style Widgets.

### Activate Image Rounded Corners

This section discusses how to enable Image Rounded Corners.

To activate Image Rounded Corners, follow these steps:

1. Log in to your developer console
2. Navigate to your application
3. Enter your application's configurations
4. Navigate to the **Enable image rounded corners** toggle
5. Toggle it to on

### Activate Cards Style Widget

This section discusses how to enable Cards Style.

Follow these steps to enable the Cards Style Widget for your application:

1. Log in to your developer console.
2. Navigate to your application.
3. Enter your application's configurations.
4. Find the **Enable cards style widgets** toggle.
5. Toggle it on.

### Implementing Rounded Corners and Card Style Using Content Defaults

You can implement the image rounded corners and cards style features using content defaults in your application's configuration. The following code snippet demonstrates how to set the properties related to these features.

```json
{
  "image": {
    "borderRadius": "30px"
  },
  "row": {
    "styles": {
      "backgroundColor": "red",
      "contentAreaBackgroundColor": "green",
      "verticalAlign": "bottom",
      "columnsBorderRadius": "10px",
      "columnsSpacing": "20px",
      "columnsStackOnMobile": false,
      "columnsReverseStackOnMobile": true,
      "columnsPadding": "42px",
      "columnsBackgroundColor": "yellow"
    }
  }
}
```

In this configuration:

* **Image Rounded Corners**: The `borderRadius` property under the `image` key sets the border radius to "30px".
* **Cards Style Widgets**: The `row` key contains styling properties for widgets, such as `columnsBorderRadius`, `columnsPadding`, and `columnsBackgroundColor`.

Visit the [Content Defaults](appearance/content-defaults.md#row) page to learn more about these configurations.

### Advanced Permissions for Customization

To control the permissions for the Cards Style and Image Round Corners features, use the following configuration sample.

```json
{
  ...
  "rows": {
    ...
    "columnsSpacing": {
      "show": true,
      "locked": false
    },
    "columnsBorderRadius": {
      "show": true,
      "locked": false
    }
  },
  "image": {
    ...
    "properties": {
      ...
      "borderRadius": {
        "show": true,
        "locked": false
      }
    }
  }
}
```

This configuration allows you to manage whether these features are visible and editable to your application's end users.

The properties in the advanced permissions code snippet control the visibility and editability of specific interface elements related to Cards Style and Image Round Corners. By setting `"show": true`, these elements will be displayed to end users. The `"locked": false` property ensures that these settings can be modified by the end users. These configurations set the permissions for these features within your host application.

Visit the [Advanced Permissions page](advanced-options/advanced-permissions.md#rows) to learn more about these configurations.

### Additional Considerations

Consider the following when using Cards Style and Image Round Corners:

* Round corners for Cards, Images, and Content Areas are not rendered in Outlook clients. The fallback is squared corners.
* Visit Using Cards Style and Image Round Corners to learn more about how end users can use these features in your application's user interface.
