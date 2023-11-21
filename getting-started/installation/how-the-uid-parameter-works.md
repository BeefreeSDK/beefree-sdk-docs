# How the UID parameter works

[Pricing for Beefree SDK](https://dam.beefree.io/pluginpricing) is based on the concept of unique users of the editor. A unique user is one that is identified by a unique **UID**, as described below. The system counts unique UIDs within a billing period, and resets the count to zero at the start of the next billing period.

### Properties

The UID parameter:

* Is an alphanumeric string passed to Beefree SDK in the [editor configuration file](https://docs.beefree.io/configuration-parameters/).
* Has a minimum length of 3 characters.
* Can contain letters from a to z (uppercase or lowercase), numbers and the special characters “\_” (underscore) and “-” (dash).
* Make sure that you pass a string, not a numeric value. So even if your UID is a number, pass `"12345"` and not `12345`.
* The UID should not be Personal Data, as indicated in the Beefree SDK License Agreement. Further information about how your use of a Beefree SDK service relates to the EU’s General Data Protection Regulation (GDPR) may be found [here](https://beefree.io/gdpr/). Our Privacy Policy, which describes the processing activities carried out by Beefree SDK as Data Controller, is available [here](https://beefree.io/privacy-cookies-policy/).

### Unique identifier

It uniquely identifies a user of the application. When we say “uniquely”, we mean that:

1. It will be counted as a unique user for [monthly billing purposes](https://dam.beefree.io/pluginpricing).
2. Images (and other files) used by the user when creating and editing messages will be associated with it and not visible to other users (when using the default storage).

### Users, sub-users and client accounts

It’s entirely up to you – the application that has embedded BEE – when to use a new UID at the time you initialize the editor for your users. In 99% of the cases: one UID = one CLIENT ACCOUNT in your application. Sub-users of a client account typically share the same UID.

A quick example to help you visualize this.

* We use the UID in the File Manager to identify where images will be stored
* You typically don’t want client ABC to see client XYZ’s images
* So you will use a certain UID for client ABC and another UID for client XYZ
* If there are 5 users within client ABC account in your application, however, it’s OK that they see the same images, since they are likely collaborating on the same emails or landing pages, so you don’t need to use a different UID: all 5 will share the same UID.

### Related resources

* [How much do you charge for Beefree SDK?](https://beefree.io/bee-plugin/pricing/)
* [How do I configure the editor?](https://docs.beefree.io/configuration-parameters/)
* [Client vs. server-side configurations](https://docs.beefree.io/server-side-options/)
