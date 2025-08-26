---
description: >-
  This page discusses how to use dynamic images in Beefree SDK to personalize
  email images using recipient data.
---

# Use Dynamic Images for Email Personalization

{% hint style="info" %}
Dynamic Images are available on [Beefree SDK Essentials plan and higher](https://developers.beefree.io/pricing-plans).
{% endhint %}

## Overview

Dynamic images let your end users personalize email designs by swapping static image URLs with dynamic ones that include merge tags or variables (for example, `{{ customer_id }}` or `{{ item.image }}`). This enables them to create an additional layer of email personalization, and dynamically add images to their email designs based on the recipient's data. When the design is exported and sent through a platform like Klaviyo, the sending system replaces the merge tag with the actual value for each recipient based on the available data.

**Examples of dynamic images:**

* Personalized birthday cards (`Happy Birthday {{firstname}}`)
* Countdown timers (for example, `{{ event_date }}` injected into a URL)
* Product recommendations (`{{ item.image }}` from abandoned cart JSON)
* Dynamic ads (monetized newsletter placements)

## How to Activate

By default, the Dynamic images are off. You can enable them by checking them to on within the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).

### Developer Console Steps

Take the following steps within the Developer Console to enable Dynamic images.

1. Navigate to the application you'd like to activate Dynamic images for in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Click on the application’s **Details**.
3. Select **Configure Application**.
4. Scroll to the **Services** section.
5. In the **Content personalization** section, check **Dynamic Images** to **ON**.
6. Save your configuration.

Now, every Image block on the frontend of the editor will show the **Dynamic image toggle** and the **Dynamic URL field**.

The following GIF displays a visual example of what this toggle looks like in the user interface.

<figure><img src="../../.gitbook/assets/CleanShot 2025-08-25 at 15.10.31 (1).gif" alt="GIF displaying the Dynamic images toggle on the frontend of the Beefree SDK email editor" width="275"><figcaption></figcaption></figure>

### End User Workflow

This section discusses what an end user workflow could look like once Dynamic images are enabled within the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu) and available on the email editor's frontend for the end user to use.

1. **Drag an Image block** into a row.
2. In the **Content** tab, navigate to **Image Properties** and toggle **Dynamic image ON**.
3. Enter a **Dynamic URL**.

{% hint style="info" %}
**Note:** Example dynamic URLs are available for reference in the [Example Dynamic Image URL section](use-dynamic-images-for-email-personalization.md#example-dynamic-image-url).
{% endhint %}

Consider the following editor behaviors for end users:

* While designing, the static `URL` field shows a sample placeholder image. This is so end users can envision the layout and size of the dynamic images when the populate the placeholder.
* At send time, the **Dynamic URL** replaces the static image `URL` with recipient-specific content.

## Example Dynamic Image URL

This section provides example static and dynamic URLs.&#x20;

Instead of using a static image like:

```
https://example.com/banners/summer-sale.jpg
```

A dynamic URL with a merge tag might look like:

```
https://example.com/banners/?cust_id={{ customer_id }}&offer={{ offer_id }}
```

Or for abandoned cart product images:

```
{{ item.image }}
```

<figure><img src="../../.gitbook/assets/CleanShot 2025-08-25 at 19.51.39@2x.png" alt="Email of a product loop abandoned cart example showing two dynamic images in separate rows" width="375"><figcaption></figcaption></figure>

Or for countdown timers:

```
https://img.countdownmail.com/timer.png?end={{ event_date }}
```

<figure><img src="../../.gitbook/assets/CleanShot 2025-08-25 at 19.54.27@2x.png" alt="" width="563"><figcaption></figcaption></figure>

These variables (`{{ customer_id }}`, `{{ item.image }}`, `{{ event_date }}`) are replaced by your sending platform (for example, Klaviyo, Salesforce, Mailchimp, and so on) with each recipient’s actual data.

### End User Result

The final result for the end user is the following:

* **In the editor:** They see a sample image (placeholder) for design purposes.
* **In the sent email:** The placeholder is replaced by a unique image URL per recipient.

This allows them to design once, while ensuring each email recipient receives a personalized image.

### References for Developers

The following resources are also helpful when working with dynamic images and email:

* [Using dynamic images for countdown timers and personalized content](https://support.beefree.io/hc/en-us/articles/360004546091-Using-dynamic-images-for-countdown-timers-and-personalized-content)
* [Using dynamic images in product loops for abandoned carts](https://support.beefree.io/hc/en-us/articles/20739290016914-Adding-Dynamic-Content-in-Beefree-for-Klaviyo)
* [Dynamic Image Services like NiftyImages](https://niftyimages.com/)
* [CountdownMail (dynamic timers)](https://countdownmail.com/)
