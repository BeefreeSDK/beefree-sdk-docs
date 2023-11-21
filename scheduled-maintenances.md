# Scheduled maintenances

### When is the next scheduled maintenance? <a href="#when-is-the-next-scheduled-maintenance" id="when-is-the-next-scheduled-maintenance"></a>

There are currently no scheduled maintenance or downtime planned for our services.

### FAQs about scheduled maintenances <a href="#faqs-about-scheduled-maintenances" id="faqs-about-scheduled-maintenances"></a>

#### Will the builder be unavailable? <a href="#will-the-builder-be-unavailable" id="will-the-builder-be-unavailable"></a>

Yes. We usually estimate a downtime for the builder. We always make every effort to ensure that maintenance is performed as quickly as possible.

Services not directly related to the builder itself, such as delivery of images hosted in our default storage, are not impacted. In other words, images in messages already created or sent, even if they are hosted by us, will display correctly.

#### What will users of the Beefree SDK builder see? <a href="#what-will-users-of-the-beefree-sdk-builder-see" id="what-will-users-of-the-beefree-sdk-builder-see"></a>

Users that launch the builder during the period of downtime within a maintenance window will see a “We’ll be back soon!” service page, similar to the following.

![](https://docs.beefree.io/wp-content/uploads/2020/03/BEE-maintenance-sm.png)

Note that:

* This message is only shown if you link to _BeePlugin.js_ (recommended implementation), not if you load the file as a local resource.
* The message will only be in English.
* The message will only be shown during the downtime portion of the maintenance window.
* The message will only be displayed to users that launch the builder during a downtime: those that are already using the builder will not see this message. See the next question for information about how they will be affected.

#### What if someone is already using the builder? <a href="#what-if-someone-is-already-using-the-builder" id="what-if-someone-is-already-using-the-builder"></a>

Users that are already using the builder at the time a downtime starts (i.e. “active users”) will experience the builder not responding to certain actions. Some tasks (e.g. moving a content item) will work just fine, but others (e.g. loading a new image) will not respond.

To minimize impact and optimize their user experience, we recommend the following:

1. Ensure your implementation of Beefree SDK takes advantage of the [auto-save feature](https://docs.beefree.io/configuration-parameters/) or [onChange callback](https://docs.beefree.io/tracking-message-changes/#how-it-works), so that the message is frequently auto-saved and no (or minimal) work is lost.
2. Notify users of your application in various ways (e.g. email, a courtesy message inside your application, etc.), informing them of the maintenance window and asking them not to create or edit messages/pages during that window. We recommend that you use a maintenance window that’s a bit larger than the one indicated at the top of this page.
3. Remind them about it as the maintenance window approaches.

#### Do I get notified when a maintenance ends? <a href="#do-i-get-notified-when-a-maintenance-ends" id="do-i-get-notified-when-a-maintenance-ends"></a>

We will send you a “Maintenance completed” email message once the task has been completed. You can also follow our [status page](http://status.beefree.io/) to track the progress of any maintenance work.

#### Is beefree.io affected by maintenances too? <a href="#is-beefreeio-affected-by-maintenances-too" id="is-beefreeio-affected-by-maintenances-too"></a>

Yes, all services at beefree.io are affected. And so are 3 more applications within [Growens](http://mailupgroup.com/), for a total of 5 production instances in our group of companies. And they are all users of Beefree SDK just like you. Any downtime affects us too: no shortcuts or special treatments. So we have every incentive to make sure maintenances are as short and painless as possible.
