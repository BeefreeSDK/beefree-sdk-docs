# Content options

In this box, you can enable additional content blocks that will appear in the Content panel inside the editor.

![](https://docs.beefree.io/wp-content/uploads/2022/08/new\_content\_options-300x70.png)

Currently, you can manage these content blocks:

| Block         | Description                                                                                                                     | Availability              | User guide                                        |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------- | ------------------------------------------------- |
| **HTML**      | Allows your users to include their own HTML code                                                                                | Paid plans only           | [More info](https://dam.beefree.io/htmlcontent)   |
| **Menu**      | Allows users to create simple, text-based navigation elements                                                                   | All plans, including free | [More info](https://dam.beefree.io/menucontent)   |
| **Title**     | Allows users to add text with H1,H2,H3 tags, for email and web accessibility, and for SEO on web pages.                         | All plans, including free | [More info](https://dam.beefree.io/titlecontent)  |
| **List**      | Allows users to create easy numbered and bullet lists with Paragraph’s upgrades and list type, spacing, and identation support. | All plans, including free | [More info](https://dam.beefree.io/newtextblocks) |
| **Paragraph** | Allows users to write text with support for multiple font weights, copy/paste support, easier reformatting, and more.           | All plans, including free | [More info](https://dam.beefree.io/newtextblocks) |
| **Text**      | Legacy text block. Please refer to title, paragraph and list.                                                                   | All plans, including free | [More info](https://dam.beefree.io/textcontent)   |
| **Video**     | Helps users include a visual link to video content                                                                              | Paid plans only           | [More info](https://dam.beefree.io/videocontent)  |
| **Icons**     | Enables users to create icon-based layouts, such as _star ratings, bullet lists, properties_                                    | All plans, including free | [More info](https://dam.beefree.io/iconcontent)   |
| **Spacer**    | Allows users to add a space between content                                                                                     | All plans, including free | [More info](https://dam.beefree.io/spacer)        |

**Content options in Page Builder**

If you’re configuring a Page Builder application, there are a few differences in what these blocks allow:

* the **HTML Block** also allows **script and iframe tags;**
* the **Video block** allows for video playback, either embedding a YouTube, YouTube Shorts, or Vimeo video or pointing to a hosted video ([read more](../page-builder/embedding-videos-in-a-page.md)). Supported video formats are:
  * YouTube (16:9 aspect ratio)
    * Public Videos
    * Unlisted Videos
    * Videos starting at a certain time
  * YouTube Shorts (16:9 aspect ratio)
  * Vimeo
    * Public Videos
    * Unlisted Videos
    * Cinemascope (21:9 aspect ratio)
* the **Menu block** allows menu items to be set as “internal links,” pointing to any content block in the page that is configured as a “block identifier.”

There is also an additional option for turning on the **Form block**.

![](https://docs.beefree.io/wp-content/uploads/2020/06/Enable-form.png)

Please note that you need to implement one of the two methods indicated in this article for the Form tile to appear in the Content tab of the editor:

* The [default form](../form-block/integrating-and-using-the-form-block/passing-forms-to-the-builder.md) method is available for all plans, including free
* The [content dialog](../advanced-options/content-dialog.md) method is available for paid plans only.

#### AMP Content <a href="#amp-content" id="amp-content"></a>

In this section, you can enable AMP blocks that will be available in the “Content” tab of the Email Builder.

![](https://docs.beefree.io/wp-content/uploads/2020/10/Dev-Portal-AMP-toggle.png)

We currently provide an [AMP Carousel](../amp-for-email.md) content block. After enabling the toggle, you will need to configure an [AMP-compatible workspace](../amp-for-email.md).

Please note that AMP content is not available for Page Builder.
