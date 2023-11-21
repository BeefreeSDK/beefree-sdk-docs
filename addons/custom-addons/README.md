# Custom AddOns

1. [Introduction](broken-reference)
2. [Example of a Custom AddOn](broken-reference)
3. [Availability](broken-reference)
4. [Getting started](broken-reference)

### Introduction <a href="#introduction" id="introduction"></a>

A Custom AddOn is an addon that you typically developed for your own use.

[Partner AddOns](https://docs.beefree.io/addon-development-vendor/) start as Custom AddOns, but are then published to the Partner AddOn Directory, becoming available to all applications that have embedded Beefree SDK.

Most Custom AddOns do not become Partner AddOns and therefore are not published to the Directory. That’s because, in most cases, you create a Custom AddOn to satisfy a use case that is specific to your application.

An example to clarify what we mean.

### Example of a Custom AddOn <a href="#example-of-a-custom-addon" id="example-of-a-custom-addon"></a>

Let’s say you embedded our email editor in your **event engagement platform**, which has a feature that allows event marketers to insert an event ticket’s QR code in marketing campaigns sent to create more engagement around an event.

* You want those marketers, users of your platform, to be able to easily include a QR code in the emails they send to remind people about the event. That way ticket holders can use the QR code to quickly get into the event venue.
* So you decide to create a “QR Code” addon: “QR Code” becomes a new _tile_ in the _Content_ tab in the editor.
* Marketers drag and drop the tile, click on _Select event_ to indicate which event the QR is for, and use the editor to style that section of the message (e.g. size, padding, etc.).
* The QR code is created dynamically by your platform, at the time the email is sent to a ticket buyer.
* The feature is specific to your application.

![](https://docs.beefree.io/wp-content/uploads/2020/02/QRcode\_add2-1024x527.jpg)

### Availability <a href="#availability" id="availability"></a>

Custom AddOns are an advanced feature. As a result, the feature is available on the following [plans](https://dam.beefree.io/pluginpricing):

* Superpowers
* Enterprise

Of course, there are exceptions to this requirement.

* **Testing**: if you are not yet on a Superpowers or Enterprise plan, and you want to test building a Custom AddOn:
  * Create a [development application](https://docs.beefree.io/initializing-bee-plugin/#production-vs-development-apps), as shown [here](https://docs.beefree.io/initializing-bee-plugin/#production-vs-development-apps).
  * Request an upgrade to the Superpowers plan.
  * Test as much as you want. If and when you decide that you wish to deploy your Custom AddOn in production, we will ask you to upgrade your production application to the Superpowers or Enterprise plan.
* **Development of a Partner AddOn**:
  * You provide features that could be a good fit as an extension of our editors
  * You are not a Beefree SDK customer
  * [Learn more about Partner AddOns](https://docs.beefree.io/addon-development-vendor/)

### Getting started <a href="#getting-started" id="getting-started"></a>

Log into the [Beefree SDK Console](https://dam.beefree.io/devmain) and locate any application that is on the Superpowers or Enterprise plans. Click on _Details_ to navigate to the application details page. In the lower part of the page, locate the _Application configuration_ section and click on AddOns.

![Adding a Custom AddOn](https://docs.beefree.io/wp-content/uploads/2020/02/bee-plugin-addons-create-details-icon-1024x766.png)

You will be taken to a page that lists the addons that have been installed for this application. Since you are just getting started, the list is likely empty. Click on _Create a custom addon_ to start the process of creating a Custom AddOn.

![Custom AddOns buttons](https://docs.beefree.io/wp-content/uploads/2022/06/Screenshot-2022-06-27-at-13.59.22.png)

Refer to the [AddOn Development documentation](https://docs.beefree.io/addon-development/) for all the details on building your addon.
