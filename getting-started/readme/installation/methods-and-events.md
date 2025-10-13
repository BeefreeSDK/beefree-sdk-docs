---
description: Complete reference guide for all Beefree SDK methods, callbacks, and events.
---

# Methods, Callbacks, and Events

## Overview

Beefree SDK provides a comprehensive set of methods, callback functions, and events that allow you to control the editor programmatically and respond to user interactions. This guide serves as your single source of truth for all available SDK interactions.

**TypeScript Definitions**: For complete type safety and detailed parameter information, reference the official TypeScript definitions: [Beefree SDK Types](https://github.com/BeefreeSDK/beefree-sdk-npm-official/tree/master/src/types)

## How Methods and Events Work

When you initialize Beefree SDK, you get an instance that exposes various methods for programmatic control. Additionally, you can configure callback functions in your `beeConfig` to respond to user actions and editor events.

```javascript
const bee = new BeefreeSDK(token);
const beeInstance = bee.start(beeConfig, template);

// Use methods to control the editor
beeInstance.save();
beeInstance.preview();

// Configure callbacks to respond to events
const beeConfig = {
    container: 'editor-container',
    onSave: function(jsonFile, htmlFile) {
        // Handle save event
    },
    onChange: function(jsonFile, response) {
        // Handle content changes
    }
};
```

## Instance Methods

These methods are available on the Beefree SDK instance and allow you to control the editor programmatically.

### Core Methods

#### beeInstance.start(templateToLoad, userInfo, templateInfo, options)
- **Description:** Initializes and starts the builder with optional template data
- **Parameters:**
  - `templateToLoad` (optional): JSON string with template structure
  - `userInfo` (optional): User information object for collaborative features
  - `templateInfo` (optional): Template metadata
  - `options` (optional): Additional configuration options
- **Returns:** Promise that resolves when editor is ready
- **Usage:**
```javascript
// Basic start
await beeInstance.start();

// Start with template
await beeInstance.start(templateJson);

// Start with full configuration (NPM package)
await beeInstance.start(templateJson, userInfo, templateInfo, options);
```

#### beeInstance.load(template)
- **Description:** Loads a JSON template into the editor
- **Parameters:**
  - `template`: JSON string with template structure
- **Returns:** Promise that resolves when template is loaded
- **Usage:**
```javascript
await beeInstance.load(templateJson);
```

#### beeInstance.reload(template)
- **Description:** Reloads a template without showing loading dialog (seamless reload)
- **Parameters:**
  - `template`: JSON string with template structure
- **Use Cases:** Custom undo/redo, real-time content injection
- **Usage:**
```javascript
await beeInstance.reload(templateJson);
```

### Control Methods

#### beeInstance.save()
- **Description:** Programmatically triggers the save action
- **Triggers:** `onSave` callback with JSON and HTML files
- **Usage:**
```javascript
beeInstance.save();
```

#### beeInstance.saveAsTemplate()
- **Description:** Programmatically triggers save as template action
- **Triggers:** `onSaveAsTemplate` callback with JSON file
- **Usage:**
```javascript
beeInstance.saveAsTemplate();
```

#### beeInstance.send()
- **Description:** Programmatically triggers send action (Email Builder only)
- **Triggers:** `onSend` callback with HTML file
- **Usage:**
```javascript
beeInstance.send();
```

### Preview and View Methods

#### beeInstance.preview()
- **Description:** Opens the preview mode
- **Triggers:** `onPreview` callback
- **Usage:**
```javascript
beeInstance.preview();
```

#### beeInstance.togglePreview()
- **Description:** Toggles preview mode on/off
- **Triggers:** `onTogglePreview` callback
- **Usage:**
```javascript
beeInstance.togglePreview();
```

#### beeInstance.toggleStructure()
- **Description:** Toggles visibility of structure outlines in the editor
- **Usage:**
```javascript
beeInstance.toggleStructure();
```

#### beeInstance.toggleMergeTagsPreview()
- **Description:** Toggles visibility of merge tag sample content
- **Usage:**
```javascript
beeInstance.toggleMergeTagsPreview();
```

### Advanced Methods

#### beeInstance.execCommand(command)
- **Description:** Executes specific editor commands for highlighting, scrolling, focusing, or selecting elements
- **Parameters:**
  - `command`: Object defining the action and target
- **Actions:** `highlight`, `scroll`, `focus`, `select`
- **Usage:**
```javascript
beeInstance.execCommand({
    action: 'highlight',
    target: { type: 'row', id: 'row-id' }
});

beeInstance.execCommand({
    action: 'scroll',
    target: { type: 'block', id: 'block-id' }
});
```

#### beeInstance.loadWorkspace(type)
- **Description:** Loads a specific workspace type
- **Parameters:**
  - `type`: Workspace type ('default', 'mixed', 'amp_only', 'html_only')
- **Triggers:** `onLoadWorkspace` callback
- **Usage:**
```javascript
beeInstance.loadWorkspace('mixed');
```

#### beeInstance.loadConfig(config)
- **Description:** Updates editor configuration dynamically
- **Parameters:**
  - `config`: Configuration object with updated settings
- **Usage:**
```javascript
beeInstance.loadConfig({
    debug: { all: true },
    language: 'es-ES'
});
```

### File Manager Methods

{% hint style="info" %}
**Note:** For File Manager applications, only `beeInstance.start()` without parameters is supported.
{% endhint %}

File Manager applications have a simplified method set focused on file selection and management workflows.

## Callback Functions

Callback functions are configured in your `beeConfig` and are triggered by user actions or editor events.

### Save and Template Callbacks

#### onSave
- **Trigger:** User clicks save button or `beeInstance.save()` is called
- **Parameters:** `(jsonFile, htmlFile, ampHtml, templateVersion, language)`
  - `jsonFile`: Template structure as JSON string
  - `htmlFile`: Rendered HTML output
  - `ampHtml`: AMP HTML version (if applicable)
  - `templateVersion`: Template version number
  - `language`: Template language code
- **Usage:**
```javascript
onSave: function(jsonFile, htmlFile, ampHtml, templateVersion, language) {
    console.log('Template saved:', {
        json: jsonFile,
        html: htmlFile,
        amp: ampHtml,
        version: templateVersion,
        lang: language
    });
    
    // Save to your backend
    saveTemplate({
        json: jsonFile,
        html: htmlFile,
        version: templateVersion
    });
}
```

#### onSaveAsTemplate
- **Trigger:** User clicks "Save as Template" or `beeInstance.saveAsTemplate()` is called
- **Parameters:** `(jsonFile)`
  - `jsonFile`: Template structure as JSON string
- **Usage:**
```javascript
onSaveAsTemplate: function(jsonFile) {
    console.log('Saving as template:', jsonFile);
    
    // Save template to library
    saveToTemplateLibrary(jsonFile);
}
```

#### onAutoSave
- **Trigger:** Automatic save based on `autosave` configuration
- **Parameters:** `(jsonFile)`
  - `jsonFile`: Template structure as JSON string
- **Usage:**
```javascript
onAutoSave: function(jsonFile) {
    console.log('Auto-saving template');
    
    // Perform background save
    autoSaveTemplate(jsonFile);
}
```

#### onSend
- **Trigger:** User clicks send button or `beeInstance.send()` is called (Email Builder only)
- **Parameters:** `(htmlFile)`
  - `htmlFile`: Rendered HTML ready for sending
- **Usage:**
```javascript
onSend: function(htmlFile) {
    console.log('Sending email');
    
    // Send email via your service
    sendEmail({
        html: htmlFile,
        subject: getSubject(),
        recipients: getRecipients()
    });
}
```

### Content Change Callbacks

#### onChange
- **Trigger:** Template content is modified (requires `trackChanges: true`)
- **Parameters:** `(jsonFile, response)`
  - `jsonFile`: Updated template JSON
  - `response`: Change details object with patches and metadata
- **Usage:**
```javascript
onChange: function(jsonFile, response) {
    console.log('Content changed:', response);
    
    // Track changes for analytics
    trackUserAction({
        action: response.description,
        value: response.value,
        timestamp: Date.now()
    });
    
    // Sync with other users in collaborative editing
    broadcastChange(response);
}
```

#### onRemoteChange
- **Trigger:** Changes made by other users in collaborative editing sessions
- **Parameters:** `(jsonFile, response)`
  - `jsonFile`: Updated template JSON from remote user
  - `response`: Change details from remote user
- **Usage:**
```javascript
onRemoteChange: function(jsonFile, response) {
    console.log('Remote user made changes:', response);
    
    // Update UI to show remote changes
    highlightRemoteChanges(response);
    
    // Notify current user of remote activity
    showCollaborationNotification(response.user);
}
```

### Loading and Workspace Callbacks

#### onLoad
- **Trigger:** Template is loaded into the editor
- **Parameters:** `(jsonFile)`
  - `jsonFile`: Loaded template JSON
- **Usage:**
```javascript
onLoad: function(jsonFile) {
    console.log('Template loaded successfully');
    
    // Initialize custom features
    initializeCustomModules();
    
    // Track template usage
    trackTemplateLoad(jsonFile);
}
```

#### onLoadWorkspace
- **Trigger:** Workspace is successfully loaded
- **Parameters:** `(workspace)`
  - `workspace`: Workspace configuration object
- **Usage:**
```javascript
onLoadWorkspace: function(workspace) {
    console.log('Workspace loaded:', workspace.type);
    
    // Update UI based on workspace
    updateWorkspaceUI(workspace);
}
```

### Error and Warning Callbacks

#### onError
- **Trigger:** Errors occur in the editor
- **Parameters:** `(errorMessage)`
  - `errorMessage`: Error description string
- **Usage:**
```javascript
onError: function(errorMessage) {
    console.error('Beefree SDK Error:', errorMessage);
    
    // Show user-friendly error message
    showErrorNotification('Something went wrong. Please try again.');
    
    // Log error for debugging
    logError({
        source: 'beefree-sdk',
        message: errorMessage,
        timestamp: Date.now()
    });
}
```

#### onWarning
- **Trigger:** Warnings are generated by the editor
- **Parameters:** `(alertMessage)`
  - `alertMessage`: Warning description string
- **Usage:**
```javascript
onWarning: function(alertMessage) {
    console.warn('Beefree SDK Warning:', alertMessage);
    
    // Show warning to user if needed
    if (shouldShowWarning(alertMessage)) {
        showWarningNotification(alertMessage);
    }
}
```

### Preview and View Callbacks

#### onPreview
- **Trigger:** Preview button is clicked
- **Parameters:** `(status)`
  - `status`: Boolean indicating preview state
- **Usage:**
```javascript
onPreview: function(status) {
    console.log('Preview mode:', status ? 'opened' : 'closed');
    
    // Update UI state
    updatePreviewButton(status);
}
```

#### onTogglePreview
- **Trigger:** Preview is toggled on/off
- **Parameters:** `(status)`
  - `status`: Boolean indicating preview state
- **Usage:**
```javascript
onTogglePreview: function(status) {
    console.log('Preview toggled:', status);
    
    // Adjust layout for preview mode
    adjustLayoutForPreview(status);
}
```

#### onViewChange
- **Trigger:** User navigates between different SDK views
- **Parameters:** `(view)`
  - `view`: String indicating current view
- **Possible Values:**
  - `'editor'`: Main editor view
  - `'preview'`: Preview mode
  - `'fileManager'`: File Manager opened
  - `'imageEditor'`: Image Editor opened
- **Usage:**
```javascript
onViewChange: function(view) {
    console.log('View changed to:', view);
    
    // Track user navigation
    trackViewChange(view);
    
    // Update application state
    switch(view) {
        case 'fileManager':
            showFileManagerHelp();
            break;
        case 'preview':
            hideEditingTools();
            break;
        case 'editor':
            showEditingTools();
            break;
    }
}
```

### File Management Callbacks

#### onFilePickerInsert
- **Trigger:** Insert button clicked in File Manager applications
- **Parameters:** `(data)`
  - `data`: Object containing file information
- **Usage:**
```javascript
onFilePickerInsert: function(data) {
    console.log('File selected:', data);
    
    // Process selected file
    processSelectedFile(data);
    
    // Close file picker
    closeFilePicker();
}
```

#### onFilePickerCancel
- **Trigger:** Cancel/X button clicked in File Manager applications
- **Parameters:** None
- **Usage:**
```javascript
onFilePickerCancel: function() {
    console.log('File picker cancelled');
    
    // Handle cancellation
    handleFilePickerCancel();
}
```

### Collaboration Callbacks

#### onComment
- **Trigger:** Comments or comment threads change
- **Parameters:** `(commentData)`
  - `commentData`: Comment information object
- **Usage:**
```javascript
onComment: function(commentData) {
    console.log('Comment activity:', commentData);
    
    // Update comment UI
    updateCommentInterface(commentData);
    
    // Notify relevant users
    notifyCommentActivity(commentData);
}
```

## Event Configuration Examples

### Basic Event Handling
```javascript
var beeConfig = {
    container: 'beefree-sdk-container',
    
    // Essential callbacks
    onSave: function(jsonFile, htmlFile) {
        saveToDatabase(jsonFile, htmlFile);
    },
    
    onError: function(errorMessage) {
        handleError(errorMessage);
    },
    
    onLoad: function(jsonFile) {
        console.log('Editor ready');
    }
};
```

### Advanced Event Handling
```javascript
var beeConfig = {
    container: 'beefree-sdk-container',
    trackChanges: true,
    commenting: true,
    
    // Content tracking
    onChange: function(jsonFile, response) {
        trackChanges(response);
        autoSave(jsonFile);
    },
    
    onRemoteChange: function(jsonFile, response) {
        syncRemoteChanges(response);
        showCollaboratorActivity(response);
    },
    
    // Collaboration
    onComment: function(commentData) {
        updateCommentThread(commentData);
        notifyTeamMembers(commentData);
    },
    
    // View tracking
    onViewChange: function(view) {
        analytics.track('view_change', { view });
        updateUIForView(view);
    },
    
    // Complete save handling
    onSave: function(jsonFile, htmlFile, ampHtml, version, language) {
        Promise.all([
            saveTemplate(jsonFile),
            saveHTML(htmlFile),
            saveAMP(ampHtml),
            updateVersion(version)
        ]).then(() => {
            showSuccessMessage();
        }).catch(handleSaveError);
    }
};
```

### File Manager Configuration
```javascript
var beeConfig = {
    container: 'file-manager-container',
    
    // File picker callbacks
    onFilePickerInsert: function(data) {
        insertFileIntoContent(data);
        closeFileManager();
    },
    
    onFilePickerCancel: function() {
        closeFileManager();
    },
    
    onViewChange: function(view) {
        if (view === 'fileManager') {
            showFileManagerInstructions();
        }
    }
};
```

## Method Chaining and Async Operations

Many SDK methods return promises, allowing for proper async handling:

```javascript
// Sequential operations
async function loadAndPreview(templateJson) {
    try {
        await beeInstance.load(templateJson);
        await beeInstance.preview();
        console.log('Template loaded and previewed');
    } catch (error) {
        console.error('Operation failed:', error);
    }
}

// Conditional operations
async function saveAndSend(shouldSend = false) {
    await beeInstance.save();
    
    if (shouldSend) {
        await beeInstance.send();
    }
}
```

## Best Practices

### Error Handling
- Always implement `onError` callback for production applications
- Provide user-friendly error messages
- Log errors for debugging and monitoring

### Performance
- Use `onChange` judiciously with `trackChanges: true`
- Implement debouncing for frequent operations
- Consider using `onAutoSave` for background saves

### User Experience
- Provide feedback for all user actions
- Use `onViewChange` to guide users through different modes
- Implement proper loading states

### Collaboration
- Use `onRemoteChange` to show real-time collaboration
- Implement conflict resolution for simultaneous edits
- Provide clear indicators of other users' activities

### Development
- Reference TypeScript definitions for complete type safety
- Test all callback implementations thoroughly
- Use method chaining for complex workflows

## TypeScript Support

For complete type definitions and IntelliSense support, reference the official types:

**TypeScript Definitions**: [Beefree SDK Types](https://github.com/BeefreeSDK/beefree-sdk-npm-official/tree/master/src/types)

```typescript
import { BeefreeSDK, BeeConfig, SaveCallback } from '@beefree.io/sdk';

const beeConfig: BeeConfig = {
    container: 'editor-container',
    onSave: ((jsonFile: string, htmlFile: string, ampHtml: string | null, version: number, language: string | null) => {
        // Fully typed callback
    }) as SaveCallback
};
```

This comprehensive guide covers all available methods, callbacks, and events in Beefree SDK. Use it as your reference for implementing complete editor control and event handling in your applications.

---

**TypeScript Definitions**: [Beefree SDK Types](https://github.com/BeefreeSDK/beefree-sdk-npm-official/tree/master/src/types)