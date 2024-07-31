# Workspaces

## Overview <a href="#overview" id="overview"></a>

In user interfaces, a workspace is a parameter that changes the appearance, settings, and widgets available in an builder, to help the user to focus on what matters.

In Beefree SDK, **workspaces**  are an optional parameter that can be used to provide an experience **focused on context and purpose**, and to **facilitate the outcome** of an editing session.

You can load the builder with a certain workspace, but workspaces can also be changed by the user when editing, on-the-fly.

Switching between workspaces might change:

* content visibility on the stage
* tiles availability in the content tab
* available previews
* outputs when saving a content
* …and more!

## Available workspaces <a href="#available-workspaces" id="available-workspaces"></a>

If no workspace is loaded at launch, the builder starts in its “Default” workspace.

We currently offer 3 additional workspaces, and we are planning to launch more as we evolve BEE and its capabilities.

These 3 workspaces revolve around the use of **AMP content**, and are provided so that you can tailor the experience of creating AMP emails in Beefree SDK.

Here is an overview of the different workspaces and their differences. Please [refer to this page](../../../../other-customizations/amp-for-email.md) for more information on using AMP in Beefree SDK.

|                                                   | default                    | mixed                    | amp\_only                                 | html\_only                               |
| ------------------------------------------------- | -------------------------- | ------------------------ | ----------------------------------------- | ---------------------------------------- |
| **Stage message**                                 | HTML content               | HTML & AMP content       | HTML & AMP content                        | HTML content                             |
| **Content tiles**                                 | HTML content tiles         | HTML & AMP content tiles | HTML & AMP content tiles                  | HTML content                             |
| **AMP sidebar properties**                        | No                         | Yes                      | Yes                                       | No                                       |
| **Available in preview**                          | HTML content               | HTML & AMP content       | HTML & AMP content                        | HTML content                             |
| **onSave callback files**                         | HTML                       | HTML & AMP               | HTML & AMP                                | HTML                                     |
| **Loading a template with AMP content**           | The onWarning is triggered | Template loads           | Template loads                            | Template loads                           |
| **Loading a template with HTML content only**     | Template loads             | Template loads           | Template loads                            | Template loads                           |
| **Availability of the hide on AMP/HTML property** | Not available              | Yes                      | Yes                                       | Yes                                      |
| **Behavior for hidden for HTML/AMP content**      | The onWarning is triggered | Both are visible         | Only “hidden for HTML” content is visible | Only “hidden for AMP” content is visible |

## Starting the builder with a workspace <a href="#starting-the-builder-with-a-workspace" id="starting-the-builder-with-a-workspace"></a>

Here is an example of loading Beefree SDK with a “mixed” workspace:

```javascript

type ClientConfig = {
  workspace?: {
    type:'default'|'mixed'|'amp_only'|'html_only'
  }
  // ....
}

const beeConfig: ClientConfig = {
  workspace:{
    type:'mixed'
  }
  // ....
}


//Create the instance 
function BeePlugin.create(token, beeConfig, (beePluginInstance) => { 
  //.... 
}

```

## Switching workspaces <a href="#switching-workspaces" id="switching-workspaces"></a>

You can implement a workspace selector within your application, so that users can switch between workspaces, by using the `loadWorkspace(type)` method.

First, you need to define template files for the workspaces you want to propose, as JSONs:

```javascript
{
  "type":"mixed"
}
```

Then, you can load those workspaces at runtime:

```javascript
type Workspace = 'default'|'mixed'|'amp_only'|'html_only'

const req = url => fetch(url).then(r => r.json())
const loadWorkspace = async (workspace:Workspace) => {
  const { type } = await req(`https://example.com/workspaces/${workspace}.json`)
  beePluginInstance.loadWorkspace(type) 
}
```

And here is how to create a simple select to switch workspace:

```markup
<select id="workspace" onchange="loadWorkspace(this.value)">
<option selected="selected" value="">WORKSPACE</option>
<option value="default">DEFAULT</option>
<option value="mixed">MIXED</option>
<option value="amp_only">AMP_ONLY</option>
<option value="html_only">HTML_ONLY</option>
</select>
```

## Workspace callbacks <a href="#workspace-callbacks" id="workspace-callbacks"></a>

After you load a workspace, the application will trigger one of these three callbacks:

### **Success**

```javascript
//SUCCESS 
onLoadWorkspace: function (workspace) {
  console.log(`workspace: ${workspace} has been loaded`);
},
```

### **Failure**

<pre class="language-javascript"><code class="lang-javascript"><strong>//FAILURE
</strong>onError: function (error) {
 console.error('error: ', error);
},
</code></pre>

### **Invalid workspace**

```javascript
{
 code: 1400, 
 name: "Invalid workspace type",
 message: "RANDOM : is not a valid workspace",
 details: "Available workspaces are: [ default,mixed,amp_only,html_only ]"
}
```

## Use cases <a href="#use-cases" id="use-cases"></a>

The additional workspaces for AMP (AMP-only and HTML-only) can become helpful if you want to tailor the user experience of creating AMP emails, by adding:

* a workflow where users decides if they want to create a standard message or an AMP-powered message (in the first case, AMP components will be hidden in the builder;
* an option to switch between the HTML and the AMP editing of a message.

In addition, omitting the workspace, or loading the “default” workspace for certain users, has the effect of disabling AMP for those users, even when AMP content is enabled in the [Beefree SDK Console](https://developers.beefree.io/). This way, you can decide to make the feature available to customers of your application:

* **depending on the subscription plan** that they are on (i.e. you could push users to a higher plan based on the ability to use AMP);
* **depending on the purchase** of an optional feature (same);
* only if they are **“beta” customers**, so they see it while keeping it hidden from the rest of your users.
