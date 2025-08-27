# Image Title Attribute

{% hint style="info" %}
Available on all builders and all [plans](https://developers.beefree.io/pricing-plans).
{% endhint %}

## Overview

The Image Title Attribute allows end users to add a [custom title attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img#the_title_attribute) to images in their [email](../../../visual-builders/email-builder.md), [page](../../../visual-builders/page-builder/), or [popup](../../../visual-builders/popup-builder/) designs.

Adding a title attribute is an important step toward improving accessibility and user experience. When present, the title attribute provides additional context when a user hovers over an image. Also, screen readers can use it to deliver a verbal description, helping visually impaired users better understand the image in context.

By enabling the title attribute option in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu), your end users can add a custom title attribute to images in their designs, which serves a different purpose than [alt text](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/alt).

When activated, the **Image Properties** in the editor will show a new **Title attribute** field. The following image shows an example of what this looks like in the builder.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-08-19 at 18.26.52@2x.png" alt="Screen of the Beefree SDK user interface showing the Image Properties in the sidebar with the option to add a Title Attribute"><figcaption></figcaption></figure>

## How to Activate the Feature

The Image Title Attribute is off by default and can be enabled through the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).

Take the following steps:

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application where you want to enable the feature.
3. Click on the **Details** button.
4. Navigate to **Application Configurations**.
5. Go to the **Services** section.
6. Check the option for **Title attribute**.
7. Save your configuration.

Once activated, the **Image module** in the editor will display the **Title attribute** field, allowing end users to customize it directly.

## JSON Template Example

When an end user adds a custom title attribute, it will appear in the template JSON alongside the existing image properties.

Example:

```json
{
  "type": "mailup-bee-newsletter-modules-image",
  "descriptor": {
    "image": {
      "alt": "",
      "title": ">>new title<<",
      "src": "",
      "href": "",
      "target": "_blank"
    }
  }
}
```

## Additional Considerations

Consider the following when enabling the the Title attribute for Images in Beefree SDK:

* **Alt vs. Title**: These are separate attributes. End users can define unique values for each, ensuring improved accessibility and SEO compliance.
* **Fallback behavior**: If no **Title** is defined, the field will remain empty, and only the **Alt text** will be available.
* **Accessibility best practice**: The Title attribute should complement, not duplicate, the Alt text. Alt text provides an essential image description, while Title add supplemental context.
