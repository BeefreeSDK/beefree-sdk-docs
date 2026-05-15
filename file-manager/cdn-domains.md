# CDN Domains

## Understanding Beefree's CDN Infrastructure

A CDN (Content Delivery Network) is a system of distributed servers that deliver web content, ensuring high availability and performance by distributing the service spatially relative to end-users. CDNs reduce load times, minimize latency, and enhance security for digital assets.

**Beefree's Segmented CDN Infrastructure**

If you rely on Beefree SDK storage, Beefree uses a segmented CDN infrastructure to serve your assets. We allocate distinct second-level domains per subscription tier and media type, and also assign you a dedicated third-level domain based on subscription ID.&#x20;

This unique setup isolates your content from other SDK customers, mitigating risks from potential malicious or spammy uploads. By preventing one customer's actions from impacting others, Beefree ensures robust security and maintains the integrity and reputation of all digital assets.

## How Beefree CDN Infrastructure Works

When you create or manage an SDK application, your subscription plan determines which CDN domains your files use.

### Free Plans

For **free plans**, all assets are served from the domain `beefreesdkhosting.net`. Each subscription is automatically assigned a third-level domain that uniquely identifies it.&#x20;

{% hint style="info" %}
Free plans only support image, video, and PDF MIME types. If you want to learn more about file type limitations, please visit the [dedicated page](https://docs.beefree.io/beefree-sdk/server-side-configurations/server-side-options/privacy-and-security#file-type-limitations).
{% endhint %}

**Free Plan CDN domain example**

```
https://id32514.beefreesdkhosting.net/path/to/file.png
```

### Paid Plans

For **paid plans** relying on Beefree's storage, and using the latest FSP backend component, we use two domains to serve different types of assets:

* The **Media Files** CDN Domain `sdkmedia.net` handles image, video, and audio MIME types
* The **Other Files** CDN domain `sdkhosting.net` is used for text (including HTML), office documents, XML, ZIP files, EPUB, PDF, PostScript, and fonts.

{% hint style="info" %}
New apps created by paid users are by default restricted to uploading image, video, and PDF MIME types. You can enable additional MIME types via the SDK Console—[learn how here](https://docs.beefree.io/beefree-sdk/server-side-configurations/server-side-options/privacy-and-security#custom-limitations-on-the-file-manager).&#x20;
{% endhint %}

Paid plans' subscriptions are also automatically assigned a third-level domain.&#x20;

**Paid plan Media Files domain example:**

```
https://id76302.sdkmedia.net/path/to/image.png
```

**Paid plan Other Files domain example:**

```
https://id76302.sdkhosting.net/path/to/archive.zip
```

Please note that your CDN domains are set at subscription level. If your subscription has multiple applications that rely on Beefree's default storage, those applications will be sharing the same CDN domains. At the same time, if you have multiple applications with different storage options, only those relying on both Beefree SKD's storage will serve content using the abovementioned segmented CDN domains.

You can check your CDN domains in the Storage options section of the SDK console, as seen in the screenshot below.

<figure><img src="../.gitbook/assets/CDN Console.jpg" alt=""><figcaption></figcaption></figure>

### Customize your CDN Domain

If you are a Paid User, you may request a **one-time customization** of your third-level domain, which allows aligning the CDN URL more closely with your brand identity. For example, you could replace a default `id32514.sdkmedia.net` domain with `yourbrand.sdkmedia.net`.

You can request a custom third-level domain via [this form](https://devportal.beefree.io/hc/en-us/requests/new?ticket_form_id=29348176015634\&tf_29381025990290=third-level_domain_request\&tf_subject=Custom+CDN+-+Third-level+domain+change+request\&tf_description=Please+change+the+CDN+third-level+domain+in+my+Beefree+SDK+subscription+%5Badd+details+if+needed%5D), providing:&#x20;

* your Client ID
* the new third-level domain you want to adopt

For **Enterprise plans**, you may also request to connect your own domain. Please contact your CSM for dedicated assistance.

### Allowlisting CDN Domains

To ensure the reliable delivery of your assets and prevent potential loading or connectivity issues, we strongly recommend allowlisting Beefree SDK’s CDN domains within your network security configurations, firewalls, or content filtering systems:

* `beefreesdkhosting.net`&#x20;
* `sdkmedia.net`
* `sdkhosting.net`
* `d15k2d11r6t6rl.cloudfront.net`
* `d1oco4z2z1fhwp.cloudfront.net`

***

### CDN Migration

Previously, all media for both free and paid plans were served via a single CDN domain: `d15k2d11r6t6rl.cloudfront.net`. To provide the enhanced security and segmentation described above, Beefree started migrating to the current configuration in early 2026.&#x20;

* This transition has already been completed for Free, Essential, Core, and Superpowers plans.
* Enterprise plans will be migrated starting June 17, 2026. Please reach out to your CSM to arrange the transition.

#### Impact on Media Assets and Automation

All files (images, videos, etc.) that your end users previously uploaded **will continue to be visible and work as intended** under the new, segmented CDN configuration.&#x20;

More in detail, you can now expect different behavior depending on when assets enter a message.

* **Emails sent before the migration:** Existing emails continue to serve images and media assets from the previous CDN domain.
* **Existing File Manager assets:** When you insert an existing asset into a new message, the system rewrites the URL to use the current CDN domain.
* **New uploads:** Newly uploaded files always use your segmented CDN domain.&#x20;

{% hint style="info" %}
If your integration performs post-processing on image URLs (for example, rewriting or hashing), you may need to adjust your setup to account for the new CDN domain pattern.&#x20;
{% endhint %}

#### Migrating to new CDN domains when using our legacy file system provider

In 2024, we introduced a new file system provider (FSP), and this CDN update requires you to be on the latest FSP, other than relying on the Beefree SDK storage. If you're among the customers who are still relying on our legacy file system provider, please note that we currently cannot migrate you to the improved CDN domain infrastructure. Please connect with your Customer Success Manager to discuss your migration options.&#x20;

#### Contact us for support

Although we strongly recommend the segmented infrastructure for security and reputation management, we understand that certain technical workflows may be more complex to adapt. If you have any questions or encounter any issues with the migration, [reach out to our support team](https://devportal.beefree.io/hc/en-us/requests/new) or contact your assigned CSM for assistance.
