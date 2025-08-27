# Custom Head HTML

{% hint style="info" %}
Requires [Core plan](https://developers.beefree.io/pricing-plans) or above. Available for Email or Page Builders.&#x20;
{% endhint %}

## Overview <a href="#how-to-activate-the-feature" id="how-to-activate-the-feature"></a>

With Custom Head HTML, you can offer your end users a way to inject custom HTML into the `<head>` section of their email and page templates.

More sophisticated end users might ask for this functionality to support advanced use cases, including linking to external CSS stylesheets, adding custom meta data, setting favicons, adding the required code to power Gmail Annotation functionality, and more. Whether your end users are developers refining email behavior, designers looking for different ways to control styling, or marketers embedding important tracking links, you’re giving them the flexibility they need.

The HTML block and the Custom Head HTML setting have different available tags and attributes that are unique to each feature when the sanitizer is on. You can reference a comprehensive list of available tags and attributes in the [Add Custom Head HTML end user guide](https://docs.beefree.io/end-user-guide/design-tools/add-custom-head-html). You can also reference a comprehensive list of available tags and attributes for the HTML block in the [Custom HTML end user guide](https://docs.beefree.io/end-user-guide/content-blocks/custom-html#html-tag-restrictions-in-emails).

This page will discuss how to implement and configure Custom Head HTML within your application.

## How to Activate the Feature <a href="#how-to-activate-the-feature" id="how-to-activate-the-feature"></a>

This is a server-side configuration. You can activate the Custom Head HTML option by heading over to the Developer Console and checking the option to **on** and saving your changes.

Take the following steps to enable Custom Head HTML in your server-side configurations:

1. Log in to the [Beefree SDK Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application you’d like to activate Custom Head HTML for.
3. Click the **Details** button for that application.
4. Navigate to the **Application Configuration** section of the **Details** page and click View more under **Application Configuration**.
5. Scroll to the **Settings** section and check the option for **Custom Head HTML**.
6. Save your configuration by clicking the Save button on the upper right-hand side of the screen.
7. Head over to your frontend and start adding **Custom Head HTML** in the **Setting** tab.

**Optional:** Add [Advanced Permissions](../other-customizations/advanced-options/advanced-permissions.md) to your configuration to control access on the UID level.

## JSON Template Example <a href="#how-to-activate-permissions" id="how-to-activate-permissions"></a>

When your end users add custom HTML to the `<head>` tag, it will be appended at the end of the email or page JSON. The following JSON shows an example template with custom `<head>` HTML added.

<details>

<summary>Example template with custom <code>&#x3C;head></code> HTML</summary>

The following JSON shows an example template with custom `<head>` HTML. You can reference it in the `"head"` object.

```json
{
  "page": {
    "body": {
      "container": {
        "style": {
          "background-color": "#FFFFFF"
        }
      },
      "content": {
        "computedStyle": {
          "linkColor": "#0068A5",
          "messageBackgroundColor": "transparent",
          "messageWidth": "500px"
        },
        "style": {
          "color": "#000000",
          "font-family": "Arial, Helvetica, sans-serif"
        }
      },
      "type": "mailup-bee-page-properties",
      "webFonts": []
    },
    "description": "Empty template for BEE",
    "rows": [
      {
        "columns": [
          {
            "grid-columns": 12,
            "modules": [
              {
                "type": "mailup-bee-newsletter-modules-heading",
                "descriptor": {
                  "heading": {
                    "title": "h1",
                    "text": "<span class=\"tinyMce-placeholder\">I'm a new title block</span>",
                    "style": {
                      "color": "#555555",
                      "font-size": "23px",
                      "font-family": "inherit",
                      "link-color": "#0068A5",
                      "line-height": "120%",
                      "text-align": "center",
                      "direction": "ltr",
                      "font-weight": "700",
                      "letter-spacing": "0px"
                    }
                  },
                  "style": {
                    "width": "100%",
                    "text-align": "center",
                    "padding-top": "0px",
                    "padding-right": "0px",
                    "padding-bottom": "0px",
                    "padding-left": "0px"
                  },
                  "mobileStyle": {}
                },
                "locked": false,
                "uuid": "080c2ac7-6898-48c0-a7f3-f39f20b2ecc8"
              }
            ],
            "style": {
              "background-color": "transparent",
              "border-bottom": "0px solid transparent",
              "border-left": "0px solid transparent",
              "border-right": "0px solid transparent",
              "border-top": "0px solid transparent",
              "padding-bottom": "5px",
              "padding-left": "0px",
              "padding-right": "0px",
              "padding-top": "5px"
            },
            "uuid": "1ef6284e-df55-4032-b5de-e98ee22ebcbe"
          }
        ],
        "container": {
          "style": {
            "background-color": "transparent",
            "background-image": "none",
            "background-position": "top left",
            "background-repeat": "no-repeat"
          }
        },
        "content": {
          "computedStyle": {
            "hideContentOnDesktop": false,
            "hideContentOnMobile": false,
            "rowColStackOnMobile": true,
            "rowReverseColStackOnMobile": false,
            "verticalAlign": "top"
          },
          "style": {
            "background-color": "transparent",
            "background-image": "none",
            "background-position": "top left",
            "background-repeat": "no-repeat",
            "color": "#000000",
            "width": "500px"
          }
        },
        "empty": false,
        "locked": false,
        "synced": false,
        "type": "one-column-empty",
        "uuid": "05c8500f-a206-456a-936c-2ea9bdcfe0ca"
      }
    ],
    "template": {
      "name": "template-base",
      "type": "basic",
      "version": "2.0.0"
    },
    "title": "Empty Template",
    "head": {
      "customTags": "<style>\n  h1 { color: salmon; }\n</style>"
    }
  },
  "comments": {}
}
```

</details>

Reference the Custom Head HTML white label end user guide for more examples of how your end users can apply Custom Head HTML to their email HTML.

## How to Activate Permissions <a href="#how-to-activate-permissions" id="how-to-activate-permissions"></a>

Once you enable the Custom Head Tags check, you'll have the option to set [Advanced Permissions](../other-customizations/advanced-options/advanced-permissions.md#settings) within your Beefree SDK configuration. This controls access at the UID level, allowing you to configure it for individual users or groups of users based on your configuration.

The following code snippet includes the available Advanced Permissions options for Custom Head Code.

```javascript
advancedPermissions: {
  settings: {
    customHeadTags: {
      show: true,
      locked: false,
    }
  }
}
```

## The Sanitizer and Adding Custom HTML

When using Custom HTML in the email builder, a code sanitizer will validate your code. It will automatically correct some issues, such as HTML tags that are left open. It will also strip out code that often isn't supported by email clients. For example, script and iframe tags are removed since, when used incorrectly, they often cause deliverability problems and security risks.

If the sanitizer is **off**, you can add any custom HTML in the `<head>` section you'd like. However, it is important to consider that using your own code can negatively impact rendering results and deliverability. So please make sure you (and your end users) proceed with caution.

Take the following steps to enable or disable the HTML sanitizer within your application:

1. Log in to the Developer Console
2. Navigate to your email builder application
3. Select **Details**
4. On the **Details** page, click **Application configuration**
5. Scroll down to the **Privacy and Security** section
6. Toggle **Disable the HTML sanitizer service in the HTML content block** on or off
7. Save your configuration&#x20;

<figure><img src="../.gitbook/assets/CleanShot 2025-07-17 at 17.31.02.png" alt="" width="511"><figcaption></figcaption></figure>

## Additional Considerations <a href="#how-to-activate-permissions" id="how-to-activate-permissions"></a>

Prior to adding your own custom `<head>` HTML, consider the following:

* If the sanitizer is on, you can only use the following tags in the custom `<head>` HTML section:
  * `base`
  * `link`
  * `meta`
  * `style`
  * `title`
* If the sanitizer is on, you can only use the attributes listed in the attributes by tag table. You can reference the complete table in the [Add Custom Head HTML end user guide](https://docs.beefree.io/end-user-guide/design-tools/add-custom-head-html).
  * **Note:** If the sanitizer is off, you can use any HTML attribute or tag. This option should be used carefully to ensure designs are still responsive and render correctly.
* You cannot edit existing HTML within the `<head>` tags, you can only add [custom HTML](https://docs.beefree.io/end-user-guide/content-blocks/custom-html)  that will be appended at the end of the `<head>` section.
* When the [sanitizer](custom-head-html.md#the-sanitizer-and-adding-custom-html) is on, the HTML block and Custom Head HTML setting have different available tags and attributes that are unique to each feature.
