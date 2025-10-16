---
description: Complete reference guide for all Beefree SDK configuration parameters.
---

# Configuration Parameters

## Overview

Configuration parameters allow you to customize the Beefree SDK editor to match your application's requirements. This comprehensive guide covers all available parameters, from required settings to advanced customization options.

## How Configuration Works

When initializing Beefree SDK, you pass a configuration object (`beeConfig`) that defines the editor's behavior, appearance, and functionality. The configuration is structured with high-level parameters that may contain nested sub-parameters for granular control.

```javascript
const bee = new BeefreeSDK(token);
bee.start(beeConfig, template);
```

## Complete Configuration Structure

Here's a comprehensive configuration object showing all available high-level parameters:

{% code fullWidth="false" %}
```javascript
var beeConfig = {
    // REQUIRED PARAMETERS
    container: 'beefree-sdk-container',
    
    // CORE EDITOR SETTINGS
    language: 'en-US',
    autosave: 30,
    trackChanges: true,
    preventClose: false,
    
    // CONTENT CUSTOMIZATION
    specialLinks: [],
    mergeTags: [],
    mergeContents: [],
    
    // APPEARANCE & UI
    sidebarPosition: 'left',
    editorFonts: {},
    defaultColors: [],
    disableColorHistory: false,
    disableBaseColors: false,
    
    // TITLE BLOCK CUSTOMIZATION
    titleDefaultStyles: {},
    titleDefaultConfig: {},
    titleMaxLevel: 'h3',
    
    // WORKSPACE & LAYOUT
    workspace: {
        type: 'default',
        editSingleRow: false
    },
    
    // ADVANCED FEATURES
    commenting: false,
    commentingThreadPreview: true,
    commentingNotifications: true,
    contentDialog: {},
    defaultForm: {},
    rowDisplayConditions: {},
    rowsConfiguration: {},
    advancedPermissions: {},
    hooks: {},
    metadata: {},
    
    // PERMISSIONS & SECURITY
    roleHash: '',
    disableLinkSanitize: false,
    
    // LOADING & PERFORMANCE
    loadingSpinnerDisableOnSave: false,
    loadingSpinnerDisableOnDialog: false,
    
    // CALLBACK FUNCTIONS
    onSave: function(jsonFile, htmlFile, ampHtml, templateVersion, language) {},
    onChange: function(jsonFile, response) {},
    onSaveAsTemplate: function(jsonFile) {},
    onAutoSave: function(jsonFile) {},
    onSend: function(htmlFile) {},
    onLoad: function(jsonFile) {},
    onError: function(errorMessage) {},
    onWarning: function(alertMessage) {},
    onLoadWorkspace: function(workspace) {},
    onFilePickerInsert: function(data) {},
    
    // DEBUGGING & DEVELOPMENT
    debug: {
        all: false,
        inspectJson: false,
        showTranslationKeys: false
    },
    
    // LOCALIZATION
    translations: {}
};
```
{% endcode %}

## Required Parameters

This parameter is mandatory for Beefree SDK initialization:

| Parameter | Description | Type |
|-----------|-------------|------|
| **container** | The ID of the HTML div element that will contain the Beefree SDK editor | `string` |

## Core Editor Settings

### language
- **Type:** `string`
- **Default:** `'en-US'`
- **Description:** Sets the editor interface language

**Available Languages:**

| Language | Code | Language | Code |
|----------|------|----------|------|
| English | `en-US` | German | `de-DE` |
| Spanish | `es-ES` | Danish | `da-DK` |
| French | `fr-FR` | Swedish | `sv-SE` |
| Italian | `it-IT` | Polish | `pl-PL` |
| Portuguese | `pt-BR` | Hungarian | `hu-HU` |
| Indonesian | `id-ID` | Russian | `ru-RU` |
| Japanese | `ja-JP` | Korean | `ko-KR` |
| Chinese | `zh-CN` | Dutch | `nl-NL` |
| Traditional Chinese | `zh-HK` | Finnish | `fi-FI` |
| Czech | `cs-CZ` | Romanian | `ro-RO` |
| Norwegian (Bokmål) | `nb-NO` | Slovenian | `sl-SI` |

### autosave
- **Type:** `number | false`
- **Default:** `false`
- **Description:** Enables automatic saving at specified intervals (in seconds). Set to `false` to disable.

### trackChanges
- **Type:** `boolean`
- **Default:** `false`
- **Description:** Enables change tracking to monitor template modifications via the `onChange` callback.

### preventClose
- **Type:** `boolean`
- **Default:** `false`
- **Description:** Shows an alert when users attempt to leave the page before saving changes.

## Content Customization

### specialLinks
- **Type:** `array`
- **Default:** `[]`
- **Description:** Array of custom link objects for special actions (e.g., unsubscribe links).

```javascript
specialLinks: [
    {
        name: 'Unsubscribe',
        value: '{{unsubscribe_url}}',
        target: '_blank'
    }
]
```

### mergeTags
- **Type:** `array`
- **Default:** `[]`
- **Description:** Array of merge tag objects for dynamic content personalization.

```javascript
mergeTags: [
    {
        name: 'First Name',
        value: '{{first_name}}'
    },
    {
        name: 'Company',
        value: '{{company_name}}'
    }
]
```

### mergeContents
- **Type:** `array`
- **Default:** `[]`
- **Description:** Array of reusable content blocks that can be inserted into templates.

```javascript
mergeContents: [
    {
        name: 'Footer Content',
        value: '<div>Company footer HTML</div>'
    }
]
```

## Appearance & UI Customization

### sidebarPosition
- **Type:** `string`
- **Default:** `'left'`
- **Options:** `'left'`, `'right'`
- **Description:** Controls the position of the content sidebar.

### editorFonts
- **Type:** `object`
- **Default:** See Font Management documentation
- **Description:** Customizes available fonts in the text toolbar and body settings.

```javascript
editorFonts: {
    fontList: [
        {
            name: 'Arial',
            fontFamily: 'Arial, sans-serif'
        },
        {
            name: 'Custom Font',
            fontFamily: 'CustomFont, Arial, sans-serif',
            url: 'https://fonts.googleapis.com/css?family=CustomFont'
        }
    ]
}
```

### defaultColors
- **Type:** `array`
- **Default:** `[]`
- **Description:** Array of hex color codes for the default color palette.

```javascript
defaultColors: ['#ffffff', '#000000', '#95d24f', '#ff00dd']
```

### disableColorHistory
- **Type:** `boolean`
- **Default:** `false`
- **Description:** Disables the color history feature in color pickers.

### disableBaseColors
- **Type:** `boolean`
- **Default:** `false`
- **Description:** Disables the base color palette in color pickers.

## Title Block Customization

### titleDefaultStyles
- **Type:** `object`
- **Default:** `{}`
- **Description:** Default styling for title blocks at different heading levels.

```javascript
titleDefaultStyles: {
    h1: {
        fontSize: '32px',
        fontWeight: 'bold',
        color: '#000000'
    },
    h2: {
        fontSize: '28px',
        fontWeight: 'bold',
        color: '#333333'
    }
}
```

### titleDefaultConfig
- **Type:** `object`
- **Default:** `{}`
- **Description:** Default configuration settings for title blocks.

### titleMaxLevel
- **Type:** `string`
- **Default:** `'h3'`
- **Options:** `'h1'`, `'h2'`, `'h3'`, `'h4'`, `'h5'`, `'h6'`
- **Description:** Maximum heading level available in title blocks.

## Workspace Configuration

### workspace
- **Type:** `object`
- **Default:** `{type: 'default'}`
- **Description:** Configures the editor workspace type and behavior.

#### workspace.type
- **Type:** `string`
- **Default:** `'default'`
- **Options:** `'default'`, `'mixed'`, `'amp_only'`, `'html_only'`
- **Description:** Determines workspace type for AMP content visibility.

#### workspace.editSingleRow
- **Type:** `boolean`
- **Default:** `false`
- **Description:** Enables single-row editing mode.

#### workspace.stage (Mobile Design Mode)
- **Type:** `object`
- **Description:** Mobile design mode configuration.

```javascript
workspace: {
    type: 'default',
    stage: {
        width: '375px',
        height: '667px'
    }
}
```

## Advanced Features

### commenting
- **Type:** `boolean`
- **Default:** `false`
- **Description:** Enables collaborative commenting on content blocks and rows.

### commentingThreadPreview
- **Type:** `boolean`
- **Default:** `true`
- **Description:** Shows comment preview popover on the stage.

### commentingNotifications
- **Type:** `boolean`
- **Default:** `true`
- **Description:** Enables notifications for new comments in collaborative editing.

### contentDialog
- **Type:** `object`
- **Default:** `{}`
- **Description:** Configuration for custom content dialogs to exchange data with external systems.

```javascript
contentDialog: {
    contentDialogUrl: 'https://your-app.com/content-dialog',
    triggers: ['image', 'link']
}
```

### defaultForm
- **Type:** `object`
- **Default:** `{}`
- **Description:** Default form structure for form blocks.

```javascript
defaultForm: {
    structure: {
        // Form field definitions
    }
}
```

### rowDisplayConditions
- **Type:** `object`
- **Default:** `{}`
- **Description:** Enables conditional display logic for email rows.

### rowsConfiguration
- **Type:** `object`
- **Default:** `{}`
- **Description:** Configuration for row behavior and appearance.

### advancedPermissions
- **Type:** `object`
- **Default:** `{}`
- **Description:** Granular permission controls for different user roles.

```javascript
advancedPermissions: {
    components: {
        'bee-button': {
            enabled: true,
            style: false
        }
    },
    rows: {
        enabled: true,
        canAdd: true,
        canDelete: false
    }
}
```

### hooks
- **Type:** `object`
- **Default:** `{}`
- **Description:** Custom hooks for extending editor functionality.

### metadata
- **Type:** `object`
- **Default:** `{}`
- **Description:** Custom metadata configuration for templates.

## Security & Permissions

### roleHash
- **Type:** `string`
- **Default:** `''`
- **Description:** Alphanumeric identifier for user roles (8-30 characters, no special characters).

### disableLinkSanitize
- **Type:** `boolean`
- **Default:** `false`
- **Description:** Disables URL validation to allow merge tags in links.

## Performance & Loading

### loadingSpinnerDisableOnSave
- **Type:** `boolean`
- **Default:** `false`
- **Description:** Controls loading spinner visibility during save operations.

### loadingSpinnerDisableOnDialog
- **Type:** `boolean`
- **Default:** `false`
- **Description:** Controls loading spinner visibility during dialog operations.

## Callback Functions

### onSave
- **Type:** `function`
- **Parameters:** `(jsonFile, htmlFile, ampHtml, templateVersion, language)`
- **Description:** Called when user saves the template.

```javascript
onSave: function(jsonFile, htmlFile, ampHtml, templateVersion, language) {
    console.log('Template saved:', {
        json: jsonFile,
        html: htmlFile,
        amp: ampHtml,
        version: templateVersion,
        lang: language
    });
}
```

### onChange
- **Type:** `function`
- **Parameters:** `(jsonFile, response)`
- **Description:** Called when template content changes (requires `trackChanges: true`).

### onSaveAsTemplate
- **Type:** `function`
- **Parameters:** `(jsonFile)`
- **Description:** Called when user saves template as a new template.

### onAutoSave
- **Type:** `function`
- **Parameters:** `(jsonFile)`
- **Description:** Called during automatic save operations.

### onSend
- **Type:** `function`
- **Parameters:** `(htmlFile)`
- **Description:** Called when user triggers send action.

### onLoad
- **Type:** `function`
- **Parameters:** `(jsonFile)`
- **Description:** Called when template is loaded into the editor.

### onError
- **Type:** `function`
- **Parameters:** `(errorMessage)`
- **Description:** Called when errors occur in the editor.

### onWarning
- **Type:** `function`
- **Parameters:** `(alertMessage)`
- **Description:** Called when warnings are triggered.

### onLoadWorkspace
- **Type:** `function`
- **Parameters:** `(workspace)`
- **Description:** Called when workspace is successfully loaded.

### onFilePickerInsert
- **Type:** `function`
- **Parameters:** `(data)`
- **Description:** Called when files are inserted via file picker integration.

## Development & Debugging

### debug
- **Type:** `object`
- **Default:** `{all: false, inspectJson: false, showTranslationKeys: false}`
- **Description:** Debug mode configuration for development.

```javascript
debug: {
    all: true,                    // Enables all debug features
    inspectJson: true,           // Shows JSON inspector icon
    showTranslationKeys: true    // Shows translation keys instead of text
}
```

## Localization

### translations
- **Type:** `object`
- **Default:** `{}`
- **Description:** Custom translations to override default interface text.

```javascript
translations: {
    'bee-common-widget-bar': {
        content: 'MODULES'
    }
}
```
## Quick Reference Examples

### Basic Configuration
```javascript
var beeConfig = {
    container: 'beefree-sdk-container',
    language: 'en-US',
    onSave: function(jsonFile, htmlFile) {
        console.log('Template saved!');
    },
    onError: function(errorMessage) {
        console.error('Error:', errorMessage);
    }
};
```

### Advanced Configuration
```javascript
var beeConfig = {
    container: 'beefree-sdk-container',
    language: 'en-US',
    autosave: 60,
    trackChanges: true,
    
    // Custom content
    mergeTags: [
        { name: 'First Name', value: '{{first_name}}' },
        { name: 'Company', value: '{{company}}' }
    ],
    
    // UI customization
    sidebarPosition: 'right',
    defaultColors: ['#ffffff', '#000000', '#ff6b6b', '#4ecdc4'],
    
    // Advanced features
    commenting: true,
    workspace: {
        type: 'mixed',
        editSingleRow: false
    },
    
    // Callbacks
    onSave: function(jsonFile, htmlFile, ampHtml, version, lang) {
        // Handle save
    },
    onChange: function(jsonFile, response) {
        // Handle changes
    },
    onError: function(errorMessage) {
        // Handle errors
    }
};
```

### Configuration with Advanced Permissions
```javascript
var beeConfig = {
    container: 'beefree-sdk-container',
    language: 'en-US',
    
    advancedPermissions: {
        components: {
            'bee-button': {
                enabled: true,
                style: true,
                link: false
            },
            'bee-image': {
                enabled: true,
                style: true,
                alt: false
            }
        },
        rows: {
            enabled: true,
            canAdd: true,
            canDelete: false,
            canMove: true
        },
        settings: {
            bodySettings: true,
            preheader: false,
            subject: true
        }
    },
    
    onSave: function(jsonFile, htmlFile) {
        // Handle save with permissions applied
    }
};
```

### Configuration for Collaborative Editing
```javascript
var beeConfig = {
    container: 'beefree-sdk-container',
    language: 'en-US',
    
    // Enable collaborative features
    commenting: true,
    commentingThreadPreview: true,
    commentingNotifications: true,
    trackChanges: true,
    
    // User identification for collaboration
    roleHash: 'editor123abc',
    
    // Callbacks for collaboration
    onChange: function(jsonFile, response) {
        // Sync changes with other users
    },
    onSave: function(jsonFile, htmlFile) {
        // Save collaborative changes
    }
};
```

## Best Practices

### Security Considerations
- Always validate `uid` and `roleHash` on your server
- Use `advancedPermissions` to restrict user capabilities based on roles
- Implement proper authentication before initializing the SDK

### User Experience
- Set appropriate `language` based on user preferences
- Use `preventClose: true` for important editing sessions
- Provide meaningful error handling in `onError` callback
- Use `commenting` features for team collaboration workflows

### Development Tips
- Enable `debug.all: true` during development
- Use `trackChanges: true` to monitor template modifications
- Implement all relevant callbacks for complete functionality
- Test with different `workspace.type` values for AMP compatibility

This comprehensive configuration guide serves as your single source of truth for all Beefree SDK parameters. Most parameters are documented with their type, default value, description, and practical examples to help you customize the editor to meet your specific requirements.