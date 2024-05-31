# JSON Parser errors

## Example Response

```json

{"code":4001,"message":"Authentication error","details":"Authentication header is missing"}

```

## Error Codes

### Authentication errors

| Code   | Message              | HTTP Status      | Details                          |
| ------ | -------------------- | ---------------- | -------------------------------- |
| `4001` | Authentication error | 401 Unauthorized | Authentication header is missing |
| `4005` | Authentication error | 401 Unauthorized | Bearer token format is invalid   |
| `4010` | Authentication error | 401 Unauthorized | Token expired                    |

## Preliminary JSON parsing errors

{% hint style="info" %}
The **Bump service** is the internal codename for our JSON validation/update service. You can read more in our [Template Validation and Update article](template-validation-and-update.md).
{% endhint %}

| Code   | Message            | HTTP Status     | Details                          |
| ------ | ------------------ | --------------- | -------------------------------- |
| `4015` | Bump service error | 400 Bad Request | Error while calling Bump service |
| `...`1 | Bump service error | 400 Bad Request | …1                               |

1: In case of a Bump error, the JSON parser forwards to the user the error code it receives from the Bump.

## JSON Pre-processing errors

<table><thead><tr><th width="101">Code</th><th>Message</th><th width="180">HTTP Status</th><th>Details</th></tr></thead><tbody><tr><td><code>4101</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Generic parsing error</td></tr><tr><td><code>4102</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error optimizing container CSS rules for row</td></tr><tr><td><code>4105</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while checking special &#x3C;code> tags</td></tr><tr><td><code>4110</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while checking for HTML blocks</td></tr><tr><td><code>4115</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while checking conditional statements</td></tr><tr><td><code>4120</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while adding conditional statements to rows</td></tr><tr><td><code>4125</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while adding styles to rows container</td></tr><tr><td><code>4130</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while adding classes for conditional statements</td></tr><tr><td><code>4135</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while adding computed styles for each grid block row</td></tr><tr><td><code>4140</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while calculating cell widths</td></tr><tr><td><code>4145</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while adding background on columns</td></tr><tr><td><code>4190</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while adding main CSS styles</td></tr><tr><td><code>4191</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while adding main CSS media queries styles</td></tr><tr><td><code>4192</code></td><td>JSON pre-processing failed</td><td>400 Bad Request</td><td>Error while adding client-specific CSS styles</td></tr><tr><td><code>4501</code></td><td>Pre-processing error</td><td>403 Forbidden</td><td>Error assembling CSS Rules</td></tr><tr><td><code>4502</code></td><td>Pre-processing error</td><td>403 Forbidden</td><td>Error compiling general page CSS styles</td></tr><tr><td><code>4503</code></td><td>Pre-processing error</td><td>403 Forbidden</td><td>Error compiling body CSS styles</td></tr><tr><td><code>4504</code></td><td>Pre-processing error</td><td>403 Forbidden</td><td>Error converting JSON styles rules to CSS</td></tr></tbody></table>

## HTML Creation errors

<table><thead><tr><th width="112">Code</th><th width="189">Message</th><th width="168">HTTP Status</th><th>Details</th></tr></thead><tbody><tr><td><code>4201</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Generic JSON to HTML conversion error</td></tr><tr><td><code>4202</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Communication error to JSON content workers</td></tr><tr><td><code>4210</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Communication error with text block worker</td></tr><tr><td><code>4211</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Text block worker has notified a processing Error: (…)1</td></tr><tr><td><code>4220</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Communication error with button block worker</td></tr><tr><td><code>4221</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Button block worker has notified a processing Error: (…)1</td></tr><tr><td><code>4230</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Communication error with video block worker</td></tr><tr><td><code>4231</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Video/MergeContent block worker has notified a processing Error: (…)1</td></tr><tr><td><code>4240</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Communication error with social block worker</td></tr><tr><td><code>4241</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Social block worker has notified a processing Error: (…)1</td></tr><tr><td><code>4242</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Communication error with icon block worker</td></tr><tr><td><code>4243</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Icon block worker has notified a processing Error: (…)1</td></tr><tr><td><code>4244</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Communication error with menu block worker</td></tr><tr><td><code>4245</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Menu block worker has notified a processing Error: (…)1</td></tr><tr><td><code>4250</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Communication error with image block worker</td></tr><tr><td><code>4251</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Image block worker has notified a processing Error: (…)1</td></tr><tr><td><code>4260</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Communication error with merge content worker</td></tr><tr><td><code>4270</code></td><td>HTML creation error</td><td>400 Bad Request</td><td>Error handling custom addon module</td></tr><tr><td><code>4601</code></td><td>Rendering error</td><td>403 Forbidden</td><td>Error cleaning up button module HTML code</td></tr><tr><td><code>4602</code></td><td>Rendering error</td><td>403 Forbidden</td><td>Error cleaning up text module HTML code</td></tr><tr><td><code>4603</code></td><td>Rendering error</td><td>403 Forbidden</td><td>Error checking form elements</td></tr><tr><td><code>4604</code></td><td>Form validation error</td><td>403 Forbidden</td><td>Error in (…)2</td></tr><tr><td><code>4605</code></td><td>Rendering error</td><td>403 Forbidden</td><td>Custom video format not supported</td></tr><tr><td><code>4920</code></td><td>Rendering error</td><td>403 Forbidden</td><td>Video block is corrupted</td></tr><tr><td><code>4600</code></td><td>Rendering error</td><td>403 Forbidden</td><td>(…)1</td></tr></tbody></table>

1: Additional details are provided, depending on the error that the content worker is reporting.

2: Additional details are provided, depending on the form field that missed validation.

## Post-processing errors

<table><thead><tr><th width="110">Code</th><th width="202">Message</th><th width="162">HTTP Status</th><th>Details</th></tr></thead><tbody><tr><td><code>4301</code></td><td>HTML post-processing error</td><td>400 Bad Request</td><td>Generic post-processing error</td></tr><tr><td><code>4310</code></td><td>HTML post-processing error</td><td>400 Bad Request</td><td>Error while transforming images URI</td></tr><tr><td><code>4320</code></td><td>HTML post-processing error</td><td>400 Bad Request</td><td>Error inserting custom HTML codes</td></tr><tr><td><code>4330</code></td><td>HTML post-processing error</td><td>400 Bad Request</td><td>Error replacing custom Beefree SDK code tags</td></tr><tr><td><code>4340</code></td><td>HTML post-processing error</td><td>400 Bad Request</td><td>Error inserting display conditions</td></tr><tr><td><code>4700</code></td><td>Post-processing error</td><td>403 Forbidden</td><td>Error assembling the final HTML page</td></tr></tbody></table>
