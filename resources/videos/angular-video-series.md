---
description: Video series on how to get started with Beefree SDK in an Angular application.
---

# Angular Video Series

## Angular Video Series

This video series includes the following tutorials:

* [Video #1](angular-video-series.md#video-1-quickstart-guide-no-code-email-builder-for-beefree-sdk-part-1): Quickstart Guide: No-code Email Builder for Beefree SDK (Part 1)
* [Video #2](angular-video-series.md#video-2-quickstart-guide-angular-no-code-email-builder-part-2): Quickstart Guide: Angular No-code Email Builder (Part 2)
* [Video #3](angular-video-series.md#video-3-quickstart-guide-angular-no-code-email-builder-part-3):  Quickstart Guide: Angular No-code Email Builder (Part 3)

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

### Video #2: Quickstart Guide: Angular No-code Email Builder (Part 2)

{% embed url="https://www.youtube.com/watch?v=EJsZaVK0L50" %}

{% tabs %}
{% tab title="About" %}
This quickstart video series provides a step-by-step tutorial of how to set up and run a fully functional Angular app integrated with the Beefree SDK. By the end of this guide, you’ll have a live development environment showcasing the Beefree email editor embedded in Angular—following best practices for this framework.

PART 2: introduction to installing the Beefree SDK with an Angular application
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
1
00:00:02,960 --> 00:00:05,680
Hi developers. In this video, we're 
going to talk you through using the

2
00:00:05,680 --> 00:00:10,720
Beefree SDK in an Angular application. If 
your framework of choice is React or Vue.js,

3
00:00:10,720 --> 00:00:15,120
we have separate videos for those as well. In 
this video, we'll first have you clone a sample

4
00:00:15,120 --> 00:00:19,520
Angular repo that we have available for you in 
GitHub. Then we'll talk through authentication

5
00:00:19,520 --> 00:00:24,560
both with environment variables and securing 
a token through a proxy server. After that,

6
00:00:24,560 --> 00:00:27,760
we'll look at the Angular component that we 
built to house your local instance of the

7
00:00:27,760 --> 00:00:32,480
Beefree SDK in your Angular app. And finally, 
we'll talk you through how to run it locally.
```
{% endtab %}
{% endtabs %}

***

### Video #3:  Quickstart Guide: Angular No-code Email Builder (Part 3)

{% embed url="https://www.youtube.com/watch?v=Kw5SnJRdpGY" %}

{% tabs %}
{% tab title="About" %}
This quickstart video series provides a step-by-step walkthrough of how to set up and run a fully functional Angular app integrated with the Beefree SDK. By the end of this guide, you’ll have a live development environment showcasing the Beefree email editor embedded in Angular—following best practices for this framework.

PART 3: in this video, you'll learn how to:

* How to create a new Angular app
* Connect your application to your Beefree account by creating an .env file
* Understand the core logic of the Beefree SDK initialize it and create a new instance
* Run your Angular app locally with the builder fully integrated
{% endtab %}

{% tab title="Transcript" %}
The following text includes the complete transcript for this video.

```
1
00:00:01,440 --> 00:00:05,440
To get the most out of this video, make 
sure you’ve set up your Beefree account

2
00:00:05,440 --> 00:00:09,360
and the Beefree SDK console, and that you 
have access to your Client ID and Client

3
00:00:09,360 --> 00:00:13,920
Secret. As long as you have that and a current 
version of Node.js, you’re ready to get started.

4
00:00:13,920 --> 00:00:19,680
First, navigate to the GitHub repo called Beefree 
Angular demo, within the Beefree SDK account.

5
00:00:29,120 --> 00:00:32,400
Once that’s downloaded, cd 
into the project folder,

6
00:00:32,400 --> 00:00:48,400
which should be beefree-angular-demo. 
Then run npm install beefree.io-sdk.

7
00:00:48,400 --> 00:00:54,320
That went smoothly. Next, install the 
supporting packages for our proxy server, which

8
00:00:55,600 --> 00:00:58,720
will handle authentication. All of these 
commands are available in the README.

9
00:01:00,960 --> 00:01:08,320
Excellent—now we’re ready to connect this 
Beefree SDK instance with your credentials.

10
00:01:09,040 --> 00:01:18,800
If we list the files, you’ll see a 
.env.example file. Open it. Where it

11
00:01:18,800 --> 00:01:22,880
says YOUR_CLIENT_ID and YOUR_CLIENT_SECRET, 
replace those with your actual Client ID and

12
00:01:22,880 --> 00:01:30,240
Secret from the developer console. 
For example, select a test instance,

13
00:01:30,240 --> 00:01:49,280
click "Details" or "Reveal" to see both the 
ID and secret, and copy-paste them here.

14
00:02:08,560 --> 00:02:11,440
Two more things to do with this environment file:

15
00:02:11,440 --> 00:02:20,320
Rename it from .env.example to .env 
so it works correctly in our package.

16
00:02:21,200 --> 00:02:27,520
Add it to your .gitignore file. We don’t want 
these sensitive variables pushed into version

17
00:02:27,520 --> 00:02:38,000
control. Check under Environment files—if 
.env is already listed, you’re good to go.

18
00:02:38,000 --> 00:02:42,480
Next, a quick note about authentication. To 
run the Beefree SDK, you need a secure way

19
00:02:42,480 --> 00:02:50,470
to fetch authentication tokens. We provide an 
example in proxyServer.js in the root directory.

20
00:02:50,470 --> 00:02:58,880
Open that file. You’ll see we’re making a 
POST request using Axios to log into Beefree,

21
00:02:58,880 --> 00:03:04,160
populating the necessary fields with your 
Client ID and Secret, and returning the

22
00:03:04,160 --> 00:03:11,120
full JSON body. This authenticates and 
initializes the Beefree SDK. You can use

23
00:03:11,120 --> 00:03:15,840
this implementation or replace it with one 
suitable for your development environment.

24
00:03:15,840 --> 00:03:19,440
With the project and proxy set up, let’s look 
at the Angular components that render the

25
00:03:19,440 --> 00:03:26,240
Beefree SDK editor. We created a standalone 
Angular component called BeefreeEditor.

26
00:03:26,240 --> 00:03:31,920
In the TypeScript file, the main logic lives 
inside the ngOnInit lifecycle hook. First,

27
00:03:31,920 --> 00:03:38,240
we securely fetch the token from the 
local proxy server. Once we have the

28
00:03:38,240 --> 00:03:43,120
token, we create a new Beefree SDK 
instance and call its start method.

29
00:03:44,800 --> 00:03:50,120
This method takes a configuration object 
where we define key properties, such as:

30
00:03:50,120 --> 00:03:54,080
container: the ID of the HTML 
element where the editor will load

31
00:03:54,640 --> 00:04:01,760
Callback functions like onSave and onError, 
letting our Angular app react to editor events

32
00:04:01,760 --> 00:04:03,840
Now that the editor component is ready, we just

33
00:04:03,840 --> 00:04:11,360
need to use it. Open the main app component 
(AppComponent.ts). Import the BeefreeEditor

34
00:04:13,360 --> 00:04:17,440
component and add its selector 
<beefree-editor> inside the template.

35
00:04:17,440 --> 00:04:23,120
At this point, we’re ready. Within 
our sample Angular application,

36
00:04:23,120 --> 00:04:27,920
we’ve installed a local instance of the 
Beefree SDK, handled authentication,

37
00:04:27,920 --> 00:04:32,400
and created a component to house the editor.

38
00:04:32,400 --> 00:04:38,640
To run the application, open two 
terminal windows. In the first,

39
00:04:38,640 --> 00:04:45,520
run node proxyServer.js to handle 
token authorization. In the second,

40
00:04:46,240 --> 00:04:51,200
run ng serve to start the Angular application. 
Once built, it will be served at localhost:4200.

41
00:04:51,200 --> 00:04:58,960
Open your browser and navigate there. 
You’ll see your Angular application,

42
00:04:58,960 --> 00:05:05,680
including the H1 heading and the 
documentation button. The Beefree

43
00:05:05,680 --> 00:05:09,760
SDK editor is embedded and ready to start 
adding content blocks of your choice.
```
{% endtab %}
{% endtabs %}
