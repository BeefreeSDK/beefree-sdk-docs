# Custom CSS

{% hint style="info" %}
This feature is available on Beefree SDK [Superpowers plan](https://dam.beefree.io/pluginpricing) and above. Upgrade a [development application](../../../getting-started/readme/development-applications.md) at no extra charge to explore features from higher plan tiers. **Note:** Usage on a development application still counts toward [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) and limits.
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

Custom CSS is an advanced feature, which gives the host application great flexibility to customize the UI/UX of the builder. Please use this feature with caution. If you're looking to hide certain UI elements, we recommend you first check if that can be accomplished with [Advanced Permissions](../../advanced-options/advanced-permissions.md), as it may be easier to implement.

When used properly, it is a powerful tool that can be leveraged to accomplish anything from applying custom styles with fine granularity to changing icons.

When misused, however, it may harm the user experience and the rendering capability of the builder’s stage. For example, styles applied to the stage via CSS will _not_ be reflected in the preview or exported HTML.

{% hint style="danger" %}
### Important Notice

For the best results, follow these best practices:

* **Avoid global styles.** Do not use generic global styles (e.g., `*`, `p`, `input`) that could affect the editing stage.
* **Use specific CSS selectors.** Target elements using precise selectors (e.g., `body.bee--cs h3`).
* **Do not inject scripts via CSS.** JavaScript and other scripts should not be included in CSS.
* **Ensure HTTPS hosting.** The custom CSS URL must be hosted over HTTPS.
* **Avoid third-party hosting.** Do not link to CSS files hosted on GitHub or other third-party sources.
* **Do not style elements directly on the stage.** These styles will not appear in the final HTML, which may create a confusing experience.

#### Reliable Selectors

Only class names with the `--cs` suffix are reliable for **custom CSS**. Avoid the following selectors:

* **Nested tag structures** (e.g., `div > div > div`)
* **Sibling selectors** (e.g., `input + label`)
* **Class names without `--cs`** (e.g., `.icons__item`)
* **Prefixed class name selectors** (e.g., `div[class^="StageModuleIcons_itemRow"]`)

#### :warning: Changes & Updates

Class names **without** the `--cs` suffix may change **without prior notice**. However, any updates to the **HTML structure** and `--cs` classes will be communicated in advance.
{% endhint %}
