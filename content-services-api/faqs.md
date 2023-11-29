# FAQs

### API billing: why we are charging for this API <a href="#api-billing-why-we-are-charging-for-this-api" id="api-billing-why-we-are-charging-for-this-api"></a>

The [Content Services API (CSAPI)](./) allows you to carry out a number of [useful tasks](content-services-api-reference.md), like converting an email or a page into a thumbnail image or a PDF document, or updating a footer into all the emails that use it (i.e. a [_saved row_](../saved-rows/)).

These tasks consume resources in our Amazon Web Services environment, so we have to account for that. We did extensive research to define pricing that is consistent with other APIs.

Here is a quick summary:

| Plan        | Included API calls | Cost per extra API call |
| ----------- | ------------------ | ----------------------- |
| Essentials  | 15,000             | $0.01                   |
| Core        | 100,000            | $0.006                  |
| Superpowers | 250,000            | $0.003                  |
| Enterprise  | 1,000,000          | $0.003                  |

There will be no changes to the functionality of the CSAPI, except that we’ve added a really useful Merge API that allows you to update saved rows in the documents that use them. You can find complete [technical documentation on the new “merge” method here](content-services-api-reference.md).

Most changes related to CSAPI will be in the background, but there will be some changes in the Beefree SDK Console, and in terms of billing.

* **API Key Management**: when you configure an application in the Beefree SDK Console, you will see two actions – instead of a single _Revoke_ action – in the area of the application settings where your API key is shown:
  * **Regenerate**: Revokes the current key and creates a new one
  * **Disable and revoke**: Revokes the current key and disables the service, so you will not be charged for it\*

![](https://docs.beefree.io/wp-content/uploads/2020/01/bee-plugin-developer-portal-msapi-1-20200128.png)

{% hint style="info" %}
**\*Note:** Extra API calls are charged at the end of the billing period. For this reason, the first invoice after cancellation may include CSAPI charges.
{% endhint %}

* **Billing statement changes**: you will see new line items on your Beefree SDK invoice.

### Can I try the service without paying? <a href="#can-i-try-the-service-without-paying" id="can-i-try-the-service-without-paying"></a>

You can by creating a **development application**, and then creating a new API key for that app, which will be used for development purposes. Reference our [Development Applications documentation to learn how to create one](../getting-started/development-applications.md).

### How will charges appear on my bill? <a href="#how-will-charges-appear-on-my-bill" id="how-will-charges-appear-on-my-bill"></a>

An additional charge, CSAPI, will be added to your current subscription plan invoice.

### Can I use different payment methods for each app? <a href="#can-i-use-different-payment-methods-for-each-app" id="can-i-use-different-payment-methods-for-each-app"></a>

The Content Services API is provided as a component for your current subscription and the charges will be applied to the subscription payment method. Currently, there is no option to use an alternative payment method specific to these charges.

### How do you calculate request limits? <a href="#how-do-you-calculate-request-limits" id="how-do-you-calculate-request-limits"></a>

API requests rate limits exist independently of any API key’s monthly usage allowance.

As of January, 2020, the API has the following rate limits:

* **Per minute:** 500 requests
* **Per second:**  100 requests
