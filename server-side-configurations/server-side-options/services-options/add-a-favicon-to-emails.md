# Add a Favicon to Emails

{% hint style="info" %}
Available for [Email](../../../visual-builders/email-builder.md) and [Page](../../../visual-builders/page-builder/) builders and on all [plans](https://developers.beefree.io/pricing-plans). This page discusses how to enable the Favicon for the Email Builder.
{% endhint %}

## Overview

You can add favicons to email designs in the email builder. Adding a favicon directly to an email's HTML is beneficial when the email is viewed in a browser, and the end user would like a favicon to display in the browser tab.

When activated in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu), a new **Configure favicon** option becomes available in the **Settings tab** of the builder, where end users can select or edit their favicon.

The following image shows an example of what this looks like in the builder.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-08-19 at 18.41.11@2x.png" alt="Screenshot of the Beefree SDK builder showing the Settings tab and the Add favicon option" width="375"><figcaption></figcaption></figure>

## How to Activate the Feature

The Favicon option is off by default and must be enabled in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).

Take the following steps:

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application where you’d like to activate favicon support.
3. Click on the **Details** button.
4. Navigate to **Application Configurations**.
5. Go to the **Services** section.
6. Check the option for **Favicon enabled**.
7. Save your configuration.

Once enabled, a **Favicon section** will appear in the editor’s **Settings tab**, allowing end users to upload and manage favicon assets.

### JSON Template Example

When a favicon is added, the configuration is reflected in the template JSON under the `head.meta.favicon` object.

Example:

```json
{
  "page": {
    "head": {
      "meta": {
        "favicon": [
          {
            "handle": "request_image_url",
            "url": "https://d15k2d11r6t6rl.cloudfront.net/public/users/Integrators/BeeTestingMachinePage/testmachine/upgrade-trial-modal.png"
          },
          {
            "handle": "source",
            "url": "https://d15k2d11r6t6rl.cloudfront.net/public/users/Integrators/BeeTestingMachinePage/testmachine/favicon_images/upgrade-trial-modal-dbe339-source.png"
          },
          {
            "handle": "16-icon",
            "url": "https://d15k2d11r6t6rl.cloudfront.net/public/users/Integrators/BeeTestingMachinePage/testmachine/favicon_images/upgrade-trial-modal-dbe339-16-icon.png"
          },
          {
            "handle": "32-icon",
            "url": "https://d15k2d11r6t6rl.cloudfront.net/public/users/Integrators/BeeTestingMachinePage/testmachine/favicon_images/upgrade-trial-modal-dbe339-32-icon.png"
          },
          {
            "handle": "apple-touch-icon",
            "url": "https://d15k2d11r6t6rl.cloudfront.net/public/users/Integrators/BeeTestingMachinePage/testmachine/favicon_images/upgrade-trial-modal-dbe339-apple-touch-icon.png"
          }
        ]
      }
    }
  }
}
```

### Additional Considerations

Consider the following when activating the Favicon option within the Beefree SDK Developer Console:&#x20;

* **Cross-platform consistency**: Favicons will only display when an email is opened in a browser. They won’t appear directly inside email clients.
* **Multiple formats supported**: End users can upload different favicon sizes (e.g., 16x16, 32x32, Apple Touch icons) for maximum compatibility across platforms.
* **Landing page similarity**: This update brings favicon support for email in line with what was already available for [landing pages](../../../visual-builders/page-builder/), ensuring consistency across experiences.
