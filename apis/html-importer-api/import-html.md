---
description: Learn more about using the HTML Importer API endpoint.
---

# Import HTML

## Overview

This page discusses how to use the HTML Importer API endpoint. Follow the instructions outlined in this page to successfully perform API calls.

{% hint style="info" %}
**Important:** Ensure you complete the [Authentication steps](authentication.md) and obtain your API key prior to performing the steps on this page.&#x20;
{% endhint %}

## Prerequisites

Prior to performing an API call, ensure the HTML you are using in the body of the `POST` request meets the following requirements:

* `DOCTYPE` declaration
* Include `html` and `body` elements
* To prevent character encoding issues during the conversion, include the `<meta charset="UTF-8">` tag in the `head` section of your HTML before converting it.

## Steps to perform the API call

Take the following steps to perform the conversion:

1. Ensure your API method is set to `POST`
2. Enter the endpoint URL: `https://api.getbee.io/v1/conversion/html-to-json`&#x20;
   * **Note:** You can do this by setting `{collection}` equal to `conversion` in the following url: `https://api.getbee.io/v1/{collection}/html-to-json`
3. Authenticate by entering your **API key** as a **Bearer Token** in the **Auth Type** field
4. Ensure your request body's `Content-Type` is set to `text/html`
5. Paste the HTML you'd like to convert into the request body field and ensure it meets the requirements outlined in the [Prerequisites section](import-html.md#prerequisites)
6. Click **Send**

Within a few seconds, you should receive a response containing the Beefree JSON.

## Test the endpoint here

You can test the endpoint in the following interactive environment. Ensure you follow the steps outlined in the [Steps to perform the API call section](import-html.md#steps-to-perform-the-api-call) to successfully execute the API call after clicking the **Test it** button. You can copy and paste the HTML in the **Sample HTML Template to Convert** expandable section below, or use your own HTML as a request body for experimenting with the **Test it** feature.

{% hint style="warning" %}
**Required:** Ensure you manually type in `text/html` in the `Content-Type` field prior to making the API call.
{% endhint %}

<details>

<summary>Sample HTML Template to Convert</summary>

You can use the following template if you'd like to test a conversion now:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Adopt a Dog</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background-color: #f9f9f9;
            color: #333;
            text-align: center;
        }
        .container {
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            background: #fff;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        img {
            max-width: 100%;
            height: auto;
            border-radius: 8px;
        }
        p {
            font-size: 16px;
            line-height: 1.5;
        }
        .cta {
            margin-top: 20px;
        }
        .cta a {
            display: inline-block;
            padding: 10px 20px;
            background-color: #007bff;
            color: #fff;
            text-decoration: none;
            border-radius: 5px;
            font-weight: bold;
        }
        .cta a:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <img src="https://s3.amazonaws.com/cdn-origin-etr.akc.org/wp-content/uploads/2019/09/28115848/Shih-Tzu-snuggling-on-a-babys-lap-outdoors.jpg" alt="Adopt a Dog">
        <p>
            Dogs are everyone's best friend. They bring joy, love, and loyalty into our lives. <br>
            Consider adopting one today and give a furry friend a forever home.
        </p>
        <div class="cta">
            <a href="https://www.petfinder.com/" target="_blank">Adopt Now</a>
        </div>
    </div>
</body>
</html>
```

</details>

{% openapi-operation spec="html-importer" path="/v1/{collection}/html-to-json" method="post" %}
[Broken link](broken-reference)
{% endopenapi-operation %}

{% hint style="warning" %}
**Note:** You will still need to authenticate in the **Test it** environment before making an API call. Visit the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu) to obtain your API key and enter it in the `bearerAuth` field.&#x20;
{% endhint %}
