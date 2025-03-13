# Custom File Picker

{% hint style="info" %}
This feature is available on Beefree SDK [Superpowers plan](https://dam.beefree.io/pluginpricing) and above. If you're on the Core or Essentials plan, [upgrade a development application](../../getting-started/readme/development-applications.md) for free to try this and other Superpowers-level features.
{% endhint %}

## Main concepts

This feature allows you to have your own file picker for choosing files (images) in Beefree SDK's Editor, to make its integration in your platform look even more seamless. It leverages Beefree SDK’s [Content Dialog](content-dialog.md) feature. To set it up you will need to add the corresponding entry to the [configuration object](../../getting-started/readme/installation/configuration-parameters/):

```

contentDialog: {
    filePicker: {
        handler: function(resolve, reject, args) {
            // Your function
        }
    },
    ...
}

```

**The `handler` function** lets you use your own logic to retrieve the desired value, and it has a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)-like signature.

If data from Beefree SDK is available, it will be sent in the `args` parameter (see below). Once the value is available, you must call the `resolve(value)` function to pass it to the editor. In case you want to cancel the operation, call the `reject()` function.

Please note that **a `resolve` or `reject` call is mandatory**. If you miss this step, the editor will remain in waiting mode – and the error management on the host application must call the `reject()` function to unblock the editor.

**The `args` parameter** is where the File Picker’s Content Dialog will receive additional data.

```


{
    "X-BEE-UserName": "string", // e.g. image, all
    "X-BEE-Uid": "string", // e.g. the current user's id
    "X-BEE-Mimetypes": "string", // e.g. "*" -Or- "image/*"
}


```

Images dragged onto an image block or edited via the “apply effects and more” button will be passed to the image storage per your app’s file storage settings. To prevent images from passing through Beefree SDK’s file storage, the file upload can be disabled via [advanced permissions](advanced-permissions.md).

## Returned value syntax

Values must use the same pattern used in the [configuration object](../../getting-started/readme/installation/configuration-parameters/): the returned object is validated against the expected format. If the validation fails, an error will be returned to the browser console, eg: `Error getting content filePicker value, the item is malformed`

```javascript

{
   "url":"https://d1oco4z2z1fhwp.cloudfront.net/templates/default/113/rocket-color.png",
   "context":"imageModule.src"
}

```

### A basic example

The following is the most basic example, which returns an image URL immediately after clicking the “Browse” button. This example does not open a file picker.

In a real-world scenario, the host application would display a file picker UI and let the user search for and locate the file before finally returning the file’s location (URL) to Beefree SDK:

```javascript

contentDialog: {
  filePicker: {
    handler: function(resolve, reject) {
      resolve({
        url: 'string', // url to the file (e.g. http://www.example.com/myimage.jpg)
      })
    }
  },
}

```

## List of modules

The following is a list of all modules that are sent as part of the **args** parameter:

* `sidebar.link`
* `buttonModule.link`
* `imageModule.link`
* `iconsModule.link`
* `menuModule.link`
* `iconsModule.src`
* `socialModule.src`
* `textModule.link`
* `imageModule.src`
* `titleModule.link`
* `row.backgroundImage`
* `backgroundVideo.src`
* `toolbar.specialLink`
* `sidebar.specialLink`
