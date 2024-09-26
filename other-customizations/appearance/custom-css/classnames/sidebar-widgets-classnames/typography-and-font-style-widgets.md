# Typography and Font Style Widgets

## Overview

This page covers the classnames used for managing typography and font styles in your application. These widgets allow you to control the appearance of text, including font size, alignment, weight, line height, and more. Typography is essential for creating a readable and visually appealing user interface. Below, you will find detailed information on each widget’s classnames, including deprecated versions (if applicable) and current classnames to ensure your application remains up-to-date.

### 1. Font Style

**Description:** The font style widget allows you to control the appearance of text, including font weight, style (italic, normal), and decoration (underline, strike-through). It is commonly used for headings, paragraphs, and other text elements.

**Deprecated Classnames:**

* tgl-container
* item\_1-2

**New Classnames:**

* multi-toggle--cs
* multi-toggle-btns--cs

**Sample CSS:**

```css
.multi-toggle--cs {
    font-style: normal;
}

.multi-toggle-btns--cs {
    font-weight: 700;
}

.font-style-italic {
    font-style: italic;
}
```

**Sample HTML:**

```html
<p class="multi-toggle--cs multi-toggle-btns--cs">This is bold text.</p>
<p class="multi-toggle--cs font-style-italic">This is italic text.</p>
```

### 2. Text Alignment

**Description:** The text alignment widget controls the horizontal alignment of text within its container, including options for left, right, center, and justified alignment.

**Deprecated Classnames:**

* item\_1-2

**New Classnames:**

* text-align-left--cs
* text-align-center--cs
* text-align-right--cs
* text-align-justify--cs

**Sample CSS:**

```css
.text-align-left--cs {
    text-align: left;
}

.text-align-center--cs {
    text-align: center;
}

.text-align-right--cs {
    text-align: right;
}

.text-align-justify--cs {
    text-align: justify;
}
```

**Sample HTML:**

```html
<p class="text-align-left--cs">Left aligned text.</p>
<p class="text-align-center--cs">Center aligned text.</p>
<p class="text-align-right--cs">Right aligned text.</p>
<p class="text-align-justify--cs">Justified text that stretches across the width of the container.</p>
```

### 3. Line Height

**Description:** The line height widget controls the space between lines of text, improving readability or adjusting text for different designs. It is commonly used in paragraphs and headings.

**Deprecated Classnames:**

* item\_1-2

**New Classnames:**

* line-height-1--cs
* line-height-1-5--cs
* line-height-2--cs

**Sample CSS:**

```css
.line-height-1--cs {
    line-height: 1;
}

.line-height-1-5--cs {
    line-height: 1.5;
}

.line-height-2--cs {
    line-height: 2;
}
```

**Sample HTML:**

```html
<p class="line-height-1--cs">This text has a line height of 1.</p>
<p class="line-height-1-5--cs">This text has a line height of 1.5.</p>
<p class="line-height-2--cs">This text has a line height of 2.</p>
```

### 4. Font Size

**Description:** The font size widget controls the size of text. This is a crucial aspect of typography, affecting readability and the visual hierarchy of your content.

**Deprecated Classnames:**

* item\_1-2

**New Classnames:**

* font-size-sm--cs
* font-size-md--cs
* font-size-lg--cs
* font-size-xl--cs

**Sample CSS:**

```css
.font-size-sm--cs {
    font-size: 12px;
}

.font-size-md--cs {
    font-size: 16px;
}

.font-size-lg--cs {
    font-size: 18px;
}

.font-size-xl--cs {
    font-size: 24px;
}
```

**Sample HTML:**

```html
<p class="font-size-sm--cs">Small text</p>
<p class="font-size-md--cs">Medium text</p>
<p class="font-size-lg--cs">Large text</p>
<p class="font-size-xl--cs">Extra large text</p>
```

### 5. Letter Spacing

**Description:** The letter spacing widget allows you to control the spacing between characters in text. It is often used for headings or special text elements to create a unique design.

**Deprecated Classnames:**

* item\_1-2

**New Classnames:**

* letter-spacing-sm--cs
* letter-spacing-md--cs
* letter-spacing-lg--cs

**Sample CSS:**

```css
.letter-spacing-sm--cs {
    letter-spacing: 0.5px;
}

.letter-spacing-md--cs {
    letter-spacing: 1px;
}

.letter-spacing-lg--cs {
    letter-spacing: 2px;
}
```

**Sample HTML:**

```html
<p class="letter-spacing-sm--cs">This text has small letter spacing.</p>
<p class="letter-spacing-md--cs">This text has medium letter spacing.</p>
<p class="letter-spacing-lg--cs">This text has large letter spacing.</p>
```

### 6. Text Decoration

**Description:** The text decoration widget allows you to add or remove decorative elements like underlines, strike-throughs, or overlines to text elements.

**Deprecated Classnames:**

* item\_1-2

**New Classnames:**

* text-decoration-underline--cs
* text-decoration-line-through--cs
* text-decoration-none--cs

**Sample CSS:**

```css
.text-decoration-underline--cs {
    text-decoration: underline;
}

.text-decoration-line-through--cs {
    text-decoration: line-through;
}

.text-decoration-none--cs {
    text-decoration: none;
}
```

**Sample HTML:**

```html
<p class="text-decoration-underline--cs">This text is underlined.</p>
<p class="text-decoration-line-through--cs">This text has a line through it.</p>
<p class="text-decoration-none--cs">This text has no decoration.</p>
```

### 7. Font Weight

**Description:** The font weight widget adjusts the thickness or boldness of text, allowing you to emphasize certain parts of your content, such as headings or important information.

**Deprecated Classnames:**

* item\_1-2

**New Classnames:**

* font-weight-bold--cs
* font-weight-normal--cs
* font-weight-light--cs

**Sample CSS:**

```css
.font-weight-light--cs {
    font-weight: 300;
}

.font-weight-normal--cs {
    font-weight: 400;
}

.font-weight-bold--cs {
    font-weight: 700;
}
```

**Sample HTML:**

```html
<p class="font-weight-light--cs">This text is light.</p>
<p class="font-weight-normal--cs">This text is normal weight.</p>
<p class="font-weight-bold--cs">This text is bold.</p>
```

### 8. Text Transform

**Description:** The text transform widget allows you to control the capitalization of text, converting it to uppercase, lowercase, or capitalized (first letter uppercase).

**Deprecated Classnames:**

* item\_1-2

**New Classnames:**

* text-transform-uppercase--cs
* text-transform-lowercase--cs
* text-transform-capitalize--cs

**Sample CSS:**

```css
.text-transform-uppercase--cs {
    text-transform: uppercase;
}

.text-transform-lowercase--cs {
    text-transform: lowercase;
}

.text-transform-capitalize--cs {
    text-transform: capitalize;
}
```

**Sample HTML:**

```html
<p class="text-transform-uppercase--cs">THIS TEXT IS UPPERCASE.</p>
<p class="text-transform-lowercase--cs">this text is lowercase.</p>
<p class="text-transform-capitalize--cs">This Text Is Capitalized.</p>
```

This page consolidates all classnames related to typography and font styling. For deprecated classnames, make sure to transition to the new ones.

For more detailed implementation on how to customize form and input widgets, refer to the [Customizing Sidebar Widgets](./#customizing-sidebar-widgets) section on the [Sidebar Widgets Classnames page](./).
