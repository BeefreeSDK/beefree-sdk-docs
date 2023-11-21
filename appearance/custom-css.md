# Custom CSS

1. [Defining a custom look & feel through a CSS stylesheet](broken-reference)
2. [Using different values for different users of the editor](broken-reference)
3. [Best practices and risk management](broken-reference)
4. [Sample Custom CSS Theme](broken-reference)

#### Defining a custom look & feel through a CSS stylesheet <a href="#defining-a-custom-look-feel-through-a-css-stylesheet" id="defining-a-custom-look-feel-through-a-css-stylesheet"></a>

```


customCss: 'https://yourdomain.com/stylesheet.css'


```

#### Using different values for different users of the editor <a href="#using-different-values-for-different-users-of-the-editor" id="using-different-values-for-different-users-of-the-editor"></a>

```


customCss: 'https://yourdomain.com/' + users[config.user].id + '.css'


```

#### Best practices and risk management <a href="#best-practices-and-risk-management" id="best-practices-and-risk-management"></a>

Custom CSS is an advanced feature, which gives the host application great flexibility to customize the UI/UX of the editor.

Please use this feature with caution.

When used properly, it is a powerful tool that can be leveraged to accomplish anything from applying custom styles with fine granularity to changing icons.

When misused, however, it may harm the user experience and the rendering capability of the editor’s stage.  For example, styles applied to the stage via CSS will _not_ be reflected in the preview or exported HTML.

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

#### Sample Custom CSS Theme <a href="#sample-custom-css-theme" id="sample-custom-css-theme"></a>

```

https://gist.github.com/44daee53546a9f48ecad7f52784efa55.git

```
