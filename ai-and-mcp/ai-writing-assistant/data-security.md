# AI Providers and Data Security

## Overview <a href="#overview" id="overview"></a>

This document discusses the data flow of your API key from the moment you activate an AddOn with AI functionality within your Beefree SDK Developer Console. In this document, you learn more about Beefree SDK’s security practices, frameworks, and protocols in reference to protecting your sensitive data assets.

## Data Flow Diagram <a href="#data-flow-diagram" id="data-flow-diagram"></a>

The following diagram provides a visualization of the data flow for your AI AddOn API key. In the following diagram, OpenAI is shown as an example. However, this same flow applies to other AI provides available through Beefree SDK AddOns.&#x20;

These providers include:

* Azure OpenAI
* Azure Cognitive Vision
* DeepL
* Stability AI
* Anthropic

<figure><img src="../../../../.gitbook/assets/CleanShot 2024-04-04 at 12.04.07.png" alt=""><figcaption></figcaption></figure>

This data flow diagram illustrates the flow of data and the key components involved in securing the API key from developer input to end user interaction.

The following list shows each component within the data flow diagram along with the component’s description.

* **Developer Console:** This is where the developer inputs the API key, initiating the process.
* **AI AddOn:** This is where the developer enters their API key that they received from their AI Provider, and activates the AddOn for their host application.&#x20;
* **Data Store:** The encrypted API key is stored securely in the data store.
* **End User:** The end user interacts with the host application.
* **HA AddOn:** The frontend user interface of the AI AddOn that the end user engages with.
* **Proxy:** The proxy receives and forwards requests to the API, and sends responses to the AI AddOn within the host application.
* **AI Provider:** The AI Provider processes requests and provides responses.

## Data Management Details <a href="#data-management-details" id="data-management-details"></a>

The flow and management of your API key is designed to ensure its security. Security measures are implemented as soon as you enter your API key into the Developer Console. Once you enter your API key, it is immediately encrypted over [TLS](https://www.internetsociety.org/deploy360/tls/basics/). From there, the encrypted API key is securely stored in the Beefree data store. Your API key remains encrypted both at rest and during transit.&#x20;

When the end user types a prompt into the AddOn, their prompt is forwarded through a proxy. The proxy receives the request, retrieves the API key, and forwards both the API key and the prompt to the AI Provider. The AI Provider processes the request and forwards the response to the proxy. The proxy then delivers the response to the AI AddOn, which displays the response in your application’s frontend to the end user.

**Note:** The proxy _does not_ log any personal data and only facilitates secure communication from request to response. Throughout this process, the API key remains in the backend, preserving its security and ensuring no personal data is processed by the application. This approach is [GDPR compliant](https://beefree.io/gdpr-compliance).

For additional information, we recommend you reference our [Terms of Service](https://sdkwebflow.beefree.io/terms-of-service) and our [AIF third-party providers' policies](https://developers.beefree.io/aif-third-party-providers).&#x20;
