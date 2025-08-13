# How the UID parameter works

[Pricing for Beefree SDK](https://dam.beefree.io/pluginpricing) is based on the concept of unique users of the editor. A unique user is one that is identified by a unique **UID**, as described below. The system counts unique UIDs within a billing period, and resets the count to zero at the start of the next billing period.

## Properties

The UID parameter:

* Is an alphanumeric string passed to Beefree SDK throughout the [server-side authorization process](authorization-process-in-detail.md).
* Can contain letters from a to z (uppercase or lowercase), numbers and the special characters “\_” (underscore) and “-” (dash).
* Make sure that you pass a string, not a numeric value. So even if your UID is a number, pass `"12345"` and not `12345`.
* The UID should not be Personal Data, as indicated in the Beefree SDK License Agreement. Further information about how your use of a Beefree SDK service relates to the EU’s General Data Protection Regulation (GDPR) may be found [here](https://beefree.io/gdpr/). Our Privacy Policy, which describes the processing activities carried out by Beefree SDK as Data Controller, is available [here](https://beefree.io/privacy-cookies-policy/).

## Unique identifier

It uniquely identifies a user of the application. When we say “uniquely”, we mean that:

1. It will be counted as a unique user for [monthly billing purposes](https://developers.beefree.io/pricing-plans).
2. Images (and other files) used by the user when creating and editing messages will be associated with it and not visible to other users (when using the default storage).

## Users, sub-users and client accounts

It’s entirely up to you, as the host application, to determine when to use a new UID at the time you initialize the editor for your users. In 99% of the cases: one UID = one CLIENT ACCOUNT in your application. Sub-users of a client account typically share the same UID.

A quick example to help you visualize this.

* We use the UID in the File Manager to identify where images will be stored
* You typically don’t want client ABC to see client XYZ’s images
* So you will use a certain UID for client ABC and another UID for client XYZ
* If there are 5 users within client ABC account in your application, however, it’s OK that they see the same images, since they are likely collaborating on the same emails or landing pages, so you don’t need to use a different UID: all 5 will share the same UID.

## Development Applications

UIDs in production are counted separately from UIDs in a [development application](../development-applications.md). For example, if you have the following UID in both a production and development application, the unique UID will be counted twice toward your plan's allotment.

```javascript
uid: 'test1-clientside' // production uid and development application uid
```

In this scenario, Beefree SDK will treat these as two distinct users, and count this UID twice—once for each environment. Reference [Usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) for more information on Beefree SDK plan types and their corresponding `uid` allotments.

{% hint style="info" %}
**Important:** If you use a unique `uid` across multiple development applications, it will only be counted once. Similarly, if you use a unique `uid` across multiple production applications, it will only be counted once.
{% endhint %}
