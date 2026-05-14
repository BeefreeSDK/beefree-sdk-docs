---
description: >-
  Learn more about configuring the privacy and security settings of your Beefree
  SDK implementation.
---

# Privacy and Security

{% hint style="info" %}
Every Beefree SDK plan includes privacy and security customization options, with additional advanced features available on paid plans.
{% endhint %}

## Overview

In the [Beefree SDK Developer Console](https://developers.beefree.io/), you'll find categories of **Application Configurations** you can customize to personalize your application. This page discusses the customization options available under the **Privacy and Security** section.&#x20;

This category of Application Configurations enable you to customize the following:

* Anonymous error logging
* Custom limitation for the [File Manager](/broken/pages/83RZ3kjKoee6zmYCTvF1)
* [HTML sanitizer](../custom-head-html.md#the-sanitizer-and-adding-custom-html) for the HTML content block and [Custom Head HTML](../custom-head-html.md)

The following image shows how these options appear within the Developer Console.&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-04 at 10.23.08.png" alt=""><figcaption></figcaption></figure>

### Customizing Privacy and Security

This section defines what each customization option under **Privacy and Security** is. It also explains how to edit an existing configuration.

#### Edit an Existing Configuration

Take the following steps to edit an existing configuration:

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io/).
2. Navigate to the application you'd like to edit a configuration for.
3. Click on **Details**.
4. Navigate to **Application Configuration** and click **Configure Application**.
5. Scroll down to the **Privacy and Security** section.
6. Select or deselect the configuration using the checkbox.
7. Click the purple **Save changes** button to apply the updated configuration to your application.

The following image shows an example of selecting the **Disable anonymous error logging** option with the Developer Console.

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-04 at 11.39.17.png" alt=""><figcaption></figcaption></figure>

#### Anonymous Error Logging

We use third-party tools to aggregate anonymous usage data. It helps us develop a better product by assessing locations, devices, browsers, etc. This can be turned off if necessary.

#### HTML Sanitizer Service

When you enable the [Custom HTML](https://docs.beefree.io/end-user-guide/content-blocks/custom-html#html-tag-restrictions-in-emails) content block or allow users to add [Custom Head HTML](https://docs.beefree.io/end-user-guide/design-tools/add-custom-head-html), they can add custom HTML to their content. The sanitize service checks and cleans HTML, helping prevent the introduction of unsafe content or tags that might affect deliverability. However, disabling it can be useful if the host application needs custom HTML tags or attributes.

* When you disable the HTML sanitization service, you’re removing all restrictions on what users of the builder can add inside the Custom HTML content block.
* If disabled, you should implement an alternative code review process, such as using the `onChange` or `onSave` [events](../../getting-started/readme/installation/methods-and-events.md) to review content.
* The [client-side configuration](../../getting-started/readme/installation/configuration-parameters/) allows enabling (`forceSanitizeHTML: true`) per user, but cannot disable sanitization for security reasons.

**You can** [**customize the sanitizer's whitelist**](../custom-sanitize-rules.md)**.** When the HTML Sanitizer is enabled, you can override its default list of allowed tags, attributes, and link protocols — independently for the HTML content block and for Custom Head HTML — by passing the `sanitizeRules` parameter in your client-side configuration. See [Custom Sanitize Rules](../custom-sanitize-rules.md) for the full reference.

#### Custom Limitations on the File Manager

In this section, you can manage the restrictions for the [file manager](services-options/broken-reference/):

* Specify which file formats your users can upload.
* Set a maximum file size (limit: 20MB).

Instead of file extensions, categories such as image, video, or text are shown, mapped to [MIME types](../../file-manager/file-manager-application-overview/file-extensions-and-groups.md).

The following image shows how you can manage the limitations to the File Manager.

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-04 at 11.47.31.png" alt=""><figcaption></figcaption></figure>

#### File Type Limitations

The following table details which files are available for each Beefree SDK plan type.&#x20;

<table><thead><tr><th width="139">Plan type</th><th width="300">Default-allowed file types</th><th width="300">Configurable file types</th></tr></thead><tbody><tr><td>Free plans</td><td>Image, video, and PDF </td><td>No other file types can be added</td></tr><tr><td>Paid plans</td><td>Image, video, and PDF </td><td>Text, audio, office, xml, zip, epub, postscript, and font MIME types</td></tr></tbody></table>

If you’d like to allow your users to upload additional file types, you’ll need to explicitly enable those specific MIME types in the Custom Limitations section of your SDK Console.

#### Potentially Harmful Content Blocking

The system prevents harmful uploads by enforcing:

* Automatic blocking for all users of potentially dangerous file extensions such as exe, msi, bat, iso, jar, apk, SVGs containing JavaScript, HTML with redirects and more. These files can never be uploaded even if the custom limitations on the File Manager are removed.
* Antivirus scanning that targets malicious files.

