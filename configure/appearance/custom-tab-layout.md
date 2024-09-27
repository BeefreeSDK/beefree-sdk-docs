# Custom Tab Layout

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above.\
If you're on the Essentials plan, [upgrade a development application](../../getting-started/readme/development-applications.md) for free to try this and other Core-level features.
{% endhint %}

## Setting the default tab <a href="#setting-the-default-tab" id="setting-the-default-tab"></a>

The default tab configuration option lets the host application decide which content should be visible first in the sidebar when the editor is loaded.

In Beefree SDK v2, the default tab is the _Content_ tab and this behavior could not be changed. It’s still the behavior that we recommend for most scenarios.

However, apps that rely heavily on pre-built custom rows, or saved row libraries, may now choose to highlight the _Rows_ tab, using the following configuration options.

Available Options:

* content
* rows
* settings

```javascript

var beeConfig = {
        uid: config.uid,
        defaultTab: 'content',
        ...  

```

## Changing the tab order <a href="#changing-the-tab-order" id="changing-the-tab-order"></a>

Building upon the default tab configuration option, in Beefree SDK v3 you may also re-organize the way tabs are ordered.

```javascript

var beeConfig = {
        uid: config.uid,
        defaultTabsOrder: ['content', 'settings', 'rows'],
        ...  

```
