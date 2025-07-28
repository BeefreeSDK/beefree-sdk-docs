---
description: >-
  Learn how to integrate forms into Beefree SDK. This video covers how to add a
  default form, create a form library, and how to create form builder for your
  end users.
---

# Easily Add and Customize Forms in Beefree SDK

{% embed url="https://www.youtube.com/watch?v=nOkt3ztSo2A" %}

{% tabs %}
{% tab title="About" %}
In this tutorial, you'll learn how to integrate and use the Form Block in the Beefree SDK to simplify form building and customization. We’ll walk you through enabling the Form Block in the Beefree SDK developer console, creating default forms, and implementing custom UI for a fully on-brand experience. Ship forms in minutes and empower end-users to create beautiful, branded experiences—no code needed.&#x20;

**Chapters:** \
[0:00](https://www.youtube.com/watch?v=nOkt3ztSo2A) - Introduction to the Form Block \
[1:42](https://www.youtube.com/watch?v=nOkt3ztSo2A\&t=102s) - Enabling the Form Block \
[2:44](https://www.youtube.com/watch?v=nOkt3ztSo2A\&t=164s) -  Creating a defaultForm template for users  \
[6:51](https://www.youtube.com/watch?v=nOkt3ztSo2A\&t=411s) - Using contentDialog to create a custom form library \
[8:41](https://www.youtube.com/watch?v=nOkt3ztSo2A\&t=521s) - Using contentDialog to build a custom UI for form creation \
[11:03](https://www.youtube.com/watch?v=nOkt3ztSo2A\&t=663s) - Front-end customization options \
[12:15](https://www.youtube.com/watch?v=nOkt3ztSo2A\&t=735s) - Conclusion and final thoughts
{% endtab %}

{% tab title="Transcripts" %}
The following text includes the complete transcript for this video.

```
1
00:00:03,120 --> 00:00:06,640
What if you could build forms without 
the usual headaches? What if you could

2
00:00:06,640 --> 00:00:10,960
give users an easy no-code form builder 
while still keeping full control over

3
00:00:10,960 --> 00:00:15,120
everything happening behind the scenes? 
Introducing the Form Block, available

4
00:00:15,120 --> 00:00:20,640
for both page and pop-up builders with various 
pre-built templates and customization options.

5
00:00:20,640 --> 00:00:26,000
The form block is easy to integrate for 
developers and intuitive to use for end users.

6
00:00:26,000 --> 00:00:30,400
In this tutorial, you'll learn how to 
make the most of the form block. First,

7
00:00:30,400 --> 00:00:36,080
we'll show you how to enable the form block 
inside the Beefree SDK developer console. Next,

8
00:00:36,080 --> 00:00:40,080
we'll guide you through how to create 
a prebuilt default form for your users

9
00:00:40,080 --> 00:00:44,000
that they can quickly customize 
for any landing page or pop-up.

10
00:00:44,000 --> 00:00:49,520
Next, we'll guide you through two examples of how 
to use the content dialogue managed form method.

11
00:00:49,520 --> 00:00:54,960
The first example demonstrates how to trigger 
a custom-built UI that interacts with Beefree

12
00:00:54,960 --> 00:00:59,920
SDK and provides end users with a form 
library they can choose from. The second

13
00:00:59,920 --> 00:01:05,360
example walks through how to load your UI 
for form creation on top of the builder so

14
00:01:05,360 --> 00:01:10,080
you can load forms into Beefree SDK 
from those custom user interfaces.

15
00:01:10,080 --> 00:01:15,120
And finally, we'll show you how the form block 
allows your end users to customize their form

16
00:01:15,120 --> 00:01:21,040
directly inside the builder, making it flexible 
and easy to use—no coding required. By the end

17
00:01:21,040 --> 00:01:26,320
of this video, you'll see how Beefree simplifies 
form building for everyone. Developers can set

18
00:01:26,320 --> 00:01:31,280
up default templates while the SDK ensures 
a smooth experience for end users to edit

19
00:01:31,280 --> 00:01:36,800
and customize forms effortlessly. We'll also 
provide three sample forms and a readme to help

20
00:01:36,800 --> 00:01:42,320
you explore this feature. You can find them in 
our GitHub repo linked in the video description.

21
00:01:42,320 --> 00:01:47,280
First, let's enable the form block feature. 
You can enable the form block feature from

22
00:01:47,280 --> 00:01:53,600
the Beefree SDK dashboard by heading to your 
page builder application and clicking details.

23
00:01:53,600 --> 00:01:56,640
From there, you can click configure application,

24
00:01:56,640 --> 00:02:01,760
then scroll to the bottom of the page 
until you find the content section.

25
00:02:01,760 --> 00:02:07,120
Then click the checkbox to enable the 
form content block, hit save changes,

26
00:02:07,120 --> 00:02:14,720
and confirm. Now that this is enabled, you can 
maintain full control over data processing,

27
00:02:14,720 --> 00:02:20,240
default form customization, and overall 
behavior, which leads us to the next section.

28
00:02:20,240 --> 00:02:24,400
It's important to remember that in order 
for the form block to appear in the builder,

29
00:02:24,400 --> 00:02:28,080
you must enable it in the console 
and then pass a form to the

30
00:02:28,080 --> 00:02:33,360
default form parameter in the Beefree SDK 
configuration. If either step is missing,

31
00:02:33,360 --> 00:02:38,720
the form block will not appear. To ensure this is 
done correctly, you can always reference the form

32
00:02:38,720 --> 00:02:43,920
validation schema for creating your own form, 
which I've linked in the video description.

33
00:02:44,480 --> 00:02:48,960
Next, we'll show you how to pre-build 
default forms your end users can easily

34
00:02:48,960 --> 00:02:52,960
drag and drop into the builder and 
then customize however they like.

35
00:02:52,960 --> 00:02:57,760
There are two methods to enable your 
users to add forms in Beefree SDK.

36
00:02:57,760 --> 00:03:02,560
The first method is bypassing in the 
configuration parameters a single default

37
00:03:02,560 --> 00:03:07,840
form, potentially including all the fields your 
application supports, and then having customers

38
00:03:07,840 --> 00:03:15,280
customize and style forms with our form content. 
The second method is about implementing a content

39
00:03:15,280 --> 00:03:20,320
dialogue on top of the form content block 
and building a user interface on top of the

40
00:03:20,320 --> 00:03:26,640
builder so users can either browse and select 
prebuilt forms or build a new form altogether.

41
00:03:26,640 --> 00:03:29,840
Let's show you how to do both. As mentioned,

42
00:03:29,840 --> 00:03:35,360
the simplest way to allow users to add forms 
in the Beefree SDK is by including a single

43
00:03:35,360 --> 00:03:41,520
default form in the configuration parameters. 
The final product can look something like this.

44
00:03:41,520 --> 00:03:47,520
This is a car loan pre-approval banking form. 
You can see that you can add your full name here,

45
00:03:47,520 --> 00:03:52,080
your credit score range, your car 
make and model, loan amount requested,

46
00:03:52,080 --> 00:03:58,000
and whether it's a used or new car. Now let's head 
to the code to show you how we implemented this.

47
00:03:58,000 --> 00:04:03,200
It's important to note that in this example, 
the JSON has been pre-pasted into the default

48
00:04:03,200 --> 00:04:08,800
form object. You can access this JSON through 
the link provided in the video description.

49
00:04:09,520 --> 00:04:13,280
First, let's scroll down to the Beefree 
configuration because this is the most

50
00:04:13,280 --> 00:04:17,360
important part of implementing the form 
block. If a developer does not include

51
00:04:17,360 --> 00:04:22,640
this default form parameter in their code, it 
will not be available in the builder. Here,

52
00:04:22,640 --> 00:04:27,840
you'll notice that I have my auto loan preapproval 
form here, and you'll need to ensure you have the

53
00:04:27,840 --> 00:04:32,960
right structure within your JSON for your 
form to load properly for your end users.

54
00:04:32,960 --> 00:04:37,520
Make sure to check out the GitHub repository, 
as we mentioned earlier, linked in the video

55
00:04:37,520 --> 00:04:41,520
description. That's where you'll find the 
validation schema to ensure you're using

56
00:04:41,520 --> 00:04:47,360
the correct properties when creating forms within 
the default form parameter. In our example here,

57
00:04:47,360 --> 00:04:54,400
you can see the structure we've created, which 
includes structure, then title, description

58
00:04:54,400 --> 00:05:01,280
fields, and all the different fields we have here. 
These are all properties that exist within the

59
00:05:01,280 --> 00:05:09,120
validation schema. Then you also have layout, 
which you can see here. Finally, attributes.

60
00:05:09,680 --> 00:05:14,800
This layout is super important because if 
we navigate back to the end user experience,

61
00:05:14,800 --> 00:05:21,280
we want to ensure this add new field button 
is visible. This won't appear if you don't

62
00:05:21,280 --> 00:05:28,640
have this layout section in your code, as well 
as these fields defined in this section here.

63
00:05:28,640 --> 00:05:34,080
After the submit button, you'll also 
notice number, long text, data list.

64
00:05:34,080 --> 00:05:38,720
All of these different properties have to be 
defined, and part of their definition is the

65
00:05:38,720 --> 00:05:45,360
data type, the label, the options, the 
attributes, and then remove from layout.

66
00:05:45,360 --> 00:05:50,000
Another important thing to remember is if 
I go over here, you'll notice that I have

67
00:05:50,000 --> 00:05:54,720
a few true or false Boolean options 
here. The option can be removed from

68
00:05:54,720 --> 00:06:00,640
layout. If this is set to true, then in 
the builder you'll have the delete button

69
00:06:00,640 --> 00:06:06,080
available here, and it's clickable so 
your end user can delete any field.

70
00:06:06,080 --> 00:06:09,680
A few other options you can 
customize are remove from layout,

71
00:06:09,680 --> 00:06:14,240
so if this is set to false, when the default 
form is dragged and dropped onto the stage,

72
00:06:14,240 --> 00:06:20,960
it automatically includes the first and last 
name fields. This can be modified. So if you

73
00:06:20,960 --> 00:06:24,720
want your users to be able to edit different 
fields in the form, you set this to true.

74
00:06:24,720 --> 00:06:29,680
For example, if we want to give the end user 
the ability to modify their credit score range,

75
00:06:29,680 --> 00:06:37,280
we can copy "can be modified: true" and 
paste it here and save this. Then if we

76
00:06:37,280 --> 00:06:44,320
head to the builder and drag and drop our 
form onto the canvas, then click on it,

77
00:06:44,320 --> 00:06:51,040
you'll notice that credit score range has an edit 
option here that we can click on and now edit.

78
00:06:51,600 --> 00:06:55,600
Now let's cover the second way you 
can enable forms for users in Beefree

79
00:06:55,600 --> 00:07:01,120
SDK. This method uses content dialogue 
and a custom UI on top of the builder,

80
00:07:01,120 --> 00:07:08,480
which allows users to browse and select from 
any number of pre-built forms. Here's my code,

81
00:07:08,480 --> 00:07:13,120
and you can see I have Beefree 
config and content dialogue.

82
00:07:13,120 --> 00:07:17,200
Content dialogue is the parameter that 
needs to be added to the Beefree config

83
00:07:17,200 --> 00:07:21,920
to activate the button that says 
edit label. If we scroll down,

84
00:07:21,920 --> 00:07:27,600
you'll notice that within content dialogue 
we have this section here, manage form. This

85
00:07:27,600 --> 00:07:32,880
object is crucial and needs to be included 
in order for this implementation to work.

86
00:07:32,880 --> 00:07:38,320
It includes a label which triggers the content 
dialogue, and it says edit form right now,

87
00:07:38,320 --> 00:07:44,080
which is what we want it to say. But if we wanted 
to change this text to say something different,

88
00:07:44,080 --> 00:07:49,840
like "select form" for instance, I can 
simply edit this label here. Then I

89
00:07:49,840 --> 00:07:55,200
have some logic that I use to manage 
the different forms that I've added.

90
00:07:55,200 --> 00:07:58,720
Basically, what's happening here is 
that when the content dialogue modal

91
00:07:58,720 --> 00:08:02,720
is triggered by an end user clicking 
the edit form button, they have the

92
00:08:02,720 --> 00:08:08,880
option to select one of these three different 
forms: the auto loan form, the mortgage form,

93
00:08:08,880 --> 00:08:14,880
or the credit card form. Now let me show you 
what this experience looks like on the front end.

94
00:08:14,880 --> 00:08:20,160
Here we have the same template as before, 
and let's say we want to add a form at the

95
00:08:20,160 --> 00:08:26,640
bottom of the page. We can drag and drop the 
form block. To change the form type, your end

96
00:08:26,640 --> 00:08:34,960
user can head to the edit form button and select 
any of the form variables we previously created.

97
00:08:34,960 --> 00:08:38,960
Now we're going to show you how to load 
your UI for form creation on top of the

98
00:08:38,960 --> 00:08:42,880
builder. That means your users will be 
able to create a new form and add it

99
00:08:42,880 --> 00:08:48,240
to the web content they're building without 
interrupting their workflow. Let me explain.

100
00:08:48,240 --> 00:08:52,800
In this example, we want to give the user 
the power to build their own custom forms.

101
00:08:52,800 --> 00:08:57,680
The experience looks like this: The end 
user drops the form block onto the stage

102
00:08:57,680 --> 00:09:03,360
and then clicks edit form to enter the 
form builder. This is a custom-built form

103
00:09:03,360 --> 00:09:07,920
builder that I created showcasing what 
the host application is truly capable of

104
00:09:07,920 --> 00:09:12,320
implementing. You can get super creative 
with how you design this experience.

105
00:09:12,320 --> 00:09:18,800
Now let's create a simple form for a personal 
loan. To do so, we can click on each field and

106
00:09:18,800 --> 00:09:24,560
modify the text to match the information we 
want to capture. Once we're done, we can hit

107
00:09:24,560 --> 00:09:31,600
save form. The form will then automatically load 
inside the builder. If I click into the form,

108
00:09:31,600 --> 00:09:36,640
I can still make changes like editing 
or deleting fields, for example. And if

109
00:09:36,640 --> 00:09:43,120
we scroll back up and click edit form, I can 
always go back and add new fields if I choose.

110
00:09:43,120 --> 00:09:48,640
Now, if we go to the code, let's look at what 
is working behind the scenes. At a high level,

111
00:09:48,640 --> 00:09:54,560
this advanced implementation builds on the same 
basic concepts as before with one key addition:

112
00:09:54,560 --> 00:09:57,760
a new variable called form structure.

113
00:09:57,760 --> 00:10:02,240
When a user creates a form, it is passed 
through the content dialogue modal that

114
00:10:02,240 --> 00:10:08,560
appears when the end user clicks edit form. 
This form data is then passed to default form,

115
00:10:08,560 --> 00:10:11,280
which is how it's able to load in the builder.

116
00:10:11,280 --> 00:10:16,560
This approach gives developers and technical 
teams the flexibility to apply different logic,

117
00:10:16,560 --> 00:10:23,280
customize configurations, and create a similar 
experience tailored to their end users' needs.

118
00:10:23,280 --> 00:10:29,520
To recap, here's a quick comparison of the two 
form block implementation methods. Method one,

119
00:10:29,520 --> 00:10:35,280
the quick setup, requires no content dialogue 
or custom UI. It just takes three steps:

120
00:10:35,280 --> 00:10:39,760
Enable the checkbox in the Beefree SDK 
developer console, add the default form

121
00:10:39,760 --> 00:10:45,440
parameter in the Beefree configuration, and 
pass valid JSON in the default form field.

122
00:10:45,440 --> 00:10:49,520
This loads the form automatically 
when users drag and drop the block.

123
00:10:49,520 --> 00:10:55,920
Method two is the custom setup. It uses content 
dialogue and a custom UI. For more flexibility,

124
00:10:55,920 --> 00:11:01,440
choose method one for simplicity or 
method two for a more tailored experience.

125
00:11:01,440 --> 00:11:06,960
Okay, now let's talk about what your end users 
can do with the front-end customization of

126
00:11:06,960 --> 00:11:11,680
the form block. When an end user drags 
the form block onto their landing page,

127
00:11:11,680 --> 00:11:14,960
the sidebar provides full customization controls.

128
00:11:14,960 --> 00:11:20,640
As we showed earlier, you can start by selecting 
a form using the edit form button, which allows

129
00:11:20,640 --> 00:11:27,040
your end users to choose from prebuilt forms. 
Other customization options include layout,

130
00:11:27,040 --> 00:11:33,440
which lets you set the width, alignment, font 
family, weight, and size to match the page design.

131
00:11:33,440 --> 00:11:38,160
Manage fields lets you add, edit, 
or rearrange up to 10 field types,

132
00:11:38,160 --> 00:11:43,440
including multiple choice, email, 
drop-down, phone, and text fields.

133
00:11:43,440 --> 00:11:46,640
Label options allow you to format label text,

134
00:11:46,640 --> 00:11:51,760
choose top or side positioning, and 
adjust width when using side labels.

135
00:11:51,760 --> 00:11:54,560
With field options, you can 
customize background color,

136
00:11:54,560 --> 00:12:00,240
borders, selected field styles, and input 
text color for clarity and consistency.

137
00:12:00,240 --> 00:12:05,840
Finally, button options give you control to 
style the submit button with custom fonts,

138
00:12:05,840 --> 00:12:10,560
colors, and alignment for a cohesive 
look. By leveraging these options,

139
00:12:10,560 --> 00:12:15,920
users can quickly build a polished, 
on-brand form—no coding required.

140
00:12:15,920 --> 00:12:19,760
To wrap up, the Beefree Form Block 
is a powerful feature that lets you

141
00:12:19,760 --> 00:12:25,360
build sophisticated end-user experiences 
that are customizable and easy to use.

142
00:12:25,360 --> 00:12:30,960
Developers, you are in control. Just check the 
box in the developer console to enable the form

143
00:12:30,960 --> 00:12:37,040
feature to make life easy for your end users. You 
can create default forms, a custom no-code form

144
00:12:37,040 --> 00:12:43,120
builder in the UI, or even an entire form library 
for your end users to choose from. Best of all,

145
00:12:43,120 --> 00:12:48,960
your end users can enjoy a no-code tool that still 
allows them to further customize every detail.

146
00:12:48,960 --> 00:12:52,000
From form properties to field and button styles,

147
00:12:52,000 --> 00:12:56,080
this lets them achieve the 
perfect look to match their brand.
```
{% endtab %}
{% endtabs %}
