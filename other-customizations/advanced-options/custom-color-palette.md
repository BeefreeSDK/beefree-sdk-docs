# Custom Color Palette

{% hint style="info" %}
This feature is available on Beefree SDK [paid plans](https://dam.beefree.io/pluginpricing) only.
{% endhint %}

## Color picker palette overview <a href="#color-picker-palette-overview" id="color-picker-palette-overview"></a>

The builder’s color palette gathers a list of the default colors to display from multiple sources in order to create a convenient palette of color selections when the editor loads.

Specifically, colors are gathered as follows:

* 3 colors from the body (message background, content background, link) + black (#000000)
* custom colors (as many as customers want)
* 7 most recently used colors

Use the options outlined below to customize the default color palette.

## Choosing the default colors in the color picker <a href="#choosing-the-default-colors-in-the-color-picker" id="choosing-the-default-colors-in-the-color-picker"></a>

The builder allows you to configure a custom color palette (per user), by modifying the client-side configuration. This, for instance, allows you to provide users with easy access to their company’s brand colors.

If no color profile is provided, then the builder will continue to suggest a color palette based on the colors used in the template that is being loaded.

```javascript

var beeConfig = {
        uid: config.uid,
        defaultColors: ['#ffffff', '#000000', '#95d24f', '#ff00dd'],
        ...        

```

## Advanced Permissions for the Color Picker

{% hint style="info" %}
You can set [Advanced Permissions](advanced-permissions.md) for the Color Picker on any builder type (Email, Page, or Popup). Advanced Permissions are available for [Superpowers](https://developers.beefree.io/pricing-plans) and [Enterprise](https://developers.beefree.io/pricing-plans) plans.  &#x20;
{% endhint %}

Through setting [Advanced Permissions](advanced-permissions.md) for the color picker, you can control the visibility of, and access to, color codes, the slider, and swatches that appear within builder. These customization options enable you to control access to various elements of the color picker for different end users of your application.&#x20;

A few of the benefits of applying advanced permissions to the Color Picker are the following:

* **Enhanced brand control** – Gain granular control over color selection to ensure brand consistency.
* **Improved user experience** – Streamline the interface by showing only necessary elements.

A few scenarios in which these advanced permissions are particularly helpful include the following:

* Customizing the color picker UI based on user roles or workflows.
* Hiding unnecessary UI elements to improve accessibility and reduce distractions.
* Enforcing strict brand color guidelines by limiting available color options.

### Configuration Steps

Take the following steps&#x20;

1. **Update the `beeConfig` File:** Open the `beeConfig` file and locate the section for `advancedPermissions`. Within this section, ensure there is a field for `components` and add a new entry specifically for the `colorPicker`.
2. **Define Permission Settings:** Within the color picker section, specify the necessary parameters that determine user access. Set the relevant parameters to either `true` or `false`, depending on whether the feature should be enabled or restricted for the end user.

#### Code Sample

The following code sample displays an example of how to add advanced permissions for the color picker to your configuration.

```javascript
const advancedPermissions = {
    ...,
    components: {
      ...,
      colorPicker: {
        canViewColorInput: true,
        canViewSliders: true,
        canViewSwatches: true,
      }
    }
}
```

#### Available Settings

The table below outlines the configurable parameters for the color picker.

| Parameter           | Type    | Description                                                         | Additional info         |
| ------------------- | ------- | ------------------------------------------------------------------- | ----------------------- |
| `canViewColorInput` | boolean | Hides or shows the text input for the color picker in the sidebar.  |  Default value is true. |
| `canViewSliders`    | boolean | Hides or shows the sliders inside the color picker popover.         |  Default value is true. |
| `canViewSwatches`   | boolean | Hides or shows the swatches inside the color picker popover.        |  Default value is true. |

{% hint style="info" %}
**Note:** If both `canViewSliders` and `canViewSwatches` are set to `false`, the popover will not open.
{% endhint %}

## Disabling the color history <a href="#disabling-the-color-history" id="disabling-the-color-history"></a>

The builder will remember recently selected colors and add them to your color palette.  If the browser’s privacy settings allow it, the color picker history will be saved in the browser’s local storage.

If you want the color palette to be static such that recently selected colors are not included, then you can disable the history in your configuration.

```javascript

var beeConfig = {
        uid: config.uid,
        disableColorHistory: true,
        ...        

```

## Disabling the template's base colors <a href="#disabling-the-templates-base-colors" id="disabling-the-templates-base-colors"></a>

The builder by default adds colors found in the template’s body section to the color palette.

If you want the color palette to only show the colors you pass in via the bee config document, then you must disable the base colors.

```javascript

var beeConfig = {
        uid: config.uid,
        disableBaseColors: true,
        ...        

```
