# Configuration Reload

1. [Overview](broken-reference)
2. [Use cases](broken-reference)
3. [How it works](broken-reference)

### Overview <a href="#overview" id="overview"></a>

When you load a Beefree application inside the host application, you pass a [configuration object](https://docs.beefree.io/configuration-parameters/) with multiple sections that define the characteristics of the UI, UX, and available elements. However, there are cases when you may want to reload this configuration without the need to reload the Beefree application. In these cases, you can use a specific event to update the configuration while the editor is open.

### Use cases <a href="#use-cases" id="use-cases"></a>

With this event, you can make on-the-fly changes to the user experience. For example:

* Updating available categories for [Saved rows](https://docs.beefree.io/save-rows/#displaying-rows)
* Refreshing a [Custom header](https://docs.beefree.io/custom-headers/) for authorization
* Changing [Advanced permissions](https://docs.beefree.io/advanced-permissions/) for the current user
* Updating settings for the editor’s [Content defaults](https://docs.beefree.io/content-defaults/)

### How it works <a href="#how-it-works" id="how-it-works"></a>

You can load the configuration changes via a new instance event. Here’s an example:

```


var newConfig = {
  advancedPermissions: {
    // new permissions
  }
}

bee.loadConfig(newConfig)


```
