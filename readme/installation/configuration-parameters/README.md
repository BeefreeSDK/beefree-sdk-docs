---
description: Discover the configuration parameters within Beefree SDK.
---

# Configuration parameters

## Passing Configurations to Beefree SDK

Once you have initialized your Beefree application, you can pass a series of configuration parameters to it.

The following code displays an example of a default configuration:

{% code fullWidth="false" %}
```javascript
beeConfig: {
	uid: 'CmsUserName', // [mandatory]
	container: 'bee-plugin-container', // [mandatory]
	autosave: 30, // [optional, default:false]
	language: 'en-US', // [optional, default:'en-US']
	trackChanges: true or false, // [optional, default: false] 
	specialLinks: specialLinks, // [optional, default:[]] 
	mergeTags: mergeTags, // [optional, default:[]]
	mergeContents: mergeContents, // [optional, default:[]]
	preventClose: false, // [optional, default:false]
	editorFonts : {}, // [optional, default: see description]
	contentDialog : {}, // [optional, default: see description]
	defaultForm : {}, // [optional, default: {}]
	roleHash : "", // [optional, default: ""]
	rowDisplayConditions : {}, // [optional, default: {}]
    workspace: {  // [optional, default: {type : 'default'}]
        editSingleRow: false // [optional, default: false]},
    commenting: false, // [optional, default: false]}
    commentingThreadPreview: true, // [optional, default: true]}
    commentingNotifications: true, // [optional, default: true]}
    disableLinkSanitize: true, // [optional, default: false]}
	onSave: function(jsonFile, htmlFile) { /* Implements function for save */ }, // [optional]
	onChange: function(jsonFile, response) { /* Implements function for change */ }, // [optional]
	onSaveAsTemplate: function(jsonFile) { /* Implements function for save as template (only JSON file) */ }, // [optional]
	onAutoSave: function(jsonFile) { /* Implements function for auto save */ }, // [optional]
	onSend: function(htmlFile) { /* Implements function to send the message */ }, // [optional]
	onLoad: function(jsonFile) { /* Implements function to perform an action once the template is loaded */}, // [optional]
	onError: function(errorMessage) { /* Implements function to handle error messages */ } // [optional]
	onWarning: function(alertMessage) { /* Implements function to handle error messages */ } // [optional]
}
```
{% endcode %}

## Parameters

The following table provides a description of the parameters.

<table><thead><tr><th>Parameter</th><th width="331">Description</th><th width="103">Required</th><th>Default</th></tr></thead><tbody><tr><td><strong>uid</strong></td><td><p>An alphanumeric string that identifies the user and allows the plugin to load resources for that user (e.g. images).</p><ul><li>Min length: 3 characters</li><li>Can contain letters from a to z (uppercase or lowercase), numbers and the special characters _ (underscore) and – (dash)</li><li>It is a string and not a numeric value</li></ul><p>It uniquely identifies a user of the Plugin. When we say “uniquely”, we mean that:</p><ul><li>It will be counted as a unique user for monthly billing purposes.</li><li>Images (and other files) used by the user when creating and editing messages will be associated with it and not visible to other users (when using the default storage).</li></ul></td><td>Yes</td><td></td></tr><tr><td><strong>container</strong></td><td>Identifies the id of div element that contains BEE Plugin</td><td>Yes</td><td></td></tr><tr><td><strong>language</strong></td><td><p>4-letter language identifier (e.g. “en-US”, ISO 639-1 format).</p><p><strong>Available Languages</strong></p><table><thead><tr><th>English:</th><th>en-US</th></tr></thead><tbody><tr><td>Spanish:</td><td>es-ES</td></tr><tr><td>French:</td><td>fr-FR</td></tr><tr><td>Italian:</td><td>it-IT</td></tr><tr><td>Portuguese:</td><td>pt-BR</td></tr><tr><td>Indonesian:</td><td>id-ID</td></tr><tr><td>Japanese:</td><td>ja-JP</td></tr><tr><td>Chinese:</td><td>zh-CN</td></tr><tr><td>Traditional Chinese:</td><td>zh-HK</td></tr><tr><td>German:</td><td>de-DE</td></tr><tr><td>Danish:</td><td>da-DK</td></tr><tr><td>Swedish:</td><td>sv-SE</td></tr><tr><td>Poland:</td><td>pl-PL</td></tr><tr><td>Hungarian:</td><td>hu-HU</td></tr><tr><td>Russian:</td><td>ru-RU</td></tr><tr><td>Korean:</td><td>ko-KR</td></tr><tr><td>Dutch:</td><td>nl-NL</td></tr><tr><td>Finnish:</td><td>fi-FI</td></tr><tr><td>Czech:</td><td>cs-CZ</td></tr><tr><td>Romanian:</td><td>ro-RO</td></tr><tr><td>Norwegian (Bokmål):</td><td>nb-NO</td></tr><tr><td>Slovenian:</td><td>sl-SI</td></tr></tbody></table></td><td>No</td><td><code>"en-US"</code></td></tr></tbody></table>

## Events and Methods

The following table provides descriptions of the events and methods:

<table><thead><tr><th width="203">Events and Methods</th><th width="315">Description</th><th width="99">Required</th><th>Default</th></tr></thead><tbody><tr><td><strong>trackChanges</strong></td><td>Track message changes in the editor via the “onChange” callback. See “Tracking message changes” for further details.</td><td>No</td><td><code>false</code></td></tr><tr><td><strong>specialLinks</strong></td><td>An array of custom links that may be used in the message (e.g. unsubscribe). See “extending the editor” for further details.</td><td>No</td><td><code>[]</code></td></tr><tr><td><strong>mergeTags</strong></td><td>An array of merge tags that may be used in the message (e.g. first name of the recipient). See “extending the editor” for further details.</td><td>No</td><td><code>[]</code></td></tr><tr><td><strong>mergeContents</strong></td><td>An array of content elements that may be used in the message (e.g. small blocks of HTML). See “extending the editor” for further details.</td><td>No</td><td><code>[]</code></td></tr><tr><td><strong>preventClose</strong></td><td>Whether an alert should be shown when the user attempts to leave the page before saving.</td><td>No</td><td><code>false</code></td></tr><tr><td><strong>editorFonts</strong></td><td>Customize the list of available fonts in the editor’s text toolbar and the BODY settings panel.<br>See “Font management” for further details.</td><td>No</td><td>See “Font management” for the default object.</td></tr><tr><td><strong>roleHash</strong></td><td><p>Identifies the user role:</p><ul><li>Minimum length is 8, maximum is 30</li><li>Alphanumerical string only: No whitespaces, no special characters such as “_” and “-“</li></ul><p>See “Roles and permissions” for further details.</p></td><td>No</td><td><code>""</code></td></tr><tr><td><strong>rowDisplayConditions</strong></td><td>Allows for conditional statements in email messages.<br>See “Display Conditions” for further details.</td><td>No</td><td><code>{}</code></td></tr><tr><td><strong>workspace</strong></td><td>Configure the initial workspace for loading the editor. Currently used for AMP content visibility.<br>See “Workspaces” for further details.</td><td>No</td><td><code>{type : 'default'}</code></td></tr><tr><td><strong>contentDialog</strong></td><td>Allows to exchange data with BEE Plugin using a UI layer you control.<br>See the “<a href="../../../advanced-options/content-dialog.md">Content Dialog</a>” page for the complete reference.</td><td>No</td><td><code>{}</code></td></tr><tr><td><strong>defaultForm</strong></td><td>This should contain a <code>structure</code> object with the form data.<br>See “<a href="../../../form-block/integrating-and-using-the-form-block/form-structure-and-parameters.md">Passing forms to the builder</a>” for further details.</td><td>No</td><td><code>{}</code></td></tr><tr><td><strong>commenting</strong></td><td>Enables commenting on content blocks and rows. See <a href="../../../advanced-options/commenting.md">Commenting</a> for further details.</td><td>No</td><td><code>false</code></td></tr><tr><td><strong>commentingThreadPreview</strong></td><td>Enables a pop-over preview on the stage for comments.</td><td>No</td><td><code>true</code></td></tr><tr><td><strong>commentingNotifications</strong></td><td>Enables notifications of new comments in co-editing.</td><td>No</td><td><code>true</code></td></tr><tr><td><strong>disableLinkSanitize</strong></td><td>Disables link validation for URLs, including telephone number or SMS to enable merge content use.</td><td>No</td><td><code>false</code></td></tr></tbody></table>
