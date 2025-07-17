# How to Change your AI Provider

{% embed url="https://www.youtube.com/watch?v=_FybVH28DR4" %}

{% tabs %}
{% tab title="About" %}
In this video, we'll show you how to configure the AI Writing Assistant AddOn in the Beefree SDK developer console. This step-by-step tutorial covers activating and switching AI providers like OpenAI and Azure OpenAI, ensuring seamless AI integration for your end users. Follow along to take full advantage of the AI Writing Assistant and elevate your application's AI-driven features effortlessly. \*To configure the addon to customize your end user’s experience, visit our support doc: [https://docs.beefree.io/beefree-sdk/a...](https://www.youtube.com/redirect?event=video_description\&redir_token=QUFFLUhqblN6ZmtGWEZMNVpyRW5USVN3aDByTHUyRENVUXxBQ3Jtc0ttUkN3U1JXMEF4dEczNkxBU3JBQ3ByMDVHSW1hMUpFTk83a1paaXhKYTFDV2k4bklObFJRRS1LaDU0b2t4WmVZeVpZaWtNVTF4dTQtWlFPLVZndm1kUGdHbzh4YTRZdVBONDNkbVpkWEN6a0JVRnBYOA\&q=https%3A%2F%2Fdocs.beefree.io%2Fbeefree-sdk%2Faddons%2Fpartner-addons%2Fopenai-addon\&v=_FybVH28DR4)&#x20;

Chapters&#x20;

* [0:00](https://www.youtube.com/watch?v=_FybVH28DR4) Introduction&#x20;
* [0:12](https://www.youtube.com/watch?v=_FybVH28DR4\&t=12s) Lesson breakdown&#x20;
* [0:45](https://www.youtube.com/watch?v=_FybVH28DR4\&t=45s) What is Beefree's AI Writing Assistant?&#x20;
* [1:08](https://www.youtube.com/watch?v=_FybVH28DR4\&t=68s) Setting up the AI Writing Assistant AddOns&#x20;
* [2:36](https://www.youtube.com/watch?v=_FybVH28DR4\&t=156s) Activating the AddOn&#x20;
* [3:15](https://www.youtube.com/watch?v=_FybVH28DR4\&t=195s) Customizing the Addon's Configuration&#x20;
* [3:36](https://www.youtube.com/watch?v=_FybVH28DR4\&t=216s) Changing your AI provider&#x20;
* [4:08](https://www.youtube.com/watch?v=_FybVH28DR4\&t=248s) Outro
{% endtab %}

{% tab title="Transcripts" %}
The following text includes the complete transcript for this video.

```
0:00:02.960,0:00:07.200
Hey there! Mark from Beefree, and in this 
video, I'll guide you step-by-step through

0:00:07.200,0:00:13.200
configuring your AI provider for the AI 
Writing Assistant add-on within Beefree SDK.

0:00:13.200,0:00:16.600
In the first part of this tutorial, 
we'll cover how to configure the AI

0:00:16.600,0:00:20.960
Writing Assistant add-on for those 
who have not yet activated it. Here,

0:00:20.960,0:00:25.000
we'll tackle how to configure it 
with the provider of your choice.

0:00:25.000,0:00:28.960
After that, we'll move on to the second part 
of the tutorial for those who have already

0:00:28.960,0:00:34.400
configured the AI Writing Assistant in their host 
application. In this section, we'll demonstrate

0:00:34.400,0:00:41.120
how to seamlessly switch your AI Provider 
from OpenAI to Azure OpenAI or vice versa.

0:00:41.120,0:00:45.960
Before we get started, though, let's review 
the following: The AI Writing Assistant

0:00:45.960,0:00:51.600
helps your host applications and users quickly 
generate written content within their designs,

0:00:51.600,0:00:56.920
helping them get across the finish line faster. 
They can use the AI Writing Assistant to generate

0:00:56.920,0:01:01.600
content for things like the title block, 
the paragraph block, the button block,

0:01:01.600,0:01:08.320
the list block, and metadata like titles, 
descriptions, subject lines, and preheader.

0:01:08.320,0:01:13.720
Okay, let's start with the first flow now, which 
is activating the AI Writing Assistant add-on in

0:01:13.720,0:01:19.560
the Beefree SDK developer console. After you log 
in, you'll land on the dashboard. First, head to

0:01:19.560,0:01:26.520
the Email Builder application by clicking Details. 
Once you're in the details page, select Add-ons.

0:01:26.520,0:01:32.160
Now, if you haven't already installed the AI 
Writing Assistant, just click on Browse Add-ons,

0:01:32.160,0:01:36.120
and from there, you can either scroll 
through the list to find it or use the

0:01:36.120,0:01:39.240
search bar. It's important to 
remember that the AI Writing

0:01:39.240,0:01:44.640
Assistant add-on only works with Azure 
OpenAI and OpenAI. If new providers are

0:01:44.640,0:01:49.360
added in the future, be sure to check 
the description here for any updates.

0:01:49.360,0:01:54.640
Okay, let's click Install. This brings 
you to the setup modal. If you haven't

0:01:54.640,0:01:59.840
set up any providers already, you'll need 
to create one. Let's click Manage Providers

0:02:01.200,0:02:08.320
and then Add Provider. Under Type, we can 
select our AI provider. For this example,

0:02:08.320,0:02:13.920
let's go with Azure OpenAI. Next, we'll need 
to fill in the name. It needs to be at least

0:02:13.920,0:02:19.360
three characters long and should be unique, 
so we can call this "Azure OpenAI Test."

0:02:19.360,0:02:25.120
And we'll need to add the API key, the URL 
provider, and the deployment ID. You can find

0:02:25.120,0:02:31.560
all of this information in your Azure OpenAI 
account. Once that's done, we can hit Save.

0:02:31.560,0:02:37.240
Okay, awesome! We can see that the Azure OpenAI 
provider is now active. Now that we've set up

0:02:37.240,0:02:44.360
the provider, we need to activate the add-on. So 
let's go back to Enabled Add-ons, click Edit under

0:02:44.360,0:02:57.080
AI Writing Assistant, select your provider in the 
drop-down, enable the toggle, and then hit Save.

0:02:57.080,0:03:01.240
Okay, great! The add-on has successfully 
been activated. Now you'll know for

0:03:01.240,0:03:05.720
sure that the add-on is working for your 
end-users by simply entering the Builder,

0:03:05.720,0:03:09.440
dropping in a title block, 
and clicking on the text,

0:03:09.440,0:03:14.480
and we can see that the Right with AI 
button is now visible in the sidebar.

0:03:14.480,0:03:18.800
If you would like to configure the add-on 
to customize your end-user's experience, you

0:03:18.800,0:03:24.840
will need to edit your Bee config code and add the 
add-on's property. That means including the add-on

0:03:24.840,0:03:31.120
ID AI Integration. This is the only part that is 
required for your configuration. You can then add

0:03:31.120,0:03:36.120
optimal settings highlighted in our documentation, 
which I've linked in the description.

0:03:36.120,0:03:41.840
Next, let's quickly show you how to change your 
AI Provider from one to another. In this example,

0:03:41.840,0:03:47.400
let's assume we've added two AI providers to 
our application. All we need to do now is head

0:03:47.400,0:03:54.280
to Enabled Add-ons. Under AI Writing Assistant, we 
can select Edit. In the drop-down menu, we can now

0:03:54.280,0:04:00.720
select the AI provider of our choice, so let's go 
with OpenAI. We can ensure that the enable toggle

0:04:00.720,0:04:07.640
is switched to On and then hit Save. We've now 
successfully switched providers! It's that easy.

0:04:07.640,0:04:13.160
Now, that's all for this video. We hope your 
end-users enjoy the AI Writing Assistant add-on!

0:04:13.160,0:04:18.600
If you found this video helpful and want to stay 
in the loop anytime a new Beefree SDK video is

0:04:18.600,0:04:23.520
posted, make sure to hit that like button and 
subscribe to our YouTube channel. That way,

0:04:23.520,0:04:29.720
YouTube will recommend these tutorials, so you 
won't have to lift a finger. Thanks for watching!

```
{% endtab %}
{% endtabs %}
