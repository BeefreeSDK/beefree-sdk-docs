# Display Conditions

{% hint style="info" %}
This feature is available on Beefree SDK [Core plan](https://dam.beefree.io/pluginpricing) and above. If you're on the Essentials plan, [upgrade a development application](../getting-started/development-applications.md) for free to try this and other Core-level features.
{% endhint %}

## How they work <a href="#how-they-work" id="how-they-work"></a>

Display conditions allow you to change the content that is shown to recipient of an email depending on who the recipient is.

![](http://docs.beefree.io/wp-content/uploads/2017/08/display\_conditions\_row\_example\_children.png)

Your users will have the ability to pick a condition (or write one from scratch if they are technically savvy), apply it to a row, and thus show different content based on who the recipient (or viewer) is.

The feature provides a number of benefits, including:

### **Ease of use for email designers**

Display conditions allow anyone that is using the builder to easily create personalized messages without writing a line of code.

### **Any syntax for the conditional statements**

Use whatever syntax your application understands. The feature is language agnostic: it can be used with whatever syntax matches your tech stack. Does your sending engine understand the Liquid markup? Then you can use Liquid. Does it use a proprietary templating language? No problem.

### **User permissions**

Restrict access to some of the functionality based on user roles. For example, some users may be able to edit the syntax of the conditional statements, while others may not. Use this flexibility to simplify the UI or promote upselling.

## Activating and using the feature <a href="#activating-and-using-the-feature" id="activating-and-using-the-feature"></a>

Please note that the Display conditions are **disabled by default.** You can turn this feature on by enabling it under the [Server-side configurations](../server-side-options/). You must be on a paid plan (Core subscription and above) to enable this feature.

As the application hosting the builder, you can now pass an array of conditions.

```javascript

var rowDisplayConditions = [{
  type: 'Last ordered catalog',
  label: 'Women',
  description: 'Only people whose last ordered item is part of the Women catalog will see this',
  before: '{% raw %}
{% if lastOrder.catalog == \'Women\' %}',
  after: '{% endif %}',
}, {
  type: 'Last ordered catalog',
  label: 'Men',
  description: 'Only people whose last ordered item is part of the Men catalog will see this',
  before: '{% if lastOrder.catalog == \'Men\' %}',
  after: '{% endif %}',
}, {
  type: 'Last ordered catalog',
  label: 'Children',
  description: 'Only people whose last ordered item is part of the Children catalog will see this',
  before: '{% if lastOrder.catalog == \'Children\' %}',
  after: '{% endif %}
{% endraw %}',
}, { ... }]

```

Those conditions become available for users of the editor to select, assuming the feature is turned **on** and the user has permissions to apply a condition to a row.

They will do so by browsing through categories or searching by keyword. For example…

![](http://docs.beefree.io/wp-content/uploads/2017/08/display\_conditions\_select\_children.png)

The condition that they pick is applied to the row and displayed when the row is selected.

![](http://docs.beefree.io/wp-content/uploads/2017/08/display\_conditions\_row\_example\_children-1.png)

It can be changed (i.e. the user decides to apply another condition) or edited (if the user has the technical skills to do so, and its user role has been granted those permissions).

![](http://docs.beefree.io/wp-content/uploads/2017/08/display\_conditions\_edit.png)

When the _Preview_ feature is accessed, users can now simulate what recipients in a certain segment will see by toggling _Display conditions_ on and off.

![](http://docs.beefree.io/wp-content/uploads/2017/08/display\_conditions\_preview\_children.png)

## Display conditions and user roles & permissions <a href="#display-conditions-and-user-roles-permissions" id="display-conditions-and-user-roles-permissions"></a>

When active, the feature is available to all users by default. You can manage who can see and/or do what by leveraging user roles and permissions.

When the feature is ON, new permissions are available for you to configure when you create or edit a Role.

![](https://docs.beefree.io/wp-content/uploads/2018/06/DC\_useroles.png)

A basic set up allows you to have 3 user levels:

1. **Can only view & preview**
   * None of the above options are selected
   * No widget will be shown unless the loaded message has display conditions assigned to one or more rows
   * If conditions are applied:
     * They are shown as ready-only
     * They can be applied in the Preview
2. **Can only select**
   * Only Can select conditions option is selected in the role settings (remove will be automatically selected too)
   * The widget shows and the user can select and apply any of the conditions specified in the editor configuration
   * The user cannot add a new condition
   * The user cannot edit a selected condition
3. **Full control**
   * All permissions are selected
   * The user can select and edit conditions (if provided) or add a new condition

**Note:** if there are no Display conditions passed in the configuration, and the user has the rights to access the feature, the editor will only show the Add condition action, which allows users to apply a new condition to a row by manually adding the condition’s syntax.

## Additional information <a href="#additional-information" id="additional-information"></a>

#### Identifying a row with an applied display condition

It’s easy to identify a row to which a display condition has been applied. A bifurcation icon is added to the row’s “Structure” tag, which is shown as you mouse over the row. Here’s an example:

![](http://docs.beefree.io/wp-content/uploads/2017/08/display\_conditions\_row\_beacon.png)

## Custom conditions

When a default Display condition is edited – by a user that has permissions to do so – it becomes a custom condition. Custom conditions are easy to recognize because:

* A blue dot is added next to the condition’s name
* The “Change condition” button is no longer available: a custom condition can only be removed
* The cancel icon is replaced by a trash button because an edited condition, once remove, is lost: it cannot be re-added.

![](http://docs.beefree.io/wp-content/uploads/2017/08/display\_conditions\_edit\_custom.png)

Why these different behaviors for custom conditions? Because Beefree SDK does not save them to the configuration (you passed that configuration to the application: we don’t have access to the repository where you save that information). So, custom conditions do not exist in the array of conditions that the user can search and/or browse.

## HTML output

Conditional syntax and row content are isolated from each other in the HTML generated by Beefree SDK, so your system can delete, repeat or change elements inside the row without impacting other parts of the message. For example, the HTML of a row might look like this:

![](http://docs.beefree.io/wp-content/uploads/2017/08/display\_conditions\_example\_code\_html.png)

## Extending Display Conditions <a href="#extending-display-conditions" id="extending-display-conditions"></a>

You can extend this feature and allow users of the editor to build their own _Display Conditions_, on the fly, using a UI that you control. It’s part of the [Content Dialog](content-dialog.md) functionality. This is an advanced feature that requires some development on the side of the hosting application, but that provides fantastic flexibility. [Check it out!](content-dialog.md)

Here is an example of a custom builder of _Display Conditions_.

![Custom builder of display conditions](https://docs.beefree.io/wp-content/uploads/2018/02/display.condition.dialog.jpg)
