# Generating Custom Rows from existing content

Custom Rows allows you to easily generate draggable rows from your application content, or other application content, without any design process or complex user interaction.

## General row parameters <a href="#simplified-row-schema" id="simplified-row-schema"></a>

### **name**

The row’s name:

* A string of plain text that identifies the row.
* Displayed in the row card when the row is shown in the _Rows_ panel.
* Included in the textual content used in searches

### **background image**

Set a row background image.

Properties:

* background-image: valid image url
* background-repeat: repeat | no-repeat
* background-position: top | bottom + left | center | right
* background-color: #c2c2c2 // CSS value

### **display conditions**

Set a row display condition.\
Check the [display conditions documentation](../../other-customizations/advanced-options/display-conditions.md) for further details.

Properties:

* display-condition
  * type
  * label
  * description
  * before
  * after

### **mobile**

Disable stacking on mobile.  Set the value to “false” to disable stacking on mobile.  If the value is “true”, or not provided, the columns will stack on mobile.

* colStackOnMobile: true | false

### **columns**

List of the row columns. Each column type is identified with a weight parameter to indicate how much horizontal space they fill.\
We use a 12-column grid with the following values as available combinations:

* 12
* 9, 3
* 8, 4
* 6, 6
* 6, 3, 3
* 4, 8
* 4, 4, 4
* 3, 9
* 3, 3, 6
* 3, 6, 3
* 3, 3, 3, 3

All the columns weight inside a row must sum 12 as the total value.

See the example above in _General Row Schema_.

### **modules**

List of content modules inside a column

### **type**

Every module is identified by a type parameter. Available types are:

* _title_
* _paragraph_
* _image_
* _button_
* _divider_
* _HTML_

Each module type has a set of available options. If none is included, the editor will use the default values.

## Content types scheme and parameters <a href="#content-types-scheme-and-parameters" id="content-types-scheme-and-parameters"></a>

### **Text**

```javascript

{
  "type": "title",
  "text": "I'm a headline."
}, {
  "type": "paragraph",
  "text": "I can be a long paragraph, a short sentence, or a simple word."
}

```

**title** adds the text with the following attributes:

* Font-size: 18px
* Font-weight: Bold
* Text-align: left

**paragraph** will use the following formatting:

* Font-size: 14px
* Text-align: left

**text** contains the string that will be displayed as content:

* Must be a plain text string
* Quotation marks must be escaped to be compliant with the JSON format
* If not included, a default “Loren Ipsum” text string will be used

## **Additional text parameters**

```javascript

"align": "center" "left" "right"
"size": integer // value in px
"bold": boolean
"italic": boolean
"underline": boolean
"color": "#CFCFCF"
"linkColor": "#CFCFCF"

```

### **Image**

```javascript

{
    "type": "image",
    "src": "https://static.pexels.com/photos/248280/pexels-photo-248280.jpeg",
    "href": "https://www.beefree.io", //optional 
    "alt": "This is a sample image", //optional 
    "dynamicSrc": "http://srcto/dynamic/src" //optional 
}

```

**src** image public URL

**href** Image action URL (link)

**alt** alternate text

**dynamicSrc** when added, the content applies the dynamic image behavior and uses the value as dynamic URL

### **Button**

```javascript

{
  "type": "button",
  "text": "Read more",
  "href": "https://lipsum.com"
},{
  "module": "button",
  "text": "Keep in touch",
  "href": "mailto:growth@beefree.io?subject=Custom content test&body=Sent from a custom button"
}

```

**text** text string that will be displayed as the button content. Must be a plain text string.

If not included, a default text string will be used

**href** button action URL (link)

### **Additional button parameters**

```javascript

"color": "#CFCFCF"
"background-color": "#C2C2C2"

```

### **Divider**

```javascript

{"type":"divider"}

```

Currently there are no additional parameters.

### **HTML**

```json

{"type":"html","html":"<div class=\'our-class\'>This is custom HTML.<\/div>"}

```
