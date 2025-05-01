# Sync Reusable Content

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. Upgrade a [development application](../../../getting-started/readme/development-applications.md) at no extra charge to explore features from higher plan tiers. **Note:** Usage on a development application still counts toward [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) and limits.
{% endhint %}

## Synced Rows <a href="#overview" id="overview"></a>

Synced Rows expands on the foundational capabilities of [Save Rows](../create/save/) and [Edit Single Row Mode](./#edit-single-row-mode), helping users manage rows more effectively. Using the `merge-rows` and `synced-rows` methods in the [Content Services API (CSAPI)](../../api-endpoints.md), you can create an efficient row management workflow. This ensures that when users update content in one row marked as “synced,” those updates are reflected across all connected designs using that synced row.

### Prerequisites

* [Self-hosted Saved Rows](../../storage/self-hosted-saved-rows.md)

### Key features

* **Cross-design synchronization**: Sync saved row contents across multiple linked designs.
* **Design consistency**: Lock rows in linked designs to keep designs uniform.
* **Editing flexibility**: Convert rows from synced to unsynced, making individual changes as needed.
* **Intuitive edit indicator**: Look for the pencil icon at the top-right of synced rows, which provides access to editing options

### Example use cases

* **Auto-updating contacts**: Change a contact in one email, and it updates across multiple campaigns.
* **Effortless re-branding**: Edit your logo once and watch it reflect across all designs.
* **Unified transactional footers**: Update details like copyright or social links, and it automatically updates in all relevant email templates.

### Elements that can be synchronized

* **Row details**: This includes structure, settings, and styles.
* **Content details**: Settings and styles of individual content blocks.
* **Metadata**: Any metadata tied to the saved row.

## Edit Single Row Mode

With [Edit Single Row Mode](initialize-edit-single-row-mode.md) you can offer an easier way for your end users to modify a single row with a tailored UI built to edit the row structure, content, and style settings without interfering in the overall design of the email campaign, landing page, or pop-up.

[Edit Single Row mode](initialize-edit-single-row-mode.md) complements both [Saved Rows](../create/save/) and [Synced Rows](./), because it allows complete control over the content of an individual row (for example, a footer that requires an update) without the need to intervene in a full template's design. This will help you in implementing a more effective way to manage libraries of [Saved Rows](../create/save/) and[ Synced Rows](./) with a streamlined design and editing process.
