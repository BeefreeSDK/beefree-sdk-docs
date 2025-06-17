# Self-Hosted Saved Rows

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. Upgrade a [development application](../../getting-started/readme/development-applications.md) at no extra charge to explore features from higher plan tiers. **Note:** Usage on a development application still counts toward [usage-based fees](https://devportal.beefree.io/hc/en-us/articles/4403095825042-Usage-based-fees) and limits.
{% endhint %}

## Overview

**Self-Hosted Saved Rows** allow you to control where and how your rows are stored and managed, offering flexibility to meet your application's unique requirements. This option is ideal for teams with development resources who want to integrate row storage into their existing infrastructure.

When users save rows, the data includes layout, content, and style settings. This data needs to be stored and managed, typically in your own database, to make rows available for reuse within your design builder.

### **Key considerations for Self-Hosted Saved Rows:**

1. **Storage**\
   Use a database or storage solution to house self-hosted saved rows. Examples of a few options include:
   * Cloud databases (e.g., AWS RDS, Google Cloud Firestore)
   * Local databases (e.g., MySQL, PostgreSQL)
   * Document-based databases (e.g., MongoDB)
2. **Development Resources**\
   Ensure your team has the capability to connect your storage to your application. This includes:
   * Setting up secure storage with proper access controls.
   * Implementing any necessary API endpoints or backend logic to retrieve, save, and manage rows.

#### **Custom Database Integration**

You can directly save and retrieve rows using your own database.&#x20;

#### Managed Solution Alternative

For teams that prefer not to handle row storage and development in-house, we offer [Hosted Saved Rows](hosted-saved-rows.md). This solution stores rows for you and provides your end users with a UI for saving rows throughout their designing experience. This eliminates the need to create a custom infrastructure.
