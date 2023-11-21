# JSON Parser errors

### Example Response

```


{"code":4001,"message":"Authentication error","details":"Authentication header is missing"}


```

### Error Codes

#### Authentication errors

| Code   | Message              | HTTP Status      | Details                          |
| ------ | -------------------- | ---------------- | -------------------------------- |
| `4001` | Authentication error | 401 Unauthorized | Authentication header is missing |
| `4005` | Authentication error | 401 Unauthorized | Bearer token format is invalid   |
| `4010` | Authentication error | 401 Unauthorized | Token expired                    |

#### Preliminary JSON parsing errors

| Code   | Message            | HTTP Status     | Details                          |
| ------ | ------------------ | --------------- | -------------------------------- |
| `4015` | Bump service error | 400 Bad Request | Error while calling Bump service |
| `...`1 | Bump service error | 400 Bad Request | …1                               |

1: In case of a Bump error, the JSON parser forwards to the user the error code it receives from the Bump.

#### JSON Pre-processing errors

| Code   | Message                    | HTTP Status     | Details                                                    |
| ------ | -------------------------- | --------------- | ---------------------------------------------------------- |
| `4101` | JSON pre-processing failed | 400 Bad Request | Generic parsing error                                      |
| `4105` | JSON pre-processing failed | 400 Bad Request | Error while checking special \<code> tags                  |
| `4110` | JSON pre-processing failed | 400 Bad Request | Error while checking for HTML blocks                       |
| `4115` | JSON pre-processing failed | 400 Bad Request | Error while checking conditional statements                |
| `4120` | JSON pre-processing failed | 400 Bad Request | Error while adding conditional statements to rows          |
| `4125` | JSON pre-processing failed | 400 Bad Request | Error while adding styles to rows container                |
| `4130` | JSON pre-processing failed | 400 Bad Request | Error while adding classes for conditional statements      |
| `4135` | JSON pre-processing failed | 400 Bad Request | Error while adding computed styles for each grid block row |
| `4140` | JSON pre-processing failed | 400 Bad Request | Error while calculating cell widths                        |
| `4145` | JSON pre-processing failed | 400 Bad Request | Error while adding background on columns                   |
| `4190` | JSON pre-processing failed | 400 Bad Request | Error while adding main CSS styles                         |
| `4191` | JSON pre-processing failed | 400 Bad Request | Error while adding main CSS media queries styles           |
| `4192` | JSON pre-processing failed | 400 Bad Request | Error while adding client-specific CSS styles              |
| `4501` | Pre-processing error       | 403 Forbidden   | Error assembling CSS Rules                                 |
| `4502` | Pre-processing error       | 403 Forbidden   | Error compiling general page CSS styles                    |
| `4503` | Pre-processing error       | 403 Forbidden   | Error compiling body CSS styles                            |
| `4504` | Pre-processing error       | 403 Forbidden   | Error converting JSON styles rules to CSS                  |

#### HTML Creation errors

| Code   | Message               | HTTP Status     | Details                                                               |
| ------ | --------------------- | --------------- | --------------------------------------------------------------------- |
| `4201` | HTML creation error   | 400 Bad Request | Generic JSON to HTML conversion error                                 |
| `4202` | HTML creation error   | 400 Bad Request | Communication error to JSON content workers                           |
| `4210` | HTML creation error   | 400 Bad Request | Communication error with text block worker                            |
| `4211` | HTML creation error   | 400 Bad Request | Text block worker has notified a processing Error: (…)1               |
| `4220` | HTML creation error   | 400 Bad Request | Communication error with button block worker                          |
| `4221` | HTML creation error   | 400 Bad Request | Button block worker has notified a processing Error: (…)1             |
| `4230` | HTML creation error   | 400 Bad Request | Communication error with video block worker                           |
| `4231` | HTML creation error   | 400 Bad Request | Video/MergeContent block worker has notified a processing Error: (…)1 |
| `4240` | HTML creation error   | 400 Bad Request | Communication error with social block worker                          |
| `4241` | HTML creation error   | 400 Bad Request | Social block worker has notified a processing Error: (…)1             |
| `4242` | HTML creation error   | 400 Bad Request | Communication error with icon block worker                            |
| `4243` | HTML creation error   | 400 Bad Request | Icon block worker has notified a processing Error: (…)1               |
| `4244` | HTML creation error   | 400 Bad Request | Communication error with menu block worker                            |
| `4245` | HTML creation error   | 400 Bad Request | Menu block worker has notified a processing Error: (…)1               |
| `4250` | HTML creation error   | 400 Bad Request | Communication error with image block worker                           |
| `4251` | HTML creation error   | 400 Bad Request | Image block worker has notified a processing Error: (…)1              |
| `4260` | HTML creation error   | 400 Bad Request | Communication error with merge content worker                         |
| `4270` | HTML creation error   | 400 Bad Request | Error handling custom addon module                                    |
| `4601` | Rendering error       | 403 Forbidden   | Error cleaning up button module HTML code                             |
| `4602` | Rendering error       | 403 Forbidden   | Error cleaning up text module HTML code                               |
| `4603` | Rendering error       | 403 Forbidden   | Error checking form elements                                          |
| `4604` | Form validation error | 403 Forbidden   | Error in (…)2                                                         |
| `4605` | Rendering error       | 403 Forbidden   | Custom video format not supported                                     |
| `4920` | Rendering error       | 403 Forbidden   | Video block is corrupted                                              |
| `4600` | Rendering error       | 403 Forbidden   | (…)1                                                                  |

1: Additional details are provided, depending on the error that the content worker is reporting.

2: Additional details are provided, depending on the form field that missed validation.

#### Post-processing errors

| Code   | Message                    | HTTP Status     | Details                                      |
| ------ | -------------------------- | --------------- | -------------------------------------------- |
| `4301` | HTML post-processing error | 400 Bad Request | Generic post-processing error                |
| `4310` | HTML post-processing error | 400 Bad Request | Error while transforming images URI          |
| `4320` | HTML post-processing error | 400 Bad Request | Error inserting custom HTML codes            |
| `4330` | HTML post-processing error | 400 Bad Request | Error replacing custom Beefree SDK code tags |
| `4340` | HTML post-processing error | 400 Bad Request | Error inserting display conditions           |
| `4700` | Post-processing error      | 403 Forbidden   | Error assembling the final HTML page         |
