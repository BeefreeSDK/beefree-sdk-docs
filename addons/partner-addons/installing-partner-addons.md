# Installing Partner AddOns

1. [Getting started](broken-reference)
2. [Installing an AddOn](broken-reference)
3. [Adding client-side configurations for AddOns](broken-reference)

### Getting started <a href="#getting-started" id="getting-started"></a>

You can **use** ready-to-go AddOns to extend the functionality of Beefree SDK (you can also [build new AddOns](https://docs.beefree.io/addon-development/)).

To browse and install existing AddOns, log into the [Beefree SDK Console](https://dam.beefree.io/devmain) and click on _Details_ to navigate to the application details page.

In the lower part of the page, locate the _Application configuration_ section and click on AddOns.

![Configure AddOns](https://docs.beefree.io/wp-content/uploads/2020/02/Bee\_Dev\_Portal\_AddOns.png)

You will be taken to a page that lists the AddOns that have been installed for this application. If you are just getting started, the list will be empty.

Click on _Browse Partner AddOns_ to get the list of ready-to-install AddOns. We call them _Partner AddOns_ because they were developed by companies that partnered with us to extend Beefree SDK’s core functionality.

You will deal directly with those companies with regard to signing up for an account, cost, support, etc.

![](https://docs.beefree.io/wp-content/uploads/2020/02/bee-plugin-addons-create-custom.png)

You will instead click on _Create a Custom AddOn_ if you want to [build a new AddOn](https://docs.beefree.io/addon-development/) for Beefree SDK.

### Installing an AddOn <a href="#installing-an-addon" id="installing-an-addon"></a>

When you click on the _Browse Partner AddOns_ button, a list of AddOns is displayed. You can browse them and select what you need to install.

After installing a Partner AddOn, you will need to configure it by clicking on the _Edit_ action. A form will be displayed.

![](https://docs.beefree.io/wp-content/uploads/2020/02/partnerAddOnsetup-1024x741.png)

At the top of the form you will find the AddOn name and some links to the AddOn documentation. If any signup is required, that is the company that you will need to contact.

Below that, you will see the following form fields:

* **API Key**\
  Shown if this is an AddOn where a signup is required (you will be provided with an API key once you have signed up). Contact the provider of the AddOn if that is the case, so that you can learn about signing up, costs involved, the type of support they provide, etc.
* **Handle**\
  A unique identifier for this AddOn. You will use this unique identifier to pass information to the AddOn from your application, if and when needed.
* **Enabled**\
  A toggle element to enable and disable the AddOn. When toggled _OFF,_ the AddOn is not visible to end users of the builder in your application.
* **Icon**\
  If you want to customize the icon associated with the _tile_ shown in the builder _Content_ tab, you canupload an image from your local PC. Choose an image that is small in size: we recommend a 64 x 64 pixel SVG file.
* **Labels**
  * Title: This is the name that will be used for the _tile_ in the builder’s _Content_ tab (e.g. “Countdown timer”).
  * Call-to-action button: The label for the call-to-action button (e.g. “Select a Countdown Timer”), which is shown to end users on the button to configure the AddOn.
  * Placeholder text: The message shown to end users in the builder stage when the tile is first dragged and dropped into it.

With the following setup…

![](https://docs.beefree.io/wp-content/uploads/2020/02/icon.labels.setup\_-1024x194.png)

… you would get the following outcome:

**Title for the content tile**

![](https://docs.beefree.io/wp-content/uploads/2020/02/AddOn.tile\_.png)

**Placeholder text and button**

It displays when the AddOn is added to the editing stage and invites the user to take the next step.

![](https://docs.beefree.io/wp-content/uploads/2020/02/AddOn.placeholder-1024x298.png)

**AddOn selection button in content properties**

When the AddOn content is selected, the same button is displayed in the content properties.

![](https://docs.beefree.io/wp-content/uploads/2020/02/AddOn.action.png)\


### Adding client-side configurations for AddOns <a href="#adding-client-side-configurations-for-addons" id="adding-client-side-configurations-for-addons"></a>

Once you have initialized Beefree SDK, you can pass a series of [configuration parameters](https://docs.beefree.io/configuration-parameters/) to it.

The **AddOn section** of the configuration allows you to override the parameters you configured in the [Beefree SDK Console](https://dam.beefree.io/devmain), on a per-user basis.

For example:

* You can have an AddOn enabled at the application level, but disabled for users on a lower plan (so they have to upgrade to a higher plan in your app to get it).
* You could change the language used for the AddOn text labels depending on the language used for the builder, for that user.
* Etc.

**Example**

```


addOns: [
  {
    enabled: true,
    id: "", 
    label: 'Default title label override',
    ctaLabel: 'Default CTA label override',
    placeholder: 'Default stage placeholder override',       
  },
  {
    enabled: false,
    id: "",
  }
]



```

**Params:**

* Boolean. When false, the AddOn content is not displayed in the _Content_ tab.

**id**

* Identifies the AddOn by using the _handle_ provided in the configuration form.

**label**

* The text string displayed for the AddOn tile in the _Content_ tab

**ctaLabel**

* The text string displayed in the button that triggers the AddOn action.
* It’s displayed in:
  * The content placeholder (before any content is applied)
  * The content properties
* Text displayed in the content placeholder to provide further information about the content.
