# Form structure and parameters

## Overview <a href="#overview" id="overview"></a>

A form is defined through the `structure` object, which includes its main properties.

This is the object that the host application passes to Beefree SDK, and it includes `fields`, `layout,` and `attributes` along with a `title` and a `description` string values that you can use. The appearance of the form, in terms of _styling_ of labels / fields / buttons (spacing, colors, etc…) is handled directly in the application and is saved in the design’s JSON file. Therefore, the same form can be used in different designs, and have message-specific styles.

To take a look at real-world examples and samples, you can head to [our dedicated GitHub page](https://dam.beefree.io/githubbeeforms).

Let’s now examine the anatomy of a Beefree SDK form structure.

```json

{
    "structure": {
        "attributes": {},
		"fields": {},
        "layout": [],
        "title": "Form title",
        "description": "Form description"
    }
}

```

## Attributes <a href="#attributes" id="attributes"></a>

This object contains the general form attributes as strings: all of them are standard HTML5 attributes.

| **Property**     | **Value** |
| ---------------- | --------- |
| `action`         | string    |
| `method`         | string    |
| `target`         | string    |
| `accept-charset` | string    |
| `autocomplete`   | string    |
| `enctype`        | string    |
| `novalidate`     | boolean   |
| `dir`            | string    |

### Fields <a href="#fields" id="fields"></a>

An object that lists all the form fields included in the form with its relative properties. The order in which they appear only matters if you [pass a single form](passing-forms-to-the-builder.md) to an application. If you want to use the content dialog to feed forms in the builder, the order is not relevant and you can set the form layout in the layout array.

Beefree SDK supports the vast majority of standard HTML5 `form` fields. A few of them (such as `color`, `datetime`, `datalist`) have mixed browser support, so please make sure to check [browser compatibility](https://caniuse.com/) before using them.

To see them in action, you can find a few examples on [our dedicated GitHub page](https://dam.beefree.io/githubbeeforms). Head over to [allowed form fields](allowed-form-fields.md) if you need the full list of **allowed field types**, along with the available attributes and options for each of them.

If you want to use a single form, you can use the optional `canBeRemovedFromLayout` and `removeFromLayout` attributes to determine (respectively) if that specific field can be removed from the layout by the user, and if it should appear in the stage when the form is dragged in.

#### **Indicate when a field can be toggled off**

| Attribute                | Applies to | Type    | Default value |
| ------------------------ | ---------- | ------- | ------------- |
| `canBeRemovedFromLayout` | all fields | boolean | true          |

This attribute indicates that a field can be toggled off by the user. If unspecified, it will be applied as true, allowing the user to switch it on or off in the builder UI.

It’s a best practice to add `canBeRemovedFromLayout: false` to mandatory fields (e.g., the email address field in a sign-up form) so that they can’t be excluded in the HTML form.

#### **Toggle off a field when loading a form**

| Attribute          | Applies to | Type    | Default value |
| ------------------ | ---------- | ------- | ------------- |
| `removeFromLayout` | all fields | boolean | false         |

This attribute indicates that a field is toggled off by default when the form is loaded. This behavior is particularly useful to simplify the user experience when you implement forms in the builder through a [default form in the configuration parameters](passing-forms-to-the-builder.md).

## Layout <a href="#layout" id="layout"></a>

If you want to leverage the full power of Beefree SDK forms and use a content dialog to feed the form to the editor’s stage, the `layout` array will determine how the fields will appear to the user.

Each `layout` element is an array itself and represents a single line of fields. This allows different layout dispositions, including multi-column.

Probably the best way to represent this is with an example:

| <pre><code>"layout":[
["name"],
["surname"],
["email"],
["privacy_checkbox"],
["submit"]
]
</code></pre> | <pre><code>"layout":[
["email","telephone"],
["notes"],
["privacy_checkbox"],
["submit"]
]
</code></pre> |
| -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |

<figure><img src="https://docs.beefree.io/wp-content/uploads/2020/03/forms-layout.png" alt=""><figcaption></figcaption></figure>

## Title and description <a href="#title-and-description" id="title-and-description"></a>

The form **title** is a string value. It is not displayed to the user while working in the editor but provides extra information that can be used later for troubleshooting. Likewise, **description** as a string value that is not displayed to the user while working in the editor, but provides extra information that can be used later for troubleshooting or internal reference.

## Using reCAPTCHA <a href="#using-recaptcha" id="using-recaptcha"></a>

reCAPTCHA is a free service from Google that helps protect websites from spam and abuse. To learn more about reCAPTCHA, visit the [official website](https://www.google.com/recaptcha/about/) or Google [technical documentation](https://developers.google.com/recaptcha/) site.

To embed Google ReCaptcha in a Form you need a Google API key for ReCaptcha, the key has to be enabled for a specific website URL or domain; this is crucial because otherwise the script will load but will fail its validation, returning API key errors.

Here’s what’s needed in the submit action when passing a form configuration:

```javascript

"class": "g-recaptcha"
"data-action": "submit"
"data-sitekey": "___YOUR_RECAPTCHA_API_KEY___"
"data-callback": "onSubmit" (this can be optional, check reCaptcha docs)

```

In addition, you have to add an HTML block that imports the reCaptcha library inside the template that encapsulates the form:

```markup

<script src="https://www.recaptcha.net/recaptcha/api.js" async defer></script>

```

Here’s a sample JSON config for the submit button:

```json

"submit": {
  "attributes": {
    "class": "g-recaptcha",
    "data-action": "submit",
    "data-callback": "onSubmit",
    "data-sitekey": "___YOUR_RECAPTCHA_API_KEY___",
    "value": "Login"
  },
  "label": " ",
  "type": "submit"
}

```

Ensure you keep the following in mind:

* Make sure HTML sanitize is OFF (this is the default value).
* Remember that the reCaptcha UI elements will be visible neither in the Beefree SDK work area nor in the Preview, but they will be integrated when the page will be published. Furthermore, the page has to be hosted on the domain that was enabled on the Google Developers Console when setting the reCaptcha.
