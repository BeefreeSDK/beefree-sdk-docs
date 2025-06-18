# Frontend Commands

{% hint style="info" %}
Frontend Commands are available on all [Beefree SDK paid plans](https://developers.beefree.io/pricing-plans).
{% endhint %}

## Overview

Frontend Commands let you control the builder’s user interface programmatically. You can focus on specific elements, scroll to parts of the UI, highlight areas temporarily, or select content on the stage.

These commands help you build guided experiences, automate QA checks (when couple with the [Content Services API Check endpoints](../apis/content-services-api/check.md)), or create onboarding flows by directing attention exactly where it’s needed—whether on the stage or in the sidebar.

**Available actions:**

* [**Focus**](frontend-commands.md#focus-1) – Move focus to a specific element.
* [**Scroll**](frontend-commands.md#scroll) – Navigate to a precise part of the editor.
* [**Highlight**](frontend-commands.md#highlight) – Briefly emphasize a target element.
* [**Select**](frontend-commands.md#select) – Choose a row or module within the template.

{% hint style="info" %}
**Important:** You can use Frontend Commands to navigate to elements with the entire builder. This includes the stage and the sidebar. For example, if you want to navigate to an image on the stage missing alt text, and then indicate on the sidebar where the end user can add the alt text, both are possible with Frontend Commands.&#x20;
{% endhint %}

## Method <a href="#focus" id="focus"></a>

The `execCommand` method is the central function used to trigger any Frontend Command within Beefree SDK. It allows you to execute one of the four supported actions—`focus`, `scroll`, `highlight`, or `select`—by specifying both the action name and a `target` object.

## Target Object

The target object is an important concept within Frontend Commands. It defines where in the UI the Frontend Command should act. It specifies the exact element—on the stage or in the sidebar—that the action should interact with.

Depending on the action being performed, certain target fields are required. The following table provides a comprehensive reference of the target options, examples values, and a description including which actions correspond with the target option.

| Target Options            | Example Values                 | Descriptions                                                                    |
| ------------------------- | ------------------------------ | ------------------------------------------------------------------------------- |
| `key`                     | `'font-weight'`                | For sidebar controls (used in `focus`, `scroll`, `highlight`)                   |
| `selector`                | `'.my-element-class'`          | For DOM elements (used in `focus`, `scroll`)                                    |
| `uuid`                    | `'abc123-uuid-value'`          | For modules or rows (used in `scroll`, `highlight`, `select`)                   |
| `row`, `column`, `module` | `row: 2, column: 1, module: 3` | For a specific module via coordinates (used in `scroll`, `highlight`, `select`) |

## How Actions Work

Each Frontend Command is executed using a consistent structure. Here's how to construct and use them:

1. **Define the SDK instance**: Use the Beefree SDK instance you’ve initialized (e.g., `beeInstance`).
2. **Use the `execCommand` method**: This method is used to trigger all Frontend Commands.
3. **Specify the action**: Pass one of the four supported action strings: `"focus"`, `"scroll"`, `"highlight"`, or `"select"`.
4. **Define the `target` object**: This object determines where in the editor the action applies. Depending on the action, you may use `key`, `selector`, `uuid`, or coordinates in the form of `row`, `column`, and `module`.

The following code snippet provides an example of scrolling to a button in the DOM:

```javascript
beeInstance.execCommand('scroll', {
  target: { selector: 'button' }
});
```

The following sections include comprehensive steps and examples on how to use each action and target with the `execCommand` method.

## Focus <a href="#focus" id="focus"></a>

The focus command will set the focus on the first focusable DOM element based on the passed target.

The target can be defined with a `key` or a `selector`; either one or the other is mandatory. If both are provided, the `selector` will be used.

### Details <a href="#details" id="details"></a>

The following table provides additional details on the options you can use to define a target for the focus action using the `execCommand` method.

| Field      | Type   | Mandatory                                   | Description                                                                                                                                                                                                                |
| ---------- | ------ | ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `selector` | string | `true` (mutually exclusive with `key`)      | An actual valid CSS selector. If it matches, it will set the focus on the first focusable element (itself or a child element).                                                                                             |
| `key`      | string | `true` (mutually exclusive with `selector`) | A reference to a sidebar property, usually matching the label shown in the UI but converted to kebab-case (e.g., **Line height** → `line-height`). The exact value can be found in the DOM within the `data-qa` attribute. |

### How to Use Focus <a href="#errors" id="errors"></a>

Take the following steps to focus on a specific element in the builder:

1. Identify the element you want to focus on, using either a CSS selector or a sidebar control key.
2. Call the `execCommand` method on the Beefree SDK instance.
3. Set the action to `"focus"` and define the `target` using either the `selector` or `key`.

#### Examples

To focus on the selected row toolbar:

```javascript
beeInstance.execCommand('focus', {
  target: { selector: '.row-actions-toolbar--cs' }
});
```

Which results in the visual cue displayed in the following image:

<figure><img src="../.gitbook/assets/CleanShot 2025-06-10 at 16.42.19.png" alt=""><figcaption></figcaption></figure>

To focus on the “line height” property in the sidebar:

```javascript
beeInstance.execCommand('focus', {
  target: { key: 'line-height' }
});
```

Which results in the visual cue displayed in the following image:

<figure><img src="../.gitbook/assets/CleanShot 2025-06-10 at 16.43.36.png" alt=""><figcaption></figcaption></figure>

### Handle Focus Errors <a href="#errors" id="errors"></a>

If no element matches the provided `selector` or `key`, Beefree SDK throws the following error:

```json
{
  "code": 7040,
  "detail": { "selector": "[data-qa=\"line-height\"]" },
  "message": "Element not found with selector [data-qa=\"line-height\"]",
  "name": "elementNotFound"
}
```

* **What it means:** The target element isn’t present in the DOM at execution time.
* **How to fix:** Make sure the element exists and is visible before calling the command.

## Scroll <a href="#scroll" id="scroll"></a>

The scroll command will scroll to the passed target position.

The target can be defined with a `key`, a `selector,` coordinates (`row`, `column`, `module`), or `uuid`. Either the `key`, the `selector`, the `uuid`, or the coordinates need to be defined.

### Details <a href="#details.2" id="details.2"></a>

The following table provides additional details on the options you can use to define a target for the scroll action using the `execCommand` method.

| Field      | Type   | Mandatory                                             | Description                                                                                                                                                                                                                |
| ---------- | ------ | ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key`      | string | `true` (mutually exclusive with `row` and `selector`) | A reference to a sidebar property, usually matching the label shown in the UI but converted to kebab-case (e.g., **Line height** → `line-height`). The exact value can be found in the DOM within the `data-qa` attribute. |
| `selector` | string | `true` (mutually exclusive with `key` and `row`)      | An actual valid CSS selector. If it matches, it will scroll to the found element.                                                                                                                                          |
| `row`      | number | `true` (mutually exclusive with `key` and `selector`) | The positional number of the row to scroll to or the row the final target is in.                                                                                                                                           |
| `column`   | number | `true` if `module` is defined                         | The positional number of the column the module is in.                                                                                                                                                                      |
| `module`   | number | `true` if `column` is defined                         | The positional number of the module to scroll to.                                                                                                                                                                          |
| `uuid`     | string | `true` if none of the coordinates are defined         | The unique identifier of the target (row or module).                                                                                                                                                                       |

### How to Use Scroll

Take the following steps to scroll to a specific part of the editor:

1. Determine what you want to scroll to—this can be a sidebar property, a DOM element, a row/module via coordinates, or an element via UUID.
2. Call the `execCommand` method on the Beefree SDK instance.
3. Set the action to `"scroll"` and define the `target` appropriately.

#### Examples

To scroll to the 3rd module of the 1st column in the 2nd row:

```javascript
beeInstance.execCommand('scroll', {
  target: { row: 2, column: 1, module: 3 }
});
```

To scroll to an element using a UUID:

```javascript
beeInstance.execCommand('scroll', {
  target: { uuid: 'a123abcd-0a01-12a1-12a0-a12b3456789c' }
});
```

To scroll to the “Font weight” property in the sidebar:

```javascript
beeInstance.execCommand('scroll', {
  target: { key: 'font-weight' }
});
```

To scroll to a button:

```javascript
beeInstance.execCommand('scroll', {
  target: { selector: 'button'}
});
```

### Handle Scroll Errors <a href="#errors.2" id="errors.2"></a>

If the target isn’t found, the following error is returned:

```json
{
  "code": 7030,
  "name": "entityNotFound",
  "message": "Entity at target {\"row\":4} not found",
  "detail": { "target": { "row": 4 } }
}
```

* **What it means:** The specified row, UUID, key, or selector does not match any element.
* **How to fix:** Double-check that the coordinates or identifiers are correct and that the content is rendered.

## Highlight <a href="#highlight" id="highlight"></a>

The highlight command will highlight the passed target for three seconds.

The target can be defined with a `key`, coordinates (`row`, `column`, `module`), or `uuid`. Either the `key`, the `uuid`, or the coordinates need to be defined.

### Details <a href="#details.1" id="details.1"></a>

The following table provides additional details on the options you can use to define a target for the highlight action using the `execCommand` method.

| Field    | Type   | Mandatory                                     | Description                                                                                                                                                                                                                |
| -------- | ------ | --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key`    | string | `true` (mutually exclusive with `row`)        | A reference to a sidebar property, usually matching the label shown in the UI but converted to kebab-case (e.g., **Line height** → `line-height`). The exact value can be found in the DOM within the `data-qa` attribute. |
| `row`    | number | `true` (mutually exclusive with `key`)        | The positional number of the row to highlight or the row the final target is in.                                                                                                                                           |
| `column` | number | `true` if `module` is defined                 | The positional number of the column the module is in.                                                                                                                                                                      |
| `module` | number | `true` if `column` is defined                 | The positional number of the module to highlight.                                                                                                                                                                          |
| `uuid`   | string | `true` if none of the coordinates are defined | The unique identifier of the target (row or module).                                                                                                                                                                       |

### How to Use Highlight  <a href="#errors.1" id="errors.1"></a>

Take the following steps to temporarily highlight a specific element:

1. Identify the element using a `key`, `uuid`, or `coordinates`.
2. Call the `execCommand` method on the Beefree SDK instance.
3. Set the action to `"highlight"` and define the `target`.

#### Examples

To highlight the 3rd module of the 1st column in the 2nd row:

```javascript
beeInstance.execCommand('highlight', {
  target: { row: 2, column: 1, module: 3 }
});
```

Which results in the visual cue displayed in the following GIF:

<figure><img src="../.gitbook/assets/WhatsApp GIF 2025-04-15 at 18.06.14 (1).gif" alt="" width="375"><figcaption></figcaption></figure>

To highlight an element by UUID:

```javascript
beeInstance.execCommand('highlight', {
  target: { uuid: 'a123abcd-0a01-12a1-12a0-a12b3456789c' }
});
```

Which results in the visual cue displayed in the following GIF:

<figure><img src="../.gitbook/assets/WhatsApp GIF 2025-04-15 at 18.06.14 (1).gif" alt="" width="375"><figcaption></figcaption></figure>

To highlight the “Font weight” sidebar control:

```javascript
beeInstance.execCommand('highlight', {
  target: { key: 'font-weight' }
});
```

Which results in the visual cue displayed in the following GIF:

<figure><img src="../.gitbook/assets/WhatsApp GIF 2025-04-15 at 18.06.13.gif" alt="" width="375"><figcaption></figcaption></figure>

### Handle Highlight Errors <a href="#errors.1" id="errors.1"></a>

If no element matches the target, the following error is returned:

```json
{
  "code": 7030,
  "name": "entityNotFound",
  "message": "Entity at target {\"row\":4} not found",
  "detail": { "target": { "row": 4 } }
}
```

* **What it means:** The target (via coordinates, key, or UUID) doesn’t point to a valid element.
* **How to fix:** Verify that the target refers to an existing and rendered element.

## Select <a href="#select" id="select"></a>

The select command will select the passed target position module or row.

The target can be defined with coordinates (`row`, `column`, `module`).

### Details <a href="#details.3" id="details.3"></a>

The following table provides additional details on the options you can use to define a target for the select action using the `execCommand` method.

| Field    | Type   | Mandatory                                             | Description                                                                   |
| -------- | ------ | ----------------------------------------------------- | ----------------------------------------------------------------------------- |
| `row`    | number | `true` (mutually exclusive with `key` and `selector`) | The positional number of the row to select or the row the final target is in. |
| `column` | number | `true` if `module` is defined                         | The positional number of the column the module is in.                         |
| `module` | number | `true` if `column` is defined                         | The positional number of the module to select.                                |
| `uuid`   | string | `true` if none of the coordinates are defined         | The unique identifier of the target (row or module).                          |

### How to Use <a href="#errors.3" id="errors.3"></a>

Take the following steps to select a specific module or row on the stage:

1. Choose the target element using coordinates (`row`, `column`, `module`) or a `uuid`.
2. Call the `execCommand` method on the Beefree SDK instance.
3. Set the action to `"select"` and define the `target`.

#### Examples

To select the 3rd module of the 1st column in the 2nd row:

```javascript
beeInstance.execCommand('select', {
  target: { row: 2, column: 1, module: 3 }
});
```

To select an element using a UUID:

```javascript
beeInstance.execCommand('select', {
  target: { uuid: 'a123abcd-0a01-12a1-12a0-a12b3456789c' }
});
```

### Handle Select Errors <a href="#errors.3" id="errors.3"></a>

When the element can’t be located, the following error is thrown:

```json
{
  "code": 7030,
  "name": "entityNotFound",
  "message": "Entity at target {\"row\":4} not found",
  "detail": { "target": { "row": 4 } }
}
```

* **What it means:** The given coordinates or UUID don’t resolve to any element in the template.
* **How to fix:** Ensure the target exists in the current template and the row/module indexes are accurate.
