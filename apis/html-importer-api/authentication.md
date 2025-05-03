---
description: >-
  This page includes instructions on how to obtain your API key for the HTML
  Importer API.
---

# Authentication

## Bearer Token Authentication

Beefree SDK's HTML Importer API uses bearer tokens to authenticate requests. You can create, view, and manage your bearer token in the [Beefree SDK Developer Console](https://developers.beefree.io). All requests must be made over HTTPS and contain the following HTTP Header:

```http
Authorization: Bearer {token}
```

## Create a Bearer Token

To use the HTML Importer API, you will need an API Key, which is the bearer token you will use to authenticate, from the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).&#x20;

Take the following steps to obtain your API key:

1. Log in to the [Beefree SDK Developer Console](https://dam.beefree.io/devmain).
2. Navigate to the application you'd like to activate the HTML Importer API for.
3. Click on the corresponding **Details** button.
4. Navigate to the **HTML Importer API** section of the **Details** page.
5.  Click **Create New API Key**.

    A pop up will appear asking you to confirm that you understand [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) apply.
6. Click **Create Key**.

Your API key will appear under the **HTML Importer API** section of your application details.

<figure><img src="../../.gitbook/assets/CleanShot 2025-05-01 at 18.49.35.png" alt=""><figcaption><p>Screenshot of the Details page in the Developer Console with the HTML Importer section highlighted</p></figcaption></figure>
