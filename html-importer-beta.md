---
description: >-
  Welcome to the HTML Importer public Beta! We're excited to hear your feedback
  on this service, and develop it into a tool that'll bring value to your
  workflows, team, and SDK implementation.
---

# HTML Importer Beta

{% hint style="warning" %}
**Beta Feature Notice**

This feature is currently in beta and may change before its official release. We appreciate your feedback and understanding as we continue to improve the HTML Importer experience.&#x20;

**Join the Beta** \
This feature is currently in beta and is only accessible once we've enabled it on your account. If you're interested in testing the endpoint, and sending us feedback about your experience, feel free to [send us a quick note](mailto:beta-feedback@beefree.io?subject=I%27m%20interested%20in%20the%20new%20HTML%20to%20JSON%20converter).

We look forward to hearing your thoughts!

Happy testing,&#x20;

_Beefree SDK Team_
{% endhint %}

## Introduction

Currently, migrating your existing templates into Beefree SDK can be tedious and time-consuming. With the new HTML Importer endpoint, you can transform your existing HTML templates programmatically to Beefree's native JSON format, automating what used to be a majority manual process. With this endpoint, you can count on the majority of the HTML template conversion to be completed in the API call's response. You may still need to perform a few slight edits to the Beefree native JSON after the conversion, but the manual processing is significantly less than before.

## How to use the endpoint

The following diagram provides a high-level visualization of how to perform API calls using the HTML Importer endpoint.&#x20;

{% hint style="info" %}
**Tip:** Keep in mind the content types for both the request and the response bodies of the API call. The [Prerequisites section](html-importer-beta.md#prerequisites) lists important requirements for the HTML you use in the `POST` request body when making the API call. &#x20;
{% endhint %}

<figure><img src=".gitbook/assets/Untitled - Frame 1 (2).jpg" alt="" width="563"><figcaption><p>HTML Importer Endpoint Diagram</p></figcaption></figure>

### Prerequisites

Prior to performing an API call to convert your HTML to Beefree native JSON format, ensure it meets the following requirements:

* `DOCTYPE` declaration
* Include `html` and `body` elements
* To prevent character encoding issues during conversion, include the `<meta charset="UTF-8">` tag in the `head` section of your HTML before converting it.

### Steps to perform the API call

{% hint style="info" %}
**Important:** Prior to performing the steps in this section, ensure you request access to the HTML Importer Beta. If you did not request access yet, you can easily request it by [sending us an email](mailto:beta-feedback@beefree.io?subject=I%27m%20interested%20in%20the%20new%20HTML%20to%20JSON%20converter).&#x20;
{% endhint %}

Take the following steps to perform the conversion:

1. Ensure your API method is set to `POST`
2. Enter the endpoint URL: `https://api.getbee.io/v1/conversion/html-to-json`&#x20;
   1. **Note:** You can do this by setting the `{collection}` as equal to `conversion` in the url `https://api.getbee.io/v1/{collection}/html-to-json`
3. Authenticate by entering your **API key** as a **Bearer Token** in the **Auth Type** field
4. Ensure your request body's `Content-Type` is set to `text/html`
5. Paste the HTML you'd like to convert into the request body field
6. Click **Send**

Within a few seconds, you should receive a response containing the Beefree format JSON.

## Test the endpoint here

You can test the endpoint in the following interactive environment. Ensure you follow the steps outlined in the [Steps to perform the API call section](html-importer-beta.md#steps-to-perform-the-api-call) to successfully execute the API call after clicking the **Test it** button. You can copy and paste the HTML in the **Sample HTML Template to Convert** expandable section below, or use your own HTML as a request body for experimenting with the **Test it** feature.

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

{% openapi src=".gitbook/assets/html-importer-api.yaml" path="/v1/{collection}/html-to-json" method="post" %}
[html-importer-api.yaml](.gitbook/assets/html-importer-api.yaml)
{% endopenapi %}

{% hint style="info" %}
**Note:** You will still need to authenticate in the **Test it** environment before making an API call. Visit the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu) to obtain your API key and enter it in the `bearerAuth` field.&#x20;
{% endhint %}

## FAQs

#### **Explore answers to the most frequently asked questions**

We have gathered some useful questions to help you better understand the beta program and the API you're about to use.

#### What is the HTML Importer API? <a href="#what-is-the-html-to-json-converter-api" id="what-is-the-html-to-json-converter-api"></a>

The HTML Importer API is an API built to easily transform HTML email templates into Beefree's JSON format.

#### What are the benefits of the HTML Importer? <a href="#what-are-the-benefits-of-the-html-to-json-converter-api" id="what-are-the-benefits-of-the-html-to-json-converter-api"></a>

Currently, migrating your existing templates into Beefree can be tedious and time-consuming. With the new HTML Importer, you can transform your existing HTML templates programmatically to Beefree's native JSON format, automating what used to be a manual process.

#### How does it work? <a href="#how-does-it-work" id="how-does-it-work"></a>

The HTML Importer leverages a series of algorithms to map and classify all the content elements available in the email, label them, and then translate them into the Beefree's JSON format.

#### Can I convert any HTML template? <a href="#can-i-convert-any-html-template" id="can-i-convert-any-html-template"></a>

There are a few limitations you should be aware of:

* **The conversion engine is designed to convert email HTML.** It's not optimized for converting landing pages or other HTMLs.&#x20;
* **Our** **API doesn't convert dynamically created HTML documents** that leverage JavaScript to render content. We currently support static HTML and CSS content only.
* **We can't convert emails with images and resources that are only available on private networks**. For us to convert your content, all email resources must be publicly available on the internet.

#### Do you store any of the templates I convert? <a href="#do-you-store-any-of-the-templates-i-convert" id="do-you-store-any-of-the-templates-i-convert"></a>

For the duration of this beta phase, we will store the uploaded HTML templates and the JSON we generate from it to troubleshoot and fix bugs so that our engineers can perform additional tests on existing files. This means we will have access to templates for the whole duration of the beta test, but they will be deleted 60 days after the end of this beta test.

During the beta test, we won't store any user information. If you have any concerns about data and users' information, feel free to contact us directly at [beta-feedback@beefree.io](mailto:beta-feedback@beefree.io) at any time.

#### What is the applicable use policy? <a href="#what-is-the-applicable-use-policy" id="what-is-the-applicable-use-policy"></a>

You can use this tool following the provisions of [Beefree Terms of Service](https://developers.beefree.io/terms-of-service). In particular, you should use the tool in a way that ensures you will not violate the rights of third parties.

#### I have questions, feedback, or a bug to report. Who should I contact? <a href="#i-have-questions-feedback-or-a-bug-to-report.-who-should-i-contact" id="i-have-questions-feedback-or-a-bug-to-report.-who-should-i-contact"></a>

The HTML Importer is a beta test. Therefore, some hiccups may happen along the way—and we'd love for you to tell us if you experience any so we can improve the tool going forward.

If you want to contact us to report a bug or provide feedback, email us at [beta-feedback@beefree.io](mailto:beta-feedback@beefree.io).

#### What expectations do you have for me as a beta tester? <a href="#what-expectations-do-you-have-for-me-as-a-beta-tester" id="what-expectations-do-you-have-for-me-as-a-beta-tester"></a>

This program is designed to help us gather feedback and improve our product—and the more feedback we receive from customers like you, the easier it is for us to create a solution that truly meets your needs. That's why we'd love it if you would:

* Share any feedback or questions you might have while using the API. You can do that by emailing beta-feedback@beefree.io.
* Respond to our questionnaire, which we'll send to all beta users to gather feedback.
* Be open to jumping on a call with our Product team to talk about your experience and needs.

#### Is this importer free of charge? <a href="#is-this-converter-free-of-charge" id="is-this-converter-free-of-charge"></a>

Access to the HTML Importer will be free during the beta. However, please note that we may charge for the converter in the future.

#### Can I use the API access provided in the beta program for production?

No, the API access provided in the beta program is strictly for testing and development purposes. It is not intended for production use, as the beta version may be subject to changes, downtime, or limitations that could impact reliability. We recommend using the stable, production-ready API for any live applications whenever it becomes available.

## Complete the survey

Complete the survey below to share your thoughts on the HTML Importer API. We're excited to hear what you think, and to make this service widely available soon.

{% embed url="https://growens.typeform.com/to/y4Fot0Sc#source=docs" %}
