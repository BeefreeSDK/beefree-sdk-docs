# Hosted Saved Rows: A Faster Way to Save and Reuse Content

{% embed url="https://www.youtube.com/watch?v=5m80DgKW0x8" %}

{% tabs %}
{% tab title="About" %}
Are your users stuck recreating the same email header or footer over and over? Stop the endless copying and pasting! In this video, you'll discover how Hosted Saved Rows in Beefree SDK can help your end users work smarter—saving time while keeping their email and landing page designs perfectly consistent.&#x20;

What You’ll Learn:&#x20;

✅ What are Saved Rows and how they work in Beefree SDK&#x20;

✅ The difference between rows vs. saved rows&#x20;

✅ How Saved Rows improve workflow efficiency and branding consistency&#x20;

✅ The two options for implementing Saved Rows: Hosted vs. Self-Hosted&#x20;

✅ How to enable Hosted Saved Rows in just one toggle&#x20;

✅ Managing and organizing Saved Rows for seamless design updates&#x20;

✅ Advanced permissions for better control over design elements&#x20;

**Chapters:**

* [0:00](https://www.youtube.com/watch?v=5m80DgKW0x8) - Intro&#x20;
* [0:26](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=26s) - What is a Saved Row?&#x20;
* [0:53](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=53s) - Lesson overview&#x20;
* [1:50](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=110s) - Rows vs. Saved Rows in Beefree SDK&#x20;
* [2:33](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=153s) - The benefits of using Saved Rows&#x20;
* [3:14](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=194s) - The difference between Hosted vs. Self-Hosted Saved Rows&#x20;
* [4:29](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=269s) - How to enable Hosted Saved Rows&#x20;
* [5:12](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=312s) - How your users mange Saved Rows in the builder&#x20;
* [6:10](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=370s) - How Hosted Saved Rows are stored&#x20;
* [6:45](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=405s) - Using Advanced Permissions to control what your users can and cannot do&#x20;
* [8:25](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=505s) - Recap&#x20;
* [8:59](https://www.youtube.com/watch?v=5m80DgKW0x8\&t=539s) - Outro
{% endtab %}

{% tab title="Transcripts" %}
The following text includes the complete transcript for this video.

```
1
00:00:02,920 --> 00:00:08,080
Let's talk about that header or footer, the 
one your user absolutely nailed. It's clean,

2
00:00:08,080 --> 00:00:13,440
perfectly branded, and makes their emails and 
pages look sharp. It's a tiny masterpiece. But

3
00:00:13,440 --> 00:00:18,840
here's the problem: every time they want to use 
it again, they're stuck recreating it from scratch

4
00:00:18,840 --> 00:00:24,800
or, worse, digging through old designs to copy and 
paste that piece of content into your new design.

5
00:00:24,800 --> 00:00:29,960
That's where the magic of Saved Rows comes in. 
With Saved Rows, your users can lock in those

6
00:00:29,960 --> 00:00:36,280
beautifully crafted sections—headers, footers, 
product showcases, you name it—and reuse them

7
00:00:36,280 --> 00:00:42,200
whenever and wherever they need. No tedious 
recreating, no endless copying and pasting. Just

8
00:00:42,200 --> 00:00:47,560
drag and drop, and they're good to go. Saved Rows 
is the perfect solution for your end users who are

9
00:00:47,560 --> 00:00:53,240
looking to save time while keeping their designs 
clean and consistent across different projects.

10
00:00:53,240 --> 00:00:56,080
In this video, we're going to talk all about Saved

11
00:00:56,080 --> 00:00:59,920
Rows and how you can make the most 
of this feature for your end users.

12
00:00:59,920 --> 00:01:02,080
What are Rows and Saved Rows in Beefree SDK?
First, we'll break down the difference between

13
00:01:02,080 --> 00:01:08,040
rows and Saved Rows in Beefree SDK. After that, 
we'll highlight the benefits of Saved Rows,

14
00:01:08,040 --> 00:01:13,040
showing how they can save your end users 
time and boost efficiency. From there,

15
00:01:13,040 --> 00:01:18,240
we'll explain the two flexible options for 
implementing Saved Rows in Beefree SDK:

16
00:01:18,240 --> 00:01:21,680
Hosted Saved Rows and Self-Hosted Saved Rows.

17
00:01:21,680 --> 00:01:25,680
Next, we'll dive into the developer 
console and demonstrate how easy it

18
00:01:25,680 --> 00:01:31,360
is to enable Hosted Saved Rows. Spoiler 
alert: it's just one toggle! We'll also

19
00:01:31,360 --> 00:01:36,680
walk you through how your end users can manage 
and organize Saved Rows within their designs.

20
00:01:36,680 --> 00:01:41,040
Finally, for those of you who'd like to take 
things one step further, we'll explain how to

21
00:01:41,040 --> 00:01:46,760
set up Advanced Permissions inside your Beefree 
SDK configuration. This allows you to manage

22
00:01:46,760 --> 00:01:53,680
which specific actions your end users can perform 
when using Hosted Saved Rows within Beefree SDK.

23
00:01:53,680 --> 00:01:57,880
Rows are the building blocks that let 
your end users structure, organize,

24
00:01:57,880 --> 00:02:02,680
and design their content with precision. 
They're a powerful way to create layouts

25
00:02:02,680 --> 00:02:08,480
that adapt to any design need. The first step 
every content creator takes in the Beefree SDK

26
00:02:08,480 --> 00:02:14,600
Builder is to drag and drop a row onto the 
stage. This is where the magic begins. Rows

27
00:02:14,600 --> 00:02:20,360
provide the foundation for adding content blocks 
and designing layouts that bring ideas to life.

28
00:02:20,360 --> 00:02:24,360
But while regular rows are built 
for flexibility and customization,

29
00:02:24,360 --> 00:02:28,920
Saved Rows take things a step further. 
They allow your end users to save the

30
00:02:28,920 --> 00:02:34,418
rows they've already designed for 
convenient reuse in future projects.

31
00:02:34,418 --> 00:02:36,680
Benefits of Saved Rows
Saved Rows aren't just convenient;

32
00:02:36,680 --> 00:02:40,000
they're a total game-changer. And here's why:

33
00:02:40,000 --> 00:02:44,800
Save time: Skip the repetitive work 
of rebuilding sections from scratch.

34
00:02:44,800 --> 00:02:48,960
Maintain design consistency: 
Ensure key components like headers,

35
00:02:48,960 --> 00:02:53,720
footers, or product showcases remain 
perfectly aligned with your brand.

36
00:02:53,720 --> 00:03:00,000
Avoid the blank page: Repurpose existing 
content as a starting point for new designs.

37
00:03:00,000 --> 00:03:05,760
Increase efficiency: Focus more on 
creativity and strategy, not busy work.

38
00:03:05,760 --> 00:03:09,840
With Saved Rows in Beefree SDK, 
your end users can work smarter,

39
00:03:09,840 --> 00:03:15,327
not harder, while keeping their designs 
fresh, consistent, and easy to manage.

40
00:03:15,327 --> 00:03:17,800
Hosted vs. Self-Hosted Saved Rows
For teams looking to implement Saved Rows,

41
00:03:17,800 --> 00:03:21,040
we offer two flexible options based on your needs:

42
00:03:22,000 --> 00:03:27,400
Hosted Saved Rows and Self-Hosted Saved Rows. 
Let's quickly break down the differences

43
00:03:27,400 --> 00:03:32,383
to show you how Hosted and Self-Hosted 
Saved Rows are configured and managed.

44
00:03:32,383 --> 00:03:34,080
Hosted Saved Rows
Hosted Saved Rows are ideal

45
00:03:34,080 --> 00:03:40,000
for teams looking for a quick, hassle-free 
setup. Everything is managed by Beefree SDK,

46
00:03:40,000 --> 00:03:44,440
so you can activate it with a toggle 
in the developer console. This option

47
00:03:44,440 --> 00:03:49,720
provides centralized storage, security, 
and reliability, along with an easy-to-use

48
00:03:49,720 --> 00:03:54,960
interface to save and reuse rows within your 
app. It's perfect if you don't want to manage

49
00:03:54,960 --> 00:04:01,618
back-end systems and you just want to bring the 
power of reusable content to your users fast.

50
00:04:01,618 --> 00:04:02,560
Self-Hosted Saved Rows
Now, if you need full

51
00:04:02,560 --> 00:04:07,760
control over how and where rows are stored, 
Self-Hosted Saved Rows might be the way to

52
00:04:07,760 --> 00:04:14,120
go. This option is best for teams with specific 
compliance or integration needs and requires

53
00:04:14,120 --> 00:04:19,560
development resources to manage storage 
and build an interface for row management.

54
00:04:19,560 --> 00:04:24,400
We won't dive too deep into the details here, 
but if you'd like to learn more, check out our

55
00:04:24,400 --> 00:04:29,720
video tutorial and technical documentation, 
which I've linked in the video description.

56
00:04:29,720 --> 00:04:31,440
Setting up Hosted Saved Rows
Now, let's show you how to set

57
00:04:31,440 --> 00:04:37,120
up Hosted Saved Rows. First, let's enable 
Hosted Saved Rows for your application.

58
00:04:37,120 --> 00:04:40,000
We'll need to log into the developer console.

59
00:04:40,000 --> 00:04:44,200
Then, we can navigate to the 
application you'd like to configure.

60
00:04:44,200 --> 00:04:49,760
Click on Details, then View More 
under Application Configuration.

61
00:04:49,760 --> 00:04:52,840
We can scroll to the Saved Row section and then

62
00:04:52,840 --> 00:04:58,040
toggle on the option for Hosted 
on the Beefree SDK Infrastructure.

63
00:04:58,040 --> 00:05:03,640
Finally, we can review the pricing details 
and confirm to activate the feature.

64
00:05:03,640 --> 00:05:07,920
Congrats! You've officially enabled 
Hosted Saved Rows in under a minute,

65
00:05:07,920 --> 00:05:11,305
and your users can immediately 
start saving and reusing content.

66
00:05:11,305 --> 00:05:12,560
Managing Saved Rows

67
00:05:12,560 --> 00:05:17,360
Now that Hosted Saved Rows are enabled, 
here's how end users can manage them:

68
00:05:17,360 --> 00:05:20,480
You can save your row directly 
inside the Builder by selecting

69
00:05:20,480 --> 00:05:25,520
it and then clicking the save icon. To 
keep your row organized and easy to find,

70
00:05:25,520 --> 00:05:29,920
you can give them clear names. Under 
Row Name, we can call this "Header."

71
00:05:29,920 --> 00:05:35,360
We can then add this row to either a new or 
existing category to make it easy to find. Let's

72
00:05:35,360 --> 00:05:42,840
create a new category and call it "Headers for 
Flower Emails." You can then hit the Save button.

73
00:05:42,840 --> 00:05:46,760
Next, go to the Row section, 
click on the dropdown menu,

74
00:05:46,760 --> 00:05:51,240
and from the options, select "Headers for 
Flower Emails." You'll see your Saved Row

75
00:05:51,240 --> 00:05:55,920
appear there. Simply drag it onto the 
canvas to start using it right away.

76
00:05:55,920 --> 00:06:00,240
At any time, you can edit, reuse, and 
delete a Saved Row by clicking on the

77
00:06:00,240 --> 00:06:04,480
three dots here. By selecting Edit 
Info, you can edit the name of the

78
00:06:04,480 --> 00:06:11,000
Saved Row and even change the category. 
To save your changes, just hit Update.

79
00:06:11,000 --> 00:06:15,680
Keep in mind that we will store your end 
users' Hosted Saved Rows securely in a

80
00:06:15,680 --> 00:06:19,760
Beefree S3 bucket. Each row will 
be exclusively used for the given

81
00:06:19,760 --> 00:06:25,240
UID belonging to the subscription. As a 
reminder, we're proud to be SOC 2, ISO,

82
00:06:25,240 --> 00:06:32,200
and GDPR compliant. You can read more about 
our security measures at beefree.io/security.

83
00:06:32,200 --> 00:06:35,640
It's important to mention that 
this is a premium feature and

84
00:06:35,640 --> 00:06:40,040
that usage-based fees may apply 
for using Hosted Saved Rows. You

85
00:06:40,040 --> 00:06:45,100
can reference our usage-based fees 
documentation for additional details.

86
00:06:45,100 --> 00:06:46,080
Advanced Permissions
Now, what if you'd like to

87
00:06:46,080 --> 00:06:51,760
customize how specific groups of users can 
interact with your new Saved Row feature?

88
00:06:51,760 --> 00:06:57,560
For example, maybe you want admins to enjoy 
full access to add, manage, and delete rows,

89
00:06:57,560 --> 00:07:03,280
while copywriters can only add and manage but not 
delete them. Or perhaps you could limit saving and

90
00:07:03,280 --> 00:07:09,760
reusing content for premium tier users to support 
your app's business model and encourage upgrades.

91
00:07:09,760 --> 00:07:13,560
That's where Advanced Permissions comes 
in. That's your tool for controlling what

92
00:07:13,560 --> 00:07:17,960
users can and cannot do in your 
application. Hosted Saved Rows

93
00:07:17,960 --> 00:07:22,560
includes the following Advanced Permission 
options. Keep in mind that each of these

94
00:07:22,560 --> 00:07:28,120
options are boolean within your Beefree SDK 
configuration. This means if set to true,

95
00:07:28,120 --> 00:07:33,440
the end user can perform that action, and if 
set to false, they can't perform that action.

96
00:07:33,440 --> 00:07:37,720
Let me show you how easy it is to 
adjust Advanced Permissions. It's

97
00:07:37,720 --> 00:07:42,680
all done via the Advanced Permissions object 
in your config file, and you can see how we

98
00:07:42,680 --> 00:07:48,520
defined rows and behavior objects nested 
within it. Inside the behaviors object,

99
00:07:48,520 --> 00:07:53,240
you can see that we've set the 
canDeleteHostedRow property to true.

100
00:07:53,240 --> 00:07:59,560
Let's check out the end-user experience now. If we 
select a row and then click the three dots here,

101
00:07:59,560 --> 00:08:04,360
the user is able to click on this Delete 
button, and then once inside the modal,

102
00:08:04,360 --> 00:08:08,560
they can confirm that they do in fact 
want to remove this Saved Row. Okay,

103
00:08:08,560 --> 00:08:14,840
great. Now let's jump back into the code and 
change that value to false. If we head back

104
00:08:14,840 --> 00:08:20,040
to the end-user experience and then try 
clicking on a row, you can see that the

105
00:08:20,040 --> 00:08:25,340
user is no longer able to delete the Saved 
Row based on the permission we've just set.

106
00:08:25,340 --> 00:08:26,440
Recap
Okay,

107
00:08:26,440 --> 00:08:29,600
that wraps up this video. 
Let's recap what we learned:

108
00:08:29,600 --> 00:08:34,000
We covered the key differences between 
rows and Saved Rows in Beefree SDK.

109
00:08:34,000 --> 00:08:38,720
We discussed how rows can save time and 
improve efficiency for your end users.

110
00:08:38,720 --> 00:08:41,240
Then we explored the two implementation options,

111
00:08:41,240 --> 00:08:45,280
Hosted and Self-Hosted Saved Rows, 
and demonstrated how easy it is to

112
00:08:45,280 --> 00:08:49,760
enable Hosted Saved Rows with just 
one toggle in the developer console.

113
00:08:49,760 --> 00:08:53,040
We also showed how your end users 
can manage their Saved Rows.

114
00:08:53,040 --> 00:08:55,240
And finally, we covered setting up Advanced

115
00:08:55,240 --> 00:08:59,000
Permissions to control what 
your users can and cannot do.

116
00:08:59,000 --> 00:09:02,760
By adding Saved Rows to your application, 
you can help users save time,

117
00:09:02,760 --> 00:09:07,800
maintain design consistency, and boost 
satisfaction. And with Hosted Saved Rows,

118
00:09:07,800 --> 00:09:18,480
you can activate this powerful feature 
in seconds just by toggling it on.
```
{% endtab %}
{% endtabs %}
