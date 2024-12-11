---
description: Use newbutton for improved HTML button rendering in Outlook.
---

# HTML Outlook Button Rendering

{% hint style="info" %}
**Important:** You need access to the [Content Services API](../apis/content-services-api/content-services-api-reference.md), which is available on [paid plans](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees), to add the `newbutton` query string parameter to your API call when transforming Beefree SDK JSON to HTML.
{% endhint %}

### HTML Outlook Button Rendering

Outlook’s unique rendering engine often requires specific adjustments to ensure buttons display and function correctly. This article explains how to use the `newbutton` query string parameter when transforming Beefree SDK JSON into HTML using the [HTML endpoint in the Content Services API (CSAPI)](../apis/content-services-api/content-services-api-reference.md#html) to enhance button rendering in Outlook.

### HTML Without the `newbutton` Query Parameter

By default, the HTML output from the CSAPI includes a VML block for Outlook rendering placed before the \<a> tag. While this ensures compatibility with Outlook, it has the following limitations:

* **Accessibility Issues:** The \<a> tag cannot be activated using a keyboard because it resides inside the VML block.
* **Forwarding Issues:** Buttons may become unclickable when emails are forwarded in Outlook due to how Outlook handles nested elements.

**Example:** HTML Without `newbutton`

```html
<div class="alignment" align="center">
  <!--[if mso]>
  <v:roundrect xmlns:v="urn:schemas-microsoft-com:vml" 
               xmlns:w="urn:schemas-microsoft-com:office:word" 
               href="https://docs.beefree.io/beefree-sdk" 
               style="height:37px;width:80px;v-text-anchor:middle;" 
               arcsize="11%" stroke="false" fillcolor="#3AAEE0">
    <w:anchorlock/>
    <v:textbox inset="0px,0px,0px,0px">
      <center dir="false" style="color:#ffffff;font-family:Arial, sans-serif;font-size:14px">
  <![endif]-->
  <a href="https://docs.beefree.io/beefree-sdk" 
     target="_blank" 
     style="background-color:#3AAEE0;color:#ffffff;display:inline-block;
            font-family:Arial, Helvetica, sans-serif;font-size:14px;font-weight:400;
            text-align:center;text-decoration:none;width:auto;">
    <span style="padding-left:20px;padding-right:20px;line-height:28px;">Button</span>
  </a>
  <!--[if mso]>
      </center>
    </v:textbox>
  </v:roundrect>
  <![endif]-->
</div>

```

### HTML With the `newbutton` Query Parameter

Setting the `newbutton=true` query parameter ensures buttons are accessible and functional. This adjustment:

* Moves the \<a> tag outside the VML block, enabling full keyboard accessibility.
* Places the VML block after the \<a> tag, ensuring compatibility with Outlook and resolving forwarding issues.
* Wraps the button label inside a \<div>, providing improved layout control for consistent padding and word-breaking compared to the inline \<a> tag in the default HTML.

**Example:** HTML With `newbutton`

```html
<a href="https://docs.beefree.io/beefree-sdk" 
   target="_blank" 
   style="background-color:#3AAEE0;color:#ffffff;display:inline-block;
          font-family:Arial, Helvetica, sans-serif;font-size:14px;font-weight:400;
          text-align:center;text-decoration:none;width:auto;">
  <div style="padding:10px 20px;line-height:28px;">
    Button
  </div>
</a>
<!--[if mso]>
<v:roundrect xmlns:v="urn:schemas-microsoft-com:vml" 
             xmlns:w="urn:schemas-microsoft-com:office:word" 
             href="https://docs.beefree.io/beefree-sdk" 
             style="height:37px;width:80px;v-text-anchor:middle;" 
             arcsize="11%" stroke="false" fillcolor="#3AAEE0">
  <w:anchorlock/>
  <v:textbox inset="0px,0px,0px,0px">
    <center dir="false" style="color:#ffffff;font-family:Arial, sans-serif;font-size:14px">
      Button
    </center>
  </v:textbox>
</v:roundrect>
<![endif]-->

```

#### Benefits of `newbutton`

* **Accessibility:** Buttons are fully keyboard-activated due to the \<a> tag placement.
* **Forwarding Compatibility:** Buttons remain clickable in forwarded Outlook emails by addressing Outlook's handling of nested elements.
* **Styling Flexibility:** Button text is enclosed within a \<div>, allowing for easier customization and consistent padding.

### How to Use the New Button

You can enable the `newbutton` option using two options:

**Option 1: Query String Parameter**

Include `newbutton=true` in the query string of your CSAPI call:

```http
POST https://api.getbee.io/v1/{collection}/html?newbutton=true
Content-Type: application/json

{
    "page": {
        "body": {
            ...
        },
        "title": "Empty Template"
    },
    "comments": {}
}

```

**Option 2: JSON Property**

Add `"newbutton": true` to the JSON payload:

```json
{
    "page": {
        "body": {
            ...
        },
        "title": "Empty Template"
    },
    "newbutton": true,
    "comments": {}
}
```
