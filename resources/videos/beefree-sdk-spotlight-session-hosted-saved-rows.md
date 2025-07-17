---
description: >-
  Learn more about how you can easily enable reusable content into your end
  user's workflows with Hosted Saved Rows.
---

# Beefree SDK Spotlight Session: Hosted Saved Rows

{% embed url="https://www.youtube.com/watch?v=BSqWRusx2fg" %}

{% tabs %}
{% tab title="About" %}
In this Beefree SDK Spotlight session, we'll showcase how you can give your end users the ability to save and reuse their content through a simple toggle - no additional development resources needed in real time. We'll also walk through the various configuration options that'll enable upselling or provide additional customization options. For a comprehensive walkthrough of Hosted Saved Rows, check out the tutorial here: [![](https://www.gstatic.com/youtube/img/watch/yt_favicon_ringo2.png)Hosted Saved Rows: A Faster Way to Save an...](https://www.youtube.com/watch?v=5m80DgKW0x8)

Chapters:

* [1:43](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=103s) Introduction to Hosted Saved Rows&#x20;
* [2:39](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=159s) Benefits of Enabling Saved Rows&#x20;
* [3:22](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=202s) Implementation and Customization of Hosted Saved Rows&#x20;
* [4:03](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=243s) Activating the Feature in the Developer Console&#x20;
* [5:30](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=330s) Front-End Functionality Demonstration (Saving & Managing Rows)&#x20;
* [8:42](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=522s) Restricting User Access (Saved Row Boolean & Advanced Permissions)&#x20;
* [10:28](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=628s) Advanced Permissions&#x20;
* [12:17](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=737s) Customizing Tab Visibility & Order&#x20;
* [13:29](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=809s) Default Tabs Order&#x20;
* [14:30](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=870s) Customizing Modal Look and Feel (Translations & Theming)&#x20;
* [18:04](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=1084s) Exporting Hosted Saved Rows&#x20;
* [20:38](https://www.youtube.com/watch?v=BSqWRusx2fg\&t=1238s) Q\&A Session 45:44 Closing Remarks
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
0:00:03.400,0:00:10.680
And we're live! Hello, everybody! 
Hi, everyone! How's it going?

0:00:10.680,0:00:18.760
Welcome! Looks like we still have a 
few people joining. Out of curiosity,

0:00:18.760,0:00:29.960
has anybody introduced our 
Hosted Saved Rows feature yet?

0:00:33.840,0:00:37.240
Well, if not, this is the perfect webinar 
for you to be on because we're going to

0:00:37.240,0:01:00.600
walk you through everything you need 
to know. I just want you all to know,

0:01:00.600,0:01:05.760
the chat is at the bottom right-hand side 
of the screen. If you have any questions

0:01:05.760,0:01:11.360
as we go through this webinar, please 
feel free to drop them in the chat,

0:01:11.360,0:01:24.680
and we'll also be sharing some resources with you 
throughout this office hours in there as well.

0:01:24.680,0:01:27.080
I think, uh, I think we may have everyone.

0:01:27.080,0:01:29.920
The number's started to slow down. Do 
you want to go ahead and get started?

0:01:36.760,0:01:43.080
Yeah. So, alright. So, if you want to go 
ahead and go to the next slide for me, um,

0:01:43.080,0:01:47.200
just want to introduce myself real quick. Uh, my 
name is Kyle, and I'm a Senior Customer Success

0:01:47.200,0:01:53.400
Specialist at Beefree, and today I'm going to be 
introducing you to our Hosted Saved Rows feature.

0:01:53.400,0:01:57.360
Quick overview: it's a powerful feature 
in Beefree SDK that makes content creation

0:01:57.360,0:02:02.280
more efficient and streamlined. Uh, following 
that, our fantastical technical writer, Zier,

0:02:02.280,0:02:07.360
is going to walk you through how to implement the 
feature, and then we'll finish off with a Q&A.

0:02:07.360,0:02:12.520
So you may be asking yourself, what is 
a saved row? Uh, in essence, in the SDK,

0:02:12.520,0:02:17.720
uh, content is organized into groups of content 
blocks that we call rows. And a saved row allows

0:02:17.720,0:02:23.160
your end users to save and reuse these content 
structures or rows across multiple projects,

0:02:23.160,0:02:26.400
eliminating the need to recreate them 
from scratch each time. So think about

0:02:26.400,0:02:31.640
common elements like headers, footers, or product 
display layouts. By saving these rows, uh, your

0:02:31.640,0:02:37.600
users can easily insert them into new designs, 
ensuring consistency while saving valuable time.

0:02:37.600,0:02:46.720
So why should you enable saved rows in 
your application? Go to the next slide.

0:02:46.720,0:02:51.880
So first, it significantly reduces content 
creation time. Uh, your users can save hours

0:02:51.880,0:02:56.240
each week by reusing pre-designed rows instead 
of building them from the ground up every single

0:02:56.240,0:03:01.800
time. Second, it minimizes errors. So instead of 
manually creating layouts, your users can rely on

0:03:01.800,0:03:06.960
these saved content rows to ensure consistency 
and accuracy across every design. And finally,

0:03:06.960,0:03:10.960
it enhances user loyalty. By providing an 
intuitive, time-saving feature like this,

0:03:10.960,0:03:14.400
it makes your application even more 
valuable, helps increase engagement,

0:03:14.400,0:03:18.320
and most importantly, helps you retain your 
customers. So there's a little background on

0:03:18.320,0:03:21.440
what the feature is. I'm now going to pass it 
over to Zier, who's going to walk you through

0:03:21.440,0:03:26.360
the how and how you can get this feature 
set up in your application. Thank you.

0:03:26.360,0:03:30.600
Awesome. Thanks so much for that introduction, 
Kyle! Hi, everyone! My name is Zier. I'm the

0:03:30.600,0:03:35.840
Lead Technical Writer here at Beefree SDK. 
And for this portion of the presentation,

0:03:35.840,0:03:41.480
we're going to be talking about not only how 
you can implement Hosted Saved Rows within

0:03:41.480,0:03:45.280
your applications, but also talking 
a little bit more about how you can

0:03:45.280,0:03:51.000
customize the experience of Hosted Saved Rows 
altogether for your applications and users.

0:03:51.000,0:03:57.600
So to get started, we're going to do a few 
demonstrations. So I'll be navigating between

0:03:57.600,0:04:04.480
a few different tabs here as you follow along, 
but the first thing we're going to do is identify

0:04:04.480,0:04:11.440
where the toggle to activate Hosted Saved Rows 
actually is within the Builder. So to do this,

0:04:11.440,0:04:18.360
I'm going to navigate into my own developer 
console account and navigate to the application

0:04:18.360,0:04:23.880
that I want to toggle this feature on for. 
For this presentation, I decided to use

0:04:23.880,0:04:29.720
this QA environment, so it's a development 
instance. And I just click on details there

0:04:31.160,0:04:40.480
and head on over to application configuration. 
And when I click "View," now I'm in the space

0:04:40.480,0:04:45.520
where I can identify the toggle. And here in the 
Saved Row section, you'll notice that there are

0:04:45.520,0:04:51.760
two toggle options, and you'll want to toggle on 
"Hosted on the Beefree SDK infrastructure." I've

0:04:51.760,0:04:57.560
already toggled it on because this is my demo 
environment, which we'll be jumping into next.

0:04:57.560,0:05:02.960
But when you toggle this on, just keep in mind 
that you'll get a pop-up, and that pop-up will

0:05:02.960,0:05:07.360
mention that usage-based fees may apply for 
Hosted Saved Rows depending on the quantity

0:05:07.360,0:05:11.720
of rows that you're saving. So make sure you 
familiarize yourself either through reading the

0:05:11.720,0:05:19.200
documentation or connecting with a CSM like Kyle 
to make sure that you're familiar with those fees.

0:05:19.200,0:05:23.800
Alright, now that this is toggled on, and again, 
once you toggle this on, just make sure you click

0:05:23.800,0:05:29.920
"Save" in the upper right-hand corner. Um, we're 
going to go ahead and take a quick look at how

0:05:29.920,0:05:38.920
Hosted Saved Rows functions on the front 
end. So I have a test environment here.

0:05:38.920,0:05:45.160
I'm going to go ahead and reload it. If 
you want to follow along, I did include

0:05:45.160,0:05:52.560
all of the code as code samples in this GitHub 
repository, so you can use this repository to

0:05:52.560,0:05:59.640
follow along in today's presentation, or you 
can use it later on for your own reference.

0:05:59.640,0:06:05.200
I'll go ahead and share that there. Hopefully 
everyone is able to access it. Let me know if

0:06:05.200,0:06:11.920
you aren't for any reason. But basically, this 
is the code that we'll be using in today's demo.

0:06:11.920,0:06:19.400
Alright, perfect. So now I'm in my application. 
I'm in my code sandbox. When I click "Build an

0:06:19.400,0:06:27.080
Epic Email Now," I'm navigated over 
to the Builder. And in the Builder,

0:06:27.080,0:06:32.320
you'll notice that when I click on a row, I 
now have the option to save it. So this is

0:06:32.320,0:06:37.640
the out-of-the-box functionality that comes with 
Hosted Saved Rows. And you'll notice that as an

0:06:37.640,0:06:45.160
end user, I'm directed to add a row name and add 
a row category. So here, I'm going to add a row

0:06:45.160,0:06:50.960
name. It'll be "My First Row." And the category, 
I'll go with the default category, which is "My

0:06:50.960,0:06:58.800
Saved Rows." When I click "Save" there, I get a 
confirmation that my row was saved. And as an end

0:06:58.800,0:07:07.080
user, when I navigate over to the Rows tab and 
that category, I see "My First Row" here. I'll

0:07:07.080,0:07:14.080
also have the option—and I'll make this a little 
bit bigger just for the time being—I also have the

0:07:14.080,0:07:23.800
option to add a new category. So if I wanted to 
add something like "Coffee Headers" and just save

0:07:23.800,0:07:32.160
that new category, I absolutely can. And then I 
can also manage existing categories. So let's say

0:07:32.160,0:07:41.800
maybe I don't actually need that new category, I 
can delete it. And we also have row-level actions

0:07:41.800,0:07:48.520
that end users can perform. So there's the "Edit 
Info." So actually, I lied, this isn't "My First

0:07:48.520,0:07:54.440
Row," it looks like it's actually "My Third 
Row." So I'm going to change the name to "My

0:07:54.440,0:08:02.080
Third Row," update this, and now you can see the 
new name of "My Third Row." And I can also decide

0:08:02.080,0:08:08.520
whether or not I want to delete it or keep it. So 
that's the front-end functionality in a nutshell.

0:08:08.520,0:08:13.560
Now let's talk a little bit more about how we 
can customize this experience on the front end

0:08:13.560,0:08:20.120
for application end users. I'm just going 
to keep moving along in the slide because

0:08:20.120,0:08:26.360
it helps me keep the pace on the topics that we're 
discussing. So the next topic we're actually going

0:08:26.360,0:08:34.160
to cover is once you toggle on the Hosted Saved 
Row functionality, it becomes available to your

0:08:34.160,0:08:39.680
end users. But maybe there are certain end users 
that you don't want to have access to this feature

0:08:39.680,0:08:47.880
because you want to use it as incentive for an 
upgrade or some other reason. If that's the case,

0:08:47.880,0:08:53.920
you can use the savedRow boolean, which we 
talk about in the technical documentation,

0:08:53.920,0:09:00.800
to restrict which users can and cannot access 
Hosted Saved Rows altogether. In this example,

0:09:00.800,0:09:07.080
you'll notice—and I'll make this a little bit 
bigger, hopefully it's big enough on my screen,

0:09:07.080,0:09:11.840
if not, just let me know in the chat and I'll 
make it bigger—um, so you'll notice here,

0:09:11.840,0:09:18.720
savedRows.uid can be "admin" or uid can be 
"designer." And you'll notice right here where

0:09:18.720,0:09:26.760
we have the Beefree config defined before that 
we have this variable uidIsAdmin. So right now,

0:09:26.760,0:09:34.000
what we're looking at in the Builder is the admin 
experience. This person has access to um, the save

0:09:34.000,0:09:40.280
toggle and all of the modals and functionality 
that comes with Hosted Saved Rows. And if I were

0:09:40.280,0:09:46.680
a designer, I would still have access to that 
Saved Rows icon that I clicked on. But what if

0:09:46.680,0:09:55.600
I changed the role from "admin" to "copywriter" 
because I actually don't want copywriters to

0:09:55.600,0:10:05.200
have access to saving a row within the Beefree 
SDK? So I navigate over here, click on a row,

0:10:05.200,0:10:12.000
and you'll notice that the icon, the save icon 
that we saw earlier, is no longer there. So it

0:10:12.000,0:10:20.400
means that we were accurately able to restrict 
this feature for uid equal to "copywriter."

0:10:20.400,0:10:25.680
I'll go ahead and delete that, 
set it back to "admin," save this,

0:10:25.680,0:10:29.320
and now we're going to jump into our next 
topic, which is advanced permissions.

0:10:31.080,0:10:41.680
So when we talk about advanced permissions, we're 
not talking so much about the save icon anymore,

0:10:41.680,0:10:50.040
but we're talking more about the granular level 
permissions and which role has access to which um,

0:10:50.040,0:10:57.880
type of behavior within the Builder. So here 
in advanced permissions, we have a rows object

0:10:57.880,0:11:03.600
and then behaviors, and in behaviors, we have 
four different uh, behaviors that we can set

0:11:03.600,0:11:08.880
permissions for. You'll notice that the admin 
has permissions to delete a row, edit a row,

0:11:08.880,0:11:17.400
manage a row category, and to add a row category. 
But in this case, the designer only has access to

0:11:17.400,0:11:25.320
editing the hosted row. So let's set ourselves to 
the designer experience. If I edit "admin" and put

0:11:25.320,0:11:37.720
in "designer" and save this, now when I navigate 
to the Builder, I should only be able to edit. So

0:11:37.720,0:11:43.440
the three vertical dots that we had earlier, 
they're no longer there. If I clicked on "My

0:11:43.440,0:11:50.360
Saved Rows" and I click on these three vertical 
dots for this particular row, you'll notice that

0:11:50.360,0:11:56.120
the only permission I have is to edit the row's 
information. So I can edit the name, edit the

0:11:56.120,0:12:05.560
category, but I can't delete the row or anything 
else. So that shows a simple example of how you

0:12:05.560,0:12:11.920
can leverage advanced permissions and these 
different behaviors that are set within here.

0:12:11.920,0:12:20.320
Um, on another level, let's talk a little bit 
about tabs. So within advanced permissions,

0:12:20.320,0:12:29.240
you can also determine whether or not you want 
to show or lock the Rows tab altogether. So maybe

0:12:29.240,0:12:37.200
you want to show the Rows tab but you want to 
keep it locked because we're operating within

0:12:37.200,0:12:43.840
that same um, scenario as before where maybe 
you want to use the row tabs as an incentive

0:12:43.840,0:12:49.880
for an upgrade in the future. Now your end users 
will see this experience where they're able to

0:12:49.880,0:12:54.800
navigate with the content tab or interact 
with the content tab and the settings tab,

0:12:54.800,0:13:00.920
but the Rows tab, they can't click on it. So 
it creates an element of curiosity of like,

0:13:00.920,0:13:07.720
what is beyond, what's going on with the Rows tab, 
what kind of benefit can I get out of activating

0:13:07.720,0:13:16.560
that tab in my experience? So that's locked. And 
"show" just determines whether or not we see that

0:13:16.560,0:13:26.000
tab. So I'm going to go ahead and save this back 
so now we can interact with the Rows tab again.

0:13:26.000,0:13:32.160
Alright, so we talked a bit about that. Now, 
now let's talk about another customization we

0:13:32.160,0:13:39.680
can use within the Builder, which is 
default tabs order. So you'll notice

0:13:39.680,0:13:45.800
that originally the order of the tabs 
within the Builder were content, rows,

0:13:45.800,0:13:51.160
and then settings. Let's say I want the focal 
point to be rows. That's the first tab that I

0:13:51.160,0:13:58.640
want an end user to see when they land in the 
Builder. And then I want them to see settings,

0:13:58.640,0:14:06.040
and then I want them to see content. I can 
use defaultTabsOrder and define the new order

0:14:06.040,0:14:15.320
of the tabs within this array. So I go here, 
and now you can see that "Rows" is the first

0:14:15.320,0:14:24.760
tab here. Now I'm able to easily navigate 
that, navigate to that tab as the end user.

0:14:24.760,0:14:33.360
Alright, and now let's talk a little bit about 
how you can customize the modal and the overall

0:14:33.360,0:14:40.760
experience and look and feel of Hosted Saved 
Rows that way it matches the look and feel of

0:14:40.760,0:14:50.040
your application. So let's say, for example, I 
take a look at the modal and I think to myself,

0:14:50.040,0:14:56.440
"Hmm, perhaps I want to add my own text here and 
edit this a little bit. Maybe instead of 'Save

0:14:56.440,0:15:03.840
your row,' I want it to say something like 'Enjoy 
your new saved row.'" Well, you can absolutely

0:15:03.840,0:15:09.800
do that. In the GitHub repository that I shared 
with you at the beginning of this presentation,

0:15:09.800,0:15:17.240
I include a translations.json file. And within 
that translations.json file, you will find, uh,

0:15:17.240,0:15:23.640
this type of information: hostedContent and 
then, uh, these different types of sections,

0:15:23.640,0:15:31.280
which include modals, toast messages, error 
messages, um, pretty much anything that is related

0:15:31.280,0:15:38.280
to Hosted Saved Rows altogether. And you can use 
that information to override the default text with

0:15:38.280,0:15:46.560
your own text. So in this simple example, I use 
translations within the Beefree configuration,

0:15:46.560,0:15:51.240
and instead of saying "Save row," I want the 
top to say "Hello row," and instead of the

0:15:51.240,0:15:58.920
default text for the title, I want it to say 
"Enjoy your new saved row." When I save this

0:15:59.800,0:16:08.000
and I navigate back to my Builder and I 
click on the save icon, I'll be redirected

0:16:08.000,0:16:16.520
to a modal with the uh, text that I put in the 
Beefree config to override the default text.

0:16:16.520,0:16:22.120
And if we want to take the customization one 
step further, we can also change the font and

0:16:22.120,0:16:30.520
the coloring of the modal. In this example, I'm 
going to navigate back to the developer console,

0:16:30.520,0:16:38.440
click on application defaults, and oops, not 
application defaults, application details,

0:16:38.440,0:16:45.640
click on application details and then themes. 
And I'm going to enable a theme. So here we see

0:16:45.640,0:16:52.160
the default theme that we're working with right 
now, and what we're going to do is we can use any

0:16:52.160,0:16:58.840
of these three other options, or we can scroll 
down and define the colors, fonts, and so on,

0:16:59.520,0:17:05.200
uh, in terms of styles that we want to use. But 
if we select this theme just to make it quick,

0:17:05.200,0:17:14.440
and we update the theme and we save it, and when 
we navigate back to the Builder and reload here,

0:17:14.440,0:17:22.400
we should now get a new look and feel when 
we open up the Hosted Saved Rows modal. Okay,

0:17:22.400,0:17:29.120
so now we have a new text, we also have new 
font, and we also have a new color over here.

0:17:29.120,0:17:33.800
So we're really able to customize 
that experience of Hosted Saved Rows,

0:17:33.800,0:17:39.920
just like how we're able to customize other 
things within the Beefree SDK ecosystem.

0:17:39.920,0:17:49.080
And the last thing I'll talk about is how you 
can actually, let me just make sure that this

0:17:49.080,0:17:58.840
is good to go over here, uh, all right. 
So the last thing I'll talk about today

0:18:00.080,0:18:08.840
is how you can actually use your Hosted 
Saved Rows. And the Hosted Saved Rows,

0:18:08.840,0:18:17.560
just like any other row, can be transformed in 
terms of uh, Beefree JSON into other formats. So

0:18:17.560,0:18:24.200
it is also compatible with exporting plain 
text, exporting HTML, exporting to a PDF,

0:18:24.200,0:18:32.840
and exporting to an image. So if we were to 
take one of our Hosted Saved Rows here, add it,

0:18:32.840,0:18:42.240
now we know our new row is here, save this design, 
we automatically get the entire template JSON in

0:18:42.240,0:18:49.440
here, and we can click "Export Plain Text," and 
we should be able to see the plain text. I know

0:18:49.440,0:18:58.960
this screen is a bit small, so you can also follow 
along in the um, in the GitHub repository there,

0:18:58.960,0:19:04.800
a larger environment that you can use. But for 
the purposes of this demo, I'll just show you here

0:19:04.800,0:19:09.920
the plain text appeared. You can see the plain 
text for not only the hosted row but the entire

0:19:09.920,0:19:17.240
template. You can do the same thing by exporting 
HTML and click that button. Maybe your end users

0:19:17.240,0:19:28.720
want to export the HTML. If I take the HTML 
actually, and I copy this all, I'm just going to

0:19:29.640,0:19:41.480
and over here copy and click here and type paste. 
I can also do "Export PDF." So let's see what uh,

0:19:41.480,0:19:49.120
PDF looks like. You can see, yeah, my Hosted 
Saved Row is included in there. And then the very

0:19:49.120,0:19:56.160
last thing I'll do is click the "Export Image" 
option, and then I can see, yep, the Hosted Saved

0:19:56.160,0:20:03.640
Row transformed perfectly into an image, and it 
integrates seamlessly with the rest of my design.

0:20:03.640,0:20:09.440
So that's Hosted Saved Rows in a nutshell. We 
talked about how you can implement the feature,

0:20:09.440,0:20:16.360
how you can go ahead and interact with all of 
the different types of customizations within

0:20:16.360,0:20:23.800
Beefree SDK. If you're interested in um, the type 
of experience that I created here too with these

0:20:23.800,0:20:29.680
four buttons, I can include a separate GitHub 
repository link in here where you can just copy

0:20:29.680,0:20:38.840
and paste the code um, into Glitch and use that 
as a server for these um, four export options. Uh,

0:20:38.840,0:20:46.400
thank you so much and Kyle, I think we're ready 
to open it up for questions if folks have any.

0:20:46.400,0:20:52.400
Great. So I do see one uh, question in the chat 
here about what happens to a saved row if part

0:20:52.400,0:20:58.720
of that category is deleted. Um, I don't, 
I'm not sure I have the full context here,

0:20:58.720,0:21:03.800
but uh, to answer what I think the question 
is, uh, essentially, if you delete a category,

0:21:03.800,0:21:08.120
the rows inside that category will be deleted 
as well, uh, and they won't be accessible

0:21:08.120,0:21:13.080
anymore. Um, but if the hosted rows are used 
inside a specific design, there will be no

0:21:13.080,0:21:17.640
effect on that. So I would suggest if you're 
going to delete a row or delete a category,

0:21:17.640,0:21:24.640
move that row to a separate category first so you 
don't lose that data. Um, yeah, if anybody else

0:21:24.640,0:21:37.720
has questions, feel free to put them in the uh, 
questions tab down the bottom right. Let's see.

0:21:37.720,0:21:54.480
I'll take a quick look. Um, I see a question about 
forms: "We would like to use form elements in the

0:21:54.480,0:22:01.160
landing page feature as a standalone feature 
to build and deploy uh, forms on your website.

0:22:01.160,0:22:13.160
Is this possible?" And then, so my understanding 
of rows is that they integrate as an additional

0:22:13.160,0:22:20.040
content block that you can add to your landing 
page. So if you're building a landing page within

0:22:20.040,0:22:26.960
the Beefree Builder and you drag and drop the form 
content block onto the landing page stage, that

0:22:26.960,0:22:36.280
form will uh, be integrated in there, and when 
you export it, then you can go ahead and create

0:22:36.280,0:22:45.200
your own um, your own landing page with the form 
in there. I mean, I think it would be up to you

0:22:45.840,0:22:50.440
how you want to customize the landing page, but 
the form functions as a portion of that landing

0:22:50.440,0:22:58.440
page. And I hope that answers your question. If it 
doesn't answer your question, please let me know,

0:22:59.360,0:23:03.120
and we can talk about it some more. 
I'll also leave my contact information,

0:23:03.120,0:23:07.960
so if folks want to email me after this 
webinar, you can absolutely email me,

0:23:07.960,0:23:15.240
and we can follow up with more answers to your 
questions. Um, okay, I see one about AI here:

0:23:15.240,0:23:20.640
"We are evaluating the AI features in Beefree 
SDK, but are concerned about costs and data

0:23:20.640,0:23:28.440
privacy. That's a really great question. And is 
it possible for users to integrate their own chat

0:23:28.960,0:23:37.160
API key instead of using a shared AI service?" 
Oh, I see you already answered, Kyle. We also do

0:23:37.160,0:23:42.520
have the Trust Center, um, and in the new Trust 
Center, we talk a little bit more about this,

0:23:42.520,0:23:49.920
where you can reference more resources around 
um, the data security and privacy best practices

0:23:49.920,0:23:55.560
that we use here at Beefree SDK. It's also 
linked at the very end of the docs page,

0:23:55.560,0:24:03.640
but just for easy reference, I will 
share the link within the chat too.

0:24:03.640,0:24:09.400
And Alex, just to touch on the cost piece as 
well, um, we do have some tools that you can

0:24:09.400,0:24:15.160
use to mitigate cost in this matter. You 
can limit tokens by user, uh, a lot of,

0:24:15.160,0:24:19.120
you know, individual things to help, 
you know, manage those costs. So, uh,

0:24:19.120,0:24:26.720
happy to talk after this call. Feel free to shoot 
me an email, we can talk more deeply about it.

0:24:26.720,0:24:40.200
And let's take a quick look at the other 
questions. Oh, I think that covers all

0:24:40.200,0:24:46.720
the questions. Did anyone else have any 
other questions, anything else you'd like

0:24:46.720,0:24:58.320
to know about Hosted Saved Rows or any 
Beefree SDK functionality in general?

0:25:05.720,0:25:28.320
Thank you, Jeff, for being here. We 
appreciate it. Give it another minute here.

0:25:48.320,0:26:02.240
Okay, we've got some more questions coming 
in. Oh, okay, I see a question here, um,

0:26:02.240,0:26:07.480
about: "Are there any recommended ways 
of providing default rows or templates

0:26:07.480,0:26:13.960
in Beefree?" So you can absolutely provide 
your end users with the default rows. Um,

0:26:13.960,0:26:20.400
they can either be default rows that we have 
available, um, there's actually a Boolean called

0:26:20.400,0:26:26.600
defaultRows that you can set to true within the 
Beefree configuration, and that'll activate our

0:26:26.600,0:26:32.240
default rows. But if you're more interested in 
your own that you created and built, you can use

0:26:32.240,0:26:39.200
the custom rows feature and provide your end users 
with access to the custom rows that you built um,

0:26:39.200,0:26:45.360
whenever they load the Beefree SDK Builder. 
Uh, I'll provide links to both of those,

0:26:45.360,0:26:51.520
the Boolean and also custom rows, in the chat that 
way you can read a little bit more about it and

0:26:51.520,0:26:58.240
experiment with those two features. But that would 
be our custom rows and default rows offering.

0:27:14.200,0:27:28.160
I'll go ahead and get those links 
very quickly. Yeah, let's see.

0:27:32.560,0:27:51.840
And I'll add this in the chat. Um, and then I'll 
also share my email in the chat. I think you can

0:27:51.840,0:27:57.320
reach out to me, and I'll make sure that you 
get uh, in contact with the right person to

0:27:57.320,0:28:04.720
help you out for any AI related inquiries. 
And let me see, was there another question

0:28:04.720,0:28:11.840
in here? I may have missed it, but, "Is there 
any way to limit the number of saved rows that

0:28:11.840,0:28:18.840
can be created? Uh, for example, ensure that 
someone doesn't create a thousand rows?" Yeah,

0:28:18.840,0:28:31.840
so that's an excellent question. I know, 
um, that's an excellent question. Let me

0:28:31.840,0:28:38.080
do some additional research. I know that we can 
create a maximum of how many rows are displayed,

0:28:38.080,0:28:49.200
but I don't know if we actually limit 
the number of rows a person can create,

0:28:49.200,0:28:58.040
but I'd be happy to follow up with 
you on that after this presentation.

0:29:00.600,0:29:06.760
And then I think I saw another question about 
self-hosted saved rows. Let me take a quick

0:29:06.760,0:29:15.000
look. Where was that question? "Do you have 
more documentation?" Yes, so I will share a

0:29:15.000,0:29:28.200
link in the chat here so that way you can 
take a look at that. We also in GitHub,

0:29:28.200,0:29:34.640
we have um, some sample code that you can 
reference with a simple integration or

0:29:34.640,0:29:44.160
implementation of self-hosted saved 
rows. So I'll include that here.

0:29:44.160,0:30:03.280
Okay. Alright, looks like we, we may be at 
time here, but if anybody has other questions,

0:30:03.280,0:30:07.080
feel free to follow up with us after this webinar,

0:30:07.080,0:30:11.680
and we're happy to help in any way we can. 
Uh, thank you all so much for joining!

0:30:11.680,0:30:21.160
Yeah, thank you, everyone! Have a 
great one! Enjoy the rest of your day!

```
{% endtab %}
{% endtabs %}
