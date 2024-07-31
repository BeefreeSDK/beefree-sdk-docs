---
description: Learn how to create an application within the Beefree SDK Developer Console.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Create an Application

## Overview

In this article, we will discuss how to sign up for an account in the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website\_menu), create an application, and obtain your Client ID and Client Secret.&#x20;

This article will cover steps for the following processes:

* [Sign up for an account in the Developer Console](create-an-application.md#sign-up-for-account-in-the-developer-console)
* [How to create an application](create-an-application.md#how-to-create-an-application)
* [Obtain your client secret and client id](create-an-application.md#obtain-your-client-id-and-client-secret)

## Sign up for account in the Developer Console

The first step to embedding Beefree’s visual builders in your software is to[ sign up for a Beefree SDK account](https://developers.beefree.io/accounts/signup/).&#x20;

Take the following steps to sign up for a Beefree SDK account and subscribe to the [Free plan](https://developers.beefree.io/pricing-plans):

1.  Navigate to the [Developer Console Sign Up page](https://developers.beefree.io/accounts/signup/).

    **Note:** If you already have an account, navigate to the [Developer Console Login page instead](https://developers.beefree.io/accounts/login/?from=website\_menu).
2.  Complete the required information to sign up or login.

    You will be redirected to the dashboard.
3.  In the dashboard, click **Add new subscription**.

    You will be redirected to a page that asks you to provide a name for your new subscription.
4.  Type in a name and click **Next**.

    You will be redirected to a page that asks you to select a subscription plan. If you'd like to subscribe to the Free version, click on the corresponding **Select plan** button **Free** plan type. If you'd like to subscribe to a paid plan, select the paid option that works best for your needs.
5.  A confirmation message will appear confirming that you selected the **Free** plan and that you will not be charged anything. Click **Confirm** to confirm your subscription the the free plan.

    <figure><img src="../../.gitbook/assets/CleanShot 2024-07-11 at 14.03.44@2x.png" alt=""><figcaption></figcaption></figure>
6. While the plan is free, ensure that you familiarize yourself with the scenarios in which charges would apply. The following image shows a plan summary displaying instances of when charges apply.

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-11 at 14.05.21@2x.png" alt="" width="375"><figcaption></figcaption></figure>

10. Enter and confirm your billing address.
11. Enter and confirm your card information by clicking **Place Order.**

    You will be redirected your new Free plan subscription.

{% hint style="info" %}
**Important:** Keep in mind that Beefree SDK will not change you for using the Free plan. However, there are charges related to [user and CDN overages](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees). Ensure you review our plans and familiarize yourself with these cost structures as you proceed to use the Free plan.
{% endhint %}

## How to create an application

Once that’s done, you will be able to [log into the Beefree SDK Console](https://developers.beefree.io/accounts/login/).  Your dashboard will look like the following image.

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-11 at 14.11.39@2x.png" alt=""><figcaption></figcaption></figure>

You will have the option to activate any or all of the following applications:

* [Email Builder Application](../../visual-builders/email-builder.md)
* [Page Builder Application](../../visual-builders/page-builder/)
* [Popup Builder Application](../../visual-builders/popup-builder/)
* [File manager Application](../../file-manager/file-manager-application-overview/)

Take the following steps to create an application:

1. Click the **Activate** button that corresponds with the application you'd like to create.
2. Type in a name for your new application.
3. Click **Create**.

Your application will look like the following in the dashboard once it is activated:

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-11 at 15.21.19@2x.png" alt=""><figcaption></figcaption></figure>

You have successfully created an application. Now, you can enter the application **Details** and obtain your Client ID and Client Secret.&#x20;

## Obtain your Client ID and Client Secret

Click on your application's **Details** button to view your **Client ID** and **Client Secret**. Use these to authenticate when you initialize it.

<figure><img src="../../.gitbook/assets/CleanShot 2024-07-11 at 15.25.18@2x.png" alt=""><figcaption></figcaption></figure>

With your Client ID and Client Secret, you can use our [Sample Code](../sample-code.md) to experiment with a simple integration of Beefree SDK. You can also get started with [your own implementation of Beefree SDK](installation/). &#x20;

Reference the following related topics to learn more about customizing your applications, creating development instances, and referencing sample code.&#x20;

* Create [development applications](development-applications.md)
* [Configuration parameters](installation/configuration-parameters/)
* [Toggle on features](../toggle-on-features.md)
* [Server-side options](../../server-side-configurations/server-side-options/)
* [Sample code](../sample-code.md)
