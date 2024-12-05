# Pre-build Reusable Content

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. If you're on the Essentials plan, [upgrade a development application](../../../../getting-started/readme/development-applications.md) for free to try this and other Core-level features.
{% endhint %}

There are three types of pre-built reusable content you can provide your application's end users with. These are the following:

* [Custom Rows](implement-custom-rows.md)
* [Default Rows](./#default-rows)
* [Empty Rows](./#empty-rows)

In this page, we will look at a sample `rowsConfiguration` that incorporates `defaultRows`, `emptyRows`, `selectedRowType`, and `externalContentURLs`. The [Implement Custom Rows page](implement-custom-rows.md) will discuss the steps to [integrate Custom Rows](implement-custom-rows.md).

## Rows Configuration <a href="#rows-configuration" id="rows-configuration"></a>

The following code snippet provides a sample `rowsConfiguration`.

```javascript

rowsConfiguration: {
  emptyRows: true,
  defaultRows: true,
  selectedRowType: 'my_saved_rows', // pre-select this item in the Rows select
  externalContentURLs: [
    {
      name: "Rows list 01",
      value: "https://URL-01"
    },
    {
      name: "Rows list 02",
      value: "https://URL-02"
    }
  ]
}
```

### **Rows Configuration Parameters** <a href="#rows-configuration-parameters" id="rows-configuration-parameters"></a>

This section explains each of the properties listed in the `rowConfiguration` code snippet.

These properties are the following:

* [`emptyRows`](https://docs.beefree.io/beefree-sdk/rows/custom-rows/how-it-works#emptyrows): Set of empty rows. The same rows available when `rowsConfiguration` is not included. End users can use these empty rows to structure and customize their own content within.
* [`defaultRows`](https://docs.beefree.io/beefree-sdk/rows/custom-rows/how-it-works#defaultrows): A set of rows that contain sample content. End users can use the sample content as inspiration for customizing them with their own look and feel.
* [`selectedRowType`](https://docs.beefree.io/beefree-sdk/rows/custom-rows/how-it-works#selectedrowtype): Specify which type of row should be pre-selected when the end user opens the Rows selection in the visual builder.
* [`externalContentURLs`](https://docs.beefree.io/beefree-sdk/rows/custom-rows/how-it-works#externalcontenturls): Each item in this list defines an option available in the Rows tab drop-down.

## Default Rows

You can add pre-built default rows to your builder by setting the `defaultRows` property to `true` in your `beeConfig`.&#x20;

Default rows are a set of rows that contain sample content. That’s why we also call them **sample rows**. They may be used as a supporting feature for starting templates, or to speed up the process of building a message from scratch.

**Allowed values:** `boolean`, can be set to `true` or `false`.

**Default value:** `false`

They are presented as follows in the builder’s default theme (the screenshot shows the first 2 default rows):

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FrtcF6QKySIwpoIwJKmqL%252F6rows_default.png%3Falt%3Dmedia%26token%3D5e799c5e-8065-4d08-8593-5d312b494f94&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b7c4d22&#x26;sv=2" alt=""><figcaption></figcaption></figure>

## Empty Rows

You can add pre-built empty rows to your builder by setting the `emptyRows` property to `true` in your `beeConfig`. Empty rows are a set of rows that aren't prefilled with content. However, they offer a general structure for content to be placed within them. These are the same rows available to end users when the `rowsConfiguration` parameter is not included in the [`beeConfig`](../../../../getting-started/readme/installation/configuration-parameters/).

**Allowed values:** `boolean`, can be set to `true` or `false`.

**Default value:** `true`

Will always be included as the last element if omitted in the configuration.

They are presented as follows in the builder’s default theme (the screenshot shows the first 4 empty rows with unique structures):

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FuVeV6D6mzm8YhVzV436c%252F5rows_empty.png%3Falt%3Dmedia%26token%3Da472bdb4-104f-4804-a099-20db7ca58c58&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=55a82f06&#x26;sv=2" alt=""><figcaption></figcaption></figure>

## Set a Pre-selected Row Type <a href="#selectedrowtype" id="selectedrowtype"></a>

This property is used to specify which type of row should be pre-selected when the end user opens the Rows selection in the visual builder. You have several options for what value to assign to this property, and its role is to simplify the end user's interaction with the builder by focusing their attention on a specific type of row by default.

**Possible values for `selectedRowType`:**

1. **`'defaultRows'`**: This value will automatically select the default rows that come with the builder, which usually contain pre-designed content that users can easily modify and adapt. It helps users start with a pre-configured structure and quickly adjust it to meet their needs.
2. **`'emptyRows'`**: This value pre-selects an option for the user to start with empty rows. This is useful for users who prefer to build their layouts entirely from scratch, without any predefined content or structure.
3. **The handle of a row in `externalContentURLs`**:
   * You can also pass the handle of a row that is listed in `externalContentURLs` to pre-select a row from an external source. A **handle** in this context refers to the **unique identifier** or **name** used to reference a specific row from an external list. Think of it as a unique key that allows the system to identify which external row to load or pre-select.
   * For example, if you have external content rows listed in `externalContentURLs`, such as "Rows list 01" or "Rows list 02," you can pass their respective handle (typically a string like `"Rows list 01"`) as the value for `selectedRowType`. This will automatically load and pre-select that specific external row, saving the user the step of manually selecting it from the list.

## **External Content URLs** <a href="#externalcontenturls" id="externalcontenturls"></a>

The `externalContentURLs` property accepts a row's name and url. You can add multiple items to the property. Each item in the list defines an option available in the Rows drop-down.&#x20;

**`name`:** the text displayed in the Rows drop-down

**`value`:** URL that will be called by the builder when the user selects the corresponding _name_ in the drop-down. The URL must return a set of rows as a JSON object.

```json
externalContentURLs: [
  {
    name: "Rows list 01",
    value: "https://URL-01"
  }
```

The following image displays an example of how the `name` value appears in the drop-down menu.

<figure><img src="https://docs.beefree.io/~gitbook/image?url=https%3A%2F%2F806400411-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F8c7XIQHfAtM23Dp3ozIC%252Fuploads%252FFe4qy0sUwelqFbN90pYt%252F7rows_custom.png%3Falt%3Dmedia%26token%3D9ff24720-782a-418a-9af8-2b9dfc5b9030&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7cc54de2&#x26;sv=2" alt=""><figcaption></figcaption></figure>

In the drop-down menu, you can see a visual example of each pre-built content type mentioned in this article and in [Implement Custom Rows](implement-custom-rows.md):

* **Empty rows:** When the end user clicks the **Empty** option in the drop-down menu, they will be redirected to a list of row structures to choose from.&#x20;
* **Default rows**: When the end user clicks the **Default** option in the drop-down menu, they will be redirected to a list of default rows to choose from.&#x20;
* **My Saved** **Rows**: When the end user clicks the **My Saved Rows** option in the drop-down menu, they will be redirected to a list of rows they created and [saved to reuse](../save/) at a later time.&#x20;
* **Custom rows**: The MailChimp Footers, HubSpot Footers, and Sendgrid footers are additional options added to the drop-down through the [Custom Rows feature](implement-custom-rows.md). When an end user clicks on any of these three options, they will be redirected to the lists of rows available in that external resource.

### **How a Handle Works**

A **handle** acts like a reference key to point to a specific row in an external list. Handles are typically unique names or identifiers that can be used to quickly access specific rows from an external content source, ensuring that the correct row is fetched and displayed to the user. For instance, in the following configuration:

```json
externalContentURLs: [
  {
    name: "Rows list 01",
    value: "https://URL-01"
  },
  {
    name: "Rows list 02",
    value: "https://URL-02"
  }
]
```

If you want to pre-select "Rows list 01" from the external content list, you would set `selectedRowType: 'Rows list 01'`, where `'Rows list 01'` is the handle of that specific external content row. The handle here refers to the **name** or a unique identifier that the system recognizes and uses to select the correct row from the external content list.

Visit [Manage Reusable Content](../../manage.md) to learn more about editing, deleting, categorizing, and managing rows within the builder.
