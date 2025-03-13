---
description: >-
  Learn more about Custom AddOns, and how to develop and implement your own
  custom built AddOn.
---

# Custom AddOns

{% hint style="info" %}
This feature is available on Beefree SDK [Superpowers plan](https://dam.beefree.io/pluginpricing) and above. If you're on the Core or Essentials plan, [upgrade a development application](../../../getting-started/readme/development-applications.md) for free to try this and other Superpowers-level features.
{% endhint %}

## Introduction <a href="#introduction" id="introduction"></a>

Custom AddOns are useful when there is a feature you'd like to offer within your application that is not available in our AddOn Marketplace within the Developer Console. In these instances, you can develop your own Custom AddOns for your application's end users.

## Example of a Custom AddOn <a href="#example-of-a-custom-addon" id="example-of-a-custom-addon"></a>

Let’s say you embedded our email editor in your **event engagement platform**, which has a feature that allows event marketers to insert an event ticket’s QR code in marketing campaigns sent to create more engagement around an event.

* You want those marketers, users of your platform, to be able to easily include a QR code in the emails they send to remind people about the event. That way ticket holders can use the QR code to quickly get into the event venue.
* So you decide to create a “QR Code” addon: “QR Code” becomes a new _tile_ in the _Content_ tab in the editor.
* Marketers drag and drop the tile, click on _Select event_ to indicate which event the QR is for, and use the editor to style that section of the message (e.g. size, padding, etc.).
* The QR code is created dynamically by your platform, at the time the email is sent to a ticket buyer.
* The feature is specific to your application.

<figure><img src="../../../.gitbook/assets/QRcode_add2-1024x527 (2).jpg" alt=""><figcaption></figcaption></figure>

## Availability <a href="#availability" id="availability"></a>

Custom AddOns are an advanced feature. As a result, the feature is available on the following [plans](https://dam.beefree.io/pluginpricing):

* Superpowers
* Enterprise

Of course, there are exceptions to this requirement.

* **Testing**: if you are not yet on a Superpowers or Enterprise plan, and you want to test building a Custom AddOn:
  * Create a [development application](../../../getting-started/readme/development-applications.md).
  * Request an upgrade to the Superpowers plan.
  * Test as much as you want. If and when you decide that you wish to deploy your Custom AddOn in production, we will ask you to upgrade your production application to the Superpowers or Enterprise plan.
* **Development of a Partner AddOn**:
  * You provide features that could be a good fit as an extension of our editors
  * You are not a Beefree SDK customer
  * [Learn more about Partner AddOns](../partner-addons/)

## Getting started <a href="#getting-started" id="getting-started"></a>

Log into the [Beefree SDK Console](https://dam.beefree.io/devmain) and locate any application that is on the Superpowers or Enterprise plans. Click on _Details_ to navigate to the application details page. In the lower part of the page, locate the _Application configuration_ section and click on AddOns.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-03-13 at 15.01.17.png" alt=""><figcaption></figcaption></figure>

You will be taken to a page that lists the addons that have been installed for this application. Since you are just getting started, the list is likely empty. Click on _Create a custom addon_ to start the process of creating a Custom AddOn.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-03-13 at 15.01.53.png" alt=""><figcaption></figcaption></figure>

Refer to the [AddOn Development documentation](addon-development.md) for all the details on building your addon.
