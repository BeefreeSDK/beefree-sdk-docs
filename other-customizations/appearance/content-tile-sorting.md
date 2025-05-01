# Content Tile Sorting

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. Upgrade a [development application](../../getting-started/readme/development-applications.md) at no extra charge to explore features from higher plan tiers. **Note:** Usage on a development application still counts toward [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) and limits.
{% endhint %}

## Re-ordering Content Tiles <a href="#re-ordering-content-tiles" id="re-ordering-content-tiles"></a>

The Content Tile Sorting option allows the host application to change the order of the content tiles in the editor’s sidebar. This allows the host application to display the content blocks that are most important for their users first, and even provide additional visibility for a Custom Addon.

To use this feature, the host application must simply pass in the preferred order inside the configuration passed at initialization, like so:

```javascript

{
  // ...
  defaultModulesOrder: [
    'Button',
    'Html',
    'Icons',
    'Video',
  ],
  // ...
}

```

<figure><img src="../../.gitbook/assets/image-5-e1634835450411 (1).png" alt=""><figcaption></figcaption></figure>

The host application can pass as many or as few content blocks as they want. If only one content tile is specified, then only that content tile will be placed at the top, and the rest of the content tiles will follow the default order.

For Custom/Partner AddOns, the host application passes the “Content Title” value found in the Addon section of the Beefree SDK Console Application Configuration.

## Full List of Content Tiles <a href="#full-list-of-content-tiles" id="full-list-of-content-tiles"></a>

```

1. Heading (Title)
2. Paragraph
3. List
4. Image
5. Button
6. Divider
7. Spacer
8. Social
9. DynamicContent
10. Html
11. Video
12. Form
13. Icons
14. Menu
15. Carousel
16. Text
17. ---- AddOns ----

```
