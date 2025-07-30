# Custom Headers

{% hint style="info" %}
This feature is available on Beefree SDK [Superpowers plan](https://dam.beefree.io/pluginpricing) and above. Upgrade a [development application](../../getting-started/readme/development-applications.md) at no extra charge to explore features from higher plan tiers. **Note:** Usage on a development application still counts toward [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) and limits.

Are you looking to add custom HTML tags to the head section of your designs? Find more information in our [Custom Head HTML page](../../server-side-configurations/custom-head-html.md).
{% endhint %}

## When to use it <a href="#when-to-use-it" id="when-to-use-it"></a>

This feature allows the host application to pass custom headers when it triggers a call to their services. The custom headers are added to [FSP calls](../../server-side-configurations/server-side-options/storage-options/connect-your-file-storage-system.md) and to [Custom Rows](../../rows/reusable-content/create/pre-build/implement-custom-rows.md) calls.

For example, this could be useful for the security teams of , which would like to pass a JWT (JSON Web Token) when the user, through the file manager, triggers a call to their [Custom File System Provider API](../../server-side-configurations/server-side-options/storage-options/connect-your-file-storage-system.md).

It may be also be used to protect application or customer-hosted content delivered to the editor, such as custom rows or other host app-specific content. The extra token helps the host application to apply an authentication layer to the contacted endpoints.

### How it works <a href="#how-it-works" id="how-it-works"></a>

To activate this feature, the host application must add a specific element to the [Configuration object](../../getting-started/readme/installation/configuration-parameters/):

```javascript

customHeaders: [
    {
        name: 'Authorization',
        value: 'Bearer ',
    },
    ...
],

```

Please note that **all custom headers will be prefixed with “X-BEE-“** identifier. For instance, in the example above, the header will be sent to the host app as `X-BEE-Authorization`.

{% hint style="info" %}
Please note that custom headers must be whitelisted by our team before using them. Please open a support ticket via the [Beefree SDK Console](https://dam.beefree.io/devportal) if you’re planning to use this feature.
{% endhint %}

### Using Pre-approved Custom Headers

You don't need to request whitelisting for the following custom headers. Instead, you can immediately use any of these **pre-approved** custom headers:

* `x-bee-authorization`
* `x-bee-document-id`
* `x-bee-custom-host`
* `x-bee-tenant-identifier`
* `x-bee-businessuid`

No additional approval is required when using these headers.
