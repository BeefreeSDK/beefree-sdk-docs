# Custom Sidebar Position

This feature is available on Beefree SDK[paid plans](https://dam.beefree.io/pluginpricing) only.

#### Overview <a href="#overview" id="overview"></a>

You can choose whether to display the builder sidebar on the left or on the right side of the screen.

Available positions:

* left
* right

Here is the same sample application, with the same template and same content element selected, and the sidebar displayed on the left…

![BEE editor with sidebar on the left](https://docs.beefree.io/wp-content/uploads/2019/11/BEE-v3-sidebar-position-left.png)

… and on the right.

![BEE editor with sidebar on the right](https://docs.beefree.io/wp-content/uploads/2019/11/BEE-v3-sidebar-position-right.png)

The configuration document needs the following, new parameter:

```


var beeConfig = {
        uid: config.uid,
        sidebarPosition: 'right',
        ...  


```
