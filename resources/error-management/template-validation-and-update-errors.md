# Template validation and update errors

## Example Response

```javascript

{"code":2200,"message":"required key not provided @ data[u'page'][u'body'][u'content'][u'style'][u'color']","error":"BAD REQUEST"}

```

## Error Codes

<table><thead><tr><th width="95">Code</th><th width="158">Message</th><th width="146">Error</th><th width="127">HTTP status</th><th>Info</th></tr></thead><tbody><tr><td><code>2000</code></td><td>Generic Bump Error</td><td>BAD REQUEST</td><td>400</td><td>Default generic bump error</td></tr><tr><td><code>2100</code></td><td>Invalid Target Version</td><td>BAD REQUEST</td><td>400</td><td>The target version does not exists</td></tr><tr><td><code>2200</code></td><td>[validation error detail]</td><td>BAD REQUEST</td><td>400</td><td><p>The JSON didn’t pass the validation.</p><p>The cause may be:</p><ul><li>Missing keys</li><li>Added unknown keys</li></ul><p>Message e.g.: <code>required key not provided @ data[u'page'][u'body'][u'content'][u'style'][u'color']</code></p></td></tr><tr><td><code>2300</code></td><td>Missing Template Version</td><td>BAD REQUEST</td><td>400</td><td>There is no template version in the page</td></tr><tr><td><code>2400</code></td><td>Invalid Template Version</td><td>BAD REQUEST</td><td>400</td><td>The specified version is unknown</td></tr><tr><td><code>2500</code></td><td>Transformation Error</td><td>BAD REQUEST</td><td>400</td><td>Issues during JSON version migration</td></tr><tr><td><code>2600</code></td><td>Backward Transformation Error</td><td>BAD REQUEST</td><td>400</td><td>Issues during JSON version migration</td></tr><tr><td><code>3000</code></td><td>Service Error</td><td>SERVICE FAILURE</td><td>503</td><td>System failure not related with invalid json files</td></tr></tbody></table>
