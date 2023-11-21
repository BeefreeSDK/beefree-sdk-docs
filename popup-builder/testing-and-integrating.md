# Testing and integrating

### Creating an application <a href="#creating-an-application" id="creating-an-application"></a>

When you log into the [Beefree SDK Console](https://dam.beefree.io/devmain) you can immediately see what type of applications you have already created under your Beefree SDK subscriptions.

![](https://docs.beefree.io/wp-content/uploads/2021/08/firefox\_2021-08-18\_19.05.33.png)

Just head over to the “Popup Builder Application” section and click on Activate.

![](https://docs.beefree.io/wp-content/uploads/2021/08/firefox\_2021-08-18\_19.07.52.png)

Once created, head over to “Details” for all server-side configurations. Paid applications allow you to create child [development applications](../getting-started/development-applications.md), to ease new feature testing, development, and maintenance.

All builders share the same **core functionalities**, including authentication and configuration. If you have already integrated our Email builder, you can re-use most of your work using the same configuration and callbacks.

## Integrating the Popup Builder

Out-of-the-box, the setup and configuration are the same as [Email and Page Builder](../getting-started/installation/). This section will cover the settings specific to Popup Builder. Check out our [Getting Started guide](../getting-started/installation/) if you’re new to Beefree SDK or unfamiliar with the configuration basics (as seen in the example below).

```json
beeConfig: {
  uid: 'CmsUserName', // [mandatory]
  container: 'bee-plugin-container', // [mandatory]
  ...
}
```

Loading Popup Builder with no additional settings will give the end-user a beautifully designed popup and workspace to design their content. However, Popup Builder comes with an additional, robust set of configuration options to customize the workspace. This allows the host application to build a workspace that matches their popup’s look and feel and that of the destination page.

For example, the host app can customize…

* The popup workspace background to view how the popup will look “in context” on the destination page.
* The theme and position of the popup for both desktop and mobile design modes.

Continue reading to learn more on how to customize the workspace, starting with the common settings and working up to a full custom layout.

### HTML output <a href="#html-output" id="html-output"></a>

In Email and Page Builder, the Beefree SDK HTML parser service converts your template into an HTML document customized for email or pages, respectively. However, the Popup Builder will not return a full HTML page because the host application is the final destination. In addition, Beefree SDK Popup Builder doesn’t provide the scripts to control the popup’s behavior, such as opening and closing. Rather, Popup Builder provides the HTML “partials” to embed within your popup’s content area or body.

The HTML partial will come with all the CSS required to look as it did in the preview mode. The parser service will wrap the content with a special container to clear all the host application styles and prevent style conflicts. The HTML output is designed to be embedded into any popup framework or application and still render the way it appears in the builder.

### Developer resources <a href="#developer-resources" id="developer-resources"></a>

Our Github account has some resources that might help you out when testing and integrating the Popup Builder.

[**Sample code**](https://dam.beefree.io/pluginsamplecode)

Examples of different implementations and configurations that you can draw from to speed up your development.

[**Popup templates**](https://dam.beefree.io/popuptemplates)

A collection of ready-made templates that you can use right away and add to your application.
