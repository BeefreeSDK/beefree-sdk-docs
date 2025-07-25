---
description: >-
  Learn more about Beefree SDK's Check endpoints under the Content Services API,
  and Frontend Commands. Together, these features bring a complete design QA
  experience to your end users.
---

# Build QA Tools into Your App with the Beefree SDK Check API and Frontend Commands

{% embed url="https://www.youtube.com/watch?v=L0SI9GOmw0M" %}

{% tabs %}
{% tab title="About" %}
Want to help your users catch broken links, missing alt text, and oversized images before they hit send? In this Spotlight session, we show you how to build your own email QA tools using the Beefree SDK. Join Francesco, Andrea, and Bettina from the Beefree app team as they explore:&#x20;

**Chapters:**&#x20;

* [0:00](https://www.youtube.com/watch?v=L0SI9GOmw0M) - Intro&#x20;
* [4:21](https://www.youtube.com/watch?v=L0SI9GOmw0M\&t=261s) - Importance of QA design&#x20;
* [6:39](https://www.youtube.com/watch?v=L0SI9GOmw0M\&t=399s) -  Introducing the Check API and Frontend Commands&#x20;
* [10:31](https://www.youtube.com/watch?v=L0SI9GOmw0M\&t=631s) -    Live demo: implementing QA tools&#x20;
* [10:55](https://www.youtube.com/watch?v=L0SI9GOmw0M\&t=655s) - Check API endpoints&#x20;
* [19:38](https://www.youtube.com/watch?v=L0SI9GOmw0M\&t=1178s) - Frontend commands&#x20;
* [32:38](https://www.youtube.com/watch?v=L0SI9GOmw0M\&t=1958s) - Q\&A session&#x20;
* [38:48](https://www.youtube.com/watch?v=L0SI9GOmw0M\&t=2328s) - Conclusion & resources
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
1
00:00:00,320 --> 00:00:03,200
Hey everyone. Well, we are so on 
time—we're actually one minute

2
00:00:03,200 --> 00:00:07,280
early. That rarely happens. So thanks, everyone,

3
00:00:07,280 --> 00:00:16,640
for joining. We’ll give folks another 
minute or two to get settled in and log in.

4
00:00:18,400 --> 00:00:25,520
Hello to everyone who's already here, and hi to 
Francesco and Andrea. Thank you for joining today.

5
00:00:31,200 --> 00:00:38,960
For anyone who’s new here, make sure you 
find the chat box on the right. We can’t

6
00:00:38,960 --> 00:00:46,880
see you—unfortunately—but we can interact with 
you through the chat. So feel free to say hi!

7
00:00:50,720 --> 00:00:56,720
Hello, hello. We’re always curious—again, we 
can’t see you—but we’d love to get to know you

8
00:00:56,720 --> 00:01:04,000
a bit. We were just chatting about vacation plans 
earlier while waiting for the session to start.

9
00:01:05,440 --> 00:01:12,000
Hi, Ashwin! If you all don’t mind sharing, let 
us know where you’re joining from and if you have

10
00:01:12,000 --> 00:01:24,880
any fun vacation plans this summer. Ashwin, 
where are you from? I also see Jesse typing.

11
00:01:24,880 --> 00:01:28,160
Francesco, are you doing anything 
fun for vacation this year?

12
00:01:28,160 --> 00:01:33,040
Oh, yeah, definitely. I'm going to Greece.
Ooh, nice! I’ve been wanting to go to

13
00:01:33,040 --> 00:01:36,640
Greece for the past—I don’t know—six, 
seven years. And finally, I’m doing

14
00:01:36,640 --> 00:01:43,680
it. Never been there before.
That certainly counts. Nice.

15
00:01:43,680 --> 00:01:47,120
Oh, we've got Ashwin tuning in from India.

16
00:01:47,120 --> 00:01:55,760
Hello—and good evening to you! It’s 
a late one. Thank you for tuning in.

17
00:02:00,640 --> 00:02:06,640
Hello also to folks joining 
from Washington and Florida.

18
00:02:06,640 --> 00:02:16,800
All right, it’s 2 minutes after the hour, so 
let’s get started. Francesco, Andrea—you ready?

19
00:02:17,680 --> 00:02:20,160
Okay, awesome.

20
00:02:23,040 --> 00:02:28,400
Welcome everyone to today’s spotlight session. 
We're really thrilled to have you with us

21
00:02:29,200 --> 00:02:34,560
because we’re talking about something exciting. 
And yes—we might be biased—but it’s a very cool

22
00:02:34,560 --> 00:02:41,760
topic. Today we’ll chat about how you can 
bring QA tools into your application and

23
00:02:41,760 --> 00:02:46,400
help your users create error-free 
emails using the latest Beefree SDK

24
00:02:46,400 --> 00:02:53,920
features. We recently released some powerful 
updates that enhance your QA functionality.

25
00:02:55,760 --> 00:03:02,640
Quick intro—I’m Betina. I run the 
product marketing team here at Beefree,

26
00:03:02,640 --> 00:03:09,120
and I get the pleasure of hosting this session. 
I’m joined by these two wonderful humans:

27
00:03:09,120 --> 00:03:15,360
Andrea and Francesco, who are developers on 
the Beefree app side. If you didn’t know,

28
00:03:15,360 --> 00:03:22,560
the Beefree app is our end-user-facing 
implementation of the Beefree SDK. So

29
00:03:22,560 --> 00:03:30,640
Francesco and Andrea work with the SDK a 
lot. They're basically in the same shoes

30
00:03:30,640 --> 00:03:36,080
as you are, which makes it especially exciting 
to have them share their experience with us.

31
00:03:36,080 --> 00:03:42,480
Here’s what you can expect today:

32
00:03:42,480 --> 00:03:48,480
We’ll start with context—why 
error prevention and QA matter.

33
00:03:48,480 --> 00:03:56,000
Then we’ll give an overview of two 
new features that power your QA tools:

34
00:03:56,000 --> 00:03:58,400
the Check API and Front-End Commands.

35
00:03:58,400 --> 00:04:09,440
Then, we’ll turn it over to Francesco 
and Andrea for a live demo showing

36
00:04:09,440 --> 00:04:13,840
how to build QA tools into your app.

37
00:04:13,840 --> 00:04:16,240
We’ll wrap with a Q&A.

38
00:04:18,320 --> 00:04:21,440
Let’s jump in.

39
00:04:22,800 --> 00:04:35,680
At Beefree, we care deeply about 
designing beautiful assets. But

40
00:04:37,040 --> 00:04:44,080
even the most gorgeous landing page 
or email campaign can’t perform

41
00:04:46,320 --> 00:04:52,240
if it’s riddled with mistakes. And it’s 
surprisingly easy to make mistakes.

42
00:04:52,800 --> 00:05:01,200
Those of you who’ve been in the space for a 
while know how easy it is to create a design

43
00:05:01,200 --> 00:05:18,311
that gets clipped in Gmail, forget to add a link 
to a CTA, or upload images that are too large

44
00:05:18,311 --> 00:05:22,831
and slow to load. All small mistakes—but 
with big consequences for performance.

45
00:05:22,831 --> 00:05:24,720
So, we asked ourselves: how can 
we help you (and your end users)

46
00:05:32,320 --> 00:05:34,480
catch these mistakes before they happen?

47
00:05:35,200 --> 00:05:40,320
I want to show you the end result.

48
00:05:54,400 --> 00:06:03,360
What you're seeing here is a nice-looking 
email in the editor. Looks great! But under

49
00:06:03,360 --> 00:06:12,240
the hood, there are issues. We’ve built a 
QA tool that catches these. For example,

50
00:06:14,880 --> 00:06:24,480
buttons with missing links, 
images that are over 1MB. With the

51
00:06:31,200 --> 00:07:37,680
tool, users can click directly on the 
affected element and fix it immediately.
```
{% endtab %}
{% endtabs %}
