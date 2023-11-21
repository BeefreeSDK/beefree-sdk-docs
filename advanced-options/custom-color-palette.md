# Custom Color Palette

1. [Color picker palette overview](broken-reference)
2. [Choosing the default colors in the color picker](broken-reference)
3. [Disabling the color history](broken-reference)
4. [Disabling the template's base colors](broken-reference)

#### Color picker palette overview <a href="#color-picker-palette-overview" id="color-picker-palette-overview"></a>

The builder’s color palette gathers a list of the default colors to display from multiple sources in order to create a convenient palette of color selections when the editor loads.

Specifically, colors are gathered as follows:

* 3 colors from the body (message background, content background, link) + black (#000000)
* custom colors (as many as customers want)
* 7 most recently used colors

Use the options outlined below to customize the default color palette.

#### Choosing the default colors in the color picker <a href="#choosing-the-default-colors-in-the-color-picker" id="choosing-the-default-colors-in-the-color-picker"></a>

The builder allows you to configure a custom color palette (per user), by modifying the client-side configuration. This, for instance, allows you to provide users with easy access to their company’s brand colors.

If no color profile is provided, then the builder will continue to suggest a color palette based on the colors used in the template that is being loaded.

```


var beeConfig = {
        uid: config.uid,
        defaultColors: ['#ffffff', '#000000', '#95d24f', '#ff00dd'],
        ...        


```

#### Disabling the color history <a href="#disabling-the-color-history" id="disabling-the-color-history"></a>

The builder will remember recently selected colors and add them to your color palette.  If the browser’s privacy settings allow it, the color picker history will be saved in the browser’s local storage.

If you want the color palette to be static such that recently selected colors are not included, then you can disable the history in your configuration.

```


var beeConfig = {
        uid: config.uid,
        disableColorHistory: true,
        ...        


```

#### Disabling the template's base colors <a href="#disabling-the-templates-base-colors" id="disabling-the-templates-base-colors"></a>

The builder by default adds colors found in the template’s body section to the color palette.

If you want the color palette to only show the colors you pass in via the bee config document, then you must disable the base colors.

```


var beeConfig = {
        uid: config.uid,
        disableBaseColors: true,
        ...        


```
