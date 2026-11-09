# Pop-up Builder - Getting Started

## Overview <a href="#overview" id="overview"></a>

This section provides the information you need to get started integrating [Pop-up Builder](./) in your SaaS applications. For more advanced settings, see [Pop-up Builder – Advanced Settings](popup-builder-getting-started.md#popup-default-layouts).

## Integration <a href="#integration" id="integration"></a>

Out-of-the-box, the setup and configuration are the same as Email and Page Builder. This section will cover the settings specific to Pop-up Builder. Check out our [Getting Started guide](../../getting-started/readme/installation/) if you’re new to Beefree SDK or unfamiliar with the configuration basics (as seen in the example below).

```json

beeConfig: {
  container: 'bee-plugin-container', // [mandatory]
  ...
}

```

{% hint style="info" %}
**Using an AI agent to help with setup?** Try our Beefree SDK setup skill. It supports Pop-up builder as well as Email builder. [Get the setup skill](https://github.com/BeefreeSDK/beefree-sdk-skills/tree/main/skills/beefree-sdk-setup).
{% endhint %}

Loading Pop-up Builder with no additional settings will give the end-user a beautifully designed pop-up and workspace to design their content. However, Pop-up Builder comes with an additional, robust set of configuration options to customize the workspace. This allows the host application to build a workspace that matches their popup’s look and feel and that of the destination page.

For example, the host app can customize…

* The pop-up workspace background to view how the pop-up will look “in context” on the destination page.
* The theme and position of the pop-up for both desktop and mobile design modes.

The following sections will look at how to customize the workspace, starting with the common settings and working up to a full custom layout.

## The Basics <a href="#the-basics" id="the-basics"></a>

Let’s start by looking at some of the differences between Page Builder and Pop-up Builder.

* Content Width
* HTML output

### Content Width <a href="#content-width" id="content-width"></a>

In Email and Page Builder, the content area width is saved in the template. For example, if you start with an empty template, a default width that works for most scenarios is chosen, but the designer can adjust the message width slider. If you start with an existing template, the content width was chosen by the template’s designer using the message width slider in the the builder’s _Settings_ tab.

With Pop-up Builder, the same template may have multiple contexts, and each context will likely have specific size requirements. For example, an exit-intent pop-up may have a max-width of 600px on a desktop with a classical layout centered on the screen. On the other hand, the host app may display the same template on mobile in the bar style docked at the bottom of the screen with a restricted width of 300px.

Since the content area’s width is tightly coupled to the context and layout, no one size fits all width is saved in the template. Instead, the host app will specify the width settings when the builder loads, based on the context of using the template. You’ll find an example in the common settings section below.

Pop-up Builder does not support fluid 100% width content.

### HTML Output (HTML Partials) <a href="#html-output-html-partials" id="html-output-html-partials"></a>

In Email and Page Builder, the Beefree SDK HTML parser service converts your template into an HTML document customized for email or pages, respectively. However, the Pop-up Builder will not return a full HTML page because the host application is the final destination. In addition, Beefree SDK Pop-up Builder doesn’t provide the scripts to control the pop-up’s behavior, such as opening and closing. Rather, Pop-up Builder provides the HTML “partials” to embed within your pop-up’s content area or body.

The HTML partial will come with all the CSS required to look as it did in the preview mode. The parser service will wrap the content with a special container to clear all the host application styles and prevent style conflicts. The HTML output is designed to be embedded into any pop-up framework or application and still render the way it appears in the builder.

## Pop-up workspace <a href="#popup-workspace" id="popup-workspace"></a>

Now that we covered the basic differences between Pop-up Builder and our other applications let’s discuss what you should expect when the builder starts.

As mentioned above in the Getting Started section, you will receive a ready-to-go design experience if no settings are provided. The default layout is a classic centered modal with a fixed width.

If the default pop-up style and layout suit your needs, then you are all set to start designing! You can load the builder without additional configuration and use the same standard controls and callbacks to access the HTML and JSON template.

What if you like most of the defaults but want to make some minor adjustments? We have you covered!

## Common settings <a href="#common-settings" id="common-settings"></a>

Easily change the background to make the workspace look like the destination page where you’ll embed the pop-up.

```json

beeConfig: {
  ...
  workspace: {
    popup: {
      backgroundImage: 'https://.../background.png',
      backgroundImageMobile: 'https://.../background.png',
      ...
    }
  }
}

```

If this option is not set, then we will provide a default skeleton layout. It’s worth noting at this point that you can apply every setting for both desktop and mobile design modes. That means you can have a different background when editing in _Mobile Design Mode_. We’ll show you how later!

## Pop-up default layouts <a href="#popup-default-layouts" id="popup-default-layouts"></a>

One of the most common needs is changing the pop-up’s default-centered position to better match the end-user’s use case. Out-of-the-box, the Pop-up Builder comes with many of the most common pop-up layouts preconfigured. You can use any available presets “as is” or use them as starting points that you can fine-tune to your satisfaction.

```json

beeConfig: {
  ...
  workspace: {
    popup: {
      layout: 'bar-top'
    }
  }
}

```

Here is a complete list of preset layouts:

| Name                     | Value                                                                                                                                                                                      | Description                                                             |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------- |
| Classic Pop-up           | <p><code>classic-center</code></p><p><code>classic-top-right</code></p><p><code>classic-top-left</code></p><p><code>classic-bottom-right</code></p><p><code>classic-bottom-left</code></p> | This is our default layout and works great for alerts and exit intents. |
| Drawer or Slide-in panel | <p><code>drawer-left</code></p><p><code>drawer-right</code></p>                                                                                                                            | Side panels, or drawers, can be used to design menus or display ads.    |
| Bar or Docker            | <p><code>bar-bottom</code></p><p><code>bar-top</code></p>                                                                                                                                  | This is great for cookie approval dialogs.                              |

## Pop-up default themes <a href="#popup-default-themes" id="popup-default-themes"></a>

Another useful preset available is changing the pop-up’s styles from the default to better match the end-user’s use case. For example, if you’re using the popular Bootstrap CSS framework, you can select the “Bootstrap Theme” as your default. As with the default layouts, you can use any of the available preset themes “as is” or use them as starting points that you can fine-tune to your satisfaction.

```json

beeConfig: {
  ...
  workspace: {
    popup: {
      theme: 'bootstrap'
    }
  }
}

```

Here is a complete list of preset themes:

| Name      | Value       | Description                                                                                                                                |
| --------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Custom    | `custom`    | This is our default layout and works great for alerts and exit intents.                                                                    |
| Bootstrap | `bootstrap` | This will a pop-up that looks like the popular Bootstrap CSS modal.                                                                        |
| jQuery    | `jQuery`    | This will be a pop-up that looks like the popular jQuery modal. Many of the latest CSS systems use a style similar to the original jQuery. |
| Material  | `material`  | This will be a pop-up that looks like the popular Material CSS modal.                                                                      |

## Content area width <a href="#content-area-width" id="content-area-width"></a>

As mentioned above, the content area’s width is tightly coupled to the layout, no one size fits all width is saved in the template. All Pop-up Builder preset layouts come with a default width, which you can override with the following configuration settings.

```json

workspace: {
  popup: {
    contentWidth: 600,
    contentWidthMobile: 300
  }
}

```

Continue to [Pop-up Builder- Advanced Settings](setting-layout-and-size/advanced-settings.md) if you’d like to customize more than the position, background, and content area width.
