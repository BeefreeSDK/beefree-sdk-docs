---
description: >-
  Read this page to learn more about the core concepts of implementing
  self-hosted saved rows, and to follow along in a tutorial with an example of
  how to implement it.
---

# Self-hosted Saved Rows Concepts and Tutorial

## Clone the Sample Project Demo

Clone the the sample project demo to follow along with the steps outlined on this page.

{% embed url="https://github.com/mailupinc/beefree-sdk-self-hosted-saved-rows-demo" %}

## Overview

In this guide you will:

* Enable the saved rows feature in your developer console.
* Configure the Beefree SDK with the proper hooks.
* Build a frontend with content dialogs (for saving, editing, and deleting rows).
* Manage metadata (names, categories) for each saved row.
* Create API endpoints (GET, POST, PUT, DELETE) on your backend.
* Set up a database to store row data.
* Connect your frontend with the backend through these endpoints.
* Test your endpoints using tools like Postman or Insomnia.

{% hint style="success" %}
**Important:** This guide includes sample code snippets from a [simple self-hosted saved rows implementation](https://github.com/mailupinc/beefree-sdk-self-hosted-saved-rows-demo). You can reference the code for this sample integration in [this GitHub repository](https://github.com/mailupinc/beefree-sdk-self-hosted-saved-rows-demo). As you read along in this tutorial, you can copy, edit, and customize the sample code for your own use and experimentation. &#x20;
{% endhint %}

Each step below is designed to build upon the previous ones, guiding you from initial setup to the final integration. This guide explains not only what to do, but also why each step is important and how it interacts with the other parts of the overall solution.

**Note:** Self-hosted saved rows is a highly customizable feature. While this guide provides one approach to implementing Self-hosted saved rows, it is important to note that there are several ways you can customize this implementation based on your application's needs. While this guide mentions core implementation concepts, such as toggling the feature on, setting up the `beeConfig` accordingly, and so on, it is also important to note it mentions approaches that you can customize, such as designing frontend modals, configuring your database, and so on.

### 1. Enable Saved Rows in Your Developer Console

**Overview and Context**

Before writing any code changes, ensure you first activate the **Self-hosted on your own infrastructure** toggle in your [Beefree SDK developer console account](https://developers.beefree.io). This global setting tells Beefree SDK that your application will handle:

* Creating the user interface for end users to create, save, and manage saved rows.
* Creating, configuring, and connecting your own database to store the saved rows data.
* Creating CRUD operations with your own API endpoints.

This is in contrast to the other toggle in the **Saved Rows** section of the **Application Configurations** within the Developer console, which [automatically provide a user interface for end user actions and stores row data](https://docs.beefree.io/beefree-sdk/rows/reusable-content/create/save/implement-hosted-saved-rows).

Enabling this toggle is a prerequisite for all the integration steps outlined in the subsequent sections. Without this toggle, none of the custom hooks or API endpoints will function properly.

**Steps to Complete**

To enable Self-hosted saved rows for your application, follow these steps:

1. Log in to the [Developer Console](https://developers.beefree.io/accounts/login/?from=website_menu).
2. Navigate to the application you'd like to configure Self-hosted saved rows for.
3. Click on **Details**.
4. Navigate to **Application configuration** and click **View more**.
5. Scroll to the **Saved Rows** section.
6. Toggle on the **Self-hosted on your own infrastructure** option.

{% hint style="info" %}
This step ensures your environment is configured to use self-hosted rows.
{% endhint %}

### 2. Configure the Beefree SDK

**Overview and Context**

The Beefree SDK must be configured with custom hooks to handle your saved rows. This involves defining a client configuration type and setting up a configuration object that includes your custom `getRows` handler. This step is crucial because it connects the SDK with your backend API, allowing it to fetch and update saved rows dynamically.

**Code Snippet**

Reference the Type Definition & Client Config in the following code snippet.

```typescript
// Define the type for the client configuration
type ClientConfig = {
  uid: string; // Unique client identifier
  container: string; // DOM element where the editor will mount
  language: string;
  saveRows: boolean;
  hooks: {
    // Custom hook to retrieve saved rows from your backend
    getRows: { handler: (resolve: Function, reject: Function, args: any) => void };
  };
  rowsConfiguration: {
    emptyRows: boolean;
    defaultRows: boolean;
    // Array of external content URLs dynamically generated based on categories
    externalContentURLs: Array<{
      name: string;
      value: string;
      handle: string;
      behaviors: { canEdit: boolean; canDelete: boolean };
    }>;
  };
};

// Set up the configuration object for the Beefree SDK
const beeConfig: ClientConfig = {
  uid: 'your-client-uid', // Your unique client ID
  container: 'bee-plugin-container', // ID of the container element
  language: 'en-US',
  saveRows: true,
  hooks: {
    // Assign your custom getRows handler here
    getRows: { handler: getRowsHandler },
  },
  rowsConfiguration: {
    emptyRows: true,
    defaultRows: true,
    externalContentURLs: externalContentURLs, // This array is built based on your categories
  },
};

```

{% hint style="info" %}
Inline comments explain each key property. This configuration connects Beefree SDK to your backend via the custom hook, ensuring that saved rows are properly managed.
{% endhint %}

**Additional Context**

By correctly configuring Beefree SDK, you guarantee that the editor will know how to fetch and display saved rows. The `getRows` hook becomes the bridge between the editor and your data source, while the `rowsConfiguration` object provides the necessary settings for displaying external content based on categories.

### 3. Build the Frontend with Content Dialogs

**Overview and Context**

Next, you will create the user interface (using a framework like React) that interacts with Beefree SDK. This step involves building modals for saving, editing, and deleting rows. The frontend is responsible for gathering user input and communicating with the backend, so the UX needs to be both responsive and intuitive.

**Key Tasks**

This step covers the following key tasks:

* Create a React component (e.g., `SavedRowsEditor`) that will render the Beefree SDK editor.
* Fetch saved rows and categories during the component's mounting phase.
* Implement modal dialogs that capture user input (e.g., row name, category) and trigger backend updates.

**Code Snippet**

The following code snippet is for the Save Row Modal.

```typescript
// Function to show a modal for saving a new row
function showSaveRowModal(resolve, reject, args) {
  // Create modal container with inline styles for positioning and appearance
  const modal = document.createElement('div');
  modal.style.cssText =
    'position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);padding:24px;background:#fff;border-radius:8px;box-shadow:0 4px 12px rgba(0,0,0,0.15);z-index:1000;width:320px;font-family:Arial,sans-serif;';

  // Input for Row Name
  const nameInput = document.createElement('input');
  nameInput.placeholder = 'Row Name'; // User enters the row name
  nameInput.style.cssText = 'display:block;width:100%;padding:8px;margin-bottom:16px;';
  modal.appendChild(nameInput);

  // Input for Category
  const categoryInput = document.createElement('input');
  categoryInput.placeholder = 'Category'; // User enters the category
  categoryInput.style.cssText = 'display:block;width:100%;padding:8px;margin-bottom:16px;';
  modal.appendChild(categoryInput);

  // Save button with click handler
  const saveButton = document.createElement('button');
  saveButton.textContent = 'Save';
  saveButton.style.marginRight = '8px';
  saveButton.onclick = async () => {
    // Validate inputs before proceeding
    if (!nameInput.value || !categoryInput.value) {
      alert('Please provide both a name and a category.');
      return;
    }
    // Build the row data object using provided inputs
    const rowData = {
      metadata: {
        id: args.metadata?.id || generateUniqueId(), // Use helper to generate a unique ID
        name: nameInput.value,
        category: categoryInput.value,
      },
      synced: false, // Default synced state
    };
    try {
      await updateSavedRows(rowData); // Call function to update or create the row in the backend
      resolve(rowData);
      document.body.removeChild(modal);
    } catch (error) {
      alert('Failed to save row');
      reject(error);
      document.body.removeChild(modal);
    }
  };
  modal.appendChild(saveButton);

  // Cancel button to close modal without saving
  const cancelButton = document.createElement('button');
  cancelButton.textContent = 'Cancel';
  cancelButton.onclick = () => {
    reject();
    document.body.removeChild(modal);
  };
  modal.appendChild(cancelButton);

  document.body.appendChild(modal);
}

```

{% hint style="info" %}
This snippet demonstrates the creation of a modal dialog that collects user input for a new row. Inline comments detail each part of the process.
{% endhint %}

**Code Snippet**

The following code snippet shows the React Component Skeleton.

```typescript
class SavedRowsEditor extends React.Component {
  componentDidMount() {
    // Fetch initial saved rows and categories from the backend
    fetch(`${BASE_URL}/rows`)
      .then(res => res.json())
      .then(savedRows => this.setState({ savedRows }));

    // Similarly, fetch categories then initialize the Beefree SDK editor
    this.initializeBeeEditor();
  }

  // Custom handler for retrieving rows, used by Beefree SDK
  getRowsHandler(resolve, reject, args) {
    fetch(`${BASE_URL}/rows/${encodeURIComponent(args.handle)}`)
      .then(res => res.json())
      .then(rows => resolve(rows))
      .catch(error => reject(error));
  }

  render() {
    return <div id="bee-plugin-container" style={{ minHeight: '600px' }} />;
  }
}

```

**Additional Context**

This step ties together your user interface with the Beefree SDK and backend. By using modal dialogs for CRUD actions, users can interact with the saved rows feature directly within the Beefree SDK editor. The React component handles data fetching and state updates, ensuring that the UI remains in sync with the backend.

### 4. Manage Metadata for Saved Rows

**Overview and Context**

Managing metadata is critical for organizing and retrieving saved rows. Metadata such as the row's ID, name, and category allow you to group rows, edit them, and build dynamic external content URLs. In this step, you'll update and refresh external content URLs based on current categories and see how the Beefree SDK configuration uses this data.

**Key Tasks**

* Define the metadata structure (ID, name, category) in your saved rows.
* Create a function to update the external content URLs whenever categories change.
* Ensure that the Beefree SDK's configuration (`rowsConfiguration`) is dynamically updated with these URLs.

**Code Snippet**

The following code snippet shows an example of Updating External URLs.

```typescript
function updateExternalContentURLs(categories) {
  // Map each category to an external content URL object
  const externalContentURLs = categories.map(category => ({
    name: category,
    value: `${BASE_URL}/rows/${encodeURIComponent(category)}`, // URL endpoint for the category
    handle: category, // Identifier used for row management
    behaviors: { canEdit: true, canDelete: true }, // Permissions for row actions
  }));
  return externalContentURLs;
}

```

{% hint style="info" %}
This snippet illustrates how to construct the array of external content URLs based on the list of categories fetched from your backend.
{% endhint %}

**Supplementary Code Snippet**

The following code snippet shows an example Beefree SDK Row Configuration.

```typescript
// Example snippet showing how beeConfig integrates the rows configuration
const beeConfig = {
  // ...other configuration properties...
  rowsConfiguration: {
    emptyRows: true,
    defaultRows: true,
    // External content URLs dynamically set based on current categories
    externalContentURLs: updateExternalContentURLs(currentCategories),
  },
  // ...hooks and additional configuration...
};

```

{% hint style="info" %}
Inline comments explain that the `rowsConfiguration` object receives a dynamically generated array from the `updateExternalContentURLs` function. This integration ensures that the Beefree SDK editor always uses the latest category data.
{% endhint %}

**Additional Context**

Managing metadata effectively allows you to organize saved rows into logical groups. When a new category is added or updated, refreshing the external content URLs ensures that the editor displays the correct endpoints for fetching rows. This dynamic behavior is crucial for maintaining data consistency across your frontend and backend.

### 5. Create API Endpoints in the Backend

**Overview and Context**

The backend API endpoints serve as the communication bridge between your frontend and database. These endpoints are responsible for creating, reading, updating, and deleting saved rows. Proper endpoint implementation ensures that user actions in the frontend correctly update the database and that the Beefree SDK editor receives the latest data.

**Key Tasks**

This section covers the following key tasks:

* Set up an Express server.
* Implement CRUD endpoints (GET, POST, PUT, DELETE) to handle row operations.
* Validate incoming data to ensure that required metadata (name and category) is present.

**Code Snippet**

The following code snippet shows a POST Endpoint example.

```javascript
app.post('/rows', (req, res) => {
  const rowData = req.body;
  // Validate that required metadata exists
  if (!rowData.metadata || !rowData.metadata.name || !rowData.metadata.category) {
    return res.status(400).json({ error: 'Missing required fields.' });
  }
  const { id, name, category } = rowData.metadata;
  const synced = rowData.synced || false;
  db.run(
    // Insert the new row into the database
    'INSERT INTO saved_rows (id, name, category, synced, row_data) VALUES (?, ?, ?, ?, ?)',
    [id || generateUniqueId(), name, category, synced, JSON.stringify(rowData)],
    (err) => {
      if (err) res.status(500).json({ error: err.message });
      else res.json({ message: 'Row saved successfully!' });
    }
  );
});

```

**Additional Context**

This endpoint not only creates new rows but also validates incoming data, ensuring data integrity. Similar endpoints (PUT, DELETE, GET) must be implemented to support full CRUD functionality. You can reference the full code for each endpoint in the sever.js file in [this GitHub repository](https://github.com/mailupinc/beefree-sdk-self-hosted-saved-rows-demo).

### 6. Set Up the Database

**Overview and Context**

Using SQLite in this example, you must set up a database to persist saved rows. Creating the appropriate table schema ensures that all necessary data (such as metadata and row content) is stored reliably. This database will be accessed by your API endpoints to perform CRUD operations.

**Code Snippet**

The following code shows shows the SQLite Table Creation.

```typescript
// Initialize SQLite database and create the saved_rows table if it doesn't exist
db.run(`
  CREATE TABLE IF NOT EXISTS saved_rows (
    id TEXT PRIMARY KEY,
    name TEXT,
    category TEXT,
    synced BOOLEAN,
    row_data TEXT
  )
`);

```

**Additional Context**

A well-defined database schema is essential for data consistency and performance. In a production environment, you might choose another database system, but this SQLite example provides a simple starting point to demonstrate the concept.

### 7. Connect the Frontend to the Backend

**Overview and Context**

To enable real-time data interactions, your frontend must connect to the backend via HTTP requests. This connection allows the Beefree SDK editor to fetch saved rows and update data based on user actions. The integration of fetch calls in your React component ensures that the user interface is always synchronized with the underlying data store.

**Code Snippet**

The following code snippet shows Connecting via Fetch.

```typescript
componentDidMount() {
  // Fetch saved rows from the backend
  fetch(`${BASE_URL}/rows`)
    .then(res => res.json())
    .then(savedRows => this.setState({ savedRows }));

  // Fetch categories and update external content URLs accordingly
  fetch(`${BASE_URL}/categories`)
    .then(res => res.json())
    .then(categories => {
      const urls = updateExternalContentURLs(categories);
      this.setState({ categories, externalContentURLs: urls });
    });
}

```

**Additional Context**

By establishing these fetch connections, the frontend remains dynamic and responsive. Changes in the backend are quickly reflected in the UI, which is crucial for maintaining a seamless user experience.

### 8. Test Your Endpoints

**Overview and Context**

Before deploying your solution, it's critical to test all endpoints to verify that CRUD operations work as expected. Using tools like Postman or Insomnia allows you to simulate API requests and ensure that both the backend and frontend are interacting correctly. Comprehensive testing helps catch potential errors early.

**Testing Steps**

Take the following steps to test your endpoints.

* **GET /rows:** Verify that all saved rows are returned.
* **GET /rows/:category:** Confirm that rows for a specific category are fetched.
* **GET /categories:** Check that the unique list of categories is correct.
* **POST /rows:** Ensure that a new row is added when metadata is provided.
* **PUT /rows/:id** Validate that an existing row is updated correctly.
* **DELETE /rows/:id** Confirm that a row is removed successfully.

### Final Guide Notes

By following this guide you have:

1. Enabled self-hosted saved rows in your developer console.
2. Configured the Beefree SDK with a custom `getRows` hook.
3. Built a user-friendly React component with modals to save, edit, and delete rows.
4. Managed metadata (name and category) for each row, and integrated dynamic external content URLs into the Beefree SDK configuration.
5. Created complete API endpoints (GET, POST, PUT, DELETE) on your Express backend.
6. Set up an SQLite database (or your preferred database) to store row data.
7. Connected your frontend to the backend using standard HTTP requests.
8. Tested your endpoints to ensure a smooth integration.

Each step is interconnected: enabling the feature makes it available in Beefree SDK, the frontend's modals interact with backend endpoints, and the dynamic configuration ensures that data remains consistent and up-to-date. The full code files (including the complete React component, server code, and configuration files) are available in the [GitHub repository](https://github.com/mailupinc/beefree-sdk-self-hosted-saved-rows-demo). This guide shows smaller, focused snippets to help you quickly understand the implementation while leaving the complete examples for your reference in the repository.
