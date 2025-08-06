# How to Import HTML Emails into Beefree SDK with the New HTML Importer API

{% embed url="https://www.youtube.com/watch?v=9O2mlbvFskc" %}

{% tabs %}
{% tab title="About" %}
Want to turn static HTML emails into fully editable Beefree SDK templates in seconds? In this video, we’ll show you exactly how to use the new Beefree SDK HTML Importer API to programmatically convert existing HTML email templates into editable JSON. Whether you're a developer, SaaS product team, or onboarding specialist, this video breaks down how to transform raw HTML emails into Beefree compatible designs — without the need to rebuild them from scratch. Learn how to enable the HTML Importer, set up the API, structure your HTML correctly, authenticate your requests, and embed this tool into your own application.&#x20;

**Chapters:**&#x20;

* [0:00](https://www.youtube.com/watch?v=9O2mlbvFskc) - Intro
* [0:50](https://www.youtube.com/watch?v=9O2mlbvFskc\&t=50s) - Real-world use cases for the HTML Importer API
* [1:51](https://www.youtube.com/watch?v=9O2mlbvFskc\&t=111s) - What the HTML Importer actually does
* [2:47](https://www.youtube.com/watch?v=9O2mlbvFskc\&t=167s) - How to enable the HTML Importer in the SDK Developer Console
* [3:56](https://www.youtube.com/watch?v=9O2mlbvFskc\&t=236s) - Authenticating and making your first API call
* [5:27](https://www.youtube.com/watch?v=9O2mlbvFskc\&t=327s) - Preparing your HTML for conversion (doctypes, tags, structure).
* [7:32](https://www.youtube.com/watch?v=9O2mlbvFskc\&t=452s) - Embedding HTML Importer in your workflow
* [8:03](https://www.youtube.com/watch?v=9O2mlbvFskc\&t=483s) - Live demo: HTML to JSON conversion
* [8:56](https://www.youtube.com/watch?v=9O2mlbvFskc\&t=536s) - Key takeaways
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
1
00:00:02,880 --> 00:00:08,320
What if transforming HTML email templates 
into editable Beefree content only took

2
00:00:08,320 --> 00:00:13,920
seconds? From conversations with our customers, 
we’ve heard it can take up to two hours just to

3
00:00:13,920 --> 00:00:19,600
rebuild a single email starting from 
raw HTML. With the new HTML Importer,

4
00:00:19,600 --> 00:00:25,200
you can programmatically turn existing 
email HTML into Beefree JSON with a single

5
00:00:25,200 --> 00:00:31,840
API call—transforming your templates into 
fully editable content in seconds, not hours.

6
00:00:31,840 --> 00:00:35,600
This video will guide you through 
the HTML Importer and how it works,

7
00:00:35,600 --> 00:00:40,640
in five easy-to-follow sections. 
We’ll cover real-world use cases,

8
00:00:40,640 --> 00:00:44,640
how it works, how to use it, 
embedding it into your workflow,

9
00:00:44,640 --> 00:00:50,960
and we’ll walk through a full HTML template 
example and the JSON returned from the API.

10
00:00:50,960 --> 00:00:57,440
To kick things off, let’s look at some real-world 
use cases for the HTML Importer. Slow, cumbersome

11
00:00:57,440 --> 00:01:02,960
migration processes? They’re a thing of the past. 
If you're new to the Beefree SDK, you can migrate

12
00:01:02,960 --> 00:01:08,800
all your legacy templates without asking your 
customers to manually recreate every single one.

13
00:01:08,800 --> 00:01:13,280
Do you regularly onboard new users who’d 
love to keep using the templates they

14
00:01:13,280 --> 00:01:17,520
already have? The HTML Importer lets 
them import their designs and gives

15
00:01:17,520 --> 00:01:21,920
them instant editing power—without 
the usual migration headaches.

16
00:01:21,920 --> 00:01:26,320
Or maybe you have a professional services 
team that helps new users migrate their

17
00:01:26,320 --> 00:01:32,160
templates. With the Importer API, that job 
just got a whole lot easier and faster.

18
00:01:32,160 --> 00:01:37,360
No matter how you plan to use the HTML 
Importer, it will dramatically streamline

19
00:01:37,360 --> 00:01:41,600
your processes. This isn’t just about 
saving time—it’s about empowering your

20
00:01:41,600 --> 00:01:46,000
users to finally embrace modern email 
builders without the heavy lifting,

21
00:01:46,000 --> 00:01:52,000
unlocking faster onboarding, happier customers, 
and a smoother workflow for everyone.

22
00:01:52,000 --> 00:01:56,640
Now let’s quickly talk about what 
the HTML Importer API actually does.

23
00:01:56,640 --> 00:02:03,120
It takes static HTML emails and transforms 
them into Beefree SDK’s native JSON format,

24
00:02:03,120 --> 00:02:07,200
ready to load in the builder for quick 
editing. This is great for teams looking

25
00:02:07,200 --> 00:02:12,160
to migrate existing templates or 
upload HTML templates to edit.

26
00:02:12,160 --> 00:02:16,880
Now let’s talk about how to use it—but 
before we do, one quick note: The email

27
00:02:16,880 --> 00:02:22,160
example we’ll be showing in this video comes from 
reallygoodemails.com and is used strictly for

28
00:02:22,160 --> 00:02:29,040
demonstration purposes. This example is intended 
to show how the HTML Importer API works and should

29
00:02:29,040 --> 00:02:34,960
not be seen as an endorsement or encouragement 
to copy or reuse another brand’s content.

30
00:02:34,960 --> 00:02:39,360
So, we kindly ask that you use 
any email inspiration responsibly.

31
00:02:39,360 --> 00:02:44,320
Okay—when you’re ready to transform your 
HTML email templates into editable designs

32
00:02:44,320 --> 00:02:47,760
inside the Beefree builder, here’s how to do it.

33
00:02:47,760 --> 00:02:51,280
Step one: Enable the HTML Importer API

34
00:02:51,280 --> 00:02:57,440
Before anything else, you need to enable the 
HTML Importer API for your SDK application.

35
00:02:59,440 --> 00:03:03,440
Make sure you’re logged into the 
Beefree SDK developer console. Next,

36
00:03:03,440 --> 00:03:10,080
select your application—in this example, 
our email builder. Click on “Details.”

37
00:03:11,040 --> 00:03:18,880
Now, scroll down to the section labeled HTML 
Importer API, then click “Enable the service

38
00:03:18,880 --> 00:03:27,520
and generate an API key.” You’ll see a 
popup confirming that additional fees

39
00:03:27,520 --> 00:03:33,520
may apply when using this feature. Click 
“Save,” and your API key is now available.

40
00:03:33,520 --> 00:03:37,680
This key is required for authentication, 
so be sure to keep it safe.

41
00:03:37,680 --> 00:03:39,360
It’s also worth noting that you can set

42
00:03:39,360 --> 00:03:44,320
up the HTML Importer with a free 
account—no paid plan is needed.

43
00:03:52,640 --> 00:03:56,800
Step two: Copy HTML and authenticate your API key

44
00:03:56,800 --> 00:04:01,920
Now we’ll jump into the Beefree SDK docs, 
where you’ll find details about how the

45
00:04:01,920 --> 00:04:07,040
API works—and where you can test 
it in our interactive playground.

46
00:04:07,600 --> 00:04:17,040
First, navigate to the API section, click 
on HTML Importer API, and then Import HTML.

47
00:04:17,040 --> 00:04:34,080
Scroll down to see the prerequisites—which 
we’ll talk about more in a second—and the

48
00:04:34,080 --> 00:04:35,920
API call setup (for example, making sure 
your method is POST). At the very bottom,

49
00:04:35,920 --> 00:04:40,400
you’ll find the testing 
environment. Click “Test it.”

50
00:04:41,040 --> 00:04:48,560
A window will pop up. You can expand it using 
the top-right button. You'll see information

51
00:04:48,560 --> 00:04:55,120
pre-populated here, including the URL 
and a placeholder for the collection,

52
00:04:55,120 --> 00:04:58,000
which we’ll later set to conversion.

53
00:04:58,640 --> 00:05:03,280
Before authenticating our API 
key, let’s first grab the HTML.

54
00:05:03,920 --> 00:05:09,920
Head to reallygoodemails.com. I’ve 
pre-selected an email that celebrates

55
00:05:09,920 --> 00:05:14,720
how awesome dogs are—and I love the 
layout, so I want to repurpose it.

56
00:05:19,040 --> 00:05:23,760
Copy the HTML. Head back to the playground,

57
00:05:23,760 --> 00:05:29,440
scroll down to the “body” section, 
click “Other,” and paste in the HTML.

58
00:05:31,040 --> 00:05:35,040
Step three: Structure your HTML before sending

59
00:05:35,040 --> 00:05:41,280
Correct formatting is critical for successful 
conversion. If your HTML is missing key elements

60
00:05:41,280 --> 00:05:46,000
or doesn’t follow standard structure, 
we can’t properly convert the design.

61
00:05:46,000 --> 00:05:50,320
To prepare your HTML for smooth 
conversion, make sure it includes:

62
00:05:50,320 --> 00:05:52,620
A DOCTYPE declaration

63
00:05:52,620 --> 00:05:54,960
Opening and closing html and body tags

64
00:05:54,960 --> 00:05:59,440
A meta charset="UTF-8" tag in the <head>

65
00:05:59,440 --> 00:06:05,200
Remove anything unexpected—like merge tags or 
scripts—especially if they’re outside the body or

66
00:06:05,200 --> 00:06:10,800
at the end of the file. Poor structure can cause 
the conversion to fail or generate corrupted JSON.

67
00:06:11,360 --> 00:06:15,520
Clean, well-structured HTML = best results.

68
00:06:15,520 --> 00:06:20,240
Now that our HTML is ready, we can 
complete the authentication step.

69
00:06:20,240 --> 00:06:22,960
Head back to the Beefree SDK developer console,

70
00:06:22,960 --> 00:06:28,852
copy your API key, and paste it into the 
authentication section as a Bearer Token.

71
00:06:28,852 --> 00:06:31,040
Make sure you select Bearer Token 
as the authentication method—this is

72
00:06:35,296 --> 00:06:41,600
required for Beefree SDK’s API calls.

73
00:06:42,720 --> 00:06:46,480
Step four: Import HTML via the API

74
00:06:47,680 --> 00:06:49,600
We need to input a few key 
values before converting

75
00:06:49,600 --> 00:06:52,880
our static HTML into Beefree’s editable JSON.

76
00:06:53,760 --> 00:06:58,960
We’ve already pasted our HTML 
and added our API key. Now:

77
00:06:59,840 --> 00:07:03,280
Set collection to conversion

78
00:07:03,280 --> 00:07:07,920
Set Content-Type to text/html

79
00:07:11,440 --> 00:07:13,040
Click “Send.” If everything’s set 
up correctly, you should receive

80
00:07:13,040 --> 00:07:16,560
a 200 response, confirming a successful call.

81
00:07:20,320 --> 00:07:24,320
On the right, you’ll see the JSON. This is Beefree

82
00:07:24,320 --> 00:07:32,160
SDK’s proprietary format—what gets 
loaded into the builder for editing.

83
00:07:32,160 --> 00:07:35,040
Step five: Embed in your workflow

84
00:07:35,040 --> 00:07:41,760
You can use this API however it fits your 
team’s workflow. One common use case:

85
00:07:41,760 --> 00:07:48,960
adding an Import HTML button to your app that 
lets users upload their HTML with a single click.

86
00:07:50,000 --> 00:08:00,960
We’ve made that easy—sample code is available 
in our docs and linked in the video description.

87
00:08:00,960 --> 00:08:03,440
Let’s try it out together.

88
00:08:03,440 --> 00:08:16,800
Using our demo environment, we’ll copy 
the same HTML from reallygoodemails.com,

89
00:08:16,800 --> 00:08:27,440
paste it into the Import 
HTML modal, and click Import.

90
00:08:27,440 --> 00:08:35,120
Give it a second—and just like that, the email 
is now loaded in the Beefree SDK builder.

91
00:08:37,200 --> 00:08:41,520
You’ll notice how all the 
elements—images, buttons,

92
00:08:41,520 --> 00:08:45,440
and layout—are now editable Beefree blocks.

93
00:08:46,320 --> 00:08:48,880
Once you load that JSON into the editor,

94
00:08:48,880 --> 00:08:56,800
most of the heavy lifting is done. Users 
can tweak the design or polish it as needed.

95
00:08:56,800 --> 00:09:02,400
Think of it as 95% done, with full 
control to customize the rest.

96
00:09:02,400 --> 00:09:04,640
Let’s wrap with a quick summary:

97
00:09:05,280 --> 00:09:10,400
The HTML Importer converts static 
HTML into Beefree JSON via API

98
00:09:10,400 --> 00:09:12,240
It requires well-formatted HTML

99
00:09:13,440 --> 00:09:18,800
Use POST + text/html + 
authentication via Bearer Token

100
00:09:18,800 --> 00:09:21,280
Response is ready-to-edit JSON

101
00:09:21,280 --> 00:09:23,760
Final edits can be made in the builder

102
00:09:23,760 --> 00:09:27,120
Choose this if you want to cut 
down on manual rebuilding and

103
00:09:27,120 --> 00:09:31,120
support smart migrations or quick HTML uploads.

104
00:09:31,120 --> 00:09:31,840
That’s a wrap.

105
00:09:31,840 --> 00:09:38,240
The HTML Importer makes it easier than ever to 
bring HTML templates into Beefree SDK. It’s fast,

106
00:09:38,240 --> 00:09:41,120
flexible, and saves time for both 
internal teams and end users.

107
00:09:46,480 --> 00:09:51,280
No need to rebuild templates from 
scratch—just import and edit.

108
00:09:55,760 --> 00:09:59,920
For more information on pricing, 
implementation, and getting started,

109
00:09:59,920 --> 00:10:04,080
check out the developer docs 
linked in the description.

110
00:10:04,080 --> 00:10:07,520
Thanks for watching.
```
{% endtab %}
{% endtabs %}
