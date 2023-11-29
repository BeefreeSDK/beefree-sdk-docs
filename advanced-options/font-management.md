# Font management

{% hint style="info" %}
This feature is available on Beefree SDK [paid plans](https://dam.beefree.io/pluginpricing) only.
{% endhint %}

## Introduction

You can now customize the list of fonts available in the editor’s text toolbar and the BODY settings panel.

This new feature allows you (or users of your app) to:

* Expand the list of available fonts, adding web fonts from popular services, such as Google fonts, font library.org or alike.
* Reduce the list of fonts to a limited number of options, removing some or all our default fonts.

Unlike other premium features, fonts are part of the [client-side configuration](../getting-started/installation/configuration-parameters/), so they can be defined each time the editor is started.

This flexible approach will help you to use this feature in a variety of scenarios. For example:

* You want your users to customize the list of fonts loaded in the builder when they edit designs. You can now create an interface in your app to do so, and instruct the editor accordingly (see below).
* You have multiple levels of users, and you want “contributors” to only see a subset of approved fonts, while “editors” have access to a larger list.
* You are a digital marketing agency, and you want to customize the list of fonts in the editor depending on the client/brand for which the email message is being designed.

For instance, in our hosted [email design suite](https://dam.beefree.io/beepro) (Beefree), we leveraged this Beefree SDK feature to create a “Brand styles > Brand fonts” area where an agency or marketing team can select which fonts have been approved by that brand. Only the selected fonts will be loaded in the builder when an application is initialized. Here is a screenshot.

![Selecting custom fonts in BEE Pro](https://docs.beefree.io/wp-content/uploads/2019/08/settings-new-fonts-cropped.png)

## Adding the editorFonts object

This object, passed as part of the [builder configuration](../getting-started/installation/configuration-parameters/), tells the editor which fonts to load in any drop-down where a list of fonts is shown. It defines the availability of the default fonts and provides a list of additional, custom fonts.

```javascript

editorFonts: {
    showDefaultFonts: true,
    customFonts: [{
        name: "Comic Sans",
        fontFamily: "'Comic Sans MS', cursive, sans-serif"
    }, 
    {
        name: "Lobster",
        fontFamily: "'Lobster', Georgia, Times, serif",
        url: "https://fonts.googleapis.com/css?family=Lobster"
    }]
}

```

In this example default fonts are loaded, and two new fonts are added: a web safe font (Comic Sans) and a Google hosted web font (Lobster).

Here is a more detailed description on how the editorFonts object is built:

### Parameters

<table><thead><tr><th width="220">Parameter</th><th>Description</th></tr></thead><tbody><tr><td><code>showDefaultsFonts</code></td><td>This boolean parameter indicates if the entire list of default fonts is available or not. When the value is false, only the fonts added as custom fonts will be active in the editor.</td></tr><tr><td><code>customFonts</code></td><td><p>When the default font parameter is true, the custom fonts declared inside this object will be added to the list of default fonts: both are loaded into the editor. Otherwise, only custom fonts will be shown.<br>Each <code>customFonts</code> element can have the following properties:</p><table><thead><tr><th width="100">Parameter</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>This string will be shown in the font dropdown list. You can use the term you prefer and we suggest the usage of common font names, but you can go creative and use semantic names that fit on your application. Long strings may impact the interface, so we recommend to keep it short. The characters { } [ ] : ” / \ | ? * are invalid.</td></tr><tr><td><code>fontFamily</code></td><td>Describes the CSS font stack that will be applied to the final HTML. Is important that you provide at least one fallback font to ensure that the text is not displayed using an unwanted font family. Is important that you use single quote marks with the font names instead of double quotation marks to maintain a correct JSON syntax.</td></tr><tr><td><code>url</code></td><td>This parameter is used only when we work with web fonts. Is important that the URL points to a CSS file with the @font-face properties, and not directly to the font files. To work, the CSS must be hosted in HTTPS.</td></tr><tr><td><code>fontWeight</code></td><td>Adds a new option in the dropdown of the content block’s settings for title, button, paragraph, and list blocks (e.g. 100: Thin). If not defined, only Regular (400) and Bold (700) will be available.</td></tr></tbody></table></td></tr></tbody></table>

## Working with custom fonts

When we add a set of custom fonts, we can decide between system fonts and web fonts. Let’s see some details on what you need to know:

System fonts are installed on the operative systems and don’t need any external resource to work, so we can skip the url parameter.

Web fonts are hosted online and need to be loaded by the email client when the email is opened. Beefree SDK accepts only the CSS font embedding method, and the CSS file must be hosted in HTTPS protocol. You can use services like Google fonts, that provides host, font stacks and a well formatted CSS file.

### Usage examples

We want the editor to work with only 2 fonts when creating a message, we want that only Lobster and Cabin fonts are available when editing this message:

```javascript

editorFonts: {
    showDefaultFonts: false,
    customFonts: [{
        name: "Cabin",
        fontFamily: "'Cabin', Helvetica, Arial, sans-serif",
        url: "https://fonts.googleapis.com/css?family=Lobster"
    }, 
    {
        name: "Lobster",
        fontFamily: "'Lobster', Georgia, Times, serif",
        url: "https://fonts.googleapis.com/css?family=Lobster"
    }]
}

```

In the following example, instead, we don’t want to add new fonts but restrict the default ones to our own selection:

```javascript

editorFonts: {
    showDefaultFonts: false,
    customFonts: [{
        name: "Helvetica",
        fontFamily: "'Helvetica Neue', Helvetica, Arial, sans-serif",
    },
    {
        name: "Lucida",
        fontFamily: "'Lucida Grande', 'Lucida Sans', Geneva, Verdana, sans-serif"
    },
    {
        name: "Georgia",
        fontFamily: "Georgia, Times, 'Times New Roman', serif"
     },
     {
        name: "Lato",
        fontFamily: "'Lato', Tahoma, Verdana, sans-serif",
        url: "https://fonts.googleapis.com/css?family=Lato"
     },
     {
        name: "Montserrat",
        fontFamily: "'Montserrat', Trebuchet MS, Lucida Grande, Lucida Sans Unicode, sans-serif",
        url: "https://fonts.googleapis.com/css?family=Montserrat"
      }]
}

```

Notice that if you want to change the default set of fonts, you need to disable them and use custom fonts to indicate the new set, including the URL parameter for web fonts.

This is the complete list of the default fonts in the application and its configuration, including the external URL for web fonts:

```javascript

  {
    name: "Arial",
    fontFamily: "Arial, 'Helvetica Neue', Helvetica, sans-serif"
  }, {
    name: "Courier",
    fontFamily: "'Courier New', Courier, 'Lucida Sans Typewriter', 'Lucida Typewriter', monospace"
  }, {
    name: "Georgia",
    fontFamily: "Georgia, Times, 'Times New Roman', serif"
  }, {
    name: "Helvetica",
    fontFamily: "'Helvetica Neue', Helvetica, Arial, sans-serif"
  }, {
    name: "Lucida Sans",
    fontFamily: "'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Geneva, Verdana, sans-serif"
  }, {
    name: "Tahoma",
    fontFamily: "Tahoma, Verdana, Segoe, sans-serif"
  }, {
    name: "Times New Roman",
    fontFamily: "TimesNewRoman, 'Times New Roman', Times, Beskerville, Georgia, serif"
  }, {
    name: "Trebuchet MS",
    fontFamily: "'Trebuchet MS', 'Lucida Grande', 'Lucida Sans Unicode', 'Lucida Sans', Tahoma, sans-serif"
  }, {
    name: "Verdana",
    fontFamily: "Verdana, Geneva, sans-serif"
  }, {
    name: "ヒラギノ角ゴ Pro W3",
    fontFamily: "ヒラギノ角ゴ Pro W3, Hiragino Kaku Gothic Pro,Osaka, メイリオ, Meiryo, ＭＳ Ｐゴシック, MS PGothic, sans-serif"
  }, {
    name: "メイリオ",
    fontFamily: "メイリオ, Meiryo, ＭＳ Ｐゴシック, MS PGothic, ヒラギノ角ゴ Pro W3, Hiragino Kaku Gothic Pro,Osaka, sans-serif"
  }, {
    name: "Bitter",
    fontFamily: "'Bitter', Georgia, Times, 'Times New Roman', serif",
    url: "https://fonts.googleapis.com/css?family=Bitter"
  }, {
    name: "Droid Serif",
    fontFamily: "'Droid Serif', Georgia, Times, 'Times New Roman', serif",
    url: "https://fonts.googleapis.com/css?family=Droid+Serif"
  }, {
    name: "Lato",
    fontFamily: "'Lato', Tahoma, Verdana, Segoe, sans-serif",
    url: "https://fonts.googleapis.com/css?family=Lato"
  }, {
    name: "Open Sans",
    fontFamily: "'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif",
    url: "https://fonts.googleapis.com/css?family=Open+Sans"
  }, {
    name: "Roboto",
    fontFamily: "'Roboto', Tahoma, Verdana, Segoe, sans-serif",
    url: "https://fonts.googleapis.com/css?family=Roboto"
  }, {
    name: "Source Sans Pro",
    fontFamily: "'Source Sans Pro', Tahoma, Verdana, Segoe, sans-serif",
    url: "https://fonts.googleapis.com/css?family=Source+Sans+Pro"
  }, {
    name: "Montserrat",
    fontFamily: "'Montserrat', 'Trebuchet MS', 'Lucida Grande', 'Lucida Sans Unicode', 'Lucida Sans', Tahoma, sans-serif",
    url: "https://fonts.googleapis.com/css?family=Montserrat"
  }, {
    name: "Ubuntu",
    fontFamily: "'Ubuntu', Tahoma, Verdana, Segoe, sans-serif",
    url: "https://fonts.googleapis.com/css?family=Ubuntu"
}

```

In this example, we want to add font weight options to our list:

```javascript

var editorFonts = {
        showDefaultFonts: true,
        customFonts: [{
          name: "Comic Sans MS",
          fontFamily: "'Comic Sans MS', cursive, sans-serif"
        },{
          name: "Indie Flower",
          fontFamily: "'Indie Flower', cursive",
          url: "https://fonts.googleapis.com/css?family=Indie+Flower"
        },{
          name: "Oswald",
          fontFamily: "'Oswald', sans-serif",
          url: "https://fonts.googleapis.com/css2?family=Oswald:wght@200;300;400;500;600;700&display=swap",
          fontWeight: {
            200: 'Extra-light',
            300: 'Light',
            400: 'Regular',
            500: 'Medium',
            600: 'Semi-bold',
            700: 'Bold',
          }
        }]
      };

```

## Templates with unavailable fonts

We open a saved template that uses fonts that are not available:

* System fonts will display normally in the editor and the text can be edited, but the font-family is not available in the font selector.
* Web fonts will fallback to a system font. Text can be edited and the font-family is not available on the font selector.
* We are able to save the message that already uses unavailable fonts.
