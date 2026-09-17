# Advanced Image Layout

### Overview

Advanced Image Layout enables additional size and aspect ratio controls for the Image block. In addition to the proportional scaling of images, your end-users are able to:

* Crop images to exact aspect ratios (Square, Portrait, Standard, Wide, Banner)
* Choose whether an image should fit entirely inside its frame or fill the frame edge-to-edge
* Set a focal point so cropped images stay centered on what matters

Nothing changes for your existing emails or pages. These are additive controls: any image you've already placed keeps rendering exactly as it does today until you actively change its settings.

### Why it matters

Advanced Image Layout’s additional options offer more **granular layout styling capabilities** for end users. For instance, the presets are useful for ensuring alignment in rows with multiple side-by-side images – as it happens with product recommendation emails.&#x20;

Another significant advantage is client compatibility. Advanced Image Layout Controls generates an actual new image behind the scenes for each transformation (instead of CSS cropping), which is what for instance guarantees the result renders correctly in Outlook.

Advanced Image Layout is also **efficient by design** as it doesn't create extra files to manage. Instead of saving a new asset to the File Manager for every crop or ratio your end users try, the transformation is generated on demand from the original image and cached automatically. In this way the  file library stays clean no matter how many variations your end-users test. And since settings, not files, are what carry over, swapping the source image on an existing block automatically reapplies the same ratio, fit/fill, and focal point — no need for your end users to redo the layout work.

### Availability

Advanced Image Layout is available for Email, Landing Page and Popup builders.&#x20;

You can activate Advanced Image Layout with the dedicated flag in the SDK Console. By default, the toggle is on for newly created applications.

<img src="../.gitbook/assets/unknown (4).png" alt="" height="196" width="594">

For detailed information about the infrastructure options and configuration, please refer to the section below.

### Sizing options

Once your end-users deselect “Auto width” in the image sidebar, they are presented with two sizing modes to choose.

#### Original

The image keeps its native proportions — no cropping, no fit/fill choice. This is the default for any image that hasn't been resized before, and it's the only mode compatible with Dynamic Images (see below).

#### Presets

Your end-users can crop the image by choosing from five standard ratios – Square (1:1), Portrait (4:5), Standard (4:3), Wide (16:9), Banner (2:1)

<img src="../.gitbook/assets/unknown (5).png" alt="" height="335" width="338">

With a preset selected, your users can also choose **Fit** or **Fill**. The former scales the image so it's fully visible inside the frame, without cropping anything out; the latter scales the image so it completely covers the frame, cropping any excess. Fill is the default the first time you select a preset.

When Fill is selected, a 9-point grid lets you choose which part of the image stays in frame when it's cropped — useful when the subject isn't centered in the original photo.&#x20;

<img src="../.gitbook/assets/unknown (6).png" alt="" height="268" width="646">

If your end-users remove an image and add a new one in its place, existing layout settings — ratio, fit/fill, focal point, alignment — carry over automatically.

#### Mobile

Sizing and cropping settings are shared between desktop and mobile, with one dedicated mobile option: **Full width on mobile**, available for both Original and every preset.

Mobile images are regenerated from the original file, so they stay sharp on retina screens instead of looking blurry. When Full width on mobile is on, the separate mobile-width slider is disabled, since it wouldn't have any visible effect.

#### Working with Dynamic Images

[Dynamic Images](https://docs.beefree.io/beefree-sdk/resources/cookbook/use-dynamic-images-for-email-personalization) only work with the **Original** ratio. The reason is that the real image's dimensions aren't known until the merge tag is resolved, so forcing it into a fixed preset ratio ahead of time could distort or stretch the final image.

#### Supported file types

JPEG, PNG, GIF and WebP are supported and tested. Animated GIFs are capped at 100 frames.

### Advanced Permissions

Advanced Permissions let you control which Image block settings your end-users can see or change. For example, you can hide the entire Advanced Image Layout block from a given user role.

Advanced Image Layout’s controls don't get permissions of their own. They're governed by the existing `ImageWidth` permission, which today controls show/lock behavior for the original width slider.

### What happens when Advanced Image Layout is unavailable

Once an image has been edited with Advanced Settings, the controls stay visible and fully usable in the sidebar for end-users, even after the feature is disabled in the SDK console or restricted via Advanced Permissions.

A common use case entails the [Template Catalog](https://docs.beefree.io/beefree-sdk/apis/template-catalog-api#overview-of-template-catalog-api): if a designer builds a template using Advanced Image Layout and distributes it via the Template Catalog, any user downloading it - even with the feature disabled - will be able to use the Advanced controls on that specific image.

If the ratio is switched back to **Original**, the underlying settings aren't deleted — they're cleared, but a flag (invisible to the end-user) stays in place recording that this specific image was edited with Advanced Settings at some point. That flag is what keeps the controls recoverable.

### Cost & data allotment

Every export generates a fresh, signed transform URL for whichever CDN is configured at that moment — nothing is created or stored per image in advance. This has two consequences: first, switching your CDN setting affects every export from that point forward, including re-exports of existing templates. Re-export a template after switching CDN, and it picks up fresh URLs on the new CDN — the template itself isn't locked to whatever CDN was active when it was first built.

Secondly, already-sent emails **keep the URLs they were exported with**. Signed URLs never expire, so an email exported while Beefree SDK's CDN was configured keeps counting toward your data allotment indefinitely — even after you disable the feature or switch to a custom CDN. There's no way to retroactively move or re-serve a URL that's already gone out.

Whether a given export counts toward your allotment also depends on the image's aspect ratio setting at export time:

* If you're on **custom storage** and haven't configured a dedicated CDN route for Advanced Image Layout, exporting with Original selected (instead of a preset) uses the image's original URL, keeping it on your own CDN instead of Beefree's.
* If you're on **default** (Beefree-hosted) **storage**, none of this changes your CDN costs — you're billed for CDN traffic the same way whether or not Advanced Image Layout is active. The ratio distinction above only matters for custom storage.

{% hint style="info" %}
**Existing images keep their capabilities**: Image blocks already edited with Advanced Image Layout keep their layout controls and keep counting toward your data allotment — served by Beefree SDK's CDN — until an end-user removes them. This applies whether the feature was later disabled in the console, or a template containing these images is opened without the feature enabled and the related custom CDN settings configured.
{% endhint %}

### Image sidebar update

With the release of Advanced Image Layout (Beefree SDK 3.56), we took the chance to improve the Image block sidebar for all end users, regardless of Advance Image Layout’s activation. It now follows a natural, top-to-bottom flow that mirrors how users actually build:

1. **Image Source** — add or replace the image. This is the entry point: it's what unlocks the widgets below.
2. **Dynamic Image** — the alternate, merge-tag-driven source, positioned right under Image Source since it replaces the placeholder set there.
3. **Image Dimension** — sizing, ratio, fit, and crop controls, grouped together as the final step.

| Old                                                                        | New                                                                        |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| <img src="../.gitbook/assets/unknown (7).png" alt="" data-size="original"> | <img src="../.gitbook/assets/unknown (8).png" alt="" data-size="original"> |

A couple of small naming changes come along with this: Choose image has been replaced with Add Image; Change image is now Replace.

Two things stand out with the new order. Image Source now stays right at the top, no matter how many sizing options Image Dimension grows to include. Placing Dynamic Image right next to the aspect-ratio control makes the relationship between the two immediately visible.

This Image sidebar improvement ships for every builder, regardless of whether you activated Advanced Image Layout.

### CDN Configuration

Advanced Image Layout produces a real image file for each transformation, and that file has to be hosted somewhere it can be loaded from when the email, landing page, or popup is opened.

If Beefree SDK [stores and serves your images](http://docs.beefree.io/beefree-sdk/file-manager/cdn-domains), transformed images are delivered from the same segmented CDN domain that already serves the rest of your assets. There's nothing to configure and no new domains to allowlist. If you're unsure whether you're on a custom CDN, open your application in the [Developer Console](https://developers.beefree.io/login), go to Configure Application > Storage options, and check the CDN domains listed there. If you see “Use the default storage” option selected then there’s nothing additional you need to configure.

{% hint style="info" %}
**How usage is tracked**

If you've set up your own CDN, every cache miss triggers a call to Beefree SDK's Content Services API, which counts toward your data allotment. Subsequent renders of the same image are served from your CDN's cache and don't generate additional calls, which is why caching correctly (see [Caching is an operating requirement](advanced-image-layout.md#caching-is-an-operating-requirement) below) keeps your usage proportional to unique images rather than total opens. If you're on default (Beefree-hosted) storage, this tracking doesn't apply — the equivalent lookup happens entirely within Beefree SDK's own infrastructure.
{% endhint %}

### Who needs this

You need to configure a transform route if you use custom storage and serve those images from your own CDN. Custom storage covers three options, and the route is required for all of them: [a custom S3 bucket or custom File System Provider](https://docs.beefree.io/beefree-sdk/server-side-configurations/server-side-options/storage-options) or a [custom File Picker](https://docs.beefree.io/beefree-sdk/other-customizations/advanced-options/custom-file-picker#a-basic-example). Beefree SDK can't serve transformed images from infrastructure it doesn't own, so without this route there's nowhere for the transformed image to come from.

See [Storage options](https://docs.beefree.io/beefree-sdk/server-side-configurations/server-side-options/storage-options) if you're not sure which storage your application uses.

You have two other options if you'd rather not configure a CDN:

* Route through Beefree SDK's CDN. Available on opt-in for custom storage. Your transformed images are then served from Beefree SDK infrastructure rather than your own, which matters if you chose custom storage for data-residency or compliance reasons.
* Don't enable Advanced Image Layout. Your end users stay on Original sizing, which is today's proportional-scaling behavior. Crop, fit, fill, and focal point options won’t be available.

There's no automatic fallback. Beefree SDK won't serve your transformed images without your explicit opt-in, so if you don't configure the route, your end users won't get the Advanced Image Layout controls.

### How it works

With Advanced Image Layout enabled, exported HTML embeds signed image URLs pointing at Beefree SDK's CDN. Once you set a base URL and path prefix in the Developer Console, those URLs point at your domain instead:

```html
https://<your-domain>/<your-prefix>/<signature>/<payload>/<filename>
```

Your CDN forwards cache misses to the Content Services API (CSAPI), authenticated with your own CSAPI key. CSAPI verifies the signature, unpacks the URL, fetches the original image from its source URL, and returns the transformed result. Beefree SDK sends `Cache-Control: public, max-age=86400`, so a CDN that honors the origin caches each image for up to a day.

Three properties are worth understanding before you configure anything:

* **URLs are content-addressed and deterministic**. The same template always mints the same URL, and any edit produces a new one. You never need to invalidate your cache.
* **Only the first request for a given URL reaches Beefree SDK**. Everything after that is served from your cache until the entry expires.
* **Nothing is persisted on the Beefree SDK side**. The transform runs in memory, then transformed images live only in your CDN cache, under your own retention policy.

The URL keeps the original filename as its last segment, so a recipient who saves the image gets it under a recognizable name rather than an opaque hash.

Order is critical when making these changes. First you’ll need to create the API key, then configure the CDN, and finally change the Developer Console setting. The Console switch takes effect immediately in the editor, so leave it until your CDN is answering correctly.

{% hint style="warning" %}
Nothing enforces this order server-side. If you configure the Console before your CDN answers correctly, every export from that moment embeds image URLs on a host that can't serve them, and recipients see broken images in any template using Advanced Image Layout. Validate the full setup on a development application first, then apply the same configuration to production.
{% endhint %}

#### Step 1: Create a Content Services API key

In the Developer Console, open your application, go to the **Content Services API section**, and create an API key or use an existing one.

Treat the key as a server-side credential. It belongs in your CDN's origin configuration and nowhere else. Never put it in frontend code or anywhere the browser can read it.

#### Step 2: Configure your CDN

Any vendor works, and the requirements are the same across all of them. The following table lists what your CDN needs to do.

<table><thead><tr><th width="74.39996337890625">#</th><th>Requirement</th><th>Value</th></tr></thead><tbody><tr><td>1</td><td>Serve your chosen hostname over HTTPS</td><td>For example <code>images.example.com</code>, with a valid TLS certificate</td></tr><tr><td>2</td><td>Route the prefix to the Beefree SDK origin</td><td><code>/&#x3C;your-prefix>/*</code> → <code>api.getbee.io</code></td></tr><tr><td>3</td><td>Prepend the origin base path</td><td>Origin path <code>/v1/transform</code>. CDNs prepend rather than rewrite, and the endpoint ignores the prefix segment in between, so you don't need rewrite rules</td></tr><tr><td>4</td><td>Add the auth header on origin requests</td><td><code>Authorization: Bearer &#x3C;your-api-key></code>, set as an origin or custom header</td></tr><tr><td>5</td><td>Cache, honoring the origin <code>Cache-Control</code></td><td>Successful responses carry <code>Cache-Control: public, max-age=86400</code>. Error responses are <code>no-store</code> and must not be cached.</td></tr></tbody></table>

Allow GET and HEAD only, and leave compression on. Most CDNs default to both of these options already. Your prefix can be a single segment such as `edited-images` or a nested path such as `images/edited/`. Leading and trailing slashes are normalized, so no need to match the Console field exactly.

#### AWS CloudFront example

To configure CloudFront, take the following steps:

1. **Add an alternate domain name**. Add `images.example.com` as a CNAME along with an ACM certificate, then point DNS at the distribution.
2. **Create a dedicated origin**. Set the domain to `api.getbee.io`, the origin path to `/v1/transform`, and the protocol to HTTPS only. Add a custom header `Authorization` with the value `Bearer <your-api-key>`.
3. **Add a cache behavior**. Use the path pattern `/<your-prefix>/*`, which must match the prefix you'll set in the Console. Select the origin from step 2, redirect HTTP to HTTPS, allow GET and HEAD, turn compression on, and respect the origin `Cache-Control`. Confirm the behavior points at the new origin, because duplicated behaviors tend to keep the old one.
4. **Deploy and test** before you change anything in the Console. See Verifying your setup.

Azure Front Door and Google Cloud CDN use the same concepts under different names.

#### Step 3: Configure the Developer Console

Open application settings, go to **Advanced Image Layout**, and select **Served by your own infrastructure**. Two fields need values:

<img src="../.gitbook/assets/unknown (11).png" alt="" height="196" width="594">

<img src="../.gitbook/assets/CustomFontModalURL (1).png" alt="" width="459">



* **Base url** is your hostname, for example `https://images.example.com`. HTTPS is required.
* **Path prefix** is the prefix you routed, for example `edited-images`. Slashes around it are normalized either way.

The change takes effect immediately in the editor, for both preview and editor-side export. HTML exports through the Content Services API pick it up within one hour, because the API caches each application's serving configuration for that long. Switching back to Beefree SDK's CDN behaves the same way.

### Caching is an operating requirement

{% hint style="warning" %}
**Important:** Your CDN must cache transformed images. `/v1/transform` is rate-limited per application because it's an API entry point, not a content-delivery service. Cached correctly, the limit never comes into play, since each unique URL reaches Beefree SDK at most once a day. Uncached, every email open goes straight to the API, exhausts the limit, and recipients see broken images.&#x20;
{% endhint %}

### Verifying your setup

You can test your CDN before changing the Developer Console. Take a transformed URL from an export that used the default CDN, then swap the host and prefix for your own:

{% code overflow="wrap" %}
```shellscript
curl -sv "https://images.example.com/<your-prefix>/<signature>/<payload>/<filename>" -o /dev/null
```
{% endcode %}

A working configuration returns 200, a content-type of image/..., and cache-control: public, max-age=86400. Run the same call again and the second response should be a cache hit.

The following table lists the failures you're most likely to see.

| Symptom                                     | Cause                                                                                                                            |
| ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `Access Denied`, or a storage-bucket error  | The path pattern didn't match, so the request fell through to the default behavior. Check `/<your-prefix>/*`                     |
| `401` with "missing authorization header"   | The header isn't reaching the origin. Either the behavior points at the wrong origin, or the header was added to a different one |
| `401` with the header present               | The key is wrong or revoked, or the value is malformed. It must be `Bearer <your-api-key>` exactly                               |
| `404`                                       | The origin path is missing or isn't `/v1/transform`                                                                              |
| curl works but the editor preview is broken | The Console was configured before the CDN was ready, or the page is stale. Reload the editor                                     |

### What happens if a transform fails?

Transform failures return an uncached error rather than falling back to the original image, since an uncropped original would break the layouts the crop settings were meant to fix. The recipient sees their email client's broken-image placeholder while the surrounding layout stays intact.

Because error responses are never cached, the image recovers on its own. The next open after the service returns produces a working image with no additional action from you.

### Limitations

* Transformed output is capped at 1920px wide, matching the upper limit already applied to file manager uploads.
* Cache invalidation isn't available and isn't needed. Because URLs are content-addressed, an edited image is always a new URL.
* Transforms keep the source format and original quality, so there's no automatic weight optimization.
* Advanced Image Layout is not currently compatible with the [Image type Custom AddOns](https://docs.beefree.io/beefree-sdk/builder-addons/custom-addons/custom-addon-types/image-addon).
