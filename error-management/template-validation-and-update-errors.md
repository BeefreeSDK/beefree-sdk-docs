# Template validation and update errors

#### Example Response

```


{"code":2200,"message":"required key not provided @ data[u'page'][u'body'][u'content'][u'style'][u'color']","error":"BAD REQUEST"}


```

#### Error Codes

| Code   | Message                       | Error           | HTTP status | Info                                                                                                                                                                                                                                             |
| ------ | ----------------------------- | --------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `2000` | Generic Bump Error            | BAD REQUEST     | 400         | Default generic bump error                                                                                                                                                                                                                       |
| `2100` | Invalid Target Version        | BAD REQUEST     | 400         | The target version does not exists                                                                                                                                                                                                               |
| `2200` | \[validation error detail]    | BAD REQUEST     | 400         | <p>The JSON didn’t pass the validation.</p><p>The cause may be:</p><ul><li>Missing keys</li><li>Added unknown keys</li></ul><p>Message e.g.: <code>required key not provided @ data[u'page'][u'body'][u'content'][u'style'][u'color']</code></p> |
| `2300` | Missing Template Version      | BAD REQUEST     | 400         | There is no template version in the page                                                                                                                                                                                                         |
| `2400` | Invalid Template Version      | BAD REQUEST     | 400         | The specified version is unknown                                                                                                                                                                                                                 |
| `2500` | Transformation Error          | BAD REQUEST     | 400         | Issues during JSON version migration                                                                                                                                                                                                             |
| `2600` | Backward Transformation Error | BAD REQUEST     | 400         | Issues during JSON version migration                                                                                                                                                                                                             |
| `3000` | Service Error                 | SERVICE FAILURE | 503         | System failure not related with invalid json files                                                                                                                                                                                               |
