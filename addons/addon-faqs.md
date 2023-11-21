# AddOn FAQs

1. [What is an addon?](broken-reference)
2. [What if I just want to use - not build - an addon?](broken-reference)
3. [What is a Custom AddOn?](broken-reference)
4. [What is a Partner AddOn?](broken-reference)
5. [Who can build an addon for BEE?](broken-reference)
6. [Can a Custom AddOn become a Partner AddOn](broken-reference)
7. [Where are addons visibile in the BEE editor UI?](broken-reference)
8. [What kind of content block can an addon generate?](broken-reference)
9. [How do I know when new addons become available?](broken-reference)

#### What is an addon? <a href="#what-is-an-addon" id="what-is-an-addon"></a>

An addon is an application that extends the functionality of the BEE editor.

Software companies can both **use** addons and **build** addons.

You **use** an addon when you need a new feature for BEE (e.g. you want your end-users to be able to insert a _countdown timer_ in an email) and find an addon that meets your needs. You will search, find, and install addons in the [Beefree SDK Console](https://dam.beefree.io/devmain), in the application configuration area. The [end-user experience](https://docs.beefree.io/addon-end-user-experience/) will vary depending on the addon.

In some case you might decide to **build** addons for BEE. In that case:

* When you create an addon for yourself, it’s called a [**Custom AddOn**](https://docs.beefree.io/custom-addons/).
* If you build an addon for any application that uses BEE, then it’s a [**Partner AddOn**](https://docs.beefree.io/addon-development-vendor/).

#### What if I just want to use - not build - an addon? <a href="#what-if-i-just-want-to-use-not-build-an-addon" id="what-if-i-just-want-to-use-not-build-an-addon"></a>

That’s precisely why we’re excited about addons: companies like yours can easily turn on all kinds of additional features (i.e. addons), with minimal effort. You will find, select, and install the addons that meet your needs directly from within the [Beefree SDK Console](https://dam.beefree.io/devmain).

More specifically:

* The Partner AddOn Directory will go live by mid-March, 2020. [Sign up to receive updates](https://docs.beefree.io/updates/) from us on this.
* You will access the directory from within the [Beefree SDK Console](https://dam.beefree.io/devmain), from the _Details_ page of any application that you have created.
* There will be several addons listed that will help your end-users with things like countdown timers, dynamic maps, personalized cards, etc. ([here is an example](https://docs.beefree.io/addon-end-user-experience/))
* You will be able to install many addons with just a few clicks (but some addons will require that you become a customer of the addon provider and obtain an API key).
* You will be able to customize things like the name of the feature shown to your end-users in the _Content_ tab of the editor, the icon used, etc.

#### What is a Custom AddOn? <a href="#what-is-a-custom-addon" id="what-is-a-custom-addon"></a>

A [Custom AddOn](https://docs.beefree.io/custom-addons/) is an addon that you developed for your own use. You developed it to provide your own end-users with new features by extending the BEE editor, and those features may not  make sense for any other application.

You will be able to install your custom addons on your own Beefree applications. No other Beefree SDK customer (i.e. no other software application that has embedded a Beefree content builder) will see it.

These addons are not listed in the Partner AddOn Directory, unlike [Partner AddOns](https://docs.beefree.io/addon-development-vendor/).

[More about Custom AddOns](https://docs.beefree.io/custom-addons/).

#### What is a Partner AddOn? <a href="#what-is-a-partner-addon" id="what-is-a-partner-addon"></a>

A [Partner AddOn](https://docs.beefree.io/addon-development-vendor/) is an addon that you developed for any Beefree SDK customer that wishes to take advantage of it.

You created it to provide end-users of any application that has embedded a Beefree content builder with new features that extend the builder.

Any Beefree SDK customer will see it and will be able to install it, as Partner AddOns are listed in the Partner AddOn Directory.

For details on building Partner AddOns, please see [Partner AddOns](https://docs.beefree.io/addon-development-vendor/).

#### Who can build an addon for BEE? <a href="#who-can-build-an-addon-for-bee" id="who-can-build-an-addon-for-bee"></a>

To build an addon you need an eligible Beefree SDK subscription plan, including any one of the following:

1. [Superpowers plan](https://dam.beefree.io/pluginpricing)
2. [Enterprise plan](https://dam.beefree.io/pluginpricing)

If you are on a lower-level plan and wish to **test building an addon**, you can simply [**upgrade a development application**](https://docs.beefree.io/initializing-bee-plugin/#production-vs-development-apps) for free.

#### Can a Custom AddOn become a Partner AddOn <a href="#can-a-custom-addon-become-a-partner-addon" id="can-a-custom-addon-become-a-partner-addon"></a>

Yes, that’s exactly the process of developing an addon that is available to the entire community of applications that have embedded the BEE editor.

* First you develop a [Custom AddOn](https://docs.beefree.io/custom-addons/)
* Then you submit it for listing in the [Partner AddOn](https://docs.beefree.io/addon-development-vendor/) Directory

Just remember that – technically speaking – you can only use the [iFrame Method](https://docs.beefree.io/addon-development/#the-iframe-method) when developing a Partner AddOn. So a Custom AddOn that you want to later list in the Partner AddOn Directory, must be developed that way.

#### Where are addons visibile in the BEE editor UI? <a href="#where-are-addons-visibile-in-the-bee-editor-ui" id="where-are-addons-visibile-in-the-bee-editor-ui"></a>

As of January 2020, addons become visible as new _tiles_ in the _Content_ tab.

![BEE editor with addons in Content tab](https://docs.beefree.io/wp-content/uploads/2020/02/BEE-AddOns-Yes-1024x460.png)

An example would be a [Giphy](https://giphy.com/) tile (you can see it in the _Content_ tab in the screenshot below) that can be dragged to the editing stage to allow a BEE user to search, find and insert a GIF animation into the message or page they are designing.

![Giphy AddOn for BEE content editor](https://docs.beefree.io/wp-content/uploads/2020/02/BEE-AddOns-Giphy-1-1024x794.png)

In the future we may develop new types of addons that may impact other areas of the editor. If you have specific ideas or requests, certainly let us know.

In the meantime, here is an [example of the end-user experience](https://docs.beefree.io/addon-end-user-experience/) with addons.

#### What kind of content block can an addon generate? <a href="#what-kind-of-content-block-can-an-addon-generate" id="what-kind-of-content-block-can-an-addon-generate"></a>

As of October, 2022, you can generate two kinds of content with an addon:

* An **image** content block
* A **custom HTML** content block
* A **mixed Content** content block
* A **custom row** content block

A countdown timer or a live map, for example, they will mostly likely be _image content blocks_ in BEE.

For details, see: [AddOn Development](https://docs.beefree.io/addon-development/)

#### How do I know when new addons become available? <a href="#how-do-i-know-when-new-addons-become-available" id="how-do-i-know-when-new-addons-become-available"></a>

[Sign up to receive updates](https://docs.beefree.io/updates/) from us.

We email rather infrequently, and it’s typically about things that are important to Beefree SDK customers.

It’s one newsletter you don’t want to miss 🙂
