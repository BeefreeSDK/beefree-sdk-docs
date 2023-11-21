# Advanced settings

What if the default styles and standard settings aren’t enough? No worries! In the following sections, we will look at styling your popup to make it look and feel more like the one real visitors will interact with.

### Custom styles (themes) <a href="#custom-styles-themes" id="custom-styles-themes"></a>

A theme is simply a set of custom styles that give the popup its look and feel. Separate from your layout, Popup Builder comes with some preset themes.  The primary is our default theme that is loaded when no settings are specified.  We also provide an empty theme that has no styles, which you can use a blank canvas to create your own theme.  This is one of the most powerful features of Popup Builder, and we’ll be covering custom styles in depth below.

Here is a preview of the configuration:

```json
workspace: {
  popup: {
    customStyles: {
      ...
    },
  }
}
```

#### Applying styles to the HTML <a href="#applying-styles-to-the-html" id="applying-styles-to-the-html"></a>

To understand the best way to apply your styles, let’s start by inspecting the underlying HTML structure so you can view where the system will map your styles.

**Popup HTML**

```markup
<div id="popup-container">
  <div id="popup-header">
    <div></div>
    <div></div>
  </div>
  <div id="popup-content">
    <!-- BEE CONTENT -->
  </div>
  <div id="popup-footer">
    <div></div>
    <div></div>
  </div>
</div>  
```

Here is a quick break down of what each div does:

```
popup-container
```

This is where you will apply any styles related to how the popup looks, such as border-radius, drop shadows, background colors, or padding.

```
popup-header
```

The header is sometimes used to add a close icon to a popup or display a title.

```
popup-content
```

The div that holds the editable content of your Beefree application.

```
popup-footer
```

You can use this div to show a traditional footer for your popup or position some icons outside the popup container (e.g., a close button).

The above HTML structure is represented in your bee config as the following JSON object.

```json
customStyles: {
  container: {},
  header: {},
  content: {},
  footer: {},
  overlay: {},
},   
```

Add styles to the JSON section that corresponds to the HTML element you want to style.

For example, if you want to apply styles to the div with id popup-container, then you would add the styles to the following JSON:

```json
customStyles: {
  container: {
    ...styles,
  },
},   
```

We’ll go deeper into styling in the following sections.

### Order of operations <a href="#order-of-operations" id="order-of-operations"></a>

You may be wondering at this point if you have to design an entire theme to get started. Well, you can if you want to, but thanks to the order of operations, you don’t have to. You can start with our default theme and pass in the styles that you want to override. Any style you provide will take priority over any of the defaults.

#### Starting from scratch <a href="#starting-from-scratch" id="starting-from-scratch"></a>

We said that you could start from scratch if you want, and the easiest way to do that is by using our theme parameter.  This allows you to avoid overriding every default style and gives you an empty canvas to build your own theme.

Example:

```json
beeConfig: {
  workspace: {
    popup: {
      theme: 'custom'
    }
  }
}
```

#### Applying custom styles <a href="#applying-custom-styles" id="applying-custom-styles"></a>

Now that you have seen what the HTML looks like and have some idea where to apply your styles, let’s look at how you get your styles into the editor. The best way to show you is by example, so let’s get started with some common use cases!

**Adding a border**

Using the schema JSON above and your HTML structure knowledge, you probably guessed that the border is defined on the popup container. So here’s what that would look like:

Example:

```

workspace: {
  popup: {
    customStyles: {
      container: {
        border: '1px solid black'
      }   
    }
  }
}

```

**Adding a drop shadow**

**Example:**

<pre><code><strong>workspace: {
</strong>  popup: {
    customStyles: {
      container: {
        boxShadow: '0 5px 15px rgba(0, 0, 0, 0.5)'
      }
    }
  }
}
</code></pre>

#### Deep-dive into CSS properties <a href="#deep-dive-into-css-properties" id="deep-dive-into-css-properties"></a>

After looking at a couple of samples, you may notice these parameters are looking familiar. That’s because every layer of our schema maps to a layer of HTML with the same name AND can be styled with any valid CSS property.

Basically, CSS properties are the same as CSS used by web developers in style sheets, but instead of dashes to separate words, it uses a camel case.

Example:

The CSS property of the style box-shadow would be boxShadow.

Why not use CSS styles as defined by CSS3 specification directly? Well, simply put, CSS properties are better suited for JSON and can easily be shared with any FE application using the popular React framework.

### Custom layouts <a href="#custom-layouts" id="custom-layouts"></a>

We covered the default layout settings in Setting layout and size section. To recap, the layout determines the type of popup (e.g., a bar) and its location on the screen (e.g., bottom, top, or side). Our research team looked into it, and it turns out, nearly all popups fall into one of the most popular layouts, which we’ve included as presets. But, when that’s not enough, the configuration option customLayout can be used to make minor adjustments to a preset layout or create an entirely new layout from scratch.

Here is a preview of the configuration:

```
workspace: {
  popup: {
    customLayout: {
      ...
    },
  }
}
```

### The layout HTML <a href="#the-layout-html" id="the-layout-html"></a>

The popup is positioned in the workspace using divs and CSS flexbox. We created a layout structure that mimics an HTML page to map your page’s styles to the workspace.

Layout HTML:

```markup
<div id="html">
  <div id="body">
    <div id="main">    
      <div id="popup-wrapper">
        <!-- Popup -->
      </div>
      <div id="popup-overlay">
    </div>
  </div>
</div>  
```

**Overview**

Here is a quick break down of what each div does:

```
HTML
```

We will apply the styles placed here to the document HTML tag.

```
body
```

We will apply the styles placed here to the HTML body tag

```
main
```

This is the main container div of the workspace.

```
popup-wrapper
```

The wrapper of the popup is used entirely for positioning the popup within the workspace main div.

### Changing the position of a layout <a href="#changing-the-position-of-a-layout" id="changing-the-position-of-a-layout"></a>

Example:

```json
workspace: {
  popup: {
    layout: 'classic-center',
    customLayout: {
       wrapper: {
        maxWidth: '700px'
      }  
    }
  }
}
```
