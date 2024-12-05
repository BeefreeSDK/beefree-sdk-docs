# Implement Custom Rows

## Overview <a href="#overview" id="overview"></a>

Custom Rows are a powerful way to provide “ready-to-go” content directly into the builder. Think products, blog articles, events, coupons. And don’t forget that Saved Rows your customers might have will be loaded as Custom Rows the next time they load the builder.

All this content is crucial to make the most out of the Beefree SDK experience, and that’s why you can add UI elements in your app’s interface to:

* jump right to a Custom Rows category, without the need for the user to go into the _Rows_ tab, click on the dropdown and select the category;
* provide additional information on the available rows, either through a tooltip or by showing a Content dialog with all the information and the links to the rows.

With this feature, you will reduce the friction needed to discover and access the builder’s Custom Rows. To do so, you’ll use the `loadRows` event, which will trigger the _Custom Rows content dialog_.

## How it works <a href="#how-it-works" id="how-it-works"></a>

Here’s an example of our Beefree product, which integrates Beefree SDK, taking advantage of this method to load custom rows from its UI.

The toolbar in the application contains explicit call-to-action text links to load footers, which correspond to different categories of Custom Rows in the application.

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FqREnptqd4WoUiEm40b0y%252FCTAs-for-rows.jpg%3Falt%3Dmedia%26token%3D2fe13193-3dff-4e6f-9057-56e1ba603ea9&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=390df095&#x26;sv=2" alt=""><figcaption></figcaption></figure>

When users click on “Mailchimp Footers”, the Custom Rows Content Dialog is triggered, meaning that the builder opens a communication channel with your application. In this case, no additional UI will be displayed, as the host application provides the URL to the rows associated with that call-to-action. This way, the Rows tab will be immediately selected, with the “Mailchimp Footers” category already selected:

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252F7qGTMCYBM4VQePj342JK%252F2Showing-custom-rows.png%3Falt%3Dmedia%26token%3D83142623-197a-45af-9f27-99d677d25545&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=9b53ffc9&#x26;sv=2" alt=""><figcaption></figcaption></figure>

But what if you wanted users to select the email footers they need from a large catalog of pre-built content? In that scenario, you could have a more generic “Load footers” call-to-action in the toolbar.

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FBBuBYzC8dIq9xZCePNBJ%252F3Load-footers.jpeg%3Falt%3Dmedia%26token%3Da4ffb11e-5f6b-4892-9ded-03c79056037d&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c555c40d&#x26;sv=2" alt=""><figcaption></figcaption></figure>

Clicking on “Load Footers” will once again trigger the _Custom Rows content dialog_, but this time the application could provide a dialog window where users can browse or search through available footers, and get some additional context on them. Here is a visual example of how it might look like, but as with all content dialogs you have complete freedom on what to show:

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252F2AY9Y71IYu8gmyD6As4e%252F4Footers-content-dialog_s.jpeg%3Falt%3Dmedia%26token%3D23cfe433-bb9c-4dd1-887b-098efbd6dc8e&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d805b5e5&#x26;sv=2" alt=""><figcaption></figcaption></figure>

When users click on MailChimp, the modal window fades off, the builder switches to the “Rows” tab, and the MailChimp Footers are shown, ready to be dragged into the message.

## How to integrate it <a href="#how-to-integrate-it" id="how-to-integrate-it"></a>

You can trigger the **Custom Rows content dialog** via the `loadRows` instance event.

```json
bee.loadRows()
```

Once the Content Dialog is triggered, you have two options, as explained in the How it works section:

* Interact with the end user, as described in our [Content Dialog](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/content-dialog) documentation, and eventually return a URL of custom rows.
* Immediately return the rows URL, without displaying the Content Dialog. This is useful if you have a menu and already know which rows to load based on the interaction by the end user with you application’s UI.

## Extending Custom Rows with content dialog

[Content Dialog](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/content-dialog) allows you to build user interfaces that let your users locate & insert additional content (Custom Rows) while they are working on their message.

By letting you establish an interaction layer between the editor and your application (e.g., you show a modal window), it allows your users to locate/build/insert new rows, thus making the _Rows_ tab in the editor dramatically more flexible and scalable.

Note that _Content Dialog_ may be used to load other content types, as merge tags, special links, or display conditions. [Learn more about the Content dialog](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/content-dialog).

To start using it, you need to add the _contentDialog_ object to _beeConfig_, or add the _externalContentURLs_ parameter if you already use this feature in your editor configuration.

Here is an example of the syntax that needs to be added to the editor configuration document (_beeConfig_):

```

contentDialog: {
    externalContentURLs: {
            label: 'Search products',
            handler: function(resolve, reject) {
                // Your function
        }
    }
}
```

### Understanding the end-user experience <a href="#understanding-the-end-user-experience" id="understanding-the-end-user-experience"></a>

From the perspective of your users, this additional configuration adds a new item (using your text label) in the Rows drop-down.

Here is a visual example of how the “Search products” label will be shown, at the bottom of the _Rows_ drop-down.

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FZCmQGHuwEdnoteu3xz2H%252FCustomRows_ContentDialog_01.jpg%3Falt%3Dmedia%26token%3D801b797a-faa8-4548-a653-39892c1b680d&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d67cfa86&#x26;sv=2" alt=""><figcaption></figcaption></figure>

### **Initializing the dialog** <a href="#initializing-the-dialog" id="initializing-the-dialog"></a>

When the user clicks on the new menu item (e.g., “Search products” in the example above), what you define in the handler (a function with a [Promise](https://dam.beefree.io/mozillapromise)-like signature) is triggered.

You can use this event to display a form where the user can search for new items to insert in the message. Here is a visual example:

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FJ5FR3uegkM7aEityFgyF%252F2productsearch-1024x992.jpeg%3Falt%3Dmedia%26token%3D7046d990-5d85-4292-911e-27c9acdbee31&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=26223d16&#x26;sv=2" alt=""><figcaption></figcaption></figure>

You could also ask the user to enter parameters that will affect the very structure of the rows (JSON documents) that will be imported into the editor, affecting the way they will display:

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FM3XKNZcf72bjlrq7gAje%252F3product_layout.jpeg%3Falt%3Dmedia%26token%3D762b3fac-da78-4a48-968a-b6610fc9e748&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7d968389&#x26;sv=2" alt=""><figcaption></figcaption></figure>

You can also mix both forms in a 2-step pattern.

### **Returning items to the editor** <a href="#returning-items-to-the-editor" id="returning-items-to-the-editor"></a>

When the selection is made, you must return to the resolve function a URL containing the result (row’s list).

The response must match the same format used to define the externalContentURLs in beeConfig:

```

{"name":"Results name","value":"Results URL"}
```

This response will:

1. Create a new drop-down choice with the provided name
2. Display the rows provided by the URL in the rows panel

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FEDZpeXmL0t7Y5Fg8xdGL%252F4results.jpeg%3Falt%3Dmedia%26token%3D0a5dd716-7c4e-4dc5-a2ef-6f05ce8369a2&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=347a869&#x26;sv=2" alt=""><figcaption></figcaption></figure>

Notice that in the rows list, names returned by the Content Dialog display as highlighted elements to give them further visibility over starting choices.

The Content Dialog can be used as many times as the user needs and, depending on the response, the behavior may change:

#### **1. Returning the same name** <a href="#id-1.-returning-the-same-name" id="id-1.-returning-the-same-name"></a>

This overwrites the existing results, keeping the same name in the drop-down. This behavior perfectly matches our example above, where the host application returns “Your search results” every time the content dialog is resolved.

#### **2. Returning a new name** <a href="#id-2.-returning-a-new-name" id="id-2.-returning-a-new-name"></a>

This creates a new drop-down choice, keeping the previous results as selectable elements. Previous results are available directly in the drop-down.

Here is a visual example:

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FSP7mlr5iy454HsW9UjmF%252F5Search_multiple.jpeg%3Falt%3Dmedia%26token%3Dd409fb29-dd00-4ec5-aee5-0698db81a780&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=df0f0d69&#x26;sv=2" alt=""><figcaption></figcaption></figure>

#### **Live example** <a href="#live-example" id="live-example"></a>

In our example, we are using this event to display a search form and transfer the user selection to the editor as custom rows.

The form is part of the application, so we are using the same elements and styles that users of the application are used to.

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FU1uQRIwRqjYpRMBjblfH%252F6example_form-1024x939.jpeg%3Falt%3Dmedia%26token%3D359d53ba-f96e-4bff-b4f6-716fa3555c91&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1d981c47&#x26;sv=2" alt=""><figcaption></figcaption></figure>

## Displaying Saved Rows

Rows can be saved directly in the editor using the [Save Rows feature](https://docs.beefree.io/beefree-sdk/rows/saved-rows). These rows are returned to the host application as JSON objects that you can store based on your application logic.

These same rows can then be fed back into the editor by leveraging Custom Rows.

To do so, the host application must make them available in a reachable location specified through the _externalContentURLs_ parameter.

The rows are displayed based on your rows configuration, so you can categorize them, creating multiple lists of rows to improve the user experience.

### Rows Configuration <a href="#rows-configuration" id="rows-configuration"></a>

Here is an example of a rows configuration that displays saved items divided into usage categories:

```json

rowsConfiguration: {
  emptyRows: true,
  defaultRows: true,
  selectedRowType: 'Headers', // Pre-selects the "Headers" row from the external content list
  externalContentURLs: [
    {
      name: "Headers",
      value: "https://URL-01"
    },
    {
      name: "Footers",
      value: "https://URL-02"
    },
    {
      name: "Product grids",
      value: "https://URL-03"
    },
    {
      name: "Main article",
      value: "https://URL-04"
    }
  ]
}

```

And here is another example where saved rows are organized based on the campaign type:

```json

rowsConfiguration: {
  emptyRows: true,
  defaultRows: true,
  selectedRowType: 'Newsletter', // Pre-selects the "Newsletter" row from the external content list
  externalContentURLs: [
    {
      name: "Acquisition series",
      value: "https://URL-01"
    },
    {
      name: "Newsletter",
      value: "https://URL-02"
    },
    {
      name: "Transactional",
      value: "https://URL-03"
    },
    {
      name: "Post-Purchase Drip",
      value: "https://URL-04"
    }
  ]
}
```

The following is an example of the response schema when the editor calls one of the provided URLs:

```json

[{
    [{
        metadata: {
            name: 'My first row'
        }
        columns: { ... }
            ...
        }, // The row that was previously saved
        ...
    }]
},
{
    [{
        metadata: {
            name: 'My second row'
        }
        columns: { ... }
            ...
        }, // The row that was previously saved
        ...
    }]
},{
    [{
        metadata: {
            name: 'My third row'
        }
        columns: { ... }
            ...
        }, // The row that was previously saved
        ...
    }]
}]
```

### **Loading External Rows with an Instance Method** <a href="#loading-external-rows-with-an-instance-method" id="loading-external-rows-with-an-instance-method"></a>

With the introduction of Saved Rows Management, we’ve also introduced the ability to load external rows with an instance method. See [here](https://docs.beefree.io/beefree-sdk/rows/saved-rows/save-rows-overview) for more details.
