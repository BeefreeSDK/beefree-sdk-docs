# Error Management

Use this guide to implement and manage error handling for Beefree SDK in your application. You'll learn how to structure errors, classify them consistently, localize messages, and surface them effectively in your UI.

There are two primary error types:

* **Errors**: These are critical and interrupt normal execution. They typically require the end user or system to take corrective action.
* **Warnings**: These are non-blocking and indicate a recoverable or informational condition, like a locked module or a timed-out iframe.

## Attributes

Each error or warning may include the following:

| Attribute     | Type    | Description                                                                  |
| ------------- | ------- | ---------------------------------------------------------------------------- |
| `code`        | Integer | A unique numeric identifier for the error or warning.                        |
| `name`        | String  | A short identifier for internal reference and debugging.                     |
| `message`     | String  | A human-readable message summarizing the problem.                            |
| `detail`      | Object  | Additional structured information, such as invalid parameters or language.   |
| `title`       | String  | Optional. A localized title (from `useIntl` and `errorsTranslations`).       |
| `description` | String  | Optional. A localized description (from `useIntl` and `errorsTranslations`). |

## Error Code Reference

A categorized directory of all known error codes, their default messages, and classifications.

### Generic Errors

<table><thead><tr><th width="133.96875">Code</th><th>Name</th><th>Message</th></tr></thead><tbody><tr><td>9900</td><td>apiGeneric</td><td>(unlisted fallback)</td></tr><tr><td>9999</td><td>genericError</td><td>An error occurred</td></tr><tr><td>503</td><td>fspGeneric</td><td>An error occurred</td></tr></tbody></table>

### Authentication Errors

<table><thead><tr><th width="134.4375">Code</th><th>Name</th><th>Message</th></tr></thead><tbody><tr><td>4001</td><td>authHeaderMissing</td><td>—</td></tr><tr><td>4005</td><td>authBearerInvalid</td><td>—</td></tr><tr><td>4010</td><td>authTokenExpired</td><td>—</td></tr><tr><td>5001</td><td>contentTypeFormUrlError</td><td>—</td></tr><tr><td>5002</td><td>unableToAuthenticate</td><td>—</td></tr><tr><td>5003</td><td>applicationDisabled</td><td>—</td></tr><tr><td>5005</td><td>invalidUID</td><td>—</td></tr><tr><td>5101</td><td>reLoginNeeded</td><td>Must login again and inject new token</td></tr><tr><td>5102</td><td>reLoginAndUpgradeNeeded</td><td>Must login again and re-create Plugin</td></tr></tbody></table>

### Add-on Errors

<table><thead><tr><th width="134.16015625">Code</th><th>Name</th><th>Message</th><th>Type</th></tr></thead><tbody><tr><td>1810</td><td>iframeTimeout</td><td>The iframe took too long to load</td><td>Warning</td></tr><tr><td>1820</td><td>iframeAuthFailed</td><td>Error authenticating the add-on</td><td>Warning</td></tr></tbody></table>

### Template Errors

<table><thead><tr><th width="134.828125">Code</th><th>Name</th><th>Message</th></tr></thead><tbody><tr><td>1100</td><td>invalid</td><td>The template is malformed and cannot be loaded. Check it and try again.</td></tr><tr><td>1101</td><td>invalid</td><td>The template cannot have more than one row when <code>editSingleRow</code> is <code>true</code>.</td></tr><tr><td>1300</td><td>invalid</td><td>The language is not valid (conflicts with LOCKED_ROW warning)</td></tr></tbody></table>

### Locked Content Warnings

<table><thead><tr><th width="134.19921875">Code</th><th>Name</th><th>Message</th><th>Type</th></tr></thead><tbody><tr><td>1300</td><td>locked</td><td>This row is locked and therefore its content cannot be edited.</td><td>Warning</td></tr><tr><td>1310</td><td>locked</td><td>Locked content blocks cannot be edited.</td><td>Warning</td></tr><tr><td>7020</td><td>lockedEntity</td><td>Locked entity</td><td>Warning</td></tr></tbody></table>

### Frontend API Errors

<table><thead><tr><th width="134.046875">Code</th><th>Name</th><th>Message</th></tr></thead><tbody><tr><td>7005</td><td>invalidCommand</td><td>Invalid command</td></tr><tr><td>7010</td><td>invalidCommandOptions</td><td>Invalid command options</td></tr><tr><td>7030</td><td>entityNotFound</td><td>Entity not found</td></tr><tr><td>7040</td><td>elementNotFound</td><td>Element not found</td></tr><tr><td>7050</td><td>forbiddenCommand</td><td>The command execution is not allowed</td></tr></tbody></table>

### Plan Limitations

<table><thead><tr><th width="133.09765625">Code</th><th>Name</th><th>Message</th></tr></thead><tbody><tr><td>1704</td><td>featureNotAvailable</td><td>This feature is not available for this plan</td></tr><tr><td>1705</td><td>featureNotEnabled</td><td>—</td></tr><tr><td>1706</td><td>featureNotAvailableInCoedit</td><td>—</td></tr><tr><td>1710</td><td>featureLimitReachedForPlan</td><td>—</td></tr><tr><td>1702</td><td>workspaceNotAvailableForPlan</td><td>—</td></tr><tr><td>1002</td><td>workspaceNotAvailable</td><td>—</td></tr></tbody></table>

### File System Provider (FSP) Errors

<table><thead><tr><th width="135.58984375">Code</th><th>Name</th></tr></thead><tbody><tr><td>3100</td><td>fspBeGenericError</td></tr><tr><td>3200</td><td>fspResourceNotFound</td></tr><tr><td>3300</td><td>fspPermissionDenied</td></tr><tr><td>3400</td><td>fspResourceAlreadyPresent</td></tr><tr><td>3401</td><td>fspResourceAlreadyPresentNoDialog</td></tr><tr><td>3450</td><td>fspFileNotUploaded</td></tr><tr><td>3500</td><td>fspRequestError</td></tr><tr><td>3600</td><td>fspUserError</td></tr><tr><td>3650</td><td>fspWrongCredentials</td></tr><tr><td>3750</td><td>fspInvalidImportUrl</td></tr></tbody></table>

### Translation Errors

<table><thead><tr><th width="135.46484375">Code</th><th>Name</th></tr></thead><tbody><tr><td>6050</td><td>translationGenericBeError</td></tr><tr><td>6150</td><td>autoTranslateNotSupported</td></tr></tbody></table>

### JSON Preprocessing and Validation Errors

| Code      | Name                           | Message                           |
| --------- | ------------------------------ | --------------------------------- |
| 4101–4192 | Various (e.g., CSS, HTML tags) | Specific JSON validation failures |
| 4501–4504 | CSS Conversion Errors          |                                   |

Reference the following pages for more information on additional errors:

* [onWarning](warning-error-info-callbacks.md)
* [Beefree SDK Editor Errors](beefree-sdk-editor-errors.md)
* [File System Provider Errors](file-system-provider-errors.md)
* [JSON Parser Errors](json-parser-errors.md)
* [Template Validation and Update](template-validation-and-update.md)
* [Template Validation and Update Errors](template-validation-and-update-errors.md)
