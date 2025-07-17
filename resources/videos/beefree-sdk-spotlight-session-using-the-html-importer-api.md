---
description: >-
  Learn more about integrating the HTML Importer API into your application, and
  empowering your end users to upload their email HTML templates into the
  Beefree SDK builder.
---

# Beefree SDK Spotlight Session: Using the HTML Importer API

{% embed url="https://www.youtube.com/watch?v=EkcLaDR2kpc" %}

{% tabs %}
{% tab title="About" %}
Catch the on-demand recording of our 30-minute webinar, now available whenever you’re ready. In this session, we walk you through the new HTML Importer API—showing you step by step how to integrate an “Import” button into your custom Beefree SDK setup and embed it seamlessly within your interface. You’ll also learn to leverage the Brand Style Management endpoint, empowering your users to update templates instantly with their latest brand guidelines. Stick around until the end for our lively, open Q\&A—where our team answers your most pressing questions!&#x20;

**Chapters:**&#x20;

* [0:00](https://www.youtube.com/watch?v=EkcLaDR2kpc) Introduction to the HTML Importer API&#x20;
* [8:07](https://www.youtube.com/watch?v=EkcLaDR2kpc\&t=487s) Enabling the HTML Importer API&#x20;
* [9:21](https://www.youtube.com/watch?v=EkcLaDR2kpc\&t=561s) Implementing the HTML Importer API (Demo Part 1)&#x20;
* [14:25](https://www.youtube.com/watch?v=EkcLaDR2kpc\&t=865s) Combining with Brand Style Management API (Demo Part 2)&#x20;
* [20:02](https://www.youtube.com/watch?v=EkcLaDR2kpc\&t=1202s) Q\&A Session
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
1
00:00:02,000 --> 00:00:03,840
Good morning, good afternoon, and good evening,

2
00:00:03,840 --> 00:00:06,000
depending on where you're joining 
us from around the world. Welcome

3
00:00:06,000 --> 00:00:11,440
to this session of the spotlight series 
from Beefree, specifically Beefree SDK.

4
00:00:11,440 --> 00:00:14,800
Today, I'm Lawrence, your host 
and Senior Developer Advocate.

5
00:00:14,800 --> 00:00:18,400
I'm here with my friend Luca, 
Senior Fullstack Developer and

6
00:00:18,400 --> 00:00:24,800
Technical Presenter. Our topic for 
the day is the HTML Importer API.

7
00:00:25,680 --> 00:00:29,280
As you're all coming in, feel free to hop into 
the chat and leave your name and location.

8
00:00:29,280 --> 00:00:34,080
It's always nice to give a shout-out to our 
visitors, all of our users, future users,

9
00:00:34,080 --> 00:00:38,640
and even fellow employees. We love to hear where 
you're from and shout out your hometown because we

10
00:00:38,640 --> 00:00:44,560
have not only a global workforce but also a global 
user base. We definitely love to shout you out!

11
00:00:44,560 --> 00:00:50,560
Speaking of global, Luca, you and I are 
both settling in from a pretty exciting

12
00:00:50,560 --> 00:00:57,120
event last week. We had a week-long retreat 
on the sunny beaches of Spain. I just kept

13
00:00:57,120 --> 00:01:01,200
thinking, "They're working me too hard! 
They're working me way too hard!" Luca,

14
00:01:01,200 --> 00:01:04,640
let me hear your feedback. How 
are you feeling after last week?

15
00:01:04,640 --> 00:01:12,000
It went great! I got a lot of stuff done, and 
I spent an amazing time with our colleagues,

16
00:01:12,000 --> 00:01:17,120
getting to know new colleagues better 
and getting in touch with old friends

17
00:01:17,120 --> 00:01:20,880
and colleagues that I already met at 
previous retreats. What about you,

18
00:01:20,880 --> 00:01:24,880
Lawrence? This was your first 
experience with us at our retreat.

19
00:01:24,880 --> 00:01:30,080
Listen, I just kept thinking to myself, 
"For real, best first month ever!" Get

20
00:01:30,080 --> 00:01:33,760
hired in one month, get flown to Europe 
for the next month for an entire week,

21
00:01:33,760 --> 00:01:38,800
all expenses paid. That was incredible! But you 
know, it's interesting, prior to the retreat,

22
00:01:38,800 --> 00:01:44,400
I had never seen a single co-worker in 
person—not even my boss, not HR, no one.

23
00:01:44,400 --> 00:01:50,000
So, all of a sudden, I get to see the majority of 
the company all together, collaborate with them,

24
00:01:50,000 --> 00:01:54,560
have sessions, have breakout sessions, get 
their feedback on some things that I thought,

25
00:01:54,560 --> 00:02:00,320
and get some good positive responses for some 
and some gentle corrections for others. But it

26
00:02:00,320 --> 00:02:04,400
was all great because we were in person, 
and getting that feedback, and of course,

27
00:02:04,400 --> 00:02:09,600
the pool time and beach time, helped as well. So, 
I'm excited. We have some amazing initiatives that

28
00:02:09,600 --> 00:02:15,920
I heard talked about just last week, so it's 
going to be a really exciting year for Beefree.

29
00:02:15,920 --> 00:02:21,440
I agree! That being said, we have a lot of people 
in the comments. Thanks all for checking in with

30
00:02:21,440 --> 00:02:25,120
us. We have Sam from Clearwater, Florida. 
Definitely glad to have her for multiple

31
00:02:25,120 --> 00:02:30,720
reasons. Good to see you, Sam! We have Stu 
from Kick, London, using Beefree SDK. Thank

32
00:02:30,720 --> 00:02:35,360
you for that, definitely appreciate it. 
Mark checking in from Lincoln, Nebraska,

33
00:02:35,360 --> 00:02:40,640
just above me. I'm in the Memphis, Tennessee, area 
here in the States. We have Philip from Germany,

34
00:02:40,640 --> 00:02:46,640
Krishna from India. This is fantastic! We 
have David also calling in from Palm Coast,

35
00:02:46,640 --> 00:02:52,880
Yash from India, and Aaron Bird from the 
UK. And Adrian is typing as well. So,

36
00:02:52,880 --> 00:02:55,520
thank you all for joining us, 
thank you for participating.

37
00:02:55,520 --> 00:02:59,200
As you'll notice, all of you, down on the bottom 
there, we have the chat that you're engaging in

38
00:02:59,200 --> 00:03:03,360
right now. Feel free to continue to chat all 
throughout the session today. Just make friends

39
00:03:03,360 --> 00:03:07,760
with each other; you never know what kind of 
collaborations and opportunities might arise. Any

40
00:03:07,760 --> 00:03:12,880
specific questions you have, please click on the 
"Questions" tab. That way, it'll be a lot easier

41
00:03:12,880 --> 00:03:19,200
for us to find those toward the end of today's 
session. And once again, hello to Aaron from the

42
00:03:19,200 --> 00:03:28,560
UK and Adrian from sunny Ireland, and Alfred from 
Engine Mailer—I think I'm butchering that, I'm so

43
00:03:28,560 --> 00:03:33,120
sorry. I was going to say hello to Alfred, we're 
glad to have you, and I'm glad you're having a

44
00:03:33,120 --> 00:03:38,000
sunny day in Ireland, Adrian. Here in the Memphis, 
Tennessee, area, we have had three days of rain.

45
00:03:38,000 --> 00:03:44,560
I got back home, and we were forecasted to have 
three more days of rain, so I wish I had your sun.

46
00:03:44,560 --> 00:03:48,960
That being said, it's a couple of minutes after 
this is scheduled for being a 30-minute session,

47
00:03:48,960 --> 00:03:52,400
and I'm all about efficiency. 
Luca, shall we jump into it?

48
00:03:52,400 --> 00:03:53,200
Let's go!

49
00:03:53,200 --> 00:04:00,400
Fantastic! So, I'm going to share my screen 
real quick here. We'll share the window,

50
00:04:00,400 --> 00:04:05,680
and that looks a little weird, so 
hold on just a second. I didn't like

51
00:04:05,680 --> 00:04:20,320
how that looked. I'm going to share the 
window, that one there we go. And Luca,

52
00:04:20,320 --> 00:04:24,960
if you'd just be so kind to let me 
know if that is coming through okay.

53
00:04:24,960 --> 00:04:26,960
Okay, I can see that.

54
00:04:26,960 --> 00:04:32,240
Fantastic! All right, so today, folks, we are 
talking about the HTML Importer API. Again,

55
00:04:32,240 --> 00:04:35,040
I'm here with my friend Luca, who 
is a Senior Fullstack Developer,

56
00:04:35,040 --> 00:04:40,400
and I'm Lawrence Lockhart, Senior Developer 
Advocate—let me get my own name correct!

57
00:04:40,400 --> 00:04:44,000
So, the first thing we have is our agenda. 
Naturally, we're going to talk about what is the

58
00:04:44,000 --> 00:04:48,480
HTML Importer API and why does it even matter. 
Then, you're going to see some amazing demos,

59
00:04:48,480 --> 00:04:53,170
Part One and Part Two, from Luca. 
Then, we'll wrap up with a Q&A.

60
00:04:53,170 --> 00:04:55,520
What is the HTML Importer API?
But the first question is, "What the

61
00:04:55,520 --> 00:05:01,680
heck is this thing? What is an HTML Importer API, 
all those strange words and letters, and why does

62
00:05:01,680 --> 00:05:06,560
it even matter?" You all ask great questions on 
a Tuesday; I'm happy to help you out with that.

63
00:05:06,560 --> 00:05:11,120
So, the HTML Importer API is a new API; 
it's one of our latest features within

64
00:05:11,120 --> 00:05:17,520
the Beefree SDK environment. What it allows 
you to do is to take an existing HTML email

65
00:05:17,520 --> 00:05:24,560
template and have it converted to the Beefree 
proprietary JSON for use in the editor itself,

66
00:05:24,560 --> 00:05:27,040
which I think is an absolute game-changer.

67
00:05:27,040 --> 00:05:30,480
Now, I do recognize in the audience we probably 
have some new folks, so just a little bit of

68
00:05:30,480 --> 00:05:34,960
background. First of all, when it comes to 
Beefree, we have this amazing visual editor,

69
00:05:34,960 --> 00:05:40,880
the Beefree app, that allows you to build email 
landing pages, pop-ups, with simply using drag

70
00:05:40,880 --> 00:05:46,080
and drop. But we also have the SDK, and that tends 
to be where my focus is. Our Software Development

71
00:05:46,080 --> 00:05:52,320
Kit lets you get that same type of power and 
embed it within your own application. It can be

72
00:05:52,320 --> 00:05:57,520
your SaaS application so your users can have that 
text to making great emails, or for you to make

73
00:05:57,520 --> 00:06:04,160
great emails yourself using our editor power. You 
can embed our editor in your application, and the

74
00:06:04,160 --> 00:06:09,920
power behind it, the data structure underneath all 
of it, is our proprietary JSON. So, this feature,

75
00:06:09,920 --> 00:06:16,640
this API, takes your HTML and converts it to 
our JSON so you can then use it in the editor.

76
00:06:16,640 --> 00:06:18,960
Who Needs the HTML Importer API?
Who would need something like this? Another

77
00:06:18,960 --> 00:06:23,840
great question! Well, if you're a new user, 
you've just come over to the Beefree ecosystem,

78
00:06:23,840 --> 00:06:29,200
but you've already been doing emails, you already 
have this entire library of HTML, you can now,

79
00:06:29,200 --> 00:06:35,360
case by case, convert those to Beefree JSON and 
then make further iterations within the editor.

80
00:06:35,360 --> 00:06:38,880
You don't want to have all that work go to 
waste. So, that works whether you're a new

81
00:06:38,880 --> 00:06:42,640
customer or even if you're an older customer, 
you've been using us for a while, but you have

82
00:06:42,640 --> 00:06:47,120
some templates that you would love to use from 
back in the day, but they don't convert naturally,

83
00:06:47,120 --> 00:06:51,760
and the man-hour to go into that is not something 
you want to invest. We have the tool for you;

84
00:06:51,760 --> 00:06:57,520
it's called the HTML Importer API, and 
you will be able to take that HTML code,

85
00:06:57,520 --> 00:07:02,000
have it converted to our JSON, import it to 
the editor, and then you just drag and drop.

86
00:07:02,000 --> 00:07:06,960
You can literally pass it over to your marketing 
team; they can make beautiful emails from there.

87
00:07:06,960 --> 00:07:10,160
Now, regarding the billing, we looked at 
it, we did the requisite research. Again,

88
00:07:10,160 --> 00:07:14,240
those man-hours can be tremendous, and 
so it's going to only be a $2 charge

89
00:07:14,240 --> 00:07:20,480
per successful API call, and you'll see 
that at the end of your monthly usage.

90
00:07:20,480 --> 00:07:24,400
From there, it's time for the live demo, and 
as I told you, our technical presenter today is

91
00:07:24,400 --> 00:07:34,880
Luca. So Luca, I'm going to stop sharing and pass 
over control to you as soon as I find my window.

92
00:07:34,880 --> 00:07:43,040
Thank you, Lawrence! Absolutely. Stop 
sharing. There we go. That's great. I'm

93
00:07:43,040 --> 00:07:50,880
going to stop sharing my screen now. 
Do you see that, Lawrence? Am I good?

94
00:07:50,880 --> 00:07:55,360
Hold on a second, I am still on 
the wrong window. You are great.

95
00:07:55,360 --> 00:08:01,840
Thank you. So, let's jump into these hands-on. 
Let's look at the HTML importer and how you can

96
00:08:01,840 --> 00:08:07,440
make the most out of it, combining it with 
the Brand Style Management API. More on

97
00:08:07,440 --> 00:08:13,760
that later. We'll walk through both features 
and how to enable them in the SDK console by

98
00:08:13,760 --> 00:08:21,920
generating scope-specific API keys, and we'll 
plug them into a real-world integration setup.

99
00:08:22,800 --> 00:08:31,360
Our first stop is the SDK console. In order to 
enable the HTML Importer API, you need to go into

100
00:08:31,360 --> 00:08:41,760
the details section of the application you want 
to use. Then, reach for the HTML Importer API tab.

101
00:08:41,760 --> 00:08:46,800
And as you can see, I already have a key, but I 
will remove that just for the purpose of this demo

102
00:08:46,800 --> 00:08:52,560
to show you how to enable one. Bonus point: 
you can see now how to disable that as well.

103
00:08:53,360 --> 00:08:58,480
So, when you don't have a key, the card will 
look like this. If you hit "Enable and Get

104
00:08:58,480 --> 00:09:05,600
the API Key," this modal will pop up where it 
requires you to check this box to acknowledge the

105
00:09:05,600 --> 00:09:11,520
additional fees for the service, and then you can 
hit "Create Key." Once you do this and wait just

106
00:09:11,520 --> 00:09:18,880
a couple of seconds, you'll be able to see your 
newly created key where the previous one was. From

107
00:09:18,880 --> 00:09:25,200
the same card, as you saw, you can also disable 
and revoke the key and regenerate it as well.

108
00:09:25,200 --> 00:09:32,000
Now, I'll move on to the IDE to show you how 
to implement the HTML Importer inside a simple

109
00:09:32,000 --> 00:09:36,960
integration. It's nothing special, nothing 
fancy. You can customize your integration

110
00:09:36,960 --> 00:09:42,320
however you'd like. Probably, if you're 
already a customer, you already have your

111
00:09:42,320 --> 00:09:48,400
integration well customized. If you're not, 
take this as a simple example to start from.

112
00:09:48,400 --> 00:09:55,360
What I did in this simple integration is I've 
added a simple button in the top toolbar that

113
00:09:55,360 --> 00:10:01,760
opens a modal. Here, you can see the code for 
the modal. I've kept everything simple, just bare

114
00:10:01,760 --> 00:10:09,280
bone to make it work with little customization, 
just to make it good enough to see. And here,

115
00:10:09,280 --> 00:10:16,320
the customer can paste the HTML code for the 
email they want to import, and after doing that,

116
00:10:16,320 --> 00:10:25,440
they can hit "Import" and trigger the actual 
API call to the HTML Importer endpoint.

117
00:10:25,440 --> 00:10:30,480
Now, I'll move over to the code for the call. 
As you can see, this is a POST call done to

118
00:10:30,480 --> 00:10:36,480
this endpoint that you can see on the screen 
and that you can find in our documentation. All

119
00:10:36,480 --> 00:10:44,160
it requires in the body is an html field that 
contains the HTML that you want to import into

120
00:10:44,160 --> 00:10:51,600
the builder. For the authorization, you need the 
key that we created before in the SDK console,

121
00:10:51,600 --> 00:10:58,400
and the way to pass it to the service is by 
this authorization header. Just a heads-up,

122
00:10:58,400 --> 00:11:06,720
I advise you to keep your keys inside a .env file 
and not version them, just not to risk exposing

123
00:11:06,720 --> 00:11:16,400
your credentials. The HTML that you pass to the 
service has some limitations. In particular,

124
00:11:17,840 --> 00:11:24,960
we cannot parse dynamic content yet. The 
service is optimized to handle emails,

125
00:11:24,960 --> 00:11:33,440
so it's not yet optimized to handle the import of 
HTML pages. The HTML should be valid. That means

126
00:11:33,440 --> 00:11:39,200
it should include a doctype declaration, 
valid HTML and body elements, and also

127
00:11:39,200 --> 00:11:47,680
the meta charset UTF-8 tag in the head section. 
Furthermore, you need to ensure that all images

128
00:11:47,680 --> 00:11:54,080
and resources contained in the email you want to 
import are publicly available on the internet,

129
00:11:54,960 --> 00:12:01,600
and be aware that we currently don't support 
all HTML tags. For more information on this

130
00:12:01,600 --> 00:12:10,960
specification, you can look at our documentation. 
In this section, you can also handle the errors

131
00:12:10,960 --> 00:12:18,240
from the service. There's nothing specific to 
speak about the errors, so the usual stuff.

132
00:12:18,240 --> 00:12:24,400
Now, I'll quickly jump over to the demo 
environment I've created, which code you were just

133
00:12:24,400 --> 00:12:32,320
seeing, and show you how it actually works. As 
you see, here is the button I talked about before,

134
00:12:32,320 --> 00:12:40,720
and when we click on this, you see the "Import 
HTML" form. What I need now is an HTML to pass

135
00:12:40,720 --> 00:12:49,600
in here to move on with the import. What I can do 
is visit Really Good Emails and look for an email

136
00:12:49,600 --> 00:12:56,400
that I like and I want to take inspiration 
from. For example, let's pick the first one,

137
00:12:56,400 --> 00:13:02,160
view more about this email, get to the 
code—that is what we need—and copy and

138
00:13:02,160 --> 00:13:09,760
paste this code inside our demo environment and 
hit "Import." It will take just a few seconds,

139
00:13:09,760 --> 00:13:17,120
not days like when you have to do this manually, 
and you can see that we have pretty much a close

140
00:13:17,120 --> 00:13:25,920
recreation of the email. I'll quickly 
show you the original one here in RGE,

141
00:13:25,920 --> 00:13:33,040
and you can see the importer did pretty well. 
But do not expect always a one-to-one recreation.

142
00:13:33,040 --> 00:13:39,680
The job of the importer is not to import 
an exact copy of the email inside Beefree,

143
00:13:39,680 --> 00:13:46,480
but to facilitate the recreation of the email 
inside the builder. The idea is that we get

144
00:13:46,480 --> 00:13:52,000
80% to 90% of your job done, depending on 
the template and the quality of the HTML,

145
00:13:52,000 --> 00:13:59,680
and you just have to put the final tweaks to have 
the result you desired. One more important thing:

146
00:13:59,680 --> 00:14:07,040
the import process is deterministic. So, no matter 
how many times you import a specific HTML, you'll

147
00:14:07,040 --> 00:14:16,080
always get the same result. And this is important 
because you will pay all the calls you make, so be

148
00:14:16,080 --> 00:14:23,360
careful. Don't think that different iterations 
of the import can generate different results.

149
00:14:24,000 --> 00:14:30,320
So, let's go back to the tweaking we were talking 
about. One thing that the Brand Style Management

150
00:14:30,320 --> 00:14:38,640
API is great for after you have imported your 
HTML is applying your brand style to the email you

151
00:14:38,640 --> 00:14:45,520
took inspiration from. So, let's say this is the 
email that you loved, you love the style, you love

152
00:14:45,520 --> 00:14:53,840
the structure, but of course it doesn't fit your 
brand style, and you want to improve that. Well,

153
00:14:53,840 --> 00:15:01,440
the Brand Style Management API is there for you. 
What you need to do to use that API is once again

154
00:15:01,440 --> 00:15:07,760
go back to the Beefree SDK console and once again 
activate another API key. Every API key is scoped

155
00:15:07,760 --> 00:15:14,800
for a specific context. In this case, what you 
need is the Content Services API. Once again, I

156
00:15:14,800 --> 00:15:23,680
already have one, but for the scope of this demo, 
I'm going to disable and revoke the key and once

157
00:15:23,680 --> 00:15:30,000
again hit the "Enable and Get the API Key" button, 
just like we did for the HTML Importer. This time,

158
00:15:30,000 --> 00:15:37,280
the fees are already mentioned to you in the 
terms of service when you sign up for the plugin,

159
00:15:37,280 --> 00:15:47,520
so you don't have to check any boxes, and 
you can create a key. A couple of seconds,

160
00:15:47,520 --> 00:15:51,840
and you'll see that, just like with the 
importer, we have the Content Services

161
00:15:51,840 --> 00:15:57,680
API key right here. And once again, you can 
regenerate the key or disable and revoke the key.

162
00:15:57,680 --> 00:16:03,440
Once you have your key, it's time to get back 
into the IDE to see how you can implement the API

163
00:16:03,440 --> 00:16:12,400
endpoint inside the integration. Once again, all 
you need for this is a simple button or whatever

164
00:16:12,400 --> 00:16:20,000
you choose to trigger the call to the Brand Style 
Management API. The Brand Style Management API is

165
00:16:20,000 --> 00:16:25,840
once again a POST call made to this endpoint that 
you can find in our documentation. And this time,

166
00:16:25,840 --> 00:16:34,000
the body requires two fields: styles, which is 
basically a JSON object structured in a similar

167
00:16:34,000 --> 00:16:38,640
manner to this (for more information, you can 
check our documentation) where you define the

168
00:16:38,640 --> 00:16:45,760
styles—in this example, for the buttons, such 
as color, font size, and all the stuff that is

169
00:16:46,480 --> 00:16:53,920
according to your brand style management. Once 
you have your style, you simply need to pass the

170
00:16:53,920 --> 00:16:59,920
template you want that style to be applied to. In 
our case, it's the template we generated through

171
00:16:59,920 --> 00:17:06,880
the HTML Importer. Once again, to make this 
call, you need to use the key that we created

172
00:17:06,880 --> 00:17:14,240
before through this authorization header. And once 
again, I advise you, keep the same behavior as I

173
00:17:14,240 --> 00:17:22,240
told you about before with the .env file, just to 
be sure not to expose your credentials. One thing

174
00:17:22,240 --> 00:17:29,120
that needs specific mention for the Brand Style 
Management, though, is their error handling. The

175
00:17:29,120 --> 00:17:36,720
error that needs a specific mention is the status 
code 422: "Unprocessable Entity." This one doesn't

176
00:17:36,720 --> 00:17:41,920
mean that you did something wrong on your side, 
but it simply means that the styles you were

177
00:17:41,920 --> 00:17:47,280
trying to apply to the template you were trying to 
apply them to weren't compatible. What does this

178
00:17:47,280 --> 00:17:53,600
mean? In our example, we saw that we defined 
styles just for the button element. Let's say

179
00:17:53,600 --> 00:17:59,920
we have a template that has no button elements; 
in that case, there is no compatibility between

180
00:17:59,920 --> 00:18:06,400
the style and the template because there's no 
style you can apply to the template at hand. In

181
00:18:06,400 --> 00:18:11,600
this case, the service will reply with a 422 
error that simply means no changes were made

182
00:18:11,600 --> 00:18:17,280
to this template. You can decide what to do with 
that. You can bubble up the message to your user,

183
00:18:17,280 --> 00:18:23,440
maybe through a toast message telling them nothing 
happened because the style wasn't applicable,

184
00:18:23,440 --> 00:18:30,080
or you can simply reload the template. The 
behavior of the integration is up to you.

185
00:18:30,080 --> 00:18:35,120
And once again, we can go back to the demo 
environment to show you the brand style

186
00:18:35,120 --> 00:18:41,760
management in action. I've already shown you 
the template that we imported. I want you to

187
00:18:41,760 --> 00:18:48,240
pay attention specifically to the button because, 
as you saw, that's the style we defined in our

188
00:18:48,240 --> 00:18:54,640
JSON. And once I hit "Apply Brand Style," the 
template is processed, and you can see the email

189
00:18:54,640 --> 00:19:01,280
is pretty much the same, except for the button 
that now has the style we have defined inside

190
00:19:01,280 --> 00:19:08,640
our Brand Style Management API, specifically 
in the JSON that we passed to the endpoint.

191
00:19:08,640 --> 00:19:15,520
So, before moving on to the Q&A session of this 
spotlight, I'd like to quickly recap what we

192
00:19:15,520 --> 00:19:21,360
saw today. We learned how to enable the HTML 
Importer for your application by creating an

193
00:19:21,360 --> 00:19:29,120
API key and how you can manage it inside your 
application details, and specifically the HTML

194
00:19:29,120 --> 00:19:36,000
Importer API card. We saw a simple implementation 
of the endpoint in an integration of our builder,

195
00:19:36,000 --> 00:19:42,320
and then we moved to how to maximize the impact 
of the HTML Importer by combining it with the

196
00:19:42,320 --> 00:19:47,680
Brand Style Management. To do that, we 
enabled the Content Services API key,

197
00:19:47,680 --> 00:19:54,640
just like we did for the HTML Importer, 
by using the dedicated card. And then we

198
00:19:54,640 --> 00:19:59,680
saw an easy implementation of the Brand 
Style Management API endpoint into the

199
00:19:59,680 --> 00:20:07,120
same integration we used prior to show you 
the functionality of the HTML Importer.

200
00:20:07,120 --> 00:20:13,280
Now, it's time for a Q&A session where we'll 
get all your questions and hopefully give

201
00:20:13,280 --> 00:20:19,760
you all your answers. And I don't know 
if any came up during the explanation,

202
00:20:19,760 --> 00:20:23,840
we'll start with them and 
then move on to the live ones.

203
00:20:23,840 --> 00:20:28,960
First of all, Luca, fantastic explanation! You 
went through a ton of content in a miraculously

204
00:20:28,960 --> 00:20:33,520
short amount of time, so great job on 
that. Thank you for those explanations.

205
00:20:33,520 --> 00:20:38,560
We do have a robust set of questions, 
so I'm going to go to the first one,

206
00:20:38,560 --> 00:20:45,200
which is from David Cohen. I believe he was 
also from the Palm Coast. And his question is,

207
00:20:45,200 --> 00:20:50,800
"Is there an ability to test the HTML 
importer for free coming in the future?"

208
00:20:50,800 --> 00:20:56,320
So, this is more of a product question, 
so I'm not the right guy to ask it to. But

209
00:20:56,320 --> 00:21:02,160
I'll check with my colleagues, and I'll get 
back to you with an answer after the spotlight.

210
00:21:02,160 --> 00:21:08,960
Awesome, appreciate that. Let's go on to the next 
one that is from Stu. "If there are unsupported

211
00:21:08,960 --> 00:21:14,400
HTML tags in the imported file, will you either 
get an error or accept the file and strip them

212
00:21:14,400 --> 00:21:18,640
out?" And they're trying to figure out how they 
need to handle validation, if they need to handle

213
00:21:18,640 --> 00:21:24,640
it on their side or just parse the responses. 
So, what happens with unsupported HTML tags?

214
00:21:24,640 --> 00:21:34,720
The unsupported HTML tags won't break 
the endpoint, as long as the HTML is

215
00:21:34,720 --> 00:21:38,480
correctly structured. That's the only 
thing that will break the endpoint:

216
00:21:38,480 --> 00:21:49,440
an HTML that doesn't have the right structure. 
Unsupported HTML tags won't behave predictably,

217
00:21:49,440 --> 00:21:54,640
so you might not get the best result from 
your import, but you don't have to validate

218
00:21:54,640 --> 00:22:03,760
on your side which tags you are passing to 
the importer and which you need to sanitize.

219
00:22:03,760 --> 00:22:09,680
Fantastic, thank you for that. Let's 
see here, we have one from... oh okay,

220
00:22:09,680 --> 00:22:15,040
so Samantha shared one, I guess it was 
shared over in the chat, from Provo. "How

221
00:22:15,040 --> 00:22:24,080
do you import email templates from the client's 
Beefree account to their Beefree SDK editor?"

222
00:22:24,080 --> 00:22:29,280
Okay, interesting workflow there. So, 
their client has the HTML template,

223
00:22:29,280 --> 00:22:38,480
but the provider wants to import it to their SDK 
editor. Yeah, so assuming you want to use the

224
00:22:38,480 --> 00:22:45,280
tools that we are highlighting in this spotlight, 
the thing you can do is have your customer export

225
00:22:45,280 --> 00:22:53,200
the HTML for the specific template and then 
import it to the HTML importer. But since your

226
00:22:53,200 --> 00:23:01,200
customer is using the Beefree account and 
the Beefree SDK, I'd say get in touch with

227
00:23:01,200 --> 00:23:10,560
the CSM that's following you and maybe see if 
there's any other solution that we can work on.

228
00:23:10,560 --> 00:23:14,480
Fantastic, thank you for that. I'm just 
clicking a bunch of buttons here. There's

229
00:23:14,480 --> 00:23:18,240
a lot going on in the chat, but yes, 
excellent answer, excellent answer.

230
00:23:18,240 --> 00:23:25,920
I believe the next one here is from Vishnu. 
"Can they apply external CSS to their HTML?"

231
00:23:25,920 --> 00:23:32,800
Okay, so I'll split this question into two since 
I don't have the full context. If you are saying,

232
00:23:32,800 --> 00:23:38,960
"Can I apply an external CSS to the 
HTML you are importing?" I'd say no,

233
00:23:38,960 --> 00:23:46,640
unless the CSS is publicly available online, but I 
can't guarantee that because we never tested that,

234
00:23:46,640 --> 00:23:51,920
so that's something we should try on our 
end, and maybe we can let you know. The best,

235
00:23:51,920 --> 00:23:55,360
though, is to have the styling 
incorporated in the HTML. That way,

236
00:23:55,360 --> 00:24:01,120
we are certain that the importer can handle 
it correctly. If you want to apply CSS after

237
00:24:01,120 --> 00:24:07,760
you have imported the template, you can do 
that through the Brand Style Management API,

238
00:24:07,760 --> 00:24:17,360
as we saw in the second part of the demo, 
simply by defining an appropriate style JSON.

239
00:24:17,360 --> 00:24:23,520
Awesome. You're just handling these 
rapid fire, so I'm going to keep going,

240
00:24:23,520 --> 00:24:28,240
Luca. The next one is from Stu, interesting 
question regarding dynamic content: "If we

241
00:24:28,240 --> 00:24:33,040
want to import dynamic content, can we"—I think 
he means—"can we import it with two different

242
00:24:33,040 --> 00:24:40,480
rows for the content and then drag it 
into dynamic content inside the editor?"

243
00:24:40,480 --> 00:24:47,280
So, the only thing that's stopping you from using 
dynamic content is the actual import step. Once

244
00:24:47,280 --> 00:24:53,680
the template is inside the builder, you can 
handle dynamic content as you're used to. So,

245
00:24:53,680 --> 00:24:59,200
let me read the question once again. "If you want 
to import dynamic content, can we import it with

246
00:24:59,200 --> 00:25:06,160
two different rows for the content and then drag 
it into dynamic content inside the editor?" So,

247
00:25:06,160 --> 00:25:16,640
the way you're suggesting won't work because the 
HTML Importer isn't coded to work like that. But

248
00:25:16,640 --> 00:25:22,640
you can simply fix the dynamic content after you 
have imported the HTML. As I told you before,

249
00:25:22,640 --> 00:25:26,000
don't think of this as a 
way to go from zero to 100,

250
00:25:26,000 --> 00:25:31,840
but hopefully from zero to 80% to 90%. There 
are some cases where you might get 100%;

251
00:25:31,840 --> 00:25:39,040
I'm not saying it won't happen, but you don't 
have to think like that's the solution for this.

252
00:25:39,040 --> 00:25:44,240
Awesome. All right, we have one 
from Kristen, a short question:

253
00:25:44,240 --> 00:25:48,160
"Does the HTML Importer API support merge tags?"

254
00:25:49,040 --> 00:25:53,840
I'll need to double check on this, but 
I don't think so, as once again, you can

255
00:25:53,840 --> 00:26:00,160
add them after you have imported 
the HTML in the template, though.

256
00:26:00,160 --> 00:26:06,000
Got it, okay. And we have one regarding 
the users using the importer: "If we

257
00:26:06,000 --> 00:26:10,880
embed this and give users access, can we 
put a limit on how many times it's used,

258
00:26:10,880 --> 00:26:13,360
like 10 credits or something like that?"

259
00:26:13,360 --> 00:26:22,000
Yeah, that is totally up to you. The integration 
of the endpoint into your version of our builder

260
00:26:22,000 --> 00:26:27,200
is completely up to you. You can limit 
the usage per user, you can even create

261
00:26:27,200 --> 00:26:35,600
tiers where each tier has a different number of 
usages for the service. You can price each call

262
00:26:35,600 --> 00:26:44,160
like we do. It's up to you. You can do the 
implementation you think suits you better.

263
00:26:44,160 --> 00:26:48,720
Awesome. And just for clarity, would 
that limitation or those tiers be done

264
00:26:48,720 --> 00:26:52,880
within the editor feature, or 
that would be done externally?

265
00:26:53,840 --> 00:27:02,320
I'd say a little bit of both because you have to 
keep track of the limits your user is hitting.

266
00:27:02,320 --> 00:27:11,120
One simple implementation that comes to the top 
of my mind is based on the UID of your user,

267
00:27:11,120 --> 00:27:16,720
keep track of how many calls they do 
to those endpoints and keep a counter,

268
00:27:16,720 --> 00:27:22,080
for example, in a database, and once 
the counter reaches the maximum,

269
00:27:22,080 --> 00:27:30,800
you stop them from making the call, either 
monthly or with the recurrence you prefer.

270
00:27:30,800 --> 00:27:37,280
Awesome, appreciate that. We have one from 
Sam Lewis: "Are there additional improvements

271
00:27:37,280 --> 00:27:42,240
being made to the Import API to improve 
the conversion? We consistently see added

272
00:27:42,240 --> 00:27:47,840
empty columns to the imported templates 
and unaccessible background colors."

273
00:27:47,840 --> 00:27:53,120
Yes, I don't have a roadmap since 
we follow the shape methodology,

274
00:27:53,120 --> 00:27:59,200
but be sure that we'll keep 
improving the HTML Importer.

275
00:27:59,200 --> 00:28:04,400
Awesome. Gideon asks, "How does this 
work with save rows?" So he's using one

276
00:28:04,400 --> 00:28:09,920
of our other very popular features, save 
rows. How does this work with save rows?

277
00:28:09,920 --> 00:28:16,640
Okay, so what do you mean by that? 
Of course, it won't use your save

278
00:28:16,640 --> 00:28:23,280
rows because it doesn't have access while 
it's creating the template to the save

279
00:28:23,280 --> 00:28:29,360
rows, but you can use the save row 
after you have imported the email.

280
00:28:29,360 --> 00:28:34,560
Fantastic. All right. Gideon asked 
a similar question to earlier:

281
00:28:34,560 --> 00:28:37,440
"Any plans to offer a cheaper alternative?"

282
00:28:37,440 --> 00:28:41,520
Once again, I'm not the right guy 
to ask these kind of questions to,

283
00:28:41,520 --> 00:28:49,760
but I will bring the question to our 
product colleagues and let you know.

284
00:28:49,760 --> 00:28:53,840
Absolutely. And at the end, we're going 
to also supply a support email that all

285
00:28:53,840 --> 00:28:59,200
of our users can reach out to for deeper 
questions like that. Let's see here,

286
00:28:59,200 --> 00:29:02,720
here's one from Aaron Bird. And 
again, for anyone who has questions,

287
00:29:02,720 --> 00:29:06,080
put them in the question section of the 
window there. We'll be able to see them a

288
00:29:06,080 --> 00:29:10,800
lot easier. But thanks for sharing this, Sam, 
from Aaron Bird. "When importing with images,

289
00:29:10,800 --> 00:29:15,600
are the images stored on our image editor, 
or is it from the original source?"

290
00:29:15,600 --> 00:29:22,000
So, this is an interesting question, and we can 
check on the fly. So, by the looks of it, it's

291
00:29:23,120 --> 00:29:33,920
the original source. Sorry, wrong combination. 
Yep, it's the original source, and that can also

292
00:29:33,920 --> 00:29:39,840
be tested by changing the image and seeing that 
there's no image uploaded to the file manager.

293
00:29:39,840 --> 00:29:48,080
That's the reason why we specifically said before 
that any resource you are using in the HTML you

294
00:29:48,080 --> 00:29:54,160
want to import needs to be publicly available on 
the internet; otherwise, this image won't show.

295
00:29:54,160 --> 00:29:58,880
Awesome, thank you for that. The next one is a 
product question again, so I'm going to go to

296
00:29:58,880 --> 00:30:04,560
this one from Yash: "When creating email content 
from within the builder, adds a ton of additional

297
00:30:04,560 --> 00:30:10,880
information for MS and other browser vendors, 
Microsoft or other browser vendors. Simple HTML

298
00:30:10,880 --> 00:30:15,840
created without any fuss. When imported via 
HTML, will the fuss be added automatically?"

299
00:30:15,840 --> 00:30:26,800
Okay, that's a lot. Let me digest that one 
again. Okay, okay, so, oh, okay, I got you.

300
00:30:26,800 --> 00:30:33,920
Go ahead. I think the question is, "Will all 
the improvements that Beefree makes to the

301
00:30:33,920 --> 00:30:40,880
HTML to guarantee the compatibility with all 
the email clients be available if I import

302
00:30:40,880 --> 00:30:46,720
the email?" And the answer is yes, yes. Once 
you have imported the email, you're working

303
00:30:46,720 --> 00:30:53,280
with our proprietary JSON. When you want to 
get the HTML back from our proprietary JSON,

304
00:30:53,280 --> 00:30:59,280
you go through our parser, so the end 
result will be what you usually get when

305
00:30:59,280 --> 00:31:07,760
you parse an email, you export the HTML from 
Beefree, either Beefree or the Beefree SDK.

306
00:31:07,760 --> 00:31:12,320
Fantastic. And we're down to our last 
two questions. You are killing these,

307
00:31:12,320 --> 00:31:17,440
Luca, so here we go. One from Sudhir: "I'm 
building an HTML template using the AI,

308
00:31:17,440 --> 00:31:24,880
and it is using inline CSS. Can it 
be applied when I import the HTML?

309
00:31:24,880 --> 00:31:32,080
Can be applied, will the inline CSS 
be converted to the JSON properly?"

310
00:31:32,080 --> 00:31:40,880
Yeah, so you are building an HTML using AI, and 
then you want to import the HTML you built with

311
00:31:40,880 --> 00:31:47,120
AI into the builder. If I get this right, I think 
they're asking specifically about the inline CSS,

312
00:31:47,120 --> 00:31:52,320
if that's going to be applied correctly. Yeah, 
as long as it is formatted correctly, I'd say

313
00:31:52,320 --> 00:32:02,000
so. We go back to the limitation about the HTML 
being formatted correctly with those specifics

314
00:32:02,000 --> 00:32:09,920
we said earlier about the doctype, the html, 
the body, etc. And if you want more clarity on

315
00:32:10,480 --> 00:32:16,640
the specification, you can look at the 
documentation, but overall, I'd say yes.

316
00:32:16,640 --> 00:32:26,000
Fantastic. And finally, one from Bombsy here, who 
asks, "I have a plan—I have plain HTML. Can you

317
00:32:26,000 --> 00:32:32,960
add colors for that by using HTML Importer 
API based on header text? Can I get related

318
00:32:32,960 --> 00:32:40,560
images?" Sounds like two questions. You figure 
that one out. "Plan," perhaps that's plain HTML.

319
00:32:40,560 --> 00:32:46,880
Yeah, I think it means plain. "I have plain 
HTML. Can you add colors for that by using the

320
00:32:46,880 --> 00:32:58,000
HTML Importer?" So, the HTML Importer doesn't add 
anything; it simply reads the HTML and converts

321
00:32:58,000 --> 00:33:06,720
it to the JSON proprietary for Beefree so that 
you can use it in the template. What you can do

322
00:33:06,720 --> 00:33:13,920
if you want to add colors is use the Brand Style 
Management API, but then again, the Brand Style

323
00:33:13,920 --> 00:33:20,880
Management for now doesn't work in addition; it 
simply merges the style you are defining with the

324
00:33:20,880 --> 00:33:26,000
style already present inside the templates, so 
you cannot add the styles with the Brand Style

325
00:33:26,000 --> 00:33:33,280
Management, but simply modify those that already 
exist. I hope this answered your first question.

326
00:33:33,280 --> 00:33:37,920
Awesome. And by the way, our teammate Samantha 
offered this for the last question as well,

327
00:33:37,920 --> 00:33:41,600
that our simple schema, that there 
was a spotlight session for recently,

328
00:33:41,600 --> 00:33:47,200
that might also be a great option for the 
use in that AI case. So also check schema.

329
00:33:47,200 --> 00:33:54,240
Don't want to go through the HTML to do the AI. 
The AI generation, you can use simple schema,

330
00:33:54,240 --> 00:34:01,840
and it will be converted into our full schema 
using the endpoint we made available recently.

331
00:34:01,840 --> 00:34:09,920
Absolutely. The other question was about 
images. This is the last one I have here. "Okay,

332
00:34:09,920 --> 00:34:14,960
if we are onboarding a client and they provide us 
their existing emails to import, I assume there

333
00:34:14,960 --> 00:34:21,360
is no quick route to just import the EML files. 
We need to convert that to plain HTML first."

334
00:34:21,360 --> 00:34:30,080
Yes, for now, yes, we just handle plain HTML. 
So, you can develop something on your side if

335
00:34:30,080 --> 00:34:36,160
you import customers often and you want to 
speed up this process. You can implement

336
00:34:36,160 --> 00:34:45,200
some pre-processing that converts the EML 
into plain HTML, and you can also implement

337
00:34:45,200 --> 00:34:54,080
bulk imports on your side. So, you have 
plenty, this tool is very multifaceted,

338
00:34:54,080 --> 00:34:59,920
and it can be used in many ways 
on your side of the integration.

339
00:34:59,920 --> 00:35:05,120
Fantastic. All right, that is all the 
questions. You filled those very well,

340
00:35:05,120 --> 00:35:09,680
Luca. I want to go ahead and put the 
support email up here. Thanks again

341
00:35:09,680 --> 00:35:13,120
for all of you for joining us today for 
this spotlight session about the all-new

342
00:35:13,120 --> 00:35:18,400
HTML Importer API. The docs are listed 
there in the chat, and for any additional

343
00:35:18,400 --> 00:35:27,040
questions you have, definitely reach out to 
sdk.support@beefree.io. Any final thoughts, Luca?

344
00:35:27,040 --> 00:35:35,120
Well, I just hope you found this spotlight 
interesting and that you are going to be trying

345
00:35:35,120 --> 00:35:42,560
out the HTML Importer and see how you can maximize 
the result with the Brand Style Management.

346
00:35:42,560 --> 00:35:45,760
Fantastic. Thank you all for 
joining and have a great day!
```
{% endtab %}
{% endtabs %}
