# Template Validation and Update

As Beefree SDK is improved and updated over time, the JSON structure we use to describe a document may change.

The endpoint _bump.getbee.io_ validates and – when needed – updates a JSON document that had been created with an earlier version of the builder.

This guarantees backward compatibility for older documents: any document (e.g., an email campaign, a template in your email template catalog, etc.) using a JSON structure that the system finds to be out-of-date gets updated automatically the next time it is passed to the builder.

Currently, this feature is working in test mode, tracking any issue with existing JSON documents and allowing us to improve this service. During this testing phase, the system does not stop the loading of the builder when an issue is found.

#### Error response example

```javascript


{"code":2200,"message":"required key not provided @ data[u'page'][u'body'][u'content'][u'style'][u'color']","error":"BAD REQUEST"}


```

To read the full list of possible errors, please refer to [Template Validation and Update Errors](template-validation-and-update-errors.md).
