# CSAPI Overview

{% hint style="info" %}
This feature is available on Beefree SDK [paid plans](https://dam.beefree.io/pluginpricing) only.
{% endhint %}

## A richer content creation experience <a href="#a-richer-content-creation-experience" id="a-richer-content-creation-experience"></a>

Beefree SDK is a complete content design and creation platform for you to build upon. Our objective is to help you create a fantastic content creation experience for your customers inside your software applications.

As this may go beyond the interactions that happen within our email, page, and popup builders, we created an API to offer more assistance. We call it the Content Services API: it exposes a set of services that will help you provide a better experience with how emails, pages, and popups are created, updated, and transformed into different formats.

## Overview <a href="#in-a-nutshell" id="in-a-nutshell"></a>

The Content Services API (CSAPI) – helps you achieve the following:

* Retrieving the HTML of an email, page or popup created with a Beefree builder, so you can build a custom UX flow for saving messages. With the CSAPI, you can ask the Beefree system for the HTML whenever you need it.
* Updating the HTML of an email, page or popup created with a Beefree builder, without user interaction. Why? For example, the HTML of an email template might need to be updated (e.g. to resolve a newly discovered rendering issue in an email client), and you don’t want to ask your users to open the email with the builder and resave it.
* Outputting partial HTML that enables you to reuse code, increase consistency across your templates, and easily maintain your code.
* Generating a thumbnail from the HTML, because thumbnails are always nice to have, for all sorts of reasons 🙂
* Generating a PDF from the HTML, as your users may want to share or print an email or a page, and PDF is great for that.
* Merging shared content ([saved rows](../../rows/reusable-content/create/save/implement-self-hosted-saved-rows/)) into emails and pages that use it (e.g. update 30 emails that use the same footer).
* Use [Brand Style Management](brand-style-management.md) to make template-wide design changes to existing templates quickly and easily.
* Generate [plain text](content-services-api-reference.md#plain-text) versions of emails from JSON templates, ensuring emails look sharp and easy to read on any device.
* [Leverage AI](content-services-api-reference.md#ai-collection) to generate SMS, Metadata (Preheader and Subject), or Summary text from JSON templates.

### Getting the HTML from a message JSON <a href="#getting-the-html-from-a-message-json" id="getting-the-html-from-a-message-json"></a>

This service allows the host application to build a custom workflow that doesn’t rely on the `onSave` callback in the editor ([list of available callbacks](../../getting-started/readme/installation/methods-and-events.md)). Check our [reference documentation on how to use the API to get the HTML from a JSON file](content-services-api-reference.md).

### **A Few Common Use Cases**

#### **Getting newer, better HTML**

The first reason for this API to exist is a common use case: a transactional message was created months ago, it does not need to be edited in the editor, but its HTML code needs to be updated to benefit from fixes or changes that resolve rendering issues.

As you know, HTML for email is a mix of old markup – needed by email clients with a lack of support for standards – and advanced tricks used to take advantage of modern email client capabilities. The result is an environment that changes continuously, driven by the discovery of new techniques and by software updates released by the most popular email clients and browsers.

Having the ability to update the HTML without user interaction in the editor means ensuring that your customers can take advantage of the latest fixes or improvements, even if the messages are transactional notifications created years ago and never edited.

#### **Displaying the preview for incorrectly saved messages**

It’s not common, but it may happen that a browser crashes before the user saves a message they are working on. In this scenario, using the `autosave` or the `onChange` callbacks are enough to prevent any work loss. However, the host application ends up storing a message JSON without the HTML counterpart.

This presents the problem as the two files are out of sync, making things hard for the host application to get a preview, and, therefore, hard for the user to understand if they are looking at the right version of the message.

Using the API the host application can generate an updated HTML from the latest JSON, solving the issue.

#### **Eliminating the need for “Save” buttons**

A step further in the use case described above. Some modern applications remove any “Save” button from the UI, autosaving the work every time a change is applied (e.g. Google Docs). Through the `onChange` callback, your application can reproduce this behavior, and get the HTML from the saved JSON, when needed.

#### Getting additional output formats <a href="#getting-additional-output-formats" id="getting-additional-output-formats"></a>

The API provides some useful services that offer additional message formats, reducing the development effort in the host application.

#### **Generating a PDF file from an HTML**

A dedicated endpoint that transforms an HTML into a PDF document and supports the following options:

#### **Page orientation**

Landscape and portrait as available values.

#### **Page size**

Letter, A4, A3, and Full as available values.

While the other values split the message into pages, the Full option returns a single page using 900px as the page width and the proportional height.

PDF is often used in most approval processes, but is also a perfect format for printers. Check our [reference documentation on how to use the API to get a PDF from an HTML file](content-services-api-reference.md).

#### **Generating image files from an HTML**

An endpoint that creates an image from an HTML source supporting the following options:

**Width**\
The image width in pixels

**Height**\
The image height in pixels

When the height is not provided, the API applies a proportional value based on the given width, keeping the image aspect ratio. When the Height value is provided, but not proportional to the given width:\
&#xNAN;_&#x49;f it’s higher:_ the proportional value applies\
&#xNAN;_&#x49;f it’s lower:_ the image is cropped

Check our [reference documentation on how to use the API to get images from an HTML file](content-services-api-reference.md).

#### Merging saved rows in existing messages <a href="#merging-saved-rows-in-existing-messages" id="merging-saved-rows-in-existing-messages"></a>

What if a footer is shared by 10 messages and needs to be updated in all of them? The [Synced Rows](../../rows/reusable-content/sync/implement-synced-rows.md) feature was created precisely to address the scenario of content that is shared across multiple emails, pages, or popups, and it is used in conjunction with the Content Services API.

The [Merge method](content-services-api-reference.md) of the Content Services API allows you to update a row across multiple messages. More specifically, it allows the host application to update an element in an existing JSON document. This means that, for instance, you could create a feature that takes care of updating existing messages in the background, without any further action by your users.

The [Index method](content-services-api-reference.md) of the Content Services API is a complementary method, designed to retrieve the assets which contain saved rows, so that you know which assets need update using the Merge method.

There are many use cases, including:

* updating headers & footers;
* changing the expiration date in a seasonal offer;
* making price changes, link changes, etc. in content that otherwise can be re-used “as is”
* etc.
