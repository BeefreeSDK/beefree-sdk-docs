# Tracking Message Changes

1. [Overview](broken-reference)
2. [Use cases](broken-reference)
3. [How it works](broken-reference)
4. [Callback Parameters](broken-reference)
5. [Content Codes](broken-reference)
6. [Common Actions](broken-reference)
7. [Complete Event Chart](broken-reference)

### Overview <a href="#overview" id="overview"></a>

We added a new function to track message changes in the builder. This powerful new feature answers two important questions:

* How can I monitor what my customers do in the builder?
* How can I tell when a message has actually been updated?

When _onChange_ is enabled and your customers edit their message – the callback provides you valuable information on the new content or section, the kind of action that was performed on existing content, and the JSON update (as the entire page, as well as JSON patches).

_onChange_ is also the foundation on which the [Undo, Redo & Edit History](https://docs.beefree.io/undo-changes-history/) feature was built on.

### Use cases <a href="#use-cases" id="use-cases"></a>

**Usage tracking**

In today’s software, knowing how customers use an application is essential if you want to provide a good user experience (UX) and eliminate friction points. It’s also a valuable resource to understand where to invest future development effort and build something that customers love.

_onChange_ tracking gives you – the host application – the opportunity to get this information when your customers are creating designs in the builder.

You can use the _onChange_ callback to:

* Understand if your customers are actively working on the message they opened (or if instead they temporarily abandoned that task to work on something else).
* Discover if they are using one of the great new features that your team recently enabled.
* Dismiss or confirm a bug by reproducing a customer’s steps.

**Autosave**

So you might be asking: “Isn’t this similar to the existing [_Autosave_](https://docs.beefree.io/configuration-parameters/) feature?” The simple answer is “No!”.

The [_Autosave_](https://docs.beefree.io/configuration-parameters/) function is triggered at regular intervals, whether anything has even changed since the last _Autosave_ event or not, which could result in the user seeing a ‘recovery dialog’ window even if there weren’t any changes between the previously saved message and the most recent automatically saved one.

Now you can invoke the _Autosave_ event only when something has been added or updated, resulting in a better message recovery experience.

**History**

Why is having a historical log of message changes so important? As with the previous cases, this will allow you to provide a better overall user experience. Creating a good email message or campaign typically involves input from several people or departments before it’s finally ready to send, but that can lead to inadvertent mistakes that might cause hours of work to be lost. Saving the differences between versions of a message created during the email production workflow – and allowing your users to compare & restore them – could be a huge time-saver in those cases.

**Content check**

When one of your users adds or updates text or images, the _onChange_ callback returns the new input to your application, allowing you to trigger a complementary function based on it.

The use cases change from application-to-application, but the feature is flexible enough to accommodate a wide variety of scenarios. Here are just a few:

* Content suggestions
* Prevent unwanted content
* Link validation
* Link reputation check
* Custom HTML validation
* Set up an alternative workflow when conditional syntax is applied
* …

### How it works <a href="#how-it-works" id="how-it-works"></a>

To enable changes tracking you need to add in [beeConfig](https://docs.beefree.io/configuration-parameters/):

* The configuration option
* The _onChange_ callback, with the related response function

**Configuration**

**Enable "onChange" Event**

```


trackChanges: true, // boolean


```

This parameter defines when the tracking is active in the builder.

**onChange Event**

```


onChange: function (jsonFile, response) { // do something with response... },


```

The _onChange_ callback is triggered every time the builder tracks a change in the message. It returns the message JSON and a response JSON which contains all the information needed to handle any of the use cases described above.

**Callback response schema**

```


{
    "code": "01", // See content and action codes bellow
    "description": "string",
    "value": "string", // See the chart below
    "patches": {...} // JSON patch formatted object
}


```

### Callback Parameters <a href="#callback-parameters" id="callback-parameters"></a>

| Parameter   | Type   | Value                                                                                                                                                    |
| ----------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| code        | string | Unique identifier for the event created by combining the content code with the action code.                                                              |
| description | string | A text description of the event in the chosen language. (e.g. Image Block Padding Left: 5px)                                                             |
| value       | string | If available, this is the new value. (e.g. If padding changes to 5px, then the value returned is “5px”)                                                  |
| patches     | array  | An array of patches in the JSON Patch specification. JSON Patch is specified in [RFC 6902](https://datatracker.ietf.org/doc/html/rfc6902) from the IETF. |

### Content Codes <a href="#content-codes" id="content-codes"></a>

| Code   | Content               |
| ------ | --------------------- |
| **01** | Text Block            |
| **02** | Image Block           |
| **03** | Button Block          |
| **04** | Divider Block         |
| **05** | Social Block          |
| **06** | Dynamic Content Block |
| **07** | HTML Block            |
| **08** | Video Block           |
| **14** | Row                   |
| **16** | Message               |

### Common Actions <a href="#common-actions" id="common-actions"></a>

| Code    | Action                        |
| ------- | ----------------------------- |
| **00**  | Dropped                       |
| **01**  | Dragged                       |
| **02**  | Deleted                       |
| **03**  | Duplicated                    |
| **04**  | Changed                       |
| **05**  | Opened                        |
| **06**  | Closed                        |
| **07**  | Locked                        |
| **08**  | Saved                         |
| **09**  | Restored                      |
| **10**  | Content area background color |
| **11**  | Do not stack on mobile        |
| **12**  | Row background image          |
| **13**  | Background Center             |
| **14**  | Background Repeat             |
| **15**  | Background Full width         |
| **16**  | Row Display condition         |
| **17**  | Reverse stack order on mobile |
| **20**  | Text color                    |
| **21**  | Link color                    |
| **23**  | Text edited                   |
| **24**  | Line height                   |
| **25**  | Content area width            |
| **27**  | Background color              |
| **28**  | Default font                  |
| **30**  | Padding All sides             |
| **31**  | Padding Left                  |
| **32**  | Padding Right                 |
| **33**  | Padding Top                   |
| **34**  | Padding Bottom                |
| **40**  | Hide on mobile                |
| **41**  | Video url                     |
| **42**  | Play icon type                |
| **43**  | Play icon color               |
| **44**  | Play icon size                |
| **50**  | Align                         |
| **51**  | Automatic image resizing      |
| **52**  | Full width on mobile          |
| **53**  | Image width                   |
| **60**  | Alternate text                |
| **61**  | Dynamic image src             |
| **62**  | Dynamic image toggle          |
| **63**  | Change image                  |
| **64**  | Image link                    |
| **70**  | Button Align                  |
| **71**  | Button Link type              |
| **72**  | Button width                  |
| **73**  | Button Auto width             |
| **74**  | Button Background color       |
| **75**  | Border radius                 |
| **80**  | HTML edited                   |
| **81**  | Border All sides              |
| **82**  | Border Left                   |
| **83**  | Border Right                  |
| **84**  | Border Top                    |
| **85**  | Border Bottom                 |
| **90**  | Divider Line toggle           |
| **91**  | Divider Width                 |
| **92**  | Divider Height                |
| **93**  | Divider Align                 |
| **95**  | Icon Name                     |
| **96**  | Icon Alternate text           |
| **97**  | Icon Url                      |
| **98**  | Icon spacing                  |
| **99**  | Icon Align                    |
| **128** | Background Video              |
| **129** | Paragraph Spacing             |
| **130** | Font Weight                   |
| **131** | List Type                     |
| **132** | Start List                    |
| **133** | List Spacing                  |
| **134** | List Indent                   |
| **135** | List Style Position           |

### Complete Event Chart <a href="#complete-event-chart" id="complete-event-chart"></a>

| Code      | Description                                  | Type    | Value                                                                 |
| --------- | -------------------------------------------- | ------- | --------------------------------------------------------------------- |
| **0100**  | Text dropped                                 | module  |                                                                       |
| **0101**  | Text dragged                                 | module  |                                                                       |
| **0102**  | Text deleted                                 | module  |                                                                       |
| **0103**  | Text duplicated                              | module  |                                                                       |
| **0120**  | Text color \{{value\}}                       | string  | Hex color code (e.g. #FFFFFF)                                         |
| **0121**  | Link color \{{value\}}                       | string  | Hex color code (e.g. #FFFFFF)                                         |
| **0123**  | Text edited                                  | string  | HTML                                                                  |
| **0124**  | Line height \{{value\}}                      | string  | Value as percent (e.g. 150%)                                          |
| **0130**  | Padding Add sides \{{value\}}                | string  | Value in pixels (e.g. 25px)                                           |
| **0131**  | Padding Left \{{value\}}                     | string  | Value in pixels (e.g. 25px)                                           |
| **0132**  | Padding Right \{{value\}}                    | string  | Value in pixels (e.g. 25px)                                           |
| **0133**  | Padding Top \{{value\}}                      | string  | Value in pixels (e.g. 25px)                                           |
| **0134**  | Padding Bottom \{{value\}}                   | string  | Value in pixels (e.g. 25px)                                           |
| **0140**  | Hide on mobile                               | boolean | true \| false                                                         |
| **0200**  | Image dropped                                | module  |                                                                       |
| **0201**  | Image dragged                                | module  |                                                                       |
| **0202**  | Image deleted                                | module  |                                                                       |
| **0203**  | Image duplicated                             | module  |                                                                       |
| **0230**  | Padding Add sides \{{value\}}                | string  | Value in pixels (e.g. 25px)                                           |
| **0231**  | Padding Left \{{value\}}                     | string  | Value in pixels (e.g. 25px)                                           |
| **0232**  | Padding Right \{{value\}}                    | string  | Value in pixels (e.g. 25px)                                           |
| **0233**  | Padding Top \{{value\}}                      | string  | Value in pixels (e.g. 25px)                                           |
| **0234**  | Padding Bottom \{{value\}}                   | string  | Value in pixels (e.g. 25px)                                           |
| **0240**  | Hide on mobile                               | boolean | true \| false                                                         |
| **0250**  | Align \{{value\}}                            | string  | left \| right \| center                                               |
| **0251**  | Automatic image resizing                     | boolean | true \| false                                                         |
| **0252**  | Full width on mobile                         | boolean | true \| false                                                         |
| **0253**  | Image width \{{value\}}                      | string  | %                                                                     |
| **0260**  | Alternate Text                               | string  | text value                                                            |
| **0261**  | Dynamic image                                | string  | Image path                                                            |
| **0262**  | Dynamic image toggle                         | boolean | false (only triggered when disabled)                                  |
| **0263**  | Change image                                 | string  | Image path                                                            |
| **0264**  | Image link                                   | string  | Url                                                                   |
| **0300**  | Button dropped                               | module  |                                                                       |
| **0301**  | Button dragged                               | module  |                                                                       |
| **0302**  | Button deleted                               | module  |                                                                       |
| **0303**  | Button duplicated                            | module  |                                                                       |
| **0320**  | Text color \{{value\}}                       | string  | Hex color code (e.g. #FFFFFF)                                         |
| **0324**  | Line height \{{value\}}                      | string  | Value as percent (e.g. 150%)                                          |
| **0330**  | Padding Add sides \{{value\}}                | string  | Value in pixels (e.g. 25px)                                           |
| **0331**  | Padding Left \{{value\}}                     | string  | Value in pixels (e.g. 25px)                                           |
| **0332**  | Padding Right \{{value\}}                    | string  | Value in pixels (e.g. 25px)                                           |
| **0333**  | Padding Top \{{value\}}                      | string  | Value in pixels (e.g. 25px)                                           |
| **0334**  | Padding Bottom \{{value\}}                   | string  | Value in pixels (e.g. 25px)                                           |
| **0340**  | Hide on mobile                               | boolean | true \| false                                                         |
| **0370**  | Align \{{value\}}                            | string  | left \| right \| center                                               |
| **0371**  | Link type \{{value\}}                        | string  | Url                                                                   |
| **0372**  | Button width \{{value\}}                     | string  | %                                                                     |
| **0373**  | Auto width                                   | boolean | true \| false                                                         |
| **0374**  | Background color \{{value\}}                 | string  | Hex Color Code (e.g. #FFFFFF)                                         |
| **0375**  | Border radius                                | string  | Value in pixels (e.g. 5px)                                            |
| **0381**  | Border Add sides \{{value\}}                 | string  | Value in pixels \| Border Style \| Hex color (e.g. 1px solid #C7702E) |
| **0382**  | Border Left \{{value\}}                      | string  | Value in pixels \| Border Style \| Hex color 1px solid #C7702E        |
| **0383**  | Border Right \{{value\}}                     | string  | Value in pixels \| Border Style \| Hex color 1px solid #C7702E        |
| **0384**  | Border Top \{{value\}}                       | string  | Value in pixels \| Border Style \| Hex color 1px solid #C7702E        |
| **0385**  | Border Bottom \{{value\}}                    | string  | Value in pixels \| Border Style \| Hex color 1px solid #C7702E        |
| **0400**  | Divider dropped                              | module  |                                                                       |
| **0401**  | Divider dragged                              | module  |                                                                       |
| **0402**  | Divider deleted                              | module  |                                                                       |
| **0403**  | Divider duplicated                           | module  |                                                                       |
| **0430**  | Padding Add sides \{{value\}}                | string  | Value in pixels (e.g. 25px)                                           |
| **0431**  | Padding Left \{{value\}}                     | string  | Value in pixels (e.g. 25px)                                           |
| **0432**  | Padding Right \{{value\}}                    | string  | Value in pixels (e.g. 25px)                                           |
| **0433**  | Padding Top \{{value\}}                      | string  | Value in pixels (e.g. 25px)                                           |
| **0434**  | Padding Bottom \{{value\}}                   | string  | Value in pixels (e.g. 25px)                                           |
| **0440**  | Hide on mobile                               | boolean | true \| false                                                         |
| **0490**  | Line                                         | string  | Value in pixels \| Border Style \| Hex color 1px solid #C7702E        |
| **0491**  | Width \{{value\}}                            | string  | Value as percent (e.g. 150%)                                          |
| **0492**  | Height \{{value\}}                           | string  | Value in pixels (e.g. 25px)                                           |
| **0493**  | Align \{{value\}}                            | string  | left \| right \| center                                               |
| **0500**  | Social dropped                               | module  |                                                                       |
| **0501**  | Social dragged                               | module  |                                                                       |
| **0502**  | Social deleted                               | module  |                                                                       |
| **0503**  | Social duplicated                            | module  |                                                                       |
| **0530**  | Padding Add sides \{{value\}}                | string  | Value in pixels (e.g. 25px)                                           |
| **0531**  | Padding Left \{{value\}}                     | string  | Value in pixels (e.g. 25px)                                           |
| **0532**  | Padding Right \{{value\}}                    | string  | Value in pixels (e.g. 25px)                                           |
| **0533**  | Padding Top \{{value\}}                      | string  | Value in pixels (e.g. 25px)                                           |
| **0534**  | Padding Bottom \{{value\}}                   | string  | Value in pixels (e.g. 25px)                                           |
| **0540**  | Hide on mobile                               | boolean | true \| false                                                         |
| **0595**  | Name \{{value\}}                             | string  | Icon Name                                                             |
| **0596**  | Alternate Text \{{value\}}                   | string  | Icon Alternate text                                                   |
| **0597**  | Image Url                                    | string  | Icon Url                                                              |
| **0598**  | Icon spacing \{{value\}}                     | string  | Value in pixels (e.g. 0 0 5px 15px)                                   |
| **0599**  | Align \{{value\}}                            | string  | left \| right \| center                                               |
| **0600**  | Dynamic content dropped                      | module  |                                                                       |
| **0601**  | Dynamic content dragged                      | module  |                                                                       |
| **0602**  | Dynamic content deleted                      | module  |                                                                       |
| **0603**  | Dynamic content duplicated                   | module  |                                                                       |
| **0604**  | Dynamic content changed                      | string  | value                                                                 |
| **0640**  | Hide on mobile                               | boolean | true \| false                                                         |
| **0700**  | HTML dropped                                 | module  |                                                                       |
| **0701**  | HTML dragged                                 | module  |                                                                       |
| **0702**  | HTML deleted                                 | module  |                                                                       |
| **0703**  | HTML duplicated                              | module  |                                                                       |
| **0740**  | Hide on mobile                               | boolean | true \| false                                                         |
| **0780**  | HTML edited                                  | string  | HTML                                                                  |
| **0800**  | Video dropped                                | module  |                                                                       |
| **0801**  | Video dragged                                | module  |                                                                       |
| **0802**  | Video deleted                                | module  |                                                                       |
| **0803**  | Video duplicated                             | module  |                                                                       |
| **0830**  | Padding Add sides \{{value\}}                | string  | Value in pixels (e.g. 25px)                                           |
| **0831**  | Padding Left \{{value\}}                     | string  | Value in pixels (e.g. 25px)                                           |
| **0832**  | Padding Right \{{value\}}                    | string  | Value in pixels (e.g. 25px)                                           |
| **0833**  | Padding Top \{{value\}}                      | string  | Value in pixels (e.g. 25px)                                           |
| **0834**  | Padding Bottom \{{value\}}                   | string  | Value in pixels (e.g. 25px)                                           |
| **0840**  | Hide on mobile                               | boolean | true \| false                                                         |
| **0841**  | Video url                                    | string  | Video Url                                                             |
| **0842**  | Play icon type \{{value\}}                   | string  | Play icon type (e.g. Round outline)                                   |
| **0843**  | Play icon color \{{value\}}                  | string  | light \| dark                                                         |
| **0844**  | Play icon size \{{value\}}                   | string  | Value in pixels (e.g. 25px)                                           |
| **1400**  | Row dropped                                  | row     |                                                                       |
| **1401**  | Row dragged                                  | row     |                                                                       |
| **1402**  | Row deleted                                  | row     |                                                                       |
| **1403**  | Row duplicated                               | row     |                                                                       |
| **1410**  | Content background color \{{value\}}         | string  | Hex Color Code (e.g. #FFFFFF)                                         |
| **1411**  | Do not stack on mobile                       | boolean | true \| false                                                         |
| **1412**  | Row background image                         | string  | Image path                                                            |
| **1413**  | Center                                       | boolean | true \| false                                                         |
| **1414**  | Repeat                                       | boolean | true \| false                                                         |
| **1415**  | Full width                                   | boolean | true \| false                                                         |
| **1416**  | Display Condition                            | object  | Display condition object                                              |
| **1417**  | Reverse stack order on mobile                | boolean | true \| false                                                         |
| **1430**  | Padding Add sides \{{value\}}                | string  | Value in pixels (e.g. 25px)                                           |
| **1431**  | Padding Left \{{value\}}                     | string  | Value in pixels (e.g. 25px)                                           |
| **1432**  | Padding Right \{{value\}}                    | string  | Value in pixels (e.g. 25px)                                           |
| **1433**  | Padding Top \{{value\}}                      | string  | Value in pixels (e.g. 25px)                                           |
| **1434**  | Padding Bottom \{{value\}}                   | string  | Value in pixels (e.g. 25px)                                           |
| **1474**  | Background color \{{value\}}                 | string  | Hex Color Code (e.g. #FFFFFF)                                         |
| **1481**  | Border Add sides \{{value\}}                 | string  | Value in pixels \| Border Style \| Hex color 1px solid #C7702E        |
| **1482**  | Border Left \{{value\}}                      | string  | Value in pixels \| Border Style \| Hex color 1px solid #C7702E        |
| **1483**  | Border Right \{{value\}}                     | string  | Value in pixels \| Border Style \| Hex color 1px solid #C7702E        |
| **1484**  | Border Top \{{value\}}                       | string  | Value in pixels \| Border Style \| Hex color 1px solid #C7702E        |
| **1485**  | Border Bottom \{{value\}}                    | string  | Value in pixels \| Border Style \| Hex color 1px solid #C7702E        |
| **1625**  | Content area width \{{value\}}               | string  | Value in pixels (e.g. 25px)                                           |
| **1626**  | Background color \{{value\}}                 | string  | Hex Color Code (e.g. #FFFFFF)                                         |
| **1627**  | Content area background color: \{{value\}}   | string  | Hex Color Code (e.g. #FFFFFF)                                         |
| **1628**  | Default font                                 | string  | Font                                                                  |
| **1529**  | Link color \{{value\}}                       | string  | Hex Color Code (e.g. #FFFFFF)                                         |
| **1605**  | Message opened                               | page    | JSON template                                                         |
| **1609**  | Message restored (e.g. undo or redo history) | page    | JSON template                                                         |
| **13130** | Button Font Weight                           | string  |                                                                       |
| **14128** | Row Background Video                         | string  | Video URL                                                             |
|           |                                              |         |                                                                       |
| **22130** | Paragraph Font Weight                        | string  | Font Weight value                                                     |
