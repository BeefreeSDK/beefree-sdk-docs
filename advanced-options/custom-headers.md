# Custom Headers

1. [When to use it](broken-reference)
2. [How it works](broken-reference)

### When to use it <a href="#when-to-use-it" id="when-to-use-it"></a>

This feature allows the host application to pass custom headers when it triggers a call to their services.

For example, this could be useful for the security teams of , which would like to pass a JWT (JSON Web Token) when the user, through the file manager, triggers a call to their [Custom File System Provider API](https://docs.beefree.io/connect-your-own-file-storage/).

It may be also be used to protect application or customer-hosted content delivered to the editor, such as custom rows or other host app-specific content. The extra token helps the host application to apply an authentication layer to the contacted endpoints.

### How it works <a href="#how-it-works" id="how-it-works"></a>

To activate this feature, the host application must add a specific element to the [Configuration object](https://docs.beefree.io/configuration-parameters/):

```


customHeaders: [
    {
        name: 'Authorization',
        value: 'Bearer ',
    },
    ...
],


```

Please note that **all custom headers will be prefixed with “X-BEE-“** identifier. For instance, in the example above, the header will be sent to the host app as `X-BEE-Authorization`.
