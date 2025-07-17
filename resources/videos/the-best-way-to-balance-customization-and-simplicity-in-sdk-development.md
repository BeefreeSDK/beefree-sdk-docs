---
description: Learn more about how Beefree SDK balances both simplicity and customization.
---

# The BEST Way to Balance Customization and Simplicity in SDK Development

{% embed url="https://www.youtube.com/watch?v=LhNY5KGNxsg" %}

{% tabs %}
{% tab title="About" %}
Watch this DeveloperWeek 2025 talk with Beefree's Senior Fullstack Developer, Luca Filice, as he shares best practices for designing a highly customizable SDK. Learn key strategies and real-world insights from building Beefree’s Custom LLM AddOn—a feature that lets developers integrate their own AI models. Whether you're working with AI-powered tools or developing an SDK, this session covers essential lessons to help you create flexible, developer-friendly solutions. Chapters:&#x20;

* [0:00](https://www.youtube.com/watch?v=LhNY5KGNxsg) - Introduction&#x20;
* [0:27](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=27s) - Balancing customization and simplicity in SDKs&#x20;
* [0:45](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=45s) - Presentation overview&#x20;
* [1:41](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=101s) - How to build a flexible SDK without adding complexity&#x20;
* [2:46](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=166s) - Extending SDK capabilities with the AddOn interface&#x20;
* [3:56](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=236s) - Choosing between Content Dialog and iFrame&#x20;
* [4:52](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=292s) - How the Content Dialog interface works&#x20;
* [5:34](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=334s) - Improving user interactions with Callbacks&#x20;
* [7:08](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=428s) - Creating dynamic and adaptable SDKs&#x20;
* [7:47](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=467s) - Striking the right balance between customization and simplicity&#x20;
* [9:07](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=547s) - Validating features through user feedback&#x20;
* [10:09](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=609s) - Preventing missed opportunities with user involvement&#x20;
* [11:42](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=702s) - Driving adoption with clear documentation&#x20;
* [13:20](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=800s) - The AI arms race explained&#x20;
* [14:52](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=892s) - Benefits of a Custom LLM AddOn&#x20;
* [21:37](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=1297s) - 5 key lessons for building customizable SDKs&#x20;
* [23:25](https://www.youtube.com/watch?v=LhNY5KGNxsg\&t=1405s) - Conclusion
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
1
00:00:03,240 --> 00:00:09,240
Hello everyone! I'm Luca. I work as a Senior 
Full-Stack Software Engineer at Beefree,

2
00:00:09,240 --> 00:00:18,120
where we try to develop a highly 
customizable SDK without sacrificing

3
00:00:18,120 --> 00:00:24,640
ease of implementation. Have you ever tried to 
do that? It's really hard, I can tell you why.

4
00:00:24,640 --> 00:00:31,120
Why is it hard? Because you have to strike the 
right balance between giving your customer the

5
00:00:31,120 --> 00:00:38,160
right amount of customization options while 
keeping the implementation of the SDK easy,

6
00:00:38,160 --> 00:00:42,520
without requiring too much effort on their side.

7
00:00:42,520 --> 00:00:49,280
I'm going to briefly go over the agenda. I'll 
start by defining what it means to make an SDK

8
00:00:49,280 --> 00:00:55,080
customizable and telling you about some of the 
key challenges that you'll face when trying to

9
00:00:55,080 --> 00:01:01,840
do so. Then, I'll give you a brief overview of the 
customization tools we offer at Beefree, just to

10
00:01:01,840 --> 00:01:08,160
give you an example of what customization means 
and maybe give you some ideas for your products.

11
00:01:08,160 --> 00:01:16,040
Then, I'll go over the lessons we learned 
while developing our SDK. These lessons are:

12
00:01:16,040 --> 00:01:21,000
two-way communication, striking the right 
balance, starting small and iterating,

13
00:01:21,000 --> 00:01:26,760
early customer collaboration, and that 
documentation is also essential. Then,

14
00:01:26,760 --> 00:01:32,880
I'll do a deep dive into the development 
of the custom LLM Add-on feature to show

15
00:01:32,880 --> 00:01:41,760
you how these lessons are not just theory, 
but can be applied to a real-world scenario.

16
00:01:41,760 --> 00:01:49,080
To start, what can you do to make your 
SDK customizable? Well, you can imagine

17
00:01:49,080 --> 00:01:57,400
two options. The first one is to give little 
to no customization, limit the possibilities

18
00:01:57,400 --> 00:02:04,920
that the developers have by simplifying a lot the 
integration of your SDK into the host application.

19
00:02:04,920 --> 00:02:13,320
This, though, is not flexible enough and for 
sure not adaptable to huge and complex use cases.

20
00:02:13,320 --> 00:02:19,520
Another option is you can try and guess 
every possible scenario, every possible

21
00:02:19,520 --> 00:02:26,640
use case that your user might have. But even 
this way, you'll probably lose some edge cases,

22
00:02:26,640 --> 00:02:32,320
because there's no one solution to rule 
them all. So, what we did at Beefree was

23
00:02:32,320 --> 00:02:39,960
try to strike the right balance: give our 
customer enough customization options while

24
00:02:39,960 --> 00:02:47,160
still ensuring a smooth integration 
of our SDK into the host application.

25
00:02:47,160 --> 00:02:56,440
One way we do this is by leaving the SDK 
simple and providing our customer with the

26
00:02:56,440 --> 00:03:04,040
Add-on interface. This Add-on interface has 
two aspects: the partner add-ons—add-ons that

27
00:03:04,040 --> 00:03:12,240
we develop or some of our customers developed 
and then, after we approved them, were made

28
00:03:12,240 --> 00:03:19,400
available on our marketplace. These can allow our 
customer to extend the basic functionalities of

29
00:03:19,400 --> 00:03:25,760
the SDK with features we don't provide out 
of the box inside the SDK, but that you can

30
00:03:25,760 --> 00:03:32,560
activate through our Beefree SDK console. This 
is powerful, but an even more powerful version

31
00:03:32,560 --> 00:03:39,040
is the custom add-ons. The custom add-ons are 
basically the same thing as the partner add-ons,

32
00:03:39,040 --> 00:03:45,920
but completely developed by our customer that have 
full control on the logic that resides inside the

33
00:03:45,920 --> 00:03:55,120
add-on, and even the UX and the UI of the add-on, 
that can fit their needs as best as they can.

34
00:03:55,120 --> 00:04:00,720
While developing a custom add-on, we 
give two options to our customers:

35
00:04:00,720 --> 00:04:06,360
they can either go with the iframe, something a 
lot of you might be familiar with, that's great

36
00:04:06,360 --> 00:04:13,280
for hosting complex applications, pre-existing 
applications. It lives inside the SDK but it's

37
00:04:13,280 --> 00:04:19,800
not deeply integrated with it, and it interacts 
with the SDK through JavaScript API. Or, you can

38
00:04:19,800 --> 00:04:26,400
use something we developed: the Content Dialogue. 
This is a layer of interaction between the SDK and

39
00:04:26,400 --> 00:04:33,320
the host application that allows the two-way 
communication we spoke about briefly before.

40
00:04:33,320 --> 00:04:40,440
This Content Dialogue can give our customer full 
control over the UI while offering a seamless

41
00:04:40,440 --> 00:04:48,280
experience because, compared to the iframe, 
it's much more well integrated inside the SDK.

42
00:04:48,280 --> 00:04:52,800
The setup to use the Content Dialogue 
is simple. You need to specify the

43
00:04:52,800 --> 00:04:57,720
contentDialog object inside the beeConfig 
object. The beeConfig object is simply a

44
00:04:57,720 --> 00:05:03,600
JSON that allows our customer to set up 
the settings of the SDK while integrating

45
00:05:03,600 --> 00:05:10,840
it in their host application. The core of 
this is the render function, where all the

46
00:05:10,840 --> 00:05:20,560
custom logic and even the custom UI resides. 
The render function is a simple restriction:

47
00:05:20,560 --> 00:05:28,280
it must either resolve to a valid value responding 
to an interface we provide, or reject if the

48
00:05:28,280 --> 00:05:35,400
interaction is canceled by the user, to allow 
the builder activity to resume seamlessly.

49
00:05:35,400 --> 00:05:42,640
Another important tool you can use to enable 
customization inside your SDK are the callbacks.

50
00:05:42,640 --> 00:05:51,280
These allow your customer to react dynamically 
to events that take place inside the SDK,

51
00:05:51,280 --> 00:05:56,000
such as user interaction or system 
events. In response to these events,

52
00:05:56,000 --> 00:06:01,880
they can trigger custom logic to customize 
the experience for their end user to their

53
00:06:01,880 --> 00:06:09,080
needs. An example of a callback we provide 
inside our SDK is the onChange callback

54
00:06:09,080 --> 00:06:17,000
that allows our customers to react to any 
changes made to the template by the user,

55
00:06:17,000 --> 00:06:26,080
for example, by updating the version 
of the template they save on their DB.

56
00:06:26,080 --> 00:06:29,680
But customization is only the 
beginning. As I told you before,

57
00:06:29,680 --> 00:06:38,920
you cannot customize to the full extent without 
sacrificing a little ease of implementation. So

58
00:06:38,920 --> 00:06:44,200
you need to strike the right balance: make 
the tool flexible enough to respond to your

59
00:06:44,200 --> 00:06:51,160
customer's needs while keeping it intuitive, 
giving control to their developers while also

60
00:06:51,160 --> 00:06:58,680
giving them the chance to implement it into 
their host application in a little time.

61
00:06:58,680 --> 00:06:59,520
While doing this,

62
00:07:00,200 --> 00:07:06,960
we faced many challenges, but through those 
challenges, we learned some important lessons.

63
00:07:06,960 --> 00:07:15,000
The first one is that two-way communication is 
essential to make an SDK highly customizable.

64
00:07:15,000 --> 00:07:20,760
That's because it's hard to have customization 
if there's no way for the SDK to communicate

65
00:07:20,760 --> 00:07:28,080
with the host application and vice versa. An 
example of this in the features we just talked

66
00:07:28,080 --> 00:07:36,320
about are the callback triggers and the Content 
Dialogue interface. Considering your projects,

67
00:07:36,320 --> 00:07:45,280
I want you to think if there's any point where 
you can introduce better two-way communication.

68
00:07:45,280 --> 00:07:50,600
Another lesson we learned, something that I 
already anticipated a little, is that you need to

69
00:07:50,600 --> 00:07:56,960
strike the right balance between customization 
and simplicity. This sometimes boils down to

70
00:07:56,960 --> 00:08:03,000
choosing if you need to provide a tool ready 
to use out of the box or a fully customizable

71
00:08:03,000 --> 00:08:10,320
tool. The difference is that tools ready to use 
out of the box are really nice for developers

72
00:08:10,320 --> 00:08:15,640
because they can implement it in minutes if 
they're fine with the default configurations,

73
00:08:15,640 --> 00:08:22,440
but require more effort on your side as an SDK 
provider because you need to develop the feature

74
00:08:22,440 --> 00:08:29,800
basically all the way. With fully customizable 
tools instead, you shift the development effort

75
00:08:29,800 --> 00:08:35,480
to your customer. This gives them greater 
flexibility; they can do whatever they want

76
00:08:35,480 --> 00:08:41,800
with the feature basically, provided that 
you work really well on the architecture,

77
00:08:41,800 --> 00:08:49,000
because the architecture this time becomes the 
product, and they need a good architecture. You

78
00:08:49,000 --> 00:08:56,200
need to lay the foundation for them to build 
good features. In regards to your product,

79
00:08:56,200 --> 00:09:01,200
I want you to consider if there are areas 
that might be too complicated right now,

80
00:09:01,200 --> 00:09:07,160
and if you could add value for 
your customer by simplifying them.

81
00:09:07,160 --> 00:09:14,400
Another important lesson is to start small and 
iterate. Don't go all out from the get-go. Don't

82
00:09:14,400 --> 00:09:20,120
try to build the perfect product, thinking of 
everything that your customer might need from

83
00:09:20,120 --> 00:09:27,120
the start. Simply build an MVP, a Minimum Viable 
Product, with the minimum features your customer

84
00:09:27,120 --> 00:09:34,960
needs to gain value from your product. Then 
listen to them. Listen to their feedback. Ask

85
00:09:34,960 --> 00:09:42,000
for their feedback. Based on that feedback, 
iterate: change your MVP, add new features,

86
00:09:42,000 --> 00:09:47,200
modify the existing ones that don't work for 
them, and then when you get to the right point,

87
00:09:47,200 --> 00:09:54,920
scale and deliver the product your customer 
actually wants. In regard to your product,

88
00:09:54,920 --> 00:10:00,680
something that I'd like you to do with 
your next feature is to think: what's the

89
00:10:00,680 --> 00:10:09,880
minimum set of features you need to deliver 
to your customer to give them value quickly?

90
00:10:09,880 --> 00:10:15,000
Something that goes hand in hand with the previous 
lesson is that you need to collaborate with your

91
00:10:15,000 --> 00:10:21,200
customer early. The sooner you do it, the 
better it is for you. Why? Because it allows

92
00:10:21,200 --> 00:10:28,960
you to focus on what really matters for them. 
You won't waste development effort on features

93
00:10:28,960 --> 00:10:34,520
that they might not find that useful, but you 
could consider useful. And most importantly,

94
00:10:34,520 --> 00:10:40,760
you will work based on real-world needs, 
real-world considerations for your customer,

95
00:10:40,760 --> 00:10:48,080
and not just internal assumptions that no matter 
how knowledgeable you are about your area,

96
00:10:48,080 --> 00:10:54,680
might still be wrong. Introducing collaboration 
from your customer early on basically allows you

97
00:10:54,680 --> 00:11:02,680
to expand the cycle we saw in the previous slide 
by having your customer feedback even from the

98
00:11:02,680 --> 00:11:09,400
planning stage. And this allows you to have the 
prototype that's basically the MVP we spoke about

99
00:11:09,400 --> 00:11:17,560
before that's almost already what your customer 
needs. Thinking of your products, is there any

100
00:11:17,560 --> 00:11:24,640
feature you delivered in the last month/year where 
having had the customer collaboration, customer

101
00:11:24,640 --> 00:11:33,040
feedback, earlier in the process would have helped 
you deliver better value? Can you think of a next

102
00:11:33,040 --> 00:11:42,560
feature that you're going to release where you 
could benefit from involving customers early?

103
00:11:42,560 --> 00:11:48,440
Last but not least, don't forget the documentation 
is essential. You might build the best SDK,

104
00:11:48,440 --> 00:11:54,000
the most customizable SDK, but it will 
still be useless if your customers don't

105
00:11:54,000 --> 00:12:00,480
have the right documentation to understand 
how to use it and how it works. At Beefree,

106
00:12:00,480 --> 00:12:07,200
we go by the "Eat Your Own Dog Food" principle: 
be your first customer. A way you can apply that

107
00:12:07,200 --> 00:12:12,920
to documentation is once your feature is ready 
and you have the documentation for that feature,

108
00:12:12,920 --> 00:12:19,480
have someone from your team, ideally that doesn't 
work on that specific feature, try to implement or

109
00:12:19,480 --> 00:12:25,160
try to use that feature by going off of the 
documentation alone. If you can do it, your

110
00:12:25,160 --> 00:12:31,280
documentation is solid, you're good to go. If you 
cannot, that's great because you spotted a huge

111
00:12:31,280 --> 00:12:38,360
error before your customer did. This will save you 
headaches, support tickets, lost adoption, and a

112
00:12:38,360 --> 00:12:46,440
lot of frustration on your customers' developers 
that due to that frustration might even migrate to

113
00:12:46,440 --> 00:12:55,320
one of your competitors. So, thinking about your 
product, if you go home now, can you implement one

114
00:12:55,320 --> 00:13:03,360
of your important features going only off of the 
documentation without asking for internal help?

115
00:13:03,360 --> 00:13:09,200
As I told you before, all these lessons are 
not just theory, they are derived from our

116
00:13:09,200 --> 00:13:16,320
experience and can apply to specific real-world 
cases. The one I'm going to talk to you about is

117
00:13:16,320 --> 00:13:22,960
the implementation of the custom LLM Add-on. But 
before doing that, a little bit of background.

118
00:13:22,960 --> 00:13:29,480
As you know, we are in the midst of an AI race 
where everyone is striving to use the best model,

119
00:13:29,480 --> 00:13:34,200
introduce AI features in their 
product, sometimes even if they

120
00:13:34,200 --> 00:13:40,040
don't know if that's actually useful for 
the users or if the user really wants it,

121
00:13:40,040 --> 00:13:44,680
just to keep up with the trend 
and be part of the cool kids.

122
00:13:44,680 --> 00:13:52,280
What we did at Beefree was evaluate the needs 
of our customers and introduce a range of AI

123
00:13:52,280 --> 00:13:57,960
features, starting with the AI writing assistant, 
then going to the AI-generated alt text,

124
00:13:57,960 --> 00:14:06,360
image generation, and bulk translation to aid 
our customer in their daily work and speed up the

125
00:14:06,360 --> 00:14:13,880
generation of the template. Even though this tool 
was already requested and we saw good adoption,

126
00:14:13,880 --> 00:14:21,120
we saw little to no adoption for the Enterprise 
customers, and this led us to ask some questions:

127
00:14:21,120 --> 00:14:29,280
why weren't they using it? It's simple: they 
needed more control. They had strict policies on

128
00:14:29,280 --> 00:14:37,080
privacy and how their data were used, and they 
weren't fine with the fact that the feature we

129
00:14:37,080 --> 00:14:46,760
developed uses commercially available models 
such as ChatGPT or OpenAI or Stable Diffusion,

130
00:14:46,760 --> 00:14:53,240
because it's not always clear how 
those models handle your data. So we

131
00:14:53,240 --> 00:15:01,000
needed to find a way to deliver the 
custom LLM feature to our customer.

132
00:15:01,000 --> 00:15:08,160
Why did we go with the custom add-on? Because 
we went through the tools at our disposal in

133
00:15:08,160 --> 00:15:13,000
order to see if we already had something they 
could use to introduce their custom LLM inside

134
00:15:13,000 --> 00:15:20,960
the SDK. And at first, the custom add-on seemed 
like a good solution because it could allow for

135
00:15:20,960 --> 00:15:27,440
high customization inside the SDK, and it 
was basically up to them to decide what to

136
00:15:27,440 --> 00:15:34,960
do with a custom add-on. But this meant for 
them they needed to duplicate all the tiles,

137
00:15:34,960 --> 00:15:44,640
the modules we use inside our builder, where 
they wanted to use AI-powered features. This

138
00:15:44,640 --> 00:15:51,480
of course required a high development effort 
on their side, and at the same time delivered

139
00:15:51,480 --> 00:15:58,360
a poor experience for the end user, making it 
inconsistent when they were with huge differences

140
00:15:58,360 --> 00:16:04,360
when they were using our AI-provided 
features versus the custom LLM features.

141
00:16:04,360 --> 00:16:12,680
So what we decided to do: create a partner add-on 
specifically made by us to implement custom

142
00:16:12,680 --> 00:16:19,120
LLMs inside the SDK. This allowed for seamless 
integration inside the builder, the array usage

143
00:16:19,120 --> 00:16:26,640
of the same entry point we had for our AI writing 
assistant, keeping the user experience consistent.

144
00:16:26,640 --> 00:16:35,640
While doing this, we used the lessons we learned 
from previous implementations to drive the result.

145
00:16:37,000 --> 00:16:43,040
The first lesson we considered was two-way 
communication. We needed a way to establish

146
00:16:43,040 --> 00:16:49,280
communication between the SDK and the custom 
LLM of our customers. How we decided to do it:

147
00:16:49,280 --> 00:16:57,640
with the Content Dialogue interface I talked to 
you before. We knew this solution was reliable,

148
00:16:57,640 --> 00:17:05,640
could scale well, and was adaptable enough to 
change in response to the changing needs for our

149
00:17:05,640 --> 00:17:13,240
customer. What we needed to get right though was 
the interface, because compared to our AI writing

150
00:17:13,240 --> 00:17:20,520
assistant, the Content Dialogue interface is 
not that deeply integrated with the SDK. All

151
00:17:21,040 --> 00:17:29,320
the data you can access are those that we give as 
input to the Content Dialogue. And at first, we

152
00:17:29,320 --> 00:17:36,040
thought we knew what our customer needed, but 
going by the second lesson, early customer

153
00:17:36,040 --> 00:17:42,560
collaboration, we soon discovered that it wasn't 
the case. We thought all they needed to use their

154
00:17:42,560 --> 00:17:49,160
custom LLM was the content of the module they 
were working on, but after confronting with some

155
00:17:49,160 --> 00:17:55,440
of our customers, we discovered that they also 
needed the module UI and the module type to get

156
00:17:55,440 --> 00:18:01,600
better results. Why we didn't consider those 
two? Because with our AI writing assistant,

157
00:18:01,600 --> 00:18:09,680
that's deeply integrated into the SDK, 
those information are easily accessible.

158
00:18:09,680 --> 00:18:17,120
Early customer collaboration also helped us in 
making the biggest design decision we had for

159
00:18:17,120 --> 00:18:24,400
this feature. We had to decide whether 
to provide pre-built UI to our customer

160
00:18:24,400 --> 00:18:33,240
or if we wanted to let them develop their 
custom-made UI from scratch. We were going

161
00:18:33,240 --> 00:18:39,240
with option one. Why? Because we thought 
they already have to implement the backend,

162
00:18:39,240 --> 00:18:46,440
we can meet them halfway by providing 
a UI that mimics our writing assistant,

163
00:18:46,440 --> 00:18:52,800
where they can simply attach their backend. 
But after confrontation with our customer,

164
00:18:52,800 --> 00:18:58,800
we discovered that they didn't care for our 
UI because they wanted to make their own UI

165
00:18:58,800 --> 00:19:05,960
to make a seamless experience inside their host 
application. So we dropped the pre-built UI and

166
00:19:05,960 --> 00:19:11,040
basically got a win-win because there was less 
development effort on our side, effort that would

167
00:19:11,040 --> 00:19:21,320
have gone to waste either way, and the customers 
still got to keep the flexibility they desired.

168
00:19:21,320 --> 00:19:28,080
How we managed to do all of this is by keeping in 
mind the documentation is a feature. Because even

169
00:19:28,080 --> 00:19:35,600
if we had developed an MVP, if we didn't write 
documentation for the MVP, basically writing a

170
00:19:35,600 --> 00:19:42,280
first draft right after the MVP was ready, our 
customer would have had no way of knowing how to

171
00:19:42,280 --> 00:19:50,240
use the feature, how to understand how it works. 
By giving our customer the documentation for the

172
00:19:50,240 --> 00:19:57,840
MVP as soon as it was ready, they were able 
to help us in defining the interface as I told

173
00:19:57,840 --> 00:20:05,080
you before and understanding that they didn't 
need the pre-built UI. One thing we wanted to

174
00:20:05,080 --> 00:20:11,680
do but we fell short here was ask some of our 
customer to develop a PoC while we were still

175
00:20:11,680 --> 00:20:19,120
developing the MVP. But unfortunately, even though 
we involved them early in the development process,

176
00:20:19,120 --> 00:20:26,280
it was still too late because they needed 
time to allocate resources to this kind

177
00:20:26,280 --> 00:20:34,040
of test. They couldn't do it in the time we 
had at our disposal to develop the feature.

178
00:20:34,040 --> 00:20:40,680
The last lesson that we applied to this 
development was to start small and iterate.

179
00:20:40,680 --> 00:20:47,840
In this case, this meant building the minimum 
viable interface for the Content Dialogue

180
00:20:47,840 --> 00:20:53,760
with the feedback we got from our customers 
and focus only on the AI writing assistant,

181
00:20:53,760 --> 00:21:03,040
even though we provide other AI features. This was 
meant to avoid over-investing up front. Now that

182
00:21:03,040 --> 00:21:11,600
we have delivered this feature to our customer, 
we can wait for the feedback, see what they tell

183
00:21:11,600 --> 00:21:17,960
us about the feature, see if they actually adopt 
it. If they do, well, we have a solid foundation,

184
00:21:17,960 --> 00:21:24,560
solid reasons to go ahead and expand the custom 
LLM integration to all the other AI features we

185
00:21:24,560 --> 00:21:35,680
provide. If they don't, well, we won't have wasted 
development effort on features they don't use.

186
00:21:35,680 --> 00:21:41,200
So, as you saw, these lessons are not just 
theory, they can apply to real-world scenarios

187
00:21:41,200 --> 00:21:46,600
and help you shape your design decisions 
and the way you deliver the feature to

188
00:21:46,600 --> 00:21:53,040
your customer. I'd like to briefly go over 
them once more before closing this talk.

189
00:21:53,040 --> 00:21:59,000
The first lesson is that two-way communication 
is essential for customization because you need

190
00:21:59,000 --> 00:22:04,120
to establish a channel of communication between 
your SDK and the application that's integrating

191
00:22:04,120 --> 00:22:13,360
it. Second, involve your customer early. This 
will help you avoid wasted effort and deliver the

192
00:22:13,360 --> 00:22:20,000
product your customer needs earlier than you would 
without involving them. You need to strike the

193
00:22:20,000 --> 00:22:26,880
right balance between flexibility and simplicity: 
know when to use a ready-to-use tool out of

194
00:22:26,880 --> 00:22:35,200
the box and when to give your customer the full 
customization option, knowing that it will require

195
00:22:35,200 --> 00:22:42,400
more effort on their side. The fourth lesson: 
documentation is a feature. Remember, if you build

196
00:22:42,400 --> 00:22:48,800
the best SDK but don't have good documentation 
to go with it, your customer wouldn't know how to

197
00:22:48,800 --> 00:22:55,400
make the most out of your tool. They might use 
it for maybe 10% of the value they might get,

198
00:22:55,400 --> 00:23:02,640
or they might even get frustrated and abandon 
it altogether. Last, start small, iterate, and

199
00:23:02,640 --> 00:23:10,720
scale. This is another way you can avoid wasting 
development effort by launching an MVP early on,

200
00:23:10,720 --> 00:23:17,040
gather real feedback from your customer, and 
based on that, expand strategically, either

201
00:23:17,040 --> 00:23:24,600
building upon what you already did or reworking 
what you did if that doesn't suit your customer.

202
00:23:24,600 --> 00:23:30,960
I'd like you to think after this talk if these 
lessons apply in any shape or form to your SDK,

203
00:23:32,600 --> 00:23:38,360
and the challenges you faced while 
creating your SDK or the SDK you are

204
00:23:38,360 --> 00:23:51,560
thinking of creating while trying to make it 
flexible but keeping it simple to integrate.
```
{% endtab %}
{% endtabs %}
