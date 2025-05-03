---
description: Welcome to the Beefree SDK technical documentation!
---

# Introduction to Beefree SDK

## What is Beefree SDK?

Beefree SDK is an embeddable no-code [email](visual-builders/email-builder.md), [landing page,](visual-builders/page-builder/) and [popup](visual-builders/popup-builder/) builder. It enables your end users to achieve their design goals without writing a single line of code. By embedding Beefree SDK into your application, you'll provide your end users with access to a full suite of design features that include the following and more:

* **Email builder:** A [no-code email](visual-builders/email-builder.md) creation environment that helps end users quickly create beautiful emails. This environment supports your end users in following email creation best practices recommended by industry experts.
* **Page builder:** A [no-code landing page](visual-builders/page-builder/) creation environment that empowers end users to build visually stunning landing pages. They can use a landing page as a link for a call-to-action (CTA) inside emails, to embed forms and capture information, or to create standalone pages.
* **Popup builder:** The [popup builder is a no-code environment](visual-builders/popup-builder/) that provides end users with the tools they need to build compelling popups that capture attention.
* **File manager:** A tool to [manage media assets](broken-reference) (images, PDFs, and so on).
* **Template catalog:** A design template catalog that integrates industry best practices to support end users in quickly getting across the finish line with their creations and achieving quick design wins.
* **AI Writing Assistant:** A helpful AI assistant to help end users write their design content.

These builders can easily integrate into your application in minutes. Browse this documentation's latest [sample code](https://www.npmjs.com/package/@beefree.io/sdk) and implementation guides to get started.

## Quick Start <a href="#welcome" id="welcome"></a>

Take the following steps to get started with Beefree SDK in a few minutes:

1. Create an account to access the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu) and obtain your credentials.
2. [Create a new subscription](getting-started/readme/create-an-application.md#sign-up-for-account-in-the-developer-console) to get started. Beefree SDK offers a generous Free plan that includes each builder type mentioned in the previous section.
3. Create an application and [obtain your Client ID and Client Secret](getting-started/readme/create-an-application.md#obtain-your-client-id-and-client-secret).
4. Clone the [beefree-sdk-sample-client repository](https://github.com/BeefreeSDK/beefree-sdk-sample-client), which includes the code for email and popup builder implementations.
5. Add your credentials, the Client ID and Client Secret from step three, inside the placeholders in the code.
6. Once the email builder, or popup builder, depending on which environment you chose, opens, you can start experimenting with the SDK's configuration by customizing the [configuration parameters](getting-started/readme/installation/configuration-parameters/) in the `beeConfig` section of the code.
7. &#x20;You can also customize the SDK's configuration inside the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu) under the [Application configuration section](https://docs.beefree.io/beefree-sdk/server-side-configurations/server-side-options) of the application you created.

{% hint style="info" %}
**Note:** Visit the [Beefree SDK pricing page](https://developers.beefree.io/pricing-plans) for a comprehensive list of features and the plan type they correspond to.
{% endhint %}

## Beefree SDK's Embeddable Builders <a href="#welcome" id="welcome"></a>

Learn more about our three embeddable builders.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Email Builder:</strong> An email editor that makes building gorgeous, mobile-ready emails a breeze.</td><td></td><td></td><td><a href=".gitbook/assets/emailbuilder-e1629383000405.png">emailbuilder-e1629383000405.png</a></td><td><a href="visual-builders/email-builder.md">email-builder.md</a></td></tr><tr><td><strong>Page Builder:</strong> A delightful tool to design beautiful, effective landing pages in minutes, without writing a single line of code.</td><td></td><td></td><td><a href=".gitbook/assets/pagebuilder-e1629383020614.png">pagebuilder-e1629383020614.png</a></td><td><a href="visual-builders/page-builder/">page-builder</a></td></tr><tr><td><strong>Popup Builder:</strong> An easy to deploy, true WYSIWYG solution for designing standout popups.</td><td></td><td></td><td><a href=".gitbook/assets/popupbuilder-e1629383038360.png">popupbuilder-e1629383038360.png</a></td><td><a href="./#beefree-popup-builder">#beefree-popup-builder</a></td></tr></tbody></table>

## File Manager

In addition to our drag-and-drop editors, we also offer a standalone [File Manager](file-manager/file-manager-application-overview/) application, which can be used alongside any of the builders. The File Manager is specifically designed to simplify the organization and management of digital assets, which might happen outside of a content editing session. It is an image and document management user interface that can be launched as a standalone application. This allows your customers to quickly upload or manage assets, without having to load one of the builders.

Learn more about our [File Manager](file-manager/file-manager-application-overview/) and [File Storage Options](server-side-configurations/server-side-options/storage-options/).

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td></td><td>File Manager</td><td></td><td></td><td><a href="file-manager/file-manager-application-overview/">file-manager-application-overview</a></td></tr><tr><td></td><td>Storage Options</td><td></td><td></td><td><a href="server-side-configurations/server-side-options/storage-options/">storage-options</a></td></tr><tr><td></td><td>Configure Your AWS S3 Bucket</td><td></td><td></td><td><a href="server-side-configurations/server-side-options/storage-options/configure-your-aws-s3-bucket.md">configure-your-aws-s3-bucket.md</a></td></tr></tbody></table>

## Customize Your Application with AddOns <a href="#welcome" id="welcome"></a>

Learn more about how our builder AddOns can help you customize your application's offerings.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td></td><td>AI Writing Assistant with Multiple Provider Options</td><td></td><td><a href="builder-addons/addons/partner-addons/ai-writing-assistant/">ai-writing-assistant</a></td></tr><tr><td></td><td>Partner AddOns</td><td></td><td><a href="builder-addons/addons/partner-addons/">partner-addons</a></td></tr><tr><td></td><td>Custom AddOns</td><td></td><td><a href="builder-addons/addons/custom-addons/addon-development.md">addon-development.md</a></td></tr></tbody></table>

## Content Services API and Template Catalog API <a href="#welcome" id="welcome"></a>

The [Content Services API](apis/content-services-api/) allows you to perform a number of tasks (e.g. refreshing the HTML for a certain asset) and add features to your application (e.g. converting an email to a PDF document). We continue to release new API methods to help you enrich and personalize the content design experience for your customers.

The Template Catalog API enables you to incorporate design templates into your application. With this API, you can browse, retrieve, and utilize a variety of pre-designed templates to enhance your user's content creation experience. It gives you the flexibility to offer customized design solutions directly within your platform.

Learn more about [Content Services API](apis/content-services-api/) and [Template Catalog API](apis/template-catalog-api/).

<table data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td></td><td><strong>Content Services:</strong> Export plain text, transform JSON to HTML, and manage brand styles.</td><td></td><td><a href="apis/content-services-api/">content-services-api</a></td></tr><tr><td></td><td><strong>Template Catalog:</strong> Add templates to your application.</td><td></td><td><a href="apis/template-catalog-api/">template-catalog-api</a></td></tr><tr><td></td><td><strong>AI Collection:</strong> Use the AI collection to get metadata, SMS, and summary text.</td><td></td><td><a href="broken-reference">Broken link</a></td></tr></tbody></table>

## Sample Code <a href="#about-this-documentation" id="about-this-documentation"></a>

Browse our sample code to experiment and gain hands-on experience. Get up and running quickly with a simple implementation.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Full-stack application built with NextJS</td><td></td><td></td><td><a href="https://github.com/BeefreeSDK/beefree-sdk-sample-nextjs">https://github.com/BeefreeSDK/beefree-sdk-sample-nextjs</a></td></tr><tr><td>Official NPM package of Beefree SDK</td><td></td><td></td><td><a href="https://github.com/BeefreeSDK/beefree-sdk-npm-official">https://github.com/BeefreeSDK/beefree-sdk-npm-official</a></td></tr><tr><td>A simple HTML sample client to start playing with Beefree SDK</td><td></td><td></td><td><a href="https://github.com/BeefreeSDK/beefree-sdk-sample-client">https://github.com/BeefreeSDK/beefree-sdk-sample-client</a></td></tr><tr><td>Beefree SDK simple React starter</td><td></td><td></td><td><a href="https://github.com/BeefreeSDK/beefree-sdk-demo-react-starter">https://github.com/BeefreeSDK/beefree-sdk-demo-react-starter</a></td></tr><tr><td>Templates to accelerate the set-up of your Beefree SDK integration.</td><td></td><td></td><td><a href="https://github.com/BeefreeSDK/beefree-sdk-assets-templates">https://github.com/BeefreeSDK/beefree-sdk-assets-templates</a></td></tr><tr><td>Explore methods</td><td></td><td></td><td><a href="https://www.npmjs.com/package/@beefree.io/sdk">https://www.npmjs.com/package/@beefree.io/sdk</a></td></tr></tbody></table>

## Developer Essentials <a href="#about-this-documentation" id="about-this-documentation"></a>

Get your free Client ID and Client Secret in the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu) to get started. Experiment with customizing a configuration in the playground. When you're ready, install Beefree SDK.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Developer Console</td><td></td><td></td><td><a href="https://developers.beefree.io/accounts/login/?from=website_menu">https://developers.beefree.io/accounts/login/?from=website_menu</a></td></tr><tr><td>Playground</td><td></td><td></td><td><a href="https://developers.beefree.io/playground">https://developers.beefree.io/playground</a></td></tr><tr><td>Install Beefree SDK</td><td></td><td></td><td><a href="getting-started/readme/installation/">installation</a></td></tr><tr><td>Configuration Parameters</td><td></td><td></td><td><a href="getting-started/readme/installation/configuration-parameters/">configuration-parameters</a></td></tr><tr><td>Create an Application</td><td></td><td></td><td><a href="getting-started/readme/create-an-application.md">create-an-application.md</a></td></tr><tr><td>Authorization Process</td><td></td><td></td><td><a href="getting-started/readme/installation/authorization-process-in-detail.md">authorization-process-in-detail.md</a></td></tr></tbody></table>

### About this documentation <a href="#about-this-documentation" id="about-this-documentation"></a>

These products share the same, unique combination of design flexibility and ease of use. Note that the majority of the documentation applies to all builders (and in many cases to the File Manger too), unless otherwise specified.

{% hint style="info" %}
If you need support at any point throughout your integration, [contact us](https://devportal.beefree.io/hc/en-us/requests/new). We are here to support you along the way.
{% endhint %}
