# 🖼️ Displaying Saved Rows

Rows can be saved directly in the editor using the [Save Rows feature](../saved-rows/). These rows are returned to the host application as JSON objects that you can store based on your application logic.

These same rows can then be fed back into the editor by leveraging Custom Rows.

To do so, the host application must make them available in a reachable location specified through the _externalContentURLs_ parameter.

The rows are displayed based on your rows configuration, so you can categorize them, creating multiple lists of rows to improve the user experience.

## Rows Configuration

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

## **Loading External Rows with an Instance Method**

With the introduction of Saved Rows Management, we’ve also introduced the ability to load external rows with an instance method. See [here](../saved-rows/save-rows-overview.md) for more details.
