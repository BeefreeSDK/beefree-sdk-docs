---
description: Video series on how to get started with Beefree SDK in a React application.
---

# React Video Series

## React Video Series

This video series includes the following tutorials:

* [Video #1](react-video-series.md#video-1-quickstart-guide-no-code-email-builder-for-beefree-sdk-part-1): Quickstart Guide: No-code Email Builder for Beefree SDK (Part 1)
* [Video #2](react-video-series.md#video-2-quickstart-guide-react-no-code-email-builder-for-beefree-sdk-part-2): Quickstart Guide: React No-code Email Builder for Beefree SDK (Part 2)
* [Video #3](react-video-series.md#video-3-quickstart-guide-react-no-code-email-builder-for-beefree-sdk-part-3): Quickstart Guide: React No-code Email Builder for Beefree SDK (Part 3)

***

### Video #1: Quickstart Guide: No-code Email Builder for Beefree SDK (Part 1)

{% embed url="https://www.youtube.com/watch?v=Ev7ljzrTcD0" %}

{% tabs %}
{% tab title="About" %}
This video walkthroughs how to create an application within the Beefree SDK Developer Console.

PART 1: This quickstart guide provides a step by step walkthrough of:

1. How to sign up for an account in the Beefree SDK Developer Console
2. How to navigate the SDK Developer Console
3. How to create an application
4. How to obtain your Client ID and Client Secret.
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
1
00:00:01,600 --> 00:00:07,200
To get started, navigate to developers.beefree.io. 
This will be your essential hub for everything

2
00:00:07,200 --> 00:00:12,240
related to the Beefree SDK. In the top-right 
corner of the window, click Create a Developer

3
00:00:12,240 --> 00:00:15,840
Account, then fill out the form to create 
your first developer account with Beefree.

4
00:00:16,720 --> 00:00:20,800
You’ll notice there’s also a link 
to the Beefree app as a standalone

5
00:00:20,800 --> 00:00:25,920
tool. However, this video series focuses on 
the Beefree SDK as an embeddable solution.

6
00:00:26,720 --> 00:00:29,760
Once you’ve created your account and logged 
in, you’ll be taken to a screen that looks

7
00:00:29,760 --> 00:00:35,760
something like this. At the top-right, you’ll 
find links to support and documentation.

8
00:00:35,760 --> 00:00:38,880
In the main section, you’ll see the 
type of subscription you’ve chosen,

9
00:00:39,840 --> 00:00:45,520
along with four activation options: Email Builder, 
Page Builder, Popup Builder, and File Manager.

10
00:00:46,560 --> 00:00:54,160
This is where you’ll activate the SDK instance 
that will later run within your application.

11
00:00:54,160 --> 00:01:02,160
Let’s do that now by clicking Activate 
for the Email Builder application.

12
00:01:02,160 --> 00:01:04,880
On the next screen, you’ll be prompted 
to name your application. I’ll call

13
00:01:04,880 --> 00:01:10,240
mine Test Email 1. You can choose any 
name you like. Once you click Create,

14
00:01:10,240 --> 00:01:14,000
you’ll see your running SDK instance. 
Here, you’ll find the application name,

15
00:01:14,800 --> 00:01:21,040
client ID, subscription type, and a Details 
button. Let’s go ahead and click on Details.

16
00:01:21,040 --> 00:01:25,680
Inside the details screen, you’ll see important 
information such as the environment type,

17
00:01:26,240 --> 00:01:32,480
creation and update dates, and configuration 
options. From here, you can change themes,

18
00:01:32,480 --> 00:01:38,320
manage roles, and manage add-ons. 
One of the key features of the SDK

19
00:01:38,320 --> 00:01:42,400
is that it provides two critical pieces of 
information: your Client ID and Client Secret.

20
00:01:42,400 --> 00:01:45,120
Don’t worry—we’ll delete these 
credentials after this video. You’ll

21
00:01:45,120 --> 00:01:50,480
also see references to some of our APIs, 
like the HTML Importer, Content Services,

22
00:01:50,480 --> 00:01:58,000
and the Template Catalog API. All of these 
can be accessed from this single screen.

23
00:02:00,080 --> 00:02:03,600
This area is known as the Beefree 
Developer Console. As mentioned,

24
00:02:03,600 --> 00:02:11,520
this is where you’ll find your Client ID and 
Client Secret, which are used for authorization.

25
00:02:11,520 --> 00:02:15,040
Since they’re sensitive credentials, you 
should never share them. If necessary,

26
00:02:15,040 --> 00:02:18,640
you can regenerate them using the 
Regenerate button on this screen.

27
00:02:18,640 --> 00:02:21,200
Finally, in this video series, we’ll demonstrate

28
00:02:22,480 --> 00:02:26,240
a client-side authorization process for 
simplicity. But when moving to production,

29
00:02:26,240 --> 00:02:31,280
you’ll want to implement server-side 
authorization for added security.
```
{% endtab %}
{% endtabs %}

***

### Video #2: Quickstart Guide: React No-code Email Builder for Beefree SDK (Part 2)

{% embed url="https://www.youtube.com/watch?v=auyOorxU7X0" %}

{% tabs %}
{% tab title="About" %}
This quickstart video series provides a step by step walkthrough of how to embed the Beefree SDK’s Email Builder inside a React application. You’ll see the full process in action — from creating a React app to running the builder live in your browser.

PART 2: introduction to installing the Beefree SDK with a React Application
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
1
00:00:03,040 --> 00:00:06,960
Once you've set up your Beefree account, 
you're ready to install the Beefree SDK.

2
00:00:06,960 --> 00:00:10,160
This video will teach you how to do 
just that with a React application.

3
00:00:10,160 --> 00:00:14,080
We’ll also have other videos available 
if you’re working with Angular or Vue.js.

4
00:00:14,080 --> 00:00:18,240
In this video, we’ll first walk you 
through cloning a sample React demo that

5
00:00:18,240 --> 00:00:23,840
we’ve made available in a GitHub repo. Then, we’ll 
cover the SDK installation process, including

6
00:00:23,840 --> 00:00:29,040
installing with NPM, setting up authorization, 
and configuring your first BeeConfig.

7
00:00:29,040 --> 00:00:32,640
Finally, we’ll show you how 
to run your first Beefree SDK

8
00:00:32,640 --> 00:00:35,082
app locally on your machine. Let’s get started.
```
{% endtab %}
{% endtabs %}

***

### Video #3: Quickstart Guide: React No-code Email Builder for Beefree SDK (Part 3)

{% embed url="https://www.youtube.com/watch?v=TBZ1lHkPc0w" %}

{% tabs %}
{% tab title="About" %}
This Quickstart Guide shows you step by step how to embed Beefree SDK’s Email Builder into a React application. By the end of the guide, you'll have a functional React app running locally, with Beefree SDK's no-code email builder integrated and properly authenticated—following best practices for React development.

PART 3: in this video, you'll learn how to:

* Project Setup: How to clone the Beefree React demo from GitHub
* How to configure environment variables by renaming a file and adding your client ID and secret
* An overview of the sample React application
* An explanation of the secure authentication process using a local proxy server
* Launch the application locally to see the embedded Beefree editor in action
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
1
00:00:01,200 --> 00:00:04,400
Let's get started with installation. These 
instructions will work the same whether

2
00:00:04,400 --> 00:00:08,320
you're on a Windows or Mac computer. The only 
assumptions are that you have set up your account,

3
00:00:08,320 --> 00:00:13,600
have your client ID and client secret, and 
have Node version 14 or greater. You'll go

4
00:00:13,600 --> 00:00:18,480
to GitHub to the Beefree SDK account 
and find the Beefree React demo repo.

5
00:00:18,480 --> 00:00:25,920
We'll include a link for that below 
as well. Let's go ahead and clone it.

6
00:00:31,960 --> 00:00:32,960
Okay,

7
00:00:32,960 --> 00:00:37,280
that didn't take long at all. By the way, if you 
get lost during any of these steps or need more

8
00:00:37,280 --> 00:00:44,720
detail, the README for this repo contains complete 
step-by-step instructions. From here, let's cd

9
00:00:44,720 --> 00:00:53,040
into our project and run npm install to update 
our dependencies. Once that's complete, we'll run

10
00:00:53,040 --> 00:01:02,880
npm install beefree.io-sdk to install the official 
NPM package. Again, that didn't take long at all.

11
00:01:02,880 --> 00:01:08,400
Now, from either your terminal or your 
editor, let's list the files, and you'll see

12
00:01:08,400 --> 00:01:16,640
a .env.example file provided for you. Let's rename 
that to simply .env for proper configuration.

13
00:01:16,640 --> 00:01:22,080
When you open it, you'll notice that we have 
your Client ID and Client Secret typed out

14
00:01:22,080 --> 00:01:26,880
as text. You'll want to go to your developer 
console, copy your Client ID and Client Secret,

15
00:01:26,880 --> 00:01:32,560
and replace that text here. Make sure to leave 
the single quotes so it’s captured properly.

16
00:01:32,560 --> 00:01:37,600
Next, let's look at some of the files available 
in the simple React app. Navigate to the src

17
00:01:37,600 --> 00:01:42,720
directory and open App.tsx. You'll find 
a React function describing a button,

18
00:01:42,720 --> 00:01:45,840
and that button links to a convenient URL:

19
00:01:45,840 --> 00:01:50,800
our documentation. Feel free to replace the URL 
with one of your choice, or replace this entire

20
00:01:50,800 --> 00:01:55,520
function with a component that better matches 
what you’ll have in a production environment.

21
00:01:55,520 --> 00:02:01,040
All right, that last button represented a sample 
component you might have in your app. Now let's

22
00:02:01,040 --> 00:02:06,800
look at the component for the Beefree SDK itself. 
Open BeefreeEditor.tsx, a TypeScript file in the

23
00:02:06,800 --> 00:02:10,701
src directory. You'll see an example that 
uses both the useEffect and useRef hooks.

24
00:02:10,701 --> 00:02:17,600
The useEffect hook manages the 
lifecycle of the SDK component,

25
00:02:17,600 --> 00:02:22,320
and the useRef hook provides a reference 
to the HTML element where the editor will

26
00:02:22,320 --> 00:02:27,520
live. You'll see that right here as an 
HTML element using the useRef.

27
00:02:27,520 --> 00:02:32,160
Next is our useEffect hook, which is 
critical. We'll pass an empty array

28
00:02:32,160 --> 00:02:36,240
as the second argument to tell 
React: run this code just once,

29
00:02:36,240 --> 00:02:40,000
right after the component first mounts. 
This prevents the editor from trying

30
00:02:40,000 --> 00:02:44,560
to reinitialize every time the component 
re-renders, which is exactly what we want.

31
00:02:44,560 --> 00:02:46,800
Inside the useEffect, we have an async function

32
00:02:46,800 --> 00:02:53,280
called initializeEditor. The first 
part is the BConfig object itself,

33
00:02:53,280 --> 00:02:57,680
where we configure the SDK's behavior. The 
most critical property here is container,

34
00:02:58,400 --> 00:03:03,280
which is set to beefree-react-demo, matching the 
ID of the where the editor will render.

35
00:03:04,000 --> 00:03:07,440
We also have callbacks like onSave and onError,

36
00:03:08,320 --> 00:03:12,800
letting us react to events from the 
editor, such as when a user hits save.

37
00:03:12,800 --> 00:03:18,640
Now look at this fetch call. Remember our 
discussion on security? Here's that in action.

38
00:03:18,640 --> 00:03:24,960
We're making a fetch call to localhost:3001. This 
isn’t a direct call to the Beefree SDK API—it goes

39
00:03:24,960 --> 00:03:30,240
through our local proxy server, which we'll 
set up in a separate file. The proxy handles

40
00:03:30,240 --> 00:03:35,600
secure authentication and returns a temporary 
access token that the client can safely use.

41
00:03:36,320 --> 00:03:47,520
With that token, we can create a new instance of 
the Beefree SDK and call its start method. This

42
00:03:47,520 --> 00:03:52,720
is the moment the editor is initialized 
and rendered inside our container.

43
00:03:53,520 --> 00:03:59,920
The component’s return statement simply 
renders the HTML structure. The has

44
00:03:59,920 --> 00:04:04,000
the matching ID beefree-react-demo, 
and the ref attribute is set to our

45
00:04:04,000 --> 00:04:09,680
container ref. This completes the circle 
and tells the SDK exactly where to render.

46
00:04:25,920 --> 00:04:29,760
In summary, this file uses 
a ref to get a DOM element,

47
00:04:29,760 --> 00:04:35,440
a useEffect hook to safely run the code once, 
a secure fetch to get an authorization token,

48
00:04:35,440 --> 00:04:38,080
and then uses that token to initialize the Beefree

49
00:04:38,080 --> 00:04:44,000
SDK. This is a production-ready pattern for 
embedding the editor in your React application.

50
00:04:44,000 --> 00:04:51,680
Earlier, you added your Client ID and Client 
Secret to the .env file. To complete authorization

51
00:04:51,680 --> 00:04:59,600
and authentication, we use the loginV2 method. An 
example is provided in proxyServer.js in the root

52
00:04:59,600 --> 00:05:02,400
directory. You’ll want to do something 
similar in your production application.

53
00:05:03,280 --> 00:05:08,080
This handles the critical authentication process 
for running the Beefree SDK in your React app.

54
00:05:08,080 --> 00:05:19,360
The Beefree SDK requires passing the Client ID 
and Client Secret server-side. On lines 14 and 15,

55
00:05:19,360 --> 00:05:24,960
you define BE_CLIENT_ID and BE_CLIENT_SECRET 
to reference the values you pasted earlier.

56
00:05:25,680 --> 00:05:30,560
These are used in an Axios POST method 
for secure server-side authorization.

57
00:05:30,560 --> 00:05:38,240
Now comes one of the most fun parts: running your 
Beefree SDK instance locally. Open two terminal

58
00:05:38,240 --> 00:05:45,920
windows. In the first, run node proxyServer.js 
to handle backend authorization. In the other,

59
00:05:45,920 --> 00:05:53,200
run npm run dev to start the React app. 
The app is served at localhost:5173.

60
00:05:53,200 --> 00:05:59,280
Open your browser and navigate there.

61
00:05:59,280 --> 00:06:04,800
You’ll see the portion of the React app we built: 
"Welcome to Beefree Demo" and the "Read the Docs"

62
00:06:04,800 --> 00:06:10,240
button from earlier. Here, you can 
interact with the Beefree SDK editor,

63
00:06:10,240 --> 00:06:17,280
which is now fully embedded in your React 
application. From here, feel free to click

64
00:06:17,280 --> 00:06:28,888
on different content blocks and explore the 
editor’s functionality—it’s a powerful tool.
```
{% endtab %}
{% endtabs %}
