# Mobile Design Mode

1. [Overview](broken-reference)
2. [Demo](broken-reference)
3. [How to enable Mobile Design Mode](broken-reference)
4. [How it works](broken-reference)
5. [Designing content for Mobile](broken-reference)
6. [Customization options](broken-reference)

### Overview <a href="#overview" id="overview"></a>

Thanks to Mobile Design Mode, your customers can easily design responsive emails,  pages, and popups for mobile without switching between the builder stage and preview mode. When enabled, your customers will be able to:

* Easily switch between desktop and mobile view to access and edit content;
* Edit padding, text alignment, and font size optimized for Mobile;
* Instantly display the results of [**mobile optimization options**](https://dam.beefree.io/hideonmobile) – such as _do not stack/reverse stack/hide on mobile_;
* Extend Beefree SDK’s design flexibility and build mobile-first campaigns.

#### Use cases

* **Mobile-first design**: Start the builder in Mobile view, and let the user switch as needed.
* **Mobile-only editing**: Start the builder in Mobile view, and hide the widget to switch views.
* **Control hidden elements visibility**: Remove the “Visibility” toggle and decide if elements with a “hide on” property can be visible with the blur effect or are not visible during editing.
* **Custom UI controls**: start the builder in a predefined mode and offer your UI controls to switch between views and hidden elements visualization. To do so, you can use the loadStageMode method to trigger a change from your application.

```


bee.loadStageMode({
  type: 'mobile',
  display: 'hide',
})


```

You can also use the loadStageMode method to disable Mobile editing mode.

```


bee.loadStageMode({
  type: 'global',
})


```

### Demo <a href="#demo" id="demo"></a>

Here is a video explaining **why we built Mobile design mode** and how it **enhances the design UX** of Beefree SDK.

[https://docs.beefree.io/wp-content/uploads/2021/03/Introducing-mobile-design-mode.mp4](https://docs.beefree.io/wp-content/uploads/2021/03/Introducing-mobile-design-mode.mp4)

### How to enable Mobile Design Mode <a href="#how-to-enable-mobile-design-mode" id="how-to-enable-mobile-design-mode"></a>

If your application doesn’t have Mobile Design Mode enabled yet, you need to enable it. It takes just a few clicks:

* [Login into developers.beefree.io](https://dam.beefree.io/devmain)
* Select the application you want to configure > Click Details
  * We recommend testing the feature first with a DEV or QA application
* Go to Application Configuration > View More&#x20;
* Go to Services > Toggle Enable mobile design mode ON&#x20;
* Click Save on the top-right corner of the page.
* Congrats! You’ve successfully enabled Mobile Design Mode!

### How it works <a href="#how-it-works" id="how-it-works"></a>

When Mobile Design Mode is enabled for an application at [developers.beefree.io](https://devportal.beefree.io/hc/en-us), the builder will display two new icons in the upper-left corner of the content area, as highlighted below.&#x20;

![the new icons visibile when mobile design mode is active](https://docs.beefree.io/wp-content/uploads/2021/03/new-mobile-design-mode-icons.png)

The _desktop view (screen icon on the left)_ will leverage your browser’s full width.&#x20;

The _mobile view_ (mobile icon on the right) will resize the work area width to 320px to simulate a mobile screen

![Switching between desktop and mobile view](https://docs.beefree.io/wp-content/uploads/2021/03/Going-from-desktop-to-mobile\_450.gif)

#### Mobile optimization settings

Beefree SDK provides settings both for rows and content blocks.&#x20;

To change how content behaves on mobile and create a mobile version of an email, page, or popup:

* Hide on mobile/Hide on desktop (available on developers.beefree.io)
  * A content property to hide a block when displaying the email/page on a specific device.
* Do not stack on mobile (available on developers.beefree.io)
  * When this option is enabled for a row, adjacent columns will not be stacked on mobile devices. The columns will stay side-by-side, as in the desktop view.
* Reverse stacking on mobile (available on developers.beefree.io)
  * When turned on for a row, columns for that row will stack in reverse order, i.e., from the rightmost to the leftmost.

These settings become more accessible with Mobile Design Mode, as users can immediately view the desktop vs. mobile design.

#### Displaying hidden elements

There is an additional setting to preview hidden elements included in a template. With the Hide-on enabled a “Visibility” icon will appear next to the Desktop vs. Mobile stage icons.

![Visibility icon when hiding blocks for mobile/desktop](https://docs.beefree.io/wp-content/uploads/2021/03/visibility-icon.png)

When the Visibility button is ON (default behavior):

* The builder will display content blocks set as hidden for the current device;
* Hidden elements will be blurred out;
* A small icon in the outline of the block will appear whenever hovering with the mouse on the hidden element.

![Button with hide on property applied, blurred.](https://docs.beefree.io/wp-content/uploads/2021/03/hidden-element.png)

When Visibility is OFF:

* Hidden elements won’t be visible in the content area;
* The template will be available as it is;

Here is how the Visibility toggle changes the experience when editing a recent Beefree SDK newsletter.

![Using the visibility icon when editing a newsletter.](https://docs.beefree.io/wp-content/uploads/2021/03/Visibility-icon-in-a-newsletter.gif)

The device preview matches the stage selected when accessing the design preview. This doesn’t apply if you have implemented a custom-built preview.

#### Builder limitations in mobile view

When a user is working in the Mobile stage, the features available are the same as in the desktop stage, with a few exceptions:

* The content area width cannot be scaled – it can only be changed in the desktop view;
* Users can add or delete columns within a row, but they won’t be able to resize them.

### Designing content for Mobile <a href="#designing-content-for-mobile" id="designing-content-for-mobile"></a>

When designing content for Mobile, users may require more flexibility in the way they arrange or format elements to fit a smaller screen.&#x20;

Thanks to the latest Mobile Design Mode updates, users can now control individual elements straight from the mobile stage without the need to duplicate them.&#x20;

Users can optimize the design of the following content properties by switching to the Mobile Design Stage:

* Padding
* Alignment
* Font size

It is now possible to style these elements for Mobile or Desktop.&#x20;

These three mobile-optimized properties are available for the following content type modules:

* Title
* Paragraph&#x20;
* List
* Form
* Icons
* Menu
* Button

To edit a specific parameter for mobile, users must switch to the Mobile stage and select the content element they want to edit.&#x20;

They will find the Mobile-optimized properties in the sidebar menu, under the “Content Properties” tab.

Mobile-optimized elements are flagged with a clickable “Mobile” pill, as shown in the image below:

#### ![](https://docs.beefree.io/wp-content/uploads/2022/07/Screenshot-2022-07-04-at-15.35.39.png)

When the pill is highlighted in light blue, it means the property has been edited and applied in the mobile stage. The mobile pill can be styled using [Custom CSS](https://docs.beefree.io/custom-css/) if covered by your [subscription plan](https://beefree.io/bee-plugin/pricing/).

#### ![](https://docs.beefree.io/wp-content/uploads/2022/07/Screenshot-2022-07-04-at-15.34.30.png)

Users can click on the x to revert the property back to the desktop.

#### Editing Font Size on Mobile

We have also improved the user experience by moving the Font Size Controls, previously displayed in the formatting tiny menu available in the content area, to the Content Properties Tab in the sidebar menu.

#### ![](https://docs.beefree.io/wp-content/uploads/2022/07/Screenshot-2022-07-04-at-16.47.57.png)

#### ![](https://docs.beefree.io/wp-content/uploads/2022/07/Screenshot-2022-07-04-at-15.35.39.png)

#### Tracking changes in the history

All the edits performed in the Mobile Stage are tracked and flagged in the history as _(Mobile)_ edits.

![](https://docs.beefree.io/wp-content/uploads/2022/07/Screenshot-2022-07-04-at-11.15.20.png)

### Customization options <a href="#customization-options" id="customization-options"></a>

Mobile Design Mode can be considered a “plug-and-play” feature because it just needs to be enabled on the [Beefree SDK Console](http://developers.beefree.io/) and can be used by your users out of the box.

If you want to customize the user experience, Beefree SDK allows you to configure a few client-side options to control permissions and styles. Take a look at the code snippet below to see how to load these settings into the initial configuration as part of the workspace section.

```


workspace: {
  type: 'default', // default, mixed, amp_only, html_only
  stage: 'desktop', // desktop, mobile, global
  displayHidden: 'blur', // blur, hide
  hideStageToggle: true, // default = false
}


```

Here is a brief description of the parameters and their options. They are all optional.

| Parameter           | Description                                                                                                                                          | Values                                | Default                                  |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- | ---------------------------------------- |
| **type**            | loads different workspace types (currently used to handle [AMP content visibility](https://docs.beefree.io/amp-carousel/#using-workspaces-for-amp)). | default, mixed, amp\_only, html\_only | `default`                                |
| **stage**           | Define if the builder starts in desktop view, mobile view, or global (i.e. without desktop/mobile views.)                                            | desktop, mobile, global               | inherits Developer account configuration |
| **displayHidden**   | if defined, hidden elements will behave based on the parameter value.                                                                                | blur, hide                            | `blur`                                   |
| **hideStageToggle** | if true, the mobile/desktop icons to switch view are not visible                                                                                     | true, false                           | `false`                                  |
