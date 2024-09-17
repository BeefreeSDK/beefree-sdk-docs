# Input Text

This page discusses and lists the various CSS classnames relevant to the application's sidebar widgets where textual input is required. These classnames facilitate the styling and functional integration of widgets such as URLs, images, alt texts, and more, providing a comprehensive guide for developers to enhance the user interface effectively.

This page will cover button classnames for the following sidebar areas:

* [Content](https://docs.beefree.io/beefree-sdk/other-customizations/appearance/custom-css#content)
* [Rows](https://docs.beefree.io/beefree-sdk/other-customizations/appearance/custom-css#rows)
* [Settings](https://docs.beefree.io/beefree-sdk/other-customizations/appearance/custom-css#settings)

## Content <a href="#content-2" id="content-2"></a>

This section lists the classnames for widgets within the Content tab.

### Image <a href="#image-1" id="image-1"></a>

The following table lists the widget, deprecated classnames, and new classnames for the Image content type.

| Widget | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                          |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| URL    | <ul><li><code>number-selector--cs</code></li><li><code>input-image-url</code></li><li><code>item_1-2</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

{% hint style="info" %}
**Note:** The sections below list additional deprecated and new classnames for the Image content type. The table above covers classnames specific to the Image widget, while the following tables include classnames that are shared between the Image content type and other content types.
{% endhint %}

### Image, GIF, and Sticker <a href="#image-gif-and-sticker" id="image-gif-and-sticker"></a>

The following table lists the widget, deprecated classnames, and new classnames for the Image, GIF, and Sticker content types.

| Widget                      | Deprecated                                                                                                                                                                                                                                                                                    | New Classnames                                                                                                                                       |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| Alt Text                    | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul>                                                                 | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul>                                                              |
| Dynamic Image > Dynamic URL | <ul><li><code>number-selector--cs</code></li></ul><ul><li><code>alternate-text--cs</code></li></ul><ul><li><code>item_1-2</code></li></ul><ul><li><code>widget__textbox</code></li></ul><ul><li><code>widget__label</code></li></ul><ul><li><code>widget__label--textbox btn</code></li></ul> | <ul><li><code>input-text--cs input</code></li></ul><ul><li><code>text-boxed--cs</code></li></ul><ul><li><code>dynamic-image-url--cs</code></li></ul> |

### Image, Button, Icons, Menu, GIF, and Sticker <a href="#image-button-icons-menu-gif-and-sticker" id="image-button-icons-menu-gif-and-sticker"></a>

The following table lists the widget, deprecated classnames, and new classnames for the following content types:

* Image
* Button
* Icons
* Menu
* GIF
* Sticker

| Widget               | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                          |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Web page > URL       | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Send email > Mail to | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Send email > Subject | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Send email > Body    | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Tel > Tel            | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Send SMS> Tel        | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Send SMS > Message   | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Image, Button, GIF, Sticker, and Video <a href="#image-button-gif-sticker-and-video" id="image-button-gif-sticker-and-video"></a>

The following table lists the widget, deprecated classnames, and new classnames for the following content types:

* Image
* Button
* GIF
* Sticker
* Video

| Widget     | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                          |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Attributes | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Video <a href="#video" id="video"></a>

The following table lists the widget, deprecated classnames, and new classnames for the video content type.

| Widget | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                          |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| URL    | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Title  | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Social <a href="#social-1" id="social-1"></a>

The following table lists the widget, deprecated classnames, and new classnames for the social content type.

| Widget          | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                          |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Item > Title    | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Item > Alt text | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Item > URL      | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Icons <a href="#icons-1" id="icons-1"></a>

The following table lists the widget, deprecated classnames, and new classnames for the icon content types.

| Widget           | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                          |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Item > Image URL | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Item > Alt text  | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Item > Icon Text | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Item > Title     | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

### Form <a href="#form-1" id="form-1"></a>

The following table lists the widget, deprecated classnames, and new classnames for the Form content types.

| Widget      | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                          |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Field label | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

## All Modules <a href="#all-modules" id="all-modules"></a>

The following table lists the widget, deprecated classnames, and new classnames for all modules.

| Widget           | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                          |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Block identifier | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

## Rows <a href="#rows-2" id="rows-2"></a>

This section lists the classnames for widgets within the Rows tab.

| Widget               | Deprecated                                                                                                                                                                                                                    | New Classnames                                                                          |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Row background image | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |
| Row background video | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul> |

## Settings <a href="#settings-2" id="settings-2"></a>

This section lists the classnames for widgets within the Settings tab.

| Widget               | Deprecated                                                                                                                                                                                                                                                           | New Classnames                                                                                                                             |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Row background image | <ul><li><code>number-selector--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul>                                        | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li></ul>                                                    |
| Title                | <ul><li><code>number-selector--cs</code></li><li><code>alternate-txt--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li><li><code>page-metadata-title--cs</code></li></ul>       |
| Description          | <ul><li><code>number-selector--cs</code></li><li><code>alternate-txt--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul> | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li><li><code>page-metadata-description--cs</code></li></ul> |
| Subject              | <ul><li><code>number-selector--cs</code></li><li><code>alternate-text--cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textboxbtn</code></li></ul>                      | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li><li><code>page-metadata-subject--cs</code></li></ul>     |
| Preheader            | <ul><li><code>number-selector--cs</code></li><li><code>alternate-txt-cs</code></li><li><code>item_1-2</code></li><li><code>widget__textbox</code></li><li><code>widget__label</code></li><li><code>widget__label--textbox</code></li><li><code>btn</code></li></ul>  | <ul><li><code>input-text--cs</code></li><li><code>input-text-boxed--cs</code></li><li><code>page-metadata-preheader-cs</code></li></ul>    |
