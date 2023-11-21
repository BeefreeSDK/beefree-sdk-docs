# Content Tile Sorting

1. [Re-ordering Content Tiles](broken-reference)
2. [Full List of Content Tiles](broken-reference)

### Re-ordering Content Tiles <a href="#re-ordering-content-tiles" id="re-ordering-content-tiles"></a>

The Content Tile Sorting option allows the host application to change the order of the content tiles in the editor’s sidebar. This allows the host application to display the content blocks that are most important for their users first, and even provide additional visibility for a Custom Addon.

To use this feature, the host application must simply pass in the preferred order inside the configuration passed at initialization, like so:

```


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

![](https://docs.beefree.io/wp-content/uploads/2021/10/image-5-e1634835450411.png)

The host application can pass as many or as few content blocks as they want. If only one content tile is specified, then only that content tile will be placed at the top, and the rest of the content tiles will follow the default order.

For Custom/Partner Addons, the host application passes the “Content Title” value found in the Addon section of the Beefree SDK Console Application Configuration.

### Full List of Content Tiles <a href="#full-list-of-content-tiles" id="full-list-of-content-tiles"></a>

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
