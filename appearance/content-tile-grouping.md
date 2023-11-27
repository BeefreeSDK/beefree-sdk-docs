# Content Tile Grouping

{% hint style="info" %}
This feature is available on Beefree SDK [Superpowers plan](https://dam.beefree.io/pluginpricing) and above. If you're on the Core or Essentials plan, [upgrade a development application](../getting-started/development-applications.md) for free to try this and other Superpowers-level features.
{% endhint %}

### Grouping Content Tiles <a href="#grouping-content-tiles" id="grouping-content-tiles"></a>

The Content Tile Grouping option allows the host application to group content tiles in the editor’s sidebar. This allows the host application to display the content blocks into distinct groups.

Content Tile Grouping supports:

* Text labels
* Special Characters
* Emojis

{% hint style="info" %}
Please note that emoji support may be determined by the OS or browsers used. Some browsers do not support, or may display emojis incorrectly.
{% endhint %}

To display custom groups, the application must pass the groups settings in the configuration at initialization, like so:

```javascript

modulesGroups: [
  {
    label: "Text ✏️",
    collapsable: false,
    collapsedOnLoad: false,
    modulesNames: [
      "List",
      "Paragraph",
      "Heading"
    ]
  },
  {
    label: "Media",
    collapsable: true,
    collapsedOnLoad: false,
    modulesNames: [
      "Video",
      "Image"
    ]
  },
  {
    label: "AddOns",
    collapsable: true,
    collapsedOnLoad: true,
    modulesNames: [
      "Stickers",
      "Gifs"
    ]
  }
]

```

![](https://docs.beefree.io/wp-content/uploads/2022/09/Screenshot-2022-09-29-at-12.40.43.png)

Custom groups can be collapsed and opened by default by changing the `collapsable` and `collapsedOnLoad` values.\
Ungrouped tiles will be gathered at the bottom of the list under a group with no label.

Duplicated tiles are not allowed, e.g., you can’t have a tile twice in the sidebar.\
An `onWarning` notification is triggered whenever an unknown tile is added to the configuration.

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

If you want to organize or include AddOns, and Custom AddOns under a custom group, mention the name used in the Beefree SDK Console.

Please note, the AddOn needs to be enabled to appear in the sidebar.

![](https://docs.beefree.io/wp-content/uploads/2022/09/Screenshot-2022-09-29-at-13.56.41.png)
