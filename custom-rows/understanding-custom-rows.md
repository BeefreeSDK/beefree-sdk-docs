# Understanding Custom Rows

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above.\
If you're on the Essentials plan, [upgrade a development application](../getting-started/development-applications.md) for free to try this and other Core-level features.
{% endhint %}

_Custom rows_ dramatically improves this area of the builder (now renamed simply _Rows_):

1. Introducing the concept of ready-to-go rows, which provide both structure & content.
2. Allowing you – the hosting application – to pass that _ready-to-go_ content to the builder.
3. Maintaining the existing, empty structures, for continuity of the current user experience.
4. Allowing you to turn off empty structures, if you want to, and only provide _custom rows_.

These new, _custom rows_ can be dragged and dropped into the editing pane the same way users currently add other content elements.

![](https://docs.beefree.io/wp-content/uploads/2018/04/CR\_sample-574x1024.png)

### Use cases <a href="#use-cases" id="use-cases"></a>

**User saved rows**

Enabling the [Save Rows](../saved-rows/) feature, your users will be able to save into your application design elements that they want to use in other messages.

To display saved rows in the _Rows_ tab, add them to the list of rows available to users by leveraging the [Custom Rows feature](displaying-saved-rows.md).

![](https://docs.beefree.io/wp-content/uploads/2018/11/Saved\_Rows-1024x601.jpg)

**Prebuilt rows**

When using the standard, empty rows, users are forced to start from scratch every time they introduce a new row.

A set of pre-built rows may accelerate message construction, providing users with commonly used structures filled with sample content. For example, a set of headers, footers, news sections, etc.

With _Custom rows_ you – the hosting application – are in control of the content that is included. In some cases, providing canned text can speed up the email creation process and provide consistency across all the communications.

Imagine, for example, the case of a CRM where customer success representatives can quickly build curated emails selecting from a number of pre-built text blocks.

![](https://docs.beefree.io/wp-content/uploads/2018/04/CR\_text\_samples-1024x708.jpg)

**Default rows**

In addition to the _empty rows_ that have always been part of the Beefree SDK system, we now provide a set of _default rows_ that you can add to your application with a simple configuration parameter.

They feature a series of popular structures, filled with placeholder text, images, and buttons.

For some users, they may work better than _empty rows_ as they allow them to immediately visualize what they can accomplish with a specific structure.

![](https://docs.beefree.io/wp-content/uploads/2018/04/CR\_defaults-1024x653.jpg)

Check how to configure these sample rows below under _Rows configuration > Parameters > Default rows_

**User/campaign tailored contents**

Does your application onboard users asking for company or brand information?

If so, you can use _custom rows_ to provide footers with legal information already applied (and centralized), header designs that already include the company logo, etc.

Other common use cases:

* Approved promotional material
* QR codes or barcodes
* Advertising content
* Product recommendation templates

![](https://docs.beefree.io/wp-content/uploads/2018/04/CR\_contents-1024x541.jpg)

Check how to configure these sample rows below under _Rows configuration > Parameters > Default rows_

**Blog updates and other news**

Create _custom rows_ with content from different sources like blogging platforms, content management systems, etc.

This will allow your customers to save time and reduce errors by avoiding copying and pasting text, links, and images.

Additionally, this helps you ensure that only reviewed and approved contents, provided by a common repository, are used in the message creation.

![](https://docs.beefree.io/wp-content/uploads/2018/04/CR\_blog\_example-1024x769.jpg)

**E-commerce products**

Transform products from your e-commerce catalog into _custom rows_, using product images, text, and call to actions to create a promotional message with a few clicks.

You can divide the products into categories and feed them into the builder as different arrays of _custom rows_.

Or you can use different sets of _custom rows to_ provide different layout options in order to add design flexibility.

![](https://docs.beefree.io/wp-content/uploads/2018/04/CR\_products\_example-1024x643.jpg)
