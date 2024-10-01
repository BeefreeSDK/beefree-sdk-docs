# Custom CSS

{% hint style="info" %}
This feature is available on Beefree SDK [Superpowers plan](https://dam.beefree.io/pluginpricing) and above. If you're on the Core or Essentials plan, [upgrade a development application](../../getting-started/readme/development-applications.md) for free to try this and other Superpowers-level features.
{% endhint %}

## Defining a custom look & feel through a CSS stylesheet <a href="#defining-a-custom-look-feel-through-a-css-stylesheet" id="defining-a-custom-look-feel-through-a-css-stylesheet"></a>

To define a custom look and feel through a CSS stylesheet, assign the URL of your CSS file to the `customCss` property in your JavaScript code, as shown in the following example.

```javascript

customCss: 'https://yourdomain.com/stylesheet.css'

```

## Using different values for different users of the builder <a href="#using-different-values-for-different-users-of-the-editor" id="using-different-values-for-different-users-of-the-editor"></a>

You can customize the builder's CSS for different users by dynamically setting the `customCss` property with a unique CSS file URL for each user. Simply concatenate the user-specific identifier to the base URL as shown in the example code.

```javascript

customCss: 'https://yourdomain.com/' + users[config.user].id + '.css'

```

## Best practices and risk management <a href="#best-practices-and-risk-management" id="best-practices-and-risk-management"></a>

Custom CSS is an advanced feature, which gives the host application great flexibility to customize the UI/UX of the builder.

Please use this feature with caution.

When used properly, it is a powerful tool that can be leveraged to accomplish anything from applying custom styles with fine granularity to changing icons.

When misused, however, it may harm the user experience and the rendering capability of the builder’s stage. For example, styles applied to the stage via CSS will _not_ be reflected in the preview or exported HTML.

{% hint style="info" %}
If you're looking to hide certain UI elements, we recommend you first check if that can be accomplished with [Advanced Permissions](../advanced-options/advanced-permissions.md), as it may be easier to implement.
{% endhint %}

For the best possible results, please follow these best practices:

* Avoid using generic global styles. (e.g. \*, p, input, etc.) that could propagate to the editing stage.
* Use CSS selectors to select specific elements and groups (e.g. body.bee–cs h3).
* Do not attempt to pass JavaScript or any other scripts via CSS.
* Ensure the custom CSS URL is hosted over HTTPS.
* Do not link to CSS files hosted on GitHub, or by any 3rd party.
* Never style elements on the stage, since those styles will not appear in the final HTML, and therefore lead to a confusing user experience.

Please note that classnames with the `--cs` suffix are reliable selectors for customCSS.\
Other selectors such as the following should be avoided as much as possible:

* Nested tag structure (e.g. `div > div > div` )
* Siblings (`input + label`)
* Classnames without –cs (e.g. `.icons__item)`
* Prefixed classname selectors (e.g. `div[class^="StageModuleIcons_itemRow"]`)

## Sample Custom CSS Theme <a href="#sample-custom-css-theme" id="sample-custom-css-theme"></a>

Reference the following Sample Custom CSS Theme to see an example of how you can use custom CSS in your web application.

```url

https://gist.github.com/44daee53546a9f48ecad7f52784efa55.git

```
