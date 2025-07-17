---
description: >-
  Learn more about how to use Beefree SDK's Simple Schema to integrate
  AI-generated designs into your end user's workflows.
---

# Beefree SDK Spotlight Session: Simple Schema

{% embed url="https://www.youtube.com/watch?v=DEpQERhWV9E" %}

{% tabs %}
{% tab title="About" %}
Learn how to use Simple Schema to create Beefree designs programmatically—outside of the builder. This session covers how to generate designs using your own AI tools and Simple Schema, convert them to full JSON via the /simple-to-full-json API endpoint, and load them into the builder for editing. We’ll also explore what headless design creation means and how it opens up new possibilities for developers building custom workflows with the Beefree SDK.&#x20;

**Chapters:**&#x20;

* [0:00](https://www.youtube.com/watch?v=DEpQERhWV9E) Welcome & Session Overview&#x20;
* [4:45](https://www.youtube.com/watch?v=DEpQERhWV9E\&t=285s) What is Bree Simple Schema? (Problem & Solution)&#x20;
* [7:32](https://www.youtube.com/watch?v=DEpQERhWV9E\&t=452s) Live Demo: Training AI with Simple Schema&#x20;
* [16:03](https://www.youtube.com/watch?v=DEpQERhWV9E\&t=963s) Live Demo: Scenario 1 - AI-Driven Content Creation&#x20;
* [20:12](https://www.youtube.com/watch?v=DEpQERhWV9E\&t=1212s) Live Demo: Scenario 2 - Generating Multiple Template Versions&#x20;
* [24:50](https://www.youtube.com/watch?v=DEpQERhWV9E\&t=1490s) Q\&A Session&#x20;
* [45:44](https://www.youtube.com/watch?v=DEpQERhWV9E\&t=2744s) Closing Remarks
{% endtab %}

{% tab title="Transcripts" %}
The following text includes the complete transcript for this video.

```
0:00:08.240,0:00:24.160
Hello, hi everyone! Hi there. Welcome 
to Simple Schema. If you're joining us,

0:00:24.160,0:00:29.840
if you're here, put a little note in the 
chat message down on the right-hand side

0:00:29.840,0:00:37.440
and let us know where you're joining from. 
Hello! My name is McKenzie, this is Zair,

0:00:37.440,0:00:44.320
and we'll wait a few minutes to get started here, 
but we're on the West Coast of the United States,

0:00:44.320,0:00:50.080
if you can't tell from my accent. So I'm in 
Portland, Oregon. We've got Mark from Lincoln,

0:00:50.080,0:00:54.880
Nebraska. Hello, my fellow Midwesterner, 
not sure if that's what we call us. I'm

0:00:54.880,0:01:04.160
from Wisconsin originally. Hello Blaine from 
San Francisco, hi Alex, got Denver, Colorado.

0:01:04.160,0:01:16.240
California, Little Rock, Arkansas. How's 
the weather everywhere? It's really sunny

0:01:16.240,0:01:21.120
here today in Portland. We're having a 
beautiful Portland, Oregon sunny day,

0:01:21.120,0:01:28.240
which is certainly an oxymoron. It's 
quite rainy here, but spring's coming,

0:01:28.240,0:01:34.800
or spring's here, I think almost, and then it'll 
be summer soon. Thanks for joining us everyone

0:01:34.800,0:01:41.360
to talk about Simple Schema. We'll just give it 
another couple minutes before we get going. Oh,

0:01:41.360,0:01:49.200
tornado storms incoming in Arkansas. Okay, stay 
safe out there, but stay on this call because

0:01:49.200,0:02:00.480
this is very important. No, I'm kidding. Please 
stay safe in Arkansas. We've got Utah, Germany,

0:02:00.480,0:02:10.000
Berlin. I'll be in Berlin next week, maybe I'll 
see you there. We'll give it just a couple more

0:02:10.000,0:02:19.680
moments. Again, thanks for joining us. I'm located 
in Portland, Oregon, on the West Coast here in

0:02:19.680,0:02:31.920
the US. Zair's down in San Diego, right? Yep, yep, 
sunny San Diego, it's always a beautiful day here.

0:02:35.920,0:02:58.560
Um, yeah, we could use a Berlin email geek 
meetup. Okay, I think we'll get going here. So,

0:02:59.600,0:03:03.200
I'm McKenzie Wacker, and I have worked with,

0:03:03.200,0:03:08.720
um, I've worked on the Beefree SDK Customers 
team here for about a year, so perhaps I've

0:03:08.720,0:03:15.840
interacted with some of you, and hopefully 
I've helped you. And Zair here: Hey everyone,

0:03:15.840,0:03:22.880
I'm Zair. I'm the Lead Technical Writer here at 
Beefree SDK. I'm on the Product Engineering team,

0:03:22.880,0:03:28.880
and I'm excited to be with you all here today and 
to talk a little bit more about Simple Schema. And

0:03:28.880,0:03:36.320
like McKenzie mentioned, I'm located in Southern 
California, in the wonderful city of San Diego.

0:03:37.200,0:03:42.960
Yeah, so again, thank you all for joining here. 
We're going to talk about, if you want to go to

0:03:42.960,0:03:50.560
the next slide, Zair, just a couple notes first. 
So on the right-hand side, you've found the chat

0:03:50.560,0:03:56.480
box. A lot of you have found the chat box. There 
is also a Questions section down there. It's the

0:03:56.480,0:04:01.360
tab next to Questions. So throughout this, we're 
going to, yeah, I'm going to give an introduction

0:04:01.360,0:04:06.720
to the Simple Schema, talk about the benefits. 
Then I'll pop it over to Zair for a live demo,

0:04:06.720,0:04:13.440
and at the end we'll have a Q&A session. So feel 
free to put your questions down into the Question

0:04:13.440,0:04:19.520
section next to the chat, and we'll save them till 
the end. And then we'll try to get through as many

0:04:19.520,0:04:25.040
as we can, but if we don't get through them all, 
that's okay. This is being recorded, so you will

0:04:25.040,0:04:31.040
receive the recording of this afterwards. And 
then if we don't get to your question today,

0:04:31.040,0:04:38.640
we'll follow up with you individually afterwards. 
And then we also, you know, we can always email

0:04:38.640,0:04:47.040
pluginsupport@beefree.io with any further 
questions as well if something comes up later.

0:04:47.040,0:04:54.160
So let's get going. What is the Beefree Simple 
Schema? Well, let's start with the problem or

0:04:54.160,0:05:00.000
the challenge that we were having. For years now, 
we've received many requests from customers asking

0:05:00.000,0:05:06.160
if you can open up the internal JSON language 
so that they can generate Beefree-compatible

0:05:06.160,0:05:12.720
content outside of the editor. People have been 
wanting to more easily and programmatically

0:05:12.720,0:05:17.600
generate native Beefree JSON without having to 
enter the editor. So in the last couple years,

0:05:17.600,0:05:23.120
we've had even more people make this request 
because they want to train an AI model on

0:05:23.120,0:05:28.320
the structure of our JSON so the model can 
appropriately respond to prompts requesting

0:05:28.320,0:05:33.680
for content or full templates that match 
our JSON and can then be uploaded and be

0:05:33.680,0:05:39.920
compatible with the editor. So the challenge 
here is that the Beefree native JSON is just,

0:05:39.920,0:05:45.120
it's way too complex for these tasks. And 
one reason for that is it doesn't just hold

0:05:45.120,0:05:50.400
the structure of your design, it also powers 
things like the drag-and-drop functionality

0:05:50.400,0:05:55.520
within the editor and so much else. So 
what we really needed here was a simpler,

0:05:55.520,0:06:03.600
more streamlined data structure for the AI models 
and the developers alike to work with more easily.

0:06:03.600,0:06:08.560
So our team listened, and we 
developed the Simple Schema.

0:06:08.560,0:06:13.840
So the Simple Schema is a new data structure 
that is much more simple and streamlined,

0:06:13.840,0:06:20.000
and it's a versatile version of the Beefree native 
JSON. It's designed to make that programmatic

0:06:20.000,0:06:25.840
template creation much more accessible, especially 
for AI models, which we're going to really get

0:06:25.840,0:06:32.160
into today. With the Simple Schema, you can now 
generate full templates or content outside of the

0:06:32.160,0:06:38.080
visual builder, whether manually or using AI. And 
if you'd like, you can then use our new Simple to

0:06:38.080,0:06:44.800
Full Schema conversion API to turn your content 
into the full Beefree JSON schema so that it's

0:06:44.800,0:06:52.960
also editable in the editor. The key benefit 
here of the Simple Schema is that it opens

0:06:52.960,0:07:00.160
that door for AI-powered content generation, 
so you can train a large language model to

0:07:00.160,0:07:06.160
create full templates, or a small 
AI model to handle copy, images,

0:07:06.160,0:07:11.040
layout separately. So whether you're building 
templates via code or training generative AI

0:07:11.040,0:07:18.880
tools, this schema reduces that complexity that is 
with the Beefree native JSON, and it just really

0:07:18.880,0:07:24.400
speeds up development. It also significantly 
enhances custom add-on development, making that

0:07:24.400,0:07:32.720
easier and more flexible than ever with more 
properties and simplified schema management.

0:07:32.720,0:07:40.400
So now we're going to have Zair here come on 
and give us a demo. All right, thanks so much

0:07:40.400,0:07:47.040
for that awesome introduction, McKenzie, and hello 
everyone. So for this portion of the presentation,

0:07:47.040,0:07:52.960
we're going to walk through a live demo, and 
the best and easiest way for me to do that is

0:07:52.960,0:07:57.760
to navigate through these different tabs 
that I have open on my screen right now.

0:07:57.760,0:08:02.720
So just bear with me as I navigate through 
the various tabs. If for any reason along

0:08:02.720,0:08:08.960
the way there's something on my screen that's too 
tiny, just let me know and I can zoom in further

0:08:10.400,0:08:18.560
so that way you all can see what I'm doing. 
So when we talk about Simple Schema, one of

0:08:18.560,0:08:25.600
the first steps we take is to train AI with the 
Simple Schema, and in order to really understand

0:08:25.600,0:08:31.360
what that looks like, I want to go through a 
few of the resources that we created when we

0:08:31.360,0:08:38.400
first went live with Simple Schema. One of those 
resources was this GitHub repository, and I'll

0:08:38.400,0:08:45.920
actually share the link to this repository here 
in the chat that way everyone can access this as

0:08:45.920,0:08:53.600
I go along for this portion of the presentation. 
And in this repository, you'll notice that we have

0:08:54.320,0:08:59.520
many different schemas. So Simple Schema 
is actually composed of all these various

0:08:59.520,0:09:06.560
components. So you'll notice that we have the 
structure for a simple template. We also have

0:09:06.560,0:09:14.640
a definition schema, and then when we think about 
how templates are created within Beefree, we have

0:09:14.640,0:09:22.560
the infrastructure is essentially to create 
rows, and within rows, so here we have the Simple

0:09:22.560,0:09:27.840
Row Schema. Within rows, we have columns, 
we have the Simple Column Schema over here,

0:09:27.840,0:09:35.120
and then within columns, we have different 
content blocks and modules. So those options

0:09:35.120,0:09:42.240
include button, divider, HTML, icons, and so 
on. So when we talk about training an AI agent,

0:09:42.240,0:09:48.800
what we're really talking about is taking these 
files that are included in this repository and

0:09:48.800,0:09:56.640
using them as a set of instructions for an 
AI agent to learn off of. So that's step one.

0:09:56.640,0:10:03.520
Now let's talk about an example prompt. So 
when we're prompting AI, we want to make sure

0:10:03.520,0:10:09.440
that we're very clear. The instructions that 
we provide it with that way it leverages the

0:10:09.440,0:10:17.360
various files that I went over earlier to create 
valid templates, JSON templates. And the reason

0:10:17.360,0:10:23.440
why that's important is because we're in our next 
step. We're going to be making a few API calls.

0:10:23.440,0:10:32.800
So when we talk about a prompt here on the screen, 
I have a few instructions here. I'm talking about

0:10:32.800,0:10:44.160
a template that is targeted at dog lovers, and 
here I'm telling the AI agent to reference this

0:10:44.160,0:10:52.560
Simple Template Schema, which I pointed out in 
the repository earlier, and mentioning that this

0:10:52.560,0:10:58.000
defines the overall structure of the template, so 
to use it as a reference correctly. And then we

0:10:58.000,0:11:02.480
all know that sometimes AI can be a little bit 
creative. Sometimes it has a mind of its own,

0:11:02.480,0:11:07.440
and we want to make sure that when we're 
constructing templates, that AI stays on

0:11:07.440,0:11:13.760
track. So the ways that we provide instructions 
for AI to stay on track is really important,

0:11:13.760,0:11:18.800
and I include a few high-level bullet points 
over here that kind of go over that guidance,

0:11:18.800,0:11:24.880
right? So strictly follow the schemas provided, 
those are the ones that we referenced. Do not use

0:11:24.880,0:11:30.560
any properties that are not explicitly supported. 
This is just to keep AI on track and make sure it

0:11:30.560,0:11:36.880
doesn't invent any properties along the way. 
And then ensure that all required properties

0:11:36.880,0:11:42.960
are correctly included, and then the final 
output should be that valid Simple Template

0:11:42.960,0:11:50.720
JSON. So this is an example. As you train your 
own AI models to build these schemas, you're

0:11:50.720,0:11:57.040
probably going to add many more instructions, 
but this is just a high-level overview for a

0:11:57.040,0:12:02.480
minimalist type of implementation, 
which we're going to go over today.

0:12:02.480,0:12:09.120
So now let's jump into the next step. Okay, we 
talked about how to train AI, where those schemas

0:12:09.120,0:12:14.800
are, what an example prompt should look like. 
Let's talk about what this API call looks like.

0:12:15.440,0:12:21.680
So in our technical documentation, we actually 
have an interactive testing environment,

0:12:21.680,0:12:29.360
and that interactive testing environment, 
um, I'll go ahead and navigate to it very

0:12:29.360,0:12:39.360
quickly over here in this tab. And it's all 
the way over here, Simple to Full. So it's

0:12:39.360,0:12:47.440
this section of the documentation. It talks about 
the different requirements for making an API call,

0:12:47.440,0:12:55.440
and then you can actually test that out over here. 
If you click Test It, it just navigates over to

0:12:55.440,0:13:00.320
an environment that looks a lot like this, and 
you'll notice that I already prepopulated some

0:13:00.320,0:13:06.880
information here, but I'm still going to go over 
the different components. So the first part is the

0:13:06.880,0:13:14.240
URL. The endpoint is simple-to-full-json. It does 
require the collection. The collection for this

0:13:14.240,0:13:20.240
one is conversion, and in order to authenticate, 
you need to have a bearer token, and you can get

0:13:20.240,0:13:28.480
that bearer token within the Beefree SDK Developer 
Console, and that'll be, um, that'll be the token

0:13:28.480,0:13:33.040
that's associated with like API key. So it'll 
say API key, and you use that, and you enter

0:13:33.040,0:13:41.600
it as a bearer token here. And then we on our 
docs site, we actually already have an example,

0:13:41.600,0:13:50.880
um, template that was created using Simple Schema 
and AI that you can go ahead and test a conversion

0:13:50.880,0:13:56.240
with if you want to start experimenting. And 
as we scroll down, we'll notice that this

0:13:57.040,0:14:09.760
body, this request body, is only 313 lines long. 
Now when we make a request, okay, perfect. And we

0:14:09.760,0:14:19.040
now get our full Beefree SDK JSON, and we scroll 
all the way down. I'm still scrolling, so I did

0:14:19.040,0:14:28.720
scroll past line 313, and I'm still scrolling. 
Almost there, I'll try to speed this up. Okay,

0:14:28.720,0:14:39.200
so yeah, we're about a thousand lines over what 
Simple Schema was. So that's, this touches on the

0:14:39.200,0:14:49.840
point that McKenzie made earlier, right? 313 
lines, that's a very reasonable, um, quantity

0:14:49.840,0:14:56.160
to train AI off of. AI can keep up with that, 
but when we're talking about our more complex

0:14:56.160,0:15:07.200
Beefree JSON that is builder-compatible, that is 
much more difficult to train AI with because of

0:15:07.200,0:15:17.280
the volume. We're talking about 1,377 lines here 
compared to 313. That's a very large difference.

0:15:17.920,0:15:24.160
So that's what makes Simple Schema so easy 
to use is that with a simple API call,

0:15:24.160,0:15:33.200
you can convert that AI-generated template into 
the Beefree SDK-compatible JSON that can then

0:15:33.200,0:15:40.480
be loaded within the builder by end-users. 
So that's how the API call works. If you

0:15:40.480,0:15:46.480
are interested in experimenting with the APIs, 
with this API endpoint in particular, you can

0:15:46.480,0:15:52.800
check out the documentation. It'll navigate you to 
the same exact environment. The only thing you'll

0:15:52.800,0:16:00.880
need to add is your own bearer token and make 
sure that you set the collection to conversion.

0:16:00.880,0:16:10.080
All right, so now that we've gone over, um, 
the Simple Schema files, the example prompt,

0:16:10.080,0:16:20.240
and how the API call works, now we can go ahead 
and jump into scenario one. So in this repository,

0:16:20.240,0:16:26.800
you'll notice that I included this folder called 
Simple Schema Concept, and in this folder, we have

0:16:26.800,0:16:32.640
an example scenario of how you can implement 
a Simple Schema for your end-users and how to

0:16:32.640,0:16:40.000
create an AI-driven content creation experience 
for them, uh, using this folder. It's kind of

0:16:40.000,0:16:46.880
an inspirational guide. It's very minimalist, 
bare bones, but it does the job in terms of

0:16:46.880,0:16:53.680
providing that inspirational aspect. So let's 
take a visual look at all of this, and I'm going

0:16:53.680,0:17:11.200
to open my demo environment very quickly. So I 
have this, okay, awesome. So here's a very simple,

0:17:11.200,0:17:19.840
um, experience that I've created, and you can see 
on the front end, this looks like an application.

0:17:19.840,0:17:30.480
I built all of this, so it's all, um, just, uh, 
additional add-ons, um, and here you'll notice

0:17:30.480,0:17:37.200
that there is this rectangle that says "Use AI 
to build your first design." So I'm an end-user,

0:17:37.200,0:17:44.720
I'm going to go ahead and click this button, 
and I see, uh, "AI Email Design Assistance."

0:17:44.720,0:17:52.320
This is again, just an inspirational popup, 
and it's asking me to describe my email design,

0:17:52.320,0:17:58.240
and it provides me with a few tips for the best 
results. So here I'm going to go ahead and write a

0:17:58.240,0:18:15.600
prompt, uh, something like, uh, "Provide me with a 
compelling email that follows email best practices

0:18:15.600,0:18:32.640
defined by the greatest marketers of all time. The 
products should be from my product offering." And

0:18:32.640,0:18:42.560
now I'm just going to wrap this up: "Include the 
tech line of products." All set. So that's good

0:18:42.560,0:18:49.680
to go. I click Generate, and now as an end-user, 
I'm seeing this, uh, confirmation message. Again,

0:18:49.680,0:18:55.600
this is all the part of the experience that 
I created, and then I click "Customize my new

0:18:55.600,0:19:02.160
email," and I'm redirected to the Beefree 
SDK Builder, and now I have this template

0:19:02.160,0:19:08.320
that was created programmatically, automatically 
loaded within the builder, and as an end-user,

0:19:08.320,0:19:15.920
I can start editing it. So I can see that all of 
these modules are clickable, they're editable. Um,

0:19:15.920,0:19:23.760
I can add text within there, and I can also, 
um, let's say I want to add some, you know,

0:19:23.760,0:19:35.120
additional modules, I can also do that. So let's 
talk a little bit about what happened, um, when I,

0:19:35.120,0:19:43.280
uh, as the end-user, um, clicked or submitted 
my prompt. That prompt was sent to the backend

0:19:43.280,0:19:53.120
and used as context for the Simple Schema to be 
generated. And then that generated Simple Schema,

0:19:53.120,0:19:59.200
based off of the prompt that the end-user 
submitted, is then sent over to the API

0:19:59.200,0:20:05.360
endpoint. The API endpoint creates this template, 
and then this template loads within the builder,

0:20:05.360,0:20:15.040
and the end-user is redirected to that. So this 
is scenario one. And I'll go through one more

0:20:15.040,0:20:24.000
scenario. And before I jump into that second 
scenario, I want to take you to Deepseek,

0:20:24.000,0:20:32.240
where I had a quick and brief conversation with 
Deepseek about creating not just one template,

0:20:32.240,0:20:37.920
but three templates for me all at once. And the 
reason why I want to get into this is because

0:20:37.920,0:20:45.680
this concept touches upon how you can create 
multiple versions of a template and then allow

0:20:45.680,0:20:52.640
your end-users to select which version works 
best for them and their needs. And then you

0:20:52.640,0:20:58.880
can create a scenario in which you can actually 
gather more information about your end-users

0:20:58.880,0:21:07.920
and their preferences based on providing them 
with multiple options. So I attached my files,

0:21:07.920,0:21:17.120
these all came from the GitHub repository. 
Deepseek in this chat has like a ten-file limit,

0:21:17.120,0:21:22.960
so I couldn't actually attach more than ten files, 
so I pasted the last three. That's why in the

0:21:22.960,0:21:32.000
prompt, you'll see that I've attached and pasted 
the different schemas within here, within this

0:21:32.000,0:21:41.360
message. And then I provided it with the prompt 
guidelines that I mentioned in the presentation,

0:21:41.360,0:21:49.520
in this portion, in the example prompt. And then 
from there, I went on to describe the scenario.

0:21:49.520,0:21:56.800
So I mentioned that this is for dog lovers. It 
should include these different color preferences

0:21:56.800,0:22:02.960
for each template, and then it should remain 
consistent with these essential products. So I go

0:22:02.960,0:22:11.280
on to provide it with all of those instructions, 
and then it starts generating these templates.

0:22:11.280,0:22:28.080
So now let's take a look at what that looked like 
as the final result. So over here, okay, so now

0:22:28.080,0:22:37.760
this is the new version, the new environment that 
shows three versions of an email design based on

0:22:37.760,0:22:46.640
an end-user's one prompt. So I click here. I 
provide, you know, the same prompt. I want to,

0:22:46.640,0:22:57.920
well, a different prompt in this scenario. 
I want to make an email campaign for dog

0:22:57.920,0:23:10.400
lovers advertising my products. And then here I 
click Generate. Excuse me. And now I have three

0:23:10.400,0:23:16.400
different versions here, and at a glance, you can 
see that this one is a little bit slightly darker

0:23:16.400,0:23:22.560
blue, this one's a lighter blue in the background, 
and this one has a gray background. And if you're

0:23:22.560,0:23:31.680
wondering how I was able to generate these images, 
I was able to do that using the /html and /image

0:23:31.680,0:23:39.040
endpoints, which brought them, which brought these 
images into this portion. So it's really using

0:23:39.040,0:23:44.560
the Simple Schema endpoint, the HTML endpoint, 
and then also the Image endpoint, which you can

0:23:44.560,0:23:52.640
learn more about in our technical documentation. 
So I'm just going to click on Version One as the

0:23:52.640,0:23:59.600
end-user, and now I'm redirected to this template, 
and you'll notice here that I'm redirected to an

0:23:59.600,0:24:06.880
email. It includes the images that I included 
in my prompt. It includes the different products

0:24:06.880,0:24:14.480
that I wanted to advertise. And while it's not 
a perfect design, it's something that you can

0:24:14.480,0:24:21.440
absolutely iterate upon, um, as you create 
more sophisticated prompts on your backend.

0:24:22.160,0:24:30.000
And now as the end-user, because I selected this, 
uh, template, Template One, you've also learned

0:24:30.000,0:24:37.360
more about my design preferences, and you can use 
that information to create future Simple Schemas

0:24:37.360,0:24:47.520
that are then converted into other assets. All 
right, so that's scenario two, and that concludes

0:24:47.520,0:24:54.960
this portion of the presentation with the demo. 
I'll go ahead and toss it back over to McKenzie,

0:24:54.960,0:25:05.280
and we can open it up for Q&A. Well, thanks, Zair, 
that was, that was fantastic. Um, that was great.

0:25:05.280,0:25:10.960
Yeah, just a reminder, there is a question 
tab down in the bottom right-hand corner. I

0:25:10.960,0:25:16.880
see there's a couple in there right now, uh, so if 
you do have a question, please throw it in there.

0:25:17.520,0:25:22.880
So first of all, "Will the slides be made 
available to us later?" This has been recorded,

0:25:22.880,0:25:29.360
and we are going to share that recording 
with everybody who has signed up today. So

0:25:29.360,0:25:34.560
if you really would like the slides, please 
reach out, and we can get you those as well,

0:25:34.560,0:25:39.600
but they are in the recording and, and you know, 
we think that's kind of the most important part.

0:25:41.680,0:25:43.520
Q&A
Q:

0:25:48.320,0:25:56.720
Can the Simple Schema be used for 
building landing pages as well?

0:25:56.720,0:26:06.240
A: Yes, it can. You actually have to 
define the type inside of the template

0:26:06.240,0:26:12.000
when you make your API call, and that 
type field you can set it to popup,

0:26:12.000,0:26:21.520
email, or page (not landing page, just page), 
and then it'll define, it'll go from there.

0:26:21.520,0:26:32.720
Q: I know the Simple Schema is recommended 
for programmatically creating templates,

0:26:32.720,0:26:40.560
but is there a specification 
available for the full schema as well?

0:26:43.680,0:26:56.880
A: I think you might be talking about the full 
Beefree SDK native JSON. If that's not the case,

0:26:59.600,0:27:09.280
please clarify in the chat. But 
right now we have Simple Schema, and

0:27:13.520,0:27:20.240
next week we'll also have an HTML importer, 
which will allow you to use the HTML route

0:27:20.240,0:27:29.120
and convert that to Beefree SDK native JSON. 
So really, either of those two options are

0:27:29.120,0:27:37.520
the ones that we currently have available. So 
there is an endpoint that allows you to use

0:27:38.320,0:27:45.600
the Simple Schema and then hit the endpoint to 
convert it into that full native Beefree JSON.

0:29:11.520,0:29:54.320
Q: What about the elements that are not documented 
in Simple Schema docs, like forms for pages?

0:29:54.320,0:29:58.480
A: That's a good question. We 
actually have a separate GitHub

0:29:58.480,0:30:04.800
repository for forms. I can share the 
schema you can use to validate forms,

0:30:05.360,0:30:11.600
but that does exist in a separate repository. 
I'll share it in the chat right now so whoever

0:30:11.600,0:30:18.960
asked that question also has access to 
that schema, the form validation schema.

0:30:18.960,0:30:45.920
Q: Any plans for moving 
these changes to production?

0:31:04.160,0:31:13.200
A: The Simple Schema is already live, 
so you can start using it today.

0:31:26.800,0:31:35.600
Q: Will we need to convert old email JSON 
from our own schema into Beefree-compatible

0:31:35.600,0:31:40.480
JSON? Am I correct in assuming this 
would be a good workflow for that:

0:31:40.480,0:31:46.800
our JSON to Simple Schema 
JSON to Beefree native JSON?

0:31:48.480,0:31:55.120
A: Yes, I think that sounds like a good 
workflow. We also are about to release,

0:31:55.840,0:32:02.400
or have just, we're about to release on 
May 7th, an HTML to Beefree JSON converter,

0:32:02.400,0:32:06.400
which is very exciting. That's something 
different, but also something a lot of

0:32:06.400,0:32:10.880
people have been asking about. So 
that's not your native JSON, however,

0:32:10.880,0:32:18.960
if you had HTML that you wanted to convert 
to the Beefree native JSON, that's just about

0:32:18.960,0:32:29.440
possible. So we're excited about that. But 
yes, I think that this is a good workflow.

0:32:29.440,0:32:35.600
Q: Is there documentation 
that our development team

0:32:35.600,0:32:41.280
can refer to with some examples for a 
person who is new to the Beefree API?

0:32:41.280,0:32:52.400
A: Yes, I'll share that link in the chat 
right now. I'll include our GitHub URL. We

0:32:52.400,0:32:56.960
have an example repository, and then I'll 
also include the technical documentation,

0:32:56.960,0:33:06.000
and on the technical documentation, you 
can actually test all of our endpoints.

0:33:06.000,0:33:14.720
Q: Have you tested with other models other than 
DeepSeek, and if so, how have the results varied?

0:33:14.720,0:33:24.560
A: Yes, one of the developers on our team used 
GitHub Copilot, and it was in the same format too,

0:33:24.560,0:33:31.680
so it was just a chat, and they connected, they 
uploaded the schema files, and then used a similar

0:33:31.680,0:33:42.160
prompt, and it did generate the Simple Schema 
template, and the results were, you know, they

0:33:42.160,0:33:48.640
worked pretty well. And even if it doesn't work on 
that first try, again, with just a little bit of

0:33:48.640,0:33:59.120
feedback from the API call results, it'll give you 
error validation feedback. Just by applying that,

0:33:59.120,0:34:05.920
usually it gets it on the second try too, so 
it's really, really impressive and works very

0:34:05.920,0:34:14.720
quickly. There's a little bit of training 
involved, but this is completely different

0:34:14.720,0:34:22.800
than first attempts with the native JSON Beefree 
JSON here, so this should really be a great tool.

0:34:24.640,0:34:29.200
Q: Can we set up anything to 
import JavaScript as well into

0:34:29.200,0:34:38.480
JSON as a complement of HTML? I'm 
talking about pages, not email.

0:34:40.720,0:34:47.600
A: The native Beefree JSON is actually 
kind of compatible between builders,

0:34:47.600,0:34:54.160
so you could actually build an email template 
in the editor and then take that JSON and put

0:34:54.160,0:35:02.720
it into the page builder, and it would then, 
upon saving, generate HTML for the web. So

0:35:02.720,0:35:10.640
it is compatible between the builders. Therefore, 
if you are converting that into the Beefree JSON,

0:35:10.640,0:35:34.960
it's compatible across. I would recommend checking 
out the documentation to get all the very granular

0:35:35.600,0:35:41.440
level details on that so that way you can ensure 
that you're setting everything up correctly,

0:35:41.440,0:35:47.280
but there are a few instructions in there that 
I recommend following. I'll share a link right

0:35:47.280,0:35:52.720
now in the chat to that specific section, 
which includes those more granular level

0:35:53.280,0:35:59.920
instructions for folks. And in the 
email following this presentation,

0:36:00.480,0:36:06.720
we'll include all relevant links as well, so 
if you're not grabbing them from the chat,

0:36:06.720,0:36:15.520
don't worry about it, we're recording, 
and we will share in the follow-up email.

0:36:15.520,0:36:22.240
Q: Is it possible to use the full schema 
programmatically to implement own transformations,

0:36:22.240,0:36:32.400
like full schema to some other format for the spec 
needed? So it has to be stable, is that the, um...

0:36:32.400,0:36:39.200
A: I think, and the individual who asked 
this, feel free to correct me if you're

0:36:39.200,0:36:46.880
asking something else, but we do have a group 
of endpoints that are available in our Content

0:36:46.880,0:36:54.560
Services API that actually takes the Beefree 
native JSON and converts it into other formats,

0:36:54.560,0:37:01.680
and those formats can be HTML. It can 
transform the Beefree JSON to an image

0:37:03.520,0:37:18.000
using the HTML endpoint, and also you can 
export other formats like PDF. So we have a

0:37:18.000,0:37:23.280
variety of different formats that you can use 
that are available under the Content Services

0:37:23.280,0:37:30.320
API section of the documentation where you 
can transform Beefree JSON into a lot of

0:37:30.320,0:37:41.600
other things. We even have an AI collection for 
converting them to SMS metadata or also summaries.

0:37:49.680,0:37:54.480
Q: How does the Simple Schema work with saved

0:37:54.480,0:38:03.120
rows? Is it just another property 
in the JSON like everything else?

0:38:03.120,0:38:15.040
A: We have the Simple Schema section because 
really what the workflow would look like is that

0:38:15.040,0:38:22.480
you create the Simple Schema template, the Simple 
Schema is converted to the Beefree full JSON,

0:38:22.480,0:38:28.720
and then folks can interact on the front end with 
that content and save rows from there. That's one

0:38:28.720,0:38:36.640
pathway. There's also the custom add-ons where 
you can create a custom row type, and that works

0:38:36.640,0:38:42.160
a little bit differently. We won't cover that in 
this particular session, but I do know that we'll

0:38:42.160,0:38:49.120
have future sessions touching on custom add-ons, 
so we can jump into that other scenario a little

0:38:49.120,0:38:54.240
bit more there. And we do have some resources 
on that in the custom add-on section of our

0:38:54.240,0:39:00.880
documentation too, and you can also reach out 
to us at the email that McKenzie mentioned,

0:39:04.160,0:39:14.960
pluginsupport@beefree.io, is always a great way 
to tell us anything, reach out with questions.

0:39:20.880,0:39:29.360
Q: Is there documentation that 
talks more specifically about the

0:39:29.360,0:39:34.160
details of training the AI model on Simple Schema?

0:39:34.160,0:39:41.280
A: This is going to kind of depend on the AI model 
a little bit as well. So you know, we really kind

0:39:41.280,0:39:53.280
of leave it to you to pick the AI model that works 
best for you. Experiment a bit if need be. We did

0:39:53.280,0:39:57.920
mention that we would share the, I think we were 
talking just a few minutes ago about including

0:39:57.920,0:40:04.720
the prompt that we used in the documentation. I 
think that's a great idea, so I think we'll put

0:40:04.720,0:40:09.360
our sample prompt into the docs, and then we 
can, we can add in some additional notes on,

0:40:09.360,0:40:18.080
on what we did there. We can absolutely include 
some inspirational aspects to the documentation,

0:40:18.080,0:40:24.960
but it really depends on the model, like McKenzie 
mentioned, and then also the documentation

0:40:24.960,0:40:32.400
of whichever provider you decide to use and 
their own best practices and stuff like that.

0:40:32.400,0:40:43.360
But we'll definitely include the inspirational 
portion on our end so you can see how we did it.

0:40:47.600,0:41:00.400
Q: If I'd like to implement a custom 
transformation, is the full schema

0:41:00.400,0:41:13.040
stable enough for, for example, having a 
public spec, or is it just an internal JSON?

0:41:13.040,0:41:20.400
A: That's something that we'll probably want to 
touch base with our team on. I would recommend

0:41:20.400,0:41:30.560
that Hari reach out to us at the email that 
McKenzie provided, pluginsupport@beefree.io,

0:41:31.760,0:41:38.000
so that way we can follow up. We probably 
want to touch base with our internal team

0:41:38.000,0:41:42.560
on this one to make sure we give you the best 
answer for your use case. We'll take a note,

0:41:42.560,0:41:45.760
we'll bring it to our team, and then 
we can reach out to you about this.

0:41:45.760,0:41:53.840
The full schema, the native Beefree JSON, that 
full schema is not available to be completely

0:41:53.840,0:41:55.437
opened up for public use. It's why we have 
the new endpoints to get that in return.

0:41:55.437,0:42:00.640
Q: Regarding the HTML to Beefree 
JSON workflow mentioned earlier,

0:42:00.640,0:42:04.800
could you speak to any expected data loss 
between the two formats? In other words,

0:42:04.800,0:42:09.600
is it possible to fully represent 
an HTML document in Beefree JSON?

0:42:09.600,0:42:14.160
A: This is something that we can, we'll 
follow up with you afterwards on this,

0:42:14.160,0:42:19.920
but yes, we have great success with 
converting the HTML to the Beefree JSON,

0:42:19.920,0:42:23.600
and then you can use it in the 
editor to edit a little bit as

0:42:23.600,0:42:30.320
needed. It's kind of case by case, 
so we can follow up with you on that.

0:42:55.840,0:43:53.520
Q: I had a question regarding image handling. 
How will images generated using AI be managed?

0:43:57.520,0:44:09.680
A: It depends on your storage, your file manager 
and storage system. End-users can also provide

0:44:09.680,0:44:16.480
the URLs to their images in their prompts if 
they're talking about adding specific images

0:44:16.480,0:44:24.080
to their design, or if they're looking for 
just like an inspirational image placeholder,

0:44:24.080,0:44:31.680
then that placeholder will appear in the final 
output, and then they can add their image URL

0:44:31.680,0:44:38.640
later on, or they can upload images once they're 
in the builder using the file manager. I mean,

0:44:38.640,0:44:44.000
there's really a lot of flexibility, but in terms 
of the initial prompt, they can either directly

0:44:44.000,0:44:48.960
mention like, "Hey, I already have some images 
that I work with, and I know that I want to use

0:44:48.960,0:44:57.680
them in this design," or they can just ask for 
an image placeholder, and even if they don't ask,

0:44:57.680,0:45:04.880
that image placeholder will appear because 
it'll pick up that an image should go there.

0:45:04.880,0:45:10.240
There are a few other ways outside of those two 
scenarios that you can also experiment with that,

0:45:10.240,0:45:14.560
but those are the two that I used for this 
demo. But there are other ways to get more

0:45:14.560,0:45:21.840
creative and customized with that based on how 
you train your AI model and how you prompt it.

0:45:44.480,0:45:49.440
Thanks so much for joining 
everybody, we really appreciate it,

0:45:49.440,0:45:55.840
and we're really excited to just see what 
you do with this. We're always excited to,

0:45:55.840,0:45:59.920
we love to hear feedback of how 
you're customizing the SDK in general,

0:46:00.640,0:46:06.560
but as the key benefit here of Simple Schema is 
that it opens the door for AI-powered content

0:46:06.560,0:46:14.240
generation, we're really excited to see what you 
do with that, and please, if you're proud of it,

0:46:14.240,0:46:21.280
or you're excited about it, or if it's going 
terribly, please reach out, send us an email,

0:46:21.280,0:46:29.200
contact your CSM, find me on LinkedIn. We want 
to, we just, we appreciate any and all feedback.

```
{% endtab %}
{% endtabs %}
