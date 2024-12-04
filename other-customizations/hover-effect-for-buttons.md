# Hover Effect for Buttons

{% hint style="info" %}
Hover Effect for Buttons is available on [all Beefree SDK plan types](https://developers.beefree.io/pricing-plans) and is available for Email, Page, and Popup builders.
{% endhint %}

## Overview

The Hover Effect allows end users to design a standard view of buttons within their design, and a hover view of the button when a viewer of their email, page, or popup design hovers their cursor over the button. The Hover Effect for Buttons is available as a new content property available under the **Content** tab located within the builder's sidebar. Through applying this Hover Effect, your application's end users can design more attention-grabbing buttons within their design. Reference the Hover Effect for Buttons End User Guide to learn more about how this experience is for your application's end users. Continue reading this page to learn more about how to implement this feature.

To learn more about the end user experience and what it looks like to utilize this feature on the frontend, visit the [Hover Effect for Buttons](https://docs.beefree.io/end-user-guide/hover-effect-for-buttons) white label end user documentation. The markdown file is also available in our [white label docs repository](https://github.com/mailupinc/beefreeSDKwhiteLabelDocs/blob/main/hover-effect-for-buttons.md).

{% hint style="info" %}
**Important:** Hover effects are supported by about 60% of email clients, with notable limitations in Outlook on Windows. View a [list of email clients that are compatible with the Hover Effect Button](https://www.caniemail.com/features/css-pseudo-class-hover/).
{% endhint %}

### Which email clients support the hover effect for buttons?&#x20;

Hover effects are supported by about 60% of email clients, with notable limitations in Outlook on Windows. Reference [this Can I Email resource](https://www.caniemail.com/features/css-pseudo-class-hover/) to view a list of email clients that are and aren't compatible with the Hover Effect for Buttons.

The following GIF displays an example of a button within an email sent to an email client that does support the hover effect.

<figure><img src="../.gitbook/assets/CleanShot 2024-11-26 at 11.46.36.gif" alt=""><figcaption></figcaption></figure>

### What happens if an email client doesn't support the hover effect for buttons?

If an email client doesn't support the hover effect for buttons, the email recipient will see the standard button properties used to design the button when they hover their cursor over it.

The following image displays an example of a button within an email sent to an email client that does not support the hover effect.

<figure><img src="../.gitbook/assets/CleanShot 2024-11-26 at 11.47.41.png" alt=""><figcaption></figcaption></figure>

## Prerequisites

Prior to implementing the Hover Effect button, ensure you have the following:

* [Beefree SDK Developer Console account](https://developers.beefree.io/accounts/login/?from=website_menu)
* [Any Beefree SDK plan type](https://developers.beefree.io/pricing-plans)

## Activation Steps

Take the following steps to toggle on and activate the Hover Effect for Buttons for your application:

1. Log in to your [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application where you'd like to enable Hover Effect for Buttons.&#x20;
3. Click **Details** to navigate to the application's details.
4. Click **Application configuration.**
5. Scroll to the **Services** section.
6. Toggle on the **Enable button hover feature**.

The **Button Hover** section is now available under **Content Properties** within your application's builder.

{% hint style="info" %}
**Note:** This feature is disabled by default for all existing applications. For new applications, it is enabled by default in the [Page](../visual-builders/page-builder/) and [Popup](../visual-builders/popup-builder/) Builder, but is disabled by default for the [Email](../visual-builders/email-builder.md) Builder.
{% endhint %}

## Content Defaults

The following table outlines the properties available within the `hoverStyles` object for buttons. These properties define the visual styles applied to a button when hovered over, including text color, background color, and border styles. Each property can be customized to create engaging and visually dynamic buttons that respond to the viewer's interaction.

### HoverStyles Properties

The following table displays each `hoverStyles` property and its corresponding data type, example, and description.

| Name              | Data Type | Example                   | Description                                                                    |
| ----------------- | --------- | ------------------------- | ------------------------------------------------------------------------------ |
| `color`           | String    | `"#FFFFFF"`               | Sets the font color of the button when hovered.                                |
| `backgroundColor` | String    | `"#16688B"`               | Defines the background color of the button on hover.                           |
| `borderTop`       | String    | `"0px solid transparent"` | Specifies the top border's size, style, and color for the button when hovered. |
| `borderLeft`      | String    | `"0px solid transparent"` | Specifies the left border's size, style, and color for the button on hover.    |
| `borderBottom`    | String    | `"0px solid transparent"` | Specifies the bottom border's size, style, and color for the button on hover.  |
| `borderRight`     | String    | `"0px solid transparent"` | Specifies the right border's size, style, and color for the button on hover.   |

### HoverStyles Inside the Button Schema

The `hoverStyles` object defines the visual changes that occur when a viewer hovers over a button with their cursor on a desktop. It allows you to set hover-specific styles such as font color, background color, and border appearance. These properties can be customized directly in the builder's Content Properties for the button. For example, changing the `backgroundColor` in the **Button Hover** sub-section of **Content Properties** will update the button to reflect that color when hovered over. You can reference an example of a complete [Button Schema on the Content Defaults page](appearance/content-defaults.md#button).&#x20;

```json
"hoverStyles": {
  "color": "#FFFFFF",
  "backgroundColor": "#16688B",
  "borderTop": "0px solid transparent",
  "borderLeft": "0px solid transparent",
  "borderBottom": "0px solid transparent",
  "borderRight": "0px solid transparent"
}
```

## Additional Considerations

Consider the following when using this feature:

* The `mobileStyles` and `hoverStyles` properties are _not_ supported by the [Brand Style Management API](../apis/content-services-api/brand-style-management.md).
* View a [list of email clients that are compatible with the Hover Effect Button](https://www.caniemail.com/features/css-pseudo-class-hover/).
