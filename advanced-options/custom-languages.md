# Custom Languages

1. [Using a translation URL](broken-reference)
2. [Using a JSON Object](broken-reference)
3. [Sample language file](broken-reference)

#### Using a translation URL <a href="#using-a-translation-url" id="using-a-translation-url"></a>

You may now override the default Beefree SDK language file by providing a URL to your own translations.  This is an advanced feature and will replace all languages used by the editor with the languages defined in the custom file.

```


var beeConfig = {
      uid: config.uid,
      ...
      translationsUrl: 'https://www.yourdomain.com/xx-XX.json',
      ...
}


```

#### Using a JSON Object <a href="#using-a-json-object" id="using-a-json-object"></a>

The easiest method to override specific text labels is to pass a JSON object in your beeConfig, which contains the segments of the language file you want to override.

```

var beeConfig = {
      uid: config.uid,
      ...
      translations: {
         ...
      }
      ...
}

```

**Example: overriding the Help icon label in the default toolbar**

```


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

**Example: overriding the Rows tab label in the sidebar**

```


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

#### Sample language file <a href="#sample-language-file" id="sample-language-file"></a>

_Check out our Github repository for_ [_starter language templates_](https://dam.beefree.io/beecustomlanguages) _in all supported languages._
