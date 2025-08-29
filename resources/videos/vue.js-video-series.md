---
description: Video series on how to get started with Beefree SDK in a Vue.js application.
---

# Vue.js Video Series

## Vue.js Video Series

This video series includes the following tutorials:

* [Video #1](vue.js-video-series.md#video-1-quickstart-guide-no-code-email-builder-for-beefree-sdk-part-1): Quickstart Guide: No-code Email Builder for Beefree SDK (Part 1)
* [Video #2](vue.js-video-series.md#video-2-quickstart-guide-vue.js-no-code-email-builder-part-2): Quickstart Guide: Vue.js No-code Email Builder (Part 2)
* [Video #3](vue.js-video-series.md#video-3-quickstart-guide-vue.js-no-code-email-builder-part-3): [Quickstart Guide: Vue.js No-code Email Builder (Part 3)](https://www.youtube.com/watch?v=DstfPbGt6bI)

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

### Video #2: Quickstart Guide: Vue.js No-code Email Builder (Part 2)

{% embed url="https://www.youtube.com/watch?v=3xHfpMoxg2k" %}

{% tabs %}
{% tab title="About" %}
This Quickstart Guide walks you through embedding the Beefree SDK’s no-code email builder into a Vue 3 application. By the end of this guide, you’ll have a fully functional Vue app running locally with the builder embedded, authenticated, and ready to use—following Vue best practices.

PART 2: introduction to installing the Beefree SDK with a Vue Application
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
1
00:00:02,960 --> 00:00:08,560
Hi developers, this video covers working 
with the Bin a Vue.js application. If your

2
00:00:08,560 --> 00:00:13,440
framework of choice is React or Angular, we have 
separate videos for those as well. In this video,

3
00:00:13,440 --> 00:00:17,040
once we have you clone a sample 
Vue.js application from GitHub,

4
00:00:17,040 --> 00:00:21,280
we'll then go through how to install the 
Beefree SDK itself. Then we'll look at

5
00:00:21,280 --> 00:00:25,840
taking care of authentication with a proxy 
server. We'll show you how to embed the SDK

6
00:00:25,840 --> 00:00:30,880
in the Vue.js application. And finally, how 
to run and test your application locally.
```
{% endtab %}
{% endtabs %}

***

### Video #3: Quickstart Guide: Vue.js No-code Email Builder (Part 3)

{% embed url="https://www.youtube.com/watch?v=DstfPbGt6bI" %}

{% tabs %}
{% tab title="About" %}
This Quickstart Guide walks you through embedding the Beefree SDK’s no-code email builder into a Vue 3 application using the /loginV2 authorization process. By the end of this guide, you’ll have a fully functional Vue app running locally with the builder embedded, authenticated, and ready to use—following Vue best practices.

PART 3: in this video, you'll learn how to:

* Clone the Beefree React demo repository from GitHub
* Configure your environment by running npm install + adding your client ID and secret
* Learn how the SDK is initialized and managed
* Authentication process using a proxy server.
* Launch the application locally to see the embedded Beefree editor in action
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
0:00:01.440,0:00:06.080
The first thing we want to do is navigate to 
the Beefree View Demo available on GitHub,

0:00:06.080,0:00:18.880
and go ahead and clone this repository.

0:00:18.880,0:00:29.360
Once you have that cloned, install the 
Beefree SDK using the following NPM command.

0:00:29.360,0:00:34.800
That didn’t take long at all. Let’s talk for a 
moment about authentication. Secure authentication

0:00:34.800,0:00:40.080
is essential for a production environment. In 
the application provided, we leverage loginV2

0:00:40.800,0:00:46.000
to secure the Client ID and Client Secret and 
ensure they’re not exposed in frontend code.

0:00:46.000,0:00:56.000
First, open the .env.ampl file and rename it 
to .env, which is what our program expects.

0:00:57.040,0:00:59.883
Replace the placeholders with your actual Client 
ID and Client Secret from the developer console.

0:00:59.883,0:01:01.120
Next, open proxyServer.js to see how this is 
implemented. After importing .env, the Client

0:01:01.120,0:01:22.880
ID and Secret are referenced securely on the 
backend, and the token is accessed server-side.

0:01:22.880,0:01:28.160
At this point, in our sample VGS application, 
we have installed the Beefree SDK via NPM, and

0:01:29.280,0:01:33.040
handled authorization to your Beefree 
account through the proxy server. Now,

0:01:34.480,0:01:38.320
let’s embed the Beefree SDK 
editor within the application.

0:01:38.320,0:01:43.600
Similar to the Angular example, we use a 
custom component. We’ve created one called

0:01:43.600,0:01:50.720
BeefreeEditorView. In the TypeScript file, 
starting on line 15, we define the BConfig. On

0:01:50.720,0:01:59.440
line 28, we access the authorized token, and with 
that token, we instantiate the editor on line 37.

0:01:59.440,0:02:04.080
Now the SDK is embedded in a 
component and ready to use—but

0:02:04.080,0:02:11.040
we won’t see it yet because it hasn’t 
been added to the view. Go to AppView

0:02:12.000,0:02:19.200
and import the BeefreeEditorView component 
so it’s rendered in the parent component.

0:02:20.080,0:02:23.840
Everything is now in place to run 
the application locally. Open two

0:02:23.840,0:02:27.600
terminal windows. In the first, 
install a few critical packages:

0:02:28.560,0:02:30.640
express for the web server

0:02:30.640,0:02:32.880
axios for making requests

0:02:32.880,0:02:36.080
cors to handle cross-origin requests 
between the proxy and the app

0:02:36.080,0:02:44.160
Once installed, run the proxy server with node

0:02:44.160,0:02:54.480
proxyServer.js. In the other terminal, 
start the application with npm run dev.

0:02:54.480,0:03:02.240
The app will be served at localhost:5173. 
Open that in your browser, and you’ll see your

0:03:02.240,0:03:12.080
application running. In the center, the Beefree 
SDK email editor is embedded and ready to use.

0:03:12.080,0:03:14.400
You’re ready to start editing.

```
{% endtab %}
{% endtabs %}
