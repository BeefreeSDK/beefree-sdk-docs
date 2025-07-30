---
description: >-
  Learn more about what the Release Candidate Environment is, how to get started
  with it, and how to integrate it into your development life cycle.
---

# Release Candidate Environment

{% hint style="info" %}
The Release Candidate Environment is available on [Enterprise plans.](https://developers.beefree.io/pricing-plans)
{% endhint %}

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
* The program does not allow for customized release schedules per customer; all Enterprise customers follow the same cycle. Customized release schedules are available on VPC plans. For more information, contact the Beefree SDK team using this [contact form](https://developers.beefree.io/talk-to-sales) and request more information about customized release schedules with VPC plans.

### Additional Considerations

The Release Candidate Environment is specifically designed for frontend features, the JSON-to-HTML parser, and the JSON Bumper. Backend services are not currently covered under this process. Bug fixes, while critical, may bypass the RC process when necessary to expedite resolutions. By adopting the Release Candidate process, Beefree SDK provides Enterprise customers with greater predictability, quality assurance, and peace of mind in managing their integrations.
