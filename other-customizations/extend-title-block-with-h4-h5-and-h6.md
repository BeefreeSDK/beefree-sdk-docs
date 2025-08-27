# Extend Title Block with H4, H5, and H6

{% hint style="info" %}
Available on all Beefree SDK builder and [plans](https://developers.beefree.io/pricing-plans).
{% endhint %}

## Overview

The Title Block supports H4, H5, and H6 headers in addition to the existing H1–H3 options. This enhancement gives end users more flexibility to structure content with proper semantic hierarchy, improving both accessibility and readability.

## How to Activate the Feature

By default, the builder's [Title Block ](https://docs.beefree.io/end-user-guide/content-blocks/titles)will display only H1–H3. To enable additional heading levels, you need to add the `titleMaxLevel` parameter to your configuration. Ensure you set it to the maximum value you'd like to make available in the builder. For example, `h6` will allow your end users to select H1, H2, H3, H4, H5, or H6 from the drop down menu within the Title Block.

Example configuration:

```js
beeConfig: {
  titleDefaultConfig: {...},
  titleDefaultStyles: {...},
  titleMaxLevel: 'h6' // 'h3' default (min 'h1', max 'h6')
}
```

* If not set, the default value is **h3**.
* You can allow up to a specific level (for example, `h4`) or all the way to `h6`.

Here’s what the editor experience looks like if `titleMaxLevel` is set to **h4**:

<figure><img src="../.gitbook/assets/CleanShot 2025-08-19 at 19.22.33@2x.png" alt=""><figcaption></figcaption></figure>

## Default Styles for H4–H6

Just like H1–H3, you can define [Content Default](appearance/content-defaults.md#content-defaults-for-additional-title-levels) styles for H4–H6 under `titleDefaultStyles`:

```js
beeConfig: {
  titleDefaultStyles: {
    h4: {
      color: 'red',
      'font-size': '13px',
      'font-family': 'Arial, sans-serif',
      'font-weight': '700',
      'link-color': 'blue',
      'line-height': '120%',
      'text-align': 'center',
      'direction': 'ltr',
      'letter-spacing': 0,
    },
    h5: {
      color: 'black',
      'font-size': '12px',
      'font-family': 'Arial, sans-serif',
      'font-weight': '700',
      'link-color': 'blue',
      'line-height': '120%',
      'text-align': 'center',
      'direction': 'ltr',
      'letter-spacing': 0,
    },
    h6: {...}
  },
}
```

## Additional Considerations

Consider the following when adding header options:

* **Granularity**: This configuration allows enabling headings per UID, giving you control over which end users see them.
* **Customizability**: You can define distinct styling for each heading level to match brand guidelines using [Content Defaults](appearance/content-defaults.md#content-defaults-for-additional-title-levels).
