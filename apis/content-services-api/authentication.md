---
description: Learn how to authenticate to access the Content Services API's resources.
---

# Authentication

## Bearer Token Authentication

Beefree SDK's Content Services API uses bearer tokens to authenticate requests. You can create, view, and manage your bearer token in the [Beefree SDK Developer Console](https://developers.beefree.io). All requests must be made over HTTPS and contain the following HTTP Header:

```http
Authorization: Bearer {token}
```

## Create a Bearer Token

To use the Content Services API you will first need to obtain a your API Key—the bearer token you will use to authenticate to make API calls—from the Beefree SDK Developer Console.&#x20;

To obtain an API Key, take the following steps:

1. Log in to the [Beefree SDK Developer Console](https://dam.beefree.io/devmain).
2. Navigate to the application you'd like to activate the Content Services API for.
3. Click on the corresponding **Details** button.
4. Navigate to the Content Services API section of the **Details** page.
5.  Click **Create New API Key**.

    A pop up will appear asking you to confirm that you understand [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) may apply.
6. Click **Create Key**.

Your API key will appear under the **Content services API** section of your application details.

<figure><img src="../../.gitbook/assets/CleanShot 2025-05-01 at 18.53.41.png" alt=""><figcaption><p>Screenshot of the Details page in the Developer Console with the CSAPI section highlighted</p></figcaption></figure>
