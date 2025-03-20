# Meta Tags

{% hint style="info" %}
Meta Tags are available for [Email Builder](../../visual-builders/email-builder.md) and [Page Builder](../../visual-builders/page-builder/).
{% endhint %}

## Overview <a href="#overview" id="overview"></a>

With **Meta Tags**, you can now apply various tags to your HTML that can greatly benefit your SEO and accessibility needs.&#x20;

These Meta Tags include:

* Title
* Description
* Subject
* Preheader
* Language Attributes

For the Email Builder, Meta Tags promote improved deliverability performance. For the Page Builder, Meta Tags promote greater customization and improved search engine results.

## Page Builder

The following image displays the **Title** and **Description** fields from within the page builder.

<figure><img src="../../.gitbook/assets/CleanShot 2024-01-30 at 18.49.13.png" alt=""><figcaption><p>Image 1.0 Page Builder Meta Tags</p></figcaption></figure>

### Title

A page title, also known as a **Title tag**, is a short description of a webpage that appears at the top of a browser window and in SERPs (Search engine results page). This is an important element of an optimized SEO page, as it affects the page ranking in search engines. The title tag will be located within the \<title> element of a page’s HTML output, and its value will be saved inside the JSON template.

Here is an example of what a Title Tag inside Beefree SDK’s HTML output might look like:

```html

<title>Done with love using BeefreeSDK</title>

```

### Description

The **description tag** is located within the \<meta> tag element of a page’s HTML, and it has a limit of 190 characters. The tag will be located within the \<meta> element of the page’s HTML output, and its value will be saved inside the JSON template.&#x20;

Here is an example of what a description tag inside Beefree SDK’s HTML output might look like:

```html

<meta name="description" 
content="This is an example of a meta description. 
This will often show up in search results.">

```

### JSON Page Builder Example

The following code snippet is an example of what the Meta Tags will look like inside the JSON.

```json
    },
    "title": "Empty Template",
    "head": {
      "meta": {
        "title": "The Legendary Elephant King: A Tale of Love, Loss, and Redemption",
        "description": "Experience the timeless story of the elephant king and elephant son as they navigate through tragedy, friendship, and destiny in the elephant kingdom."
      }
    }
  },
```

## Email Builder

The following image displays the **Subject** and **Preheader** fields from within the email builder.

<figure><img src="../../.gitbook/assets/CleanShot 2024-01-30 at 19.22.52.png" alt=""><figcaption></figcaption></figure>

### Subject

The subject field has a maximum of 190 characters. Here is an example of what a subject tag inside Beefree SDK’s HTML output might look like:

```html
<title>🐘 Experience the Epic Tale of an Elephant King!</title>
```

### Preheader

The preheader field has a maximum of 130 characters. Here is an example of what a preheader tag inside Beefree SDK’s HTML output might look like:

```html
<div class="preheader" style="font-size:1px;line-height:1px;display:none;color:#fff;max-height:0;max-width:0;opacity:0;overflow:hidden">
  Join the elephant son on a journey of love, loss, and redemption in the animal kingdom. 🌍
</div>
```

### JSON Email Example

The following code snippet is an example of what the Meta Tags will look like inside the JSON.

```json
    },
    "title": "Empty Template",
    "head": {
      "meta": {
        "subject": "🐘 Experience the Epic Tale of an Elephant King!",
        "preheader": "Join the elephant son on a journey of love, loss, and redemption in the animal kingdom. 🌍"
      }
    }
  },
```

## Language Attribute <a href="#language-attribute" id="language-attribute"></a>

The **HTML lang attribute** is used to identify the language of text content on the web. This information helps search engines return language-specific results, and it is also used by screen readers that switch language profiles to provide the correct accent and pronunciation for accessibility purposes.

When loading the builder, the host application can specify in the configuration a list of languages for their users to choose from (e.g. en-US), see the example below where the only option “Italian, it-IT” is provided. If there are no values provided via configuration file, a standard list of common languages will be provided.

```javascript

beeConfig: {
   ...
   metadata: {
      languages: [
         { value: 'it-IT', label: 'Italian' },
         ...
      ]
    }
}

```

Here is an example of what a language attribute inside Beefree SDK’s HTML output might look like:

```javascript

<html lang="it-IT">

```
