# Open AI and Data Security

### Overview <a href="#overview" id="overview"></a>

This document discusses the data flow of your OpenAI API key from the moment you activate the OpenAI AddOn within your Beefree SDK Developer Console. In this document, you learn more about Beefree SDK’s security practices, frameworks, and protocols in reference to protecting your sensitive data assets.

### Data Flow Diagram <a href="#data-flow-diagram" id="data-flow-diagram"></a>

The following diagram provides a visualization of the data flow for the OpenAI API key.

<figure><img src="https://docs.beefree.io/wp-content/uploads/2023/10/diagram-export-10-26-2023-3_54_51-PM.png" alt=""><figcaption></figcaption></figure>

This data flow diagram illustrates the flow of data and the key components involved in securing the API key from developer input to end user interaction.

The following list shows each component within the data flow diagram along with the component’s description.

* **Developer Console:** This is where the developer inputs the API key, initiating the process.
* **OpenAI AddOn:** This is where the developer enters their OpenAI API key and activates the OpenAI AddOn for their host application.&#x20;
* **Data Store:** The encrypted API key is stored securely in the data store.
* **End User:** The end user interacts with the host application.
* **HA OpenAI AddOn:** The frontend user interface of the OpenAI AddOn that the end user engages with.
* **Proxy:** The proxy receives and forwards requests to the OpenAI API, and sends responses to the OpenAI AddOn within the host application.
* **OpenAI API:** OpenAI API processes requests and provides responses.

### Data Management Details <a href="#data-management-details" id="data-management-details"></a>

The flow and management of your OpenAI API key is designed to ensure its security. Security measures are implemented as soon as you enter your OpenAI API key into the Developer Console. Once you enter your API key, it is immediately encrypted over [TLS](https://www.internetsociety.org/deploy360/tls/basics/). From there, the encrypted API key is securely stored in the Beefree data store. Your API key remains encrypted both at rest and during transit.&#x20;

When the end user types a prompt into the OpenAI AddOn, their prompt is forwarded through a proxy. The proxy receives the request, retrieves the OpenAI API key, and forwards both the API key and the prompt to OpenAI. OpenAI processes the request and forwards the response to the proxy. The proxy then delivers the OpenAI response to the OpenAI AddOn, which displays the response in your application’s frontend to the end user.

Note: The proxy _does not_ log any personal data, and only facilitates secure communication from request to response.Throughout this process, the API key remains in the backend, preserving its security and ensuring no personal data is processed by the application. This approach is [GDPR compliant](https://beefree.io/gdpr-compliance).
