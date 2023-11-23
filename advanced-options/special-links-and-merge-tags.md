# Special Links and Merge Tags

The default configuration returned by the system can be extended by using additional configuration objects such as:

### Special links <a href="#special-links" id="special-links"></a>

Special links are links that your system generates dynamically when the message is sent, typically because they include the message ID, the recipient’s email, or some other variable. The most common one is probably the unsubscribe link.

The `type` parameter will be used to group related links in the UI and simplify the user selection.

Technically, special links are passed to the application in the configuration file as follows:

```

specialLinks: [
	{
      type: 'Frequently used',
      label: 'Unsubscribe link',
      link: 'http://[unsubscribe]/'
	},{
      type: 'Frequently used',
      label: 'Preference center link', 
      link: 'http://[preference_center]/'
	},
	/* Other special links */
];

```

and here’s an example of what the user will see in the builder UI, starting from the above code:

![Grouped links in BEE](https://docs.beefree.io/wp-content/uploads/2017/08/group\_links\_in\_BEE.png)

### Merge Tags & Merge Content <a href="#merge-tags-merge-content" id="merge-tags-merge-content"></a>

As mentioned above, when you initialize the application, in the configuration file you can submit both “merge tags” and “merge content”.

Really, they are the same thing: some syntax that your system will replace with some meaningful content at the time the email is sent. They differ in the way they are presented to the user.

Merge tags help dynamically insert text into a paragraph, such as the very common scenarios of “Dear {first\_name}”.

Merge content, instead, helps the user insert special syntax as content element in other sections of the message that are not text, such a list of recommended products.

Currently it is not possible to group merge tags and merge contents as it is for special links.

Here is an example of adding `mergeTags` and `mergeContents` in the configuration file:

```


var mergeTags = [
	{
		name: 'First Name',
		value: '[first-name]'
	}, {
		name: 'Latest order date',
		value: '[order-date]'
	}
];

var mergeContents = [
	{
		name: 'Headline news',
		value: '{headline}'
	}, {
		name: 'Image of last product viewed',
		value: '{last-product-viewed}'
	}
];


```

{% hint style="info" %}
You can now use the [Content Dialog](content-dialog.md) feature to allow users to search for additional Merge Tags and Merge Content, beyond those passed in the configuration file.
{% endhint %}

## Merge Tag Details

Merge tags can be inserted into a text block by clicking on the “Merge tags” button in the expanded text block toolbar. The button is not shown if no merge tags were submitted in the configuration file.

![](https://docs.beefree.io/wp-content/uploads/2017/08/bee\_editor\_merge\_tags.png)

Merge tags also become available to the user by pressing the @ key on the keyboard while editing a text block.

Here is an example: the user wants the date of the last order to be inserted after “\[…] placing an order on …”, so he/she presses the @ key and selects “Last order date” from the list of merge tags found by the builder in the configuration file.

![](https://docs.beefree.io/wp-content/uploads/2017/08/bee\_v2\_example\_mergeTags.png)

After inserting the merge tag, the text block now shows the placeholder for the last order date.

![](https://docs.beefree.io/wp-content/uploads/2017/08/bee\_v2\_example\_mergeTags\_2.png)

#### Ways to load Merge Tags

You can load Merge Tags in the builder when it is initialized by adding a `mergeTags` node to the JSON configuration file. For example:

```

var mergeTags = [
	{
		name: 'First Name',
		value: '[first-name]'
	}, {
		name: 'Last Name',
		value: '[last-name]'
	}, {
		name: 'Email',
		value: '[email]'
	}, {
		name: 'Latest order date',
		value: '[order-date]'
	}
];

```

… or you can allow users to search and insert a merge tag by using the flexible [Content Dialog](content-dialog.md) feature. This is especially useful when the number of merge tags is large, and picking from a list would not provide an optimal user experience.

You can use a combination of both approaches, loading frequently used merge tags at the time the builder is initialized, and then allowing users to look for additional merge tags using [Content Dialog](content-dialog.md).

{% hint style="info" %}
The syntax used for Merge Tags is entirely up to you. Curly brackets, square brackets, ... you name it. The builder is agnostic to the syntax that your system employs for these dynamic fields. The same is true for Merge Contents.
{% endhint %}

### Merge Content details <a href="#merge-content-details" id="merge-content-details"></a>

Merge content differs from merge tags in that it allows the user to drag and drop instances of it as a content element available in the _**Content**_** panel**.

For example, let’s say you have a section of an email where you want to display some recommended products: Merge Content allows you to insert some syntax into the message that your application will replace with the recommended products at the time the email is sent.

When Merge Content elements are submitted to the builder in the configuration file, a new tile is displayed in the _Content_ panel.

![](https://docs.beefree.io/wp-content/uploads/2022/01/Screen-Shot-2022-01-25-at-1.12.02-PM.png)

The user can drag and drop it into the message just like any other content element.

![](https://docs.beefree.io/wp-content/uploads/2022/01/Screen-Shot-2022-01-25-at-3.55.37-PM.png)

Once dropped in position, the settings panel will display the instances of merge content available for selection.

In the example below, the user wants to insert some banner ads into the email, using a service such as [LiveIntent](https://liveintent.com/). An array of Merge Content elements were submitted to the builder in the configuration file, so the user has several banner ads to choose from (i.e. some syntax that will be replaced with HTML when the email is sent).

To create another instance of merge content, the user can either drag and drop it again from the _Content_ tab, or duplicate the existing content element…

![](https://docs.beefree.io/wp-content/uploads/2022/01/Screen-Shot-2022-01-25-at-5.41.19-PM.png)

… choose another instance of merge content from the available selections…

![](https://docs.beefree.io/wp-content/uploads/2022/01/Screen-Shot-2022-01-25-at-5.43.41-PM.png)

… and then drag it elsewhere in the message.

#### Ways to load Merge Content

Just like with Merge Tags, you can load Merge Content in the builder at the time it is initialized by adding a `mergeContents` node to the JSON configuration file. For example:

```javascript


var mergeContents = [
	{
		name: 'Headline news',
		value: '{headlines}'
	}, {
		name: 'Lastest blog articles',
		value: '{latest-articles}'
	}, {
		name: 'Latest products viewed',
		value: '{latest-products}'
	}
];


```

… or you can allow users to search for additional instances of Merge Content by using the [Content Dialog feature](content-dialog.md).

Here too, you can certainly use a combination of both approaches, loading frequently used Merge Content at the time the builder is initialized, and then allowing users to look for additional Merge Content using [Content Dialog](content-dialog.md).

{% hint style="info" %}
NOTE: if what you need for your users is a way to load a **dynamic image** into the message or page (e.g. a countdown clock), you don't need to use Merge Content. Beefree SDK can handle dynamic images with a feature that was created specifically for that task. See: [letting your users add dynamic images](https://dam.beefree.io/dynamicimagescontent).
{% endhint %}

### Limitations to Merge Tags & Merge Content <a href="#limitations-to-merge-tags-merge-content" id="limitations-to-merge-tags-merge-content"></a>

#### Merge tags limitations

**Merge tags** are meant to be placeholders that will be replaced at the time an email is sent, or the web content is generated for visitors.

You cannot use HTML code in the text strings passed to the builder because – if you do – it will be encoded and will not function correctly in the source code of the message. Of course, you can replace the tag with HTML code at the time of saving or sending the message.

Standard merge tags do not support sample placeholder content, for now. The syntax will be displayed in the builder as your users design the message or page.

If you want to provide a better experience when working with Merge tags, including using a friendly name instead of the syntax and generating sample content, we recommend to check out [Smart merge tags](smart-merge-tags.md)**.**

#### Merge Content limitations

Additionally, there are some other limitations that are specific to the Merge Content feature. Among them:

1. Users cannot see & edit the content: what’s in it, the style used, the layout, etc..
2. Not seeing it, they could select the wrong content from the list of available Merge Content.
3. The HTML might be created outside of Beefree SDK, which could lead to rendering issues when it’s inserted into the message.
4. Since the HTML is created elsewhere, and it’s not part of the document created by Beefree SDK, it must be managed separately.

Due to these additional limitations, we now recommend an alternative approach to Merge Content in order to handle dynamic content in Beefree SDK: utilizing [Custom Rows](../custom-rows/) with Merge Content & Display Conditions.

### Further extending the builder <a href="#further-extending-the-builder" id="further-extending-the-builder"></a>

You can use the [Content Dialog](content-dialog.md) feature to introduce an interactive layer between the builder and your application, and through it extend Merge Tags, Merge Content, Special Links, and Display Conditions.
