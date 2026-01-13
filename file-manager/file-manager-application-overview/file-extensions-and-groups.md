# Mime Types and Groups

MIME types are a standardized way to indicate the nature and format of a file, specifying what kind of data it contains. Groups are categories that aggregate these MIME types for simplified handling and management in applications like File manager. This organization allows for custom limitations and processing based on file type.

The following list shows which specific mime types are mapped to our group names for custom limitations on File manager.

```
image:
    image/*
text:
    text/*
video:
    video/*
audio:
    audio/*
office:
    application/msword
    application/vnd.lotus-organize,
    application/vnd.ms-*
    application/vnd.oasis.opendocument*
    application/vnd.openxmlformats-*
    application/rtf
xml:
    application/xml
zip:
    application/zip
epub:
    application/epub+zip
pdf:
    application/pdf
postscript:
    application/postscript
font:
    application/x-font-otf
    application/x-font-ttf
```

{% hint style="warning" %}
**Note:** Beefree SDK does not manage heic files at this time.
{% endhint %}

By default, newly created applications of both free and paid plans only allow the upload of image, video and PDF file types. If you are on a paid plan and want to allow more file types, you have to enable them in the SDK Console. [More info here](https://docs.beefree.io/beefree-sdk/server-side-configurations/server-side-options/privacy-and-security#file-type-limitations).

Please also note that the system altogether prevents the upload of potentially harmful file extensions such as exe, msi, bat, iso, jar, apk, SVGs containing JavaScript, HTML with redirects and more.

## Additional Considerations

When working with files, mime types and groups, ensure you consider the following:

* The default maximum file size you can upload is 20MB.
* If you upload an image wider than 1920 pixels, when the image is uploaded or imported, it will be resized to fit within 1920px. This may cause issues with the image's appearance, including colors that change and GIFs that lose frames. Ensure your images are no wider than 1920px to avoid these issues.

Learn more about [how to activate custom limitations for the File manager](../../server-side-configurations/server-side-options/services-options/#activate-custom-limitations-on-file-manager).
