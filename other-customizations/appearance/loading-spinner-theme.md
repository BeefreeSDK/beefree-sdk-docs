# Loading Spinner Theme

{% hint style="info" %}
This feature is available on Beefree SDK [paid plans](https://dam.beefree.io/pluginpricing) only.
{% endhint %}

## Overview <a href="#overview" id="overview"></a>

The default Beefree SDK theme is grayscale and generally can be used with any color scheme.  In v3, you can now choose between a dark and light theme for the loading animation, so it can better fit the host application’s UI.  If you would like to change the loading icon and/or have more granular control of the loading theme, please view our article about [using custom CSS](custom-css.md).

## Sample Configuration <a href="#sample-configuration" id="sample-configuration"></a>

Available themes:

* light
* dark

```javascript

var beeConfig = {
      uid: config.uid,
      ...
      loadingSpinnerTheme: 'dark'
      ...
}

```
