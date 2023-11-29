# Custom Languages

{% hint style="info" %}
You can choose one of [20+ languages](../getting-started/installation/configuration-parameters/) for the visual builder's UI when initializing the builder. If you want to use custom language strings, however, you will need to use a Custom Language. This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. If you're on the Essentials plan, upgrade a [development application](../getting-started/development-applications.md#development-applications) for free to try this and other Core-level features.
{% endhint %}

## Using a Translation URL

You may now override the default Beefree SDK language file by providing a URL to your own translations.  This is an advanced feature and will replace all languages used by the editor with the languages defined in the custom file.

```javascript

var beeConfig = {
      uid: config.uid,
      ...
      translationsUrl: 'https://www.yourdomain.com/xx-XX.json',
      ...
}

```

## Using a JSON Object

The easiest method to override specific text labels is to pass a JSON object in your beeConfig, which contains the segments of the language file you want to override.

```javascript

var beeConfig = {
      uid: config.uid,
      ...
      translations: {
         ...
      }
      ...
}

```

### **Example: overriding the Help icon label in the default toolbar**

```javascript

var beeConfig = {
      uid: config.uid,
      ...
      translations: {
         "bee-common-top-bar": {
           help: "Support"
         },
      }
      ...
}

```

### **Example: overriding the Rows tab label in the sidebar**

```javascript


var beeConfig = {
      uid: config.uid,
      ...
      translations: {
          "bee-common-widget-bar": {
            "structure": "Catalog"
          }
        },
      }
      ...
}


```

## Sample language file <a href="#sample-language-file" id="sample-language-file"></a>

_Check out our Github repository for_ [_starter language templates_](https://dam.beefree.io/beecustomlanguages) _in all supported languages._
