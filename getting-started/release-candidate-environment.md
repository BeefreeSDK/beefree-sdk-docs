---
description: >-
  Learn more about what the Release Candidate Environment is, how to get started
  with it, and how to integrate it into your development life cycle.
---

# Release Candidate Environment

## Overview

A Release Candidate (RC) Environment is a crucial part of the deployment workflow designed to provide Enterprise customers with additional stability and assurance before a feature reaches full production. Unlike standard releases, which immediately roll out updates to all users, the RC environment acts as an intermediate step. It allows selected customers to access a production-ready version of the latest code before it becomes available to the wider user base. This controlled rollout process mitigates risks associated with unforeseen bugs and ensures a smoother transition. It also mitigates the risk of regressions and rollbacks. By implementing an RC environment, Beefree SDK enables Enterprise customers to conduct their own QA testing on new features, reducing potential disruptions when updates go live.

### Benefits of the Release Candidate Environment

The following list includes some of the most commonly referenced benefits of utilizing the Release Candidate Environment.

* **Risk Mitigation:** Enterprise customers can validate new updates in a stable, production-like setting before they are fully deployed.
* **Enhanced Quality Assurance:** QA teams can test features in real-world scenarios, catching regressions before broader release.
* **Predictable Deployment Schedule:** A structured release cadence (RC → General → Delayed) ensures smoother rollouts with fewer surprises.
* **Reduced Need for Rollbacks:** The phased approach minimizes critical failures in production, lessening the necessity for emergency rollbacks.
* **Customer Control:** Enterprise customers have additional time to adjust workflows and prepare internal documentation before full adoption.

## How the Release Candidate Environment Works

The RC environment operates within a structured release cycle, ensuring that new updates are progressively introduced. When a new feature is ready for release, it is first deployed to the RC environment. Only Developer applications linked to the RC version can access this release. After a one week waiting period—assuming no major regressions are found—the update moves to the stable version, making it available to non-Enterprise customers. After a week, the update reaches the Delayed version, which is linked to Enterprise Production applications. This phased approach ensures that issues are detected early while maintaining a predictable release schedule.

### Requirements for Accessing the Release Candidate Environment

Reference the following requirements for accessing the Release Candidate Environment prior to getting started with it.

* Only available to Enterprise plan customers with Developer applications.
* Contact the Beefree SDK team using this [contact form](https://developers.beefree.io/talk-to-sales) and request access to the Release Candidate Environment.
* Customers must be aware that while the RC version is production-ready, it is still subject to final testing and potential bug fixes.
* The program does not allow for customized release schedules per customer; all Enterprise customers follow the same cycle. Customized release schedules are available on VPC plans. For more information, contact the Beefree SDK team using this [contact form](https://developers.beefree.io/talk-to-sales) and request more information about customized release schedules with VPC plans.&#x20;

### How to Use the Release Candidate Environment

This section discusses how to access the release candidate environment and use it.

#### Instructions

To get the HTML version of a Beefree SDK message in the Release Candidate (RC) environment, you will need the following:

1. The Beefree SDK Support Team will provide you with a username and password (we will need a user’s email address to enable this).
2. A Beefree SDK JSON source file.
3. The ability to perform a call to a REST API. You can do that in different ways:
   * Applications like Postman or Insomnia
   * Use the “curl” command in a shell
   * With a custom script

The call should be addressed to one of the following endpoints, depending on the HTML output that you wish to receive back:

* `https://stg-bee-multiparser.getbee.io/api/v3/parser/email` - To receive HTML for Email
* `https://stg-bee-multiparser.getbee.io/api/v3/parser/pages` - To receive HTML for Webpages
* `https://stg-bee-multiparser.getbee.io/api/v3/parser/amp4email` - To receive AMP for Email
* `https://stg-bee-multiparser.getbee.io/api/v3/parser/popup` - To receive HTML for Popups
* `https://stg-bee-multiparser.getbee.io/api/v3/parser/text` - To receive the plain text version of the message

#### Additional Requirements

Reference the following additional requirements for using the Release Candidate Environment.

* It has to be a POST call.
* The Beefree SDK JSON has to be sent in the body of the REST call.
* It must include a Basic Authentication header in which you specify your username and password.

Upon success, the body of the response will contain the desired output. In case of an error, the response's body will contain the error details.

Please do not use this method in production. This is an RC environment, and it may change its behavior in the future.

**Example**

```sh
curl --request POST \
--url "https://stg-bee-multiparser.getbee.io/api/v3/parser/email" \
--user "USERNAME:PASSWORD" \
--header "Content-Type: application/json" \
--data @"JSON_FILE.json" \
--output "OUTPUT.html"
```

**Legenda**

The following fields are required in the example above.

* <mark style="background-color:yellow;">USERNAME</mark> and <mark style="background-color:yellow;">PASSWORD</mark> are your credentials provided by the Beefree SDK team.
* <mark style="background-color:yellow;">JSON\_FILE.json</mark> is the Beefree SDK source file.
* <mark style="background-color:yellow;">OUTPUT.html</mark> is the desired output file.

### Additional Considerations

The Release Candidate Environment is specifically designed for frontend features, the JSON-to-HTML parser, and the JSON Bumper. Backend services are not currently covered under this process. Bug fixes, while critical, may bypass the RC process when necessary to expedite resolutions. By adopting the Release Candidate process, Beefree SDK provides Enterprise customers with greater predictability, quality assurance, and peace of mind in managing their integrations.
