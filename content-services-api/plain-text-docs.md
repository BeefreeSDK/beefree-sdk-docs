Overview[](#overview)
-------------------------

[Insert overview of the feature]

How Getting Plain Text Works[](#how-getting-plain-text-works)
-----------------------------------------------------------------

[Explain the process here, include a diagram if you want. Basically, this section will describe how the integrator uses their email JSON as an input, and the API processes it and outputs a version in plain text.]

Authentication[](#authentication)
-------------------------------------

[How to authenticate. In this section include an example authentication.]

// Some code

Plain text

Authorization[](#authorization)
-----------------------------------

[Talk about advanced permissions here if applicable, if not delete this section]

Plain Text Endpoint[](#plain-text-endpoint)
-----------------------------------------------

`v1/text`

**HTTP Method:** POST

**Description:** The text endpoint accepts a JSON template and returns a plain text document.

### Request Parameters[](#request-parameters)

page (JSON): The JSON template to convert to plain text.
language (JSON): Optional. For multi-language templates, any valid language code sets the output language.

Example Request[](#example-request)
---------------------------------------

The following section shows an example request

    {
        "page": { },
        "language": "it-IT"
    }


Example Response[](#example-response)
-----------------------------------------

The following section shows an example response

    [BeeFree Logo](https://beefree.io/)
    *****************************
    Hi 🙂
    **Would you be interested to participate in a user research project with us?**
    The research will consist of a video call. It usually takes 30 to 45 minutes maximum... more plain text.

Plain text

Response Codes[](#response-codes)
-------------------------------------

Response Format:

-   **200 OK:** The request was successful, and the plain text was returned.

-   **400 Bad Request:** There was an issue with the request parameters.

-   **401 Unauthorized:** The API key is invalid or missing.

-   **500 Internal Server Error:** An unexpected server error occurred.

-----------------------------------------------

SMS Summary Endpoint[](#plain-text-endpoint)
-----------------------------------------------

`v1/text/sms` (for summaries geared toward SMS)

`v1/text/summary` (for general multi-purpose use.)

**HTTP Method:** POST

**Description:** The text endpoint accepts a JSON template and returns a plain text document.

### Request Parameters[](#request-parameters)

template (JSON): The JSON template to convert to summarize.
options (JSON): Optional settings that control the output.

Options parameters

| Name  | Type  | Description  |
| ------------ | ------------ | ------------ |
| toneOfVoice |  string |  e.g. Formal, Humorous, Business |
| length |  string |  Must be concise, standard, or detailed |
| instructions |  string |  Extra instruction to fine tune the AIs response |
| reportUsage |  boolean |  Return the usage data from OpenAI |
| language |  string |  A Beefree SDK language code. Multi-language templates only.  |


Example Request[](#example-request)
---------------------------------------

The following section shows an example request

    {
        "template": { },
        "options": { },
    }


Example Response[](#example-response)
-----------------------------------------

The following section shows an example response

    {
        "summary": "Ciao! Vuoi partecipare a un progetto di ricerca utente con noi? Sarà una videochiamata di massimo 45 minuti. ",
        "usage": {
            "prompt_tokens": 620,
            "completion_tokens": 94,
            "total_tokens": 714
        }
    }


Response Codes[](#response-codes)
-------------------------------------
-   **200 OK:** The request was successful, and the JSON was returned.

-   **400 Bad Request:** There was an issue with the request parameters.

-   **401 Unauthorized:** The API key is invalid or missing.

-   **500 Internal Server Error:** An unexpected server error occurred.

MetaData Endpoint[](#plain-text-endpoint)
-----------------------------------------------

`v1/text/metadata`

**HTTP Method:** POST

**Description:** The text endpoint accepts a JSON template and returns a preheader and subject.

### Request Parameters[](#request-parameters)

template (JSON): The JSON template to convert to convert into metadata.
options (JSON): Optional settings that control the output.

Options parameters

| Name  | Type  | Description  |
| ------------ | ------------ | ------------ |
| toneOfVoice |  string |  e.g. Formal, Humorous, Business |
| instructions |  string |  Extra instruction to fine tune the AIs response |
| reportUsage |  boolean |  Return the usage data from OpenAI |
| language |  string |  A Beefree SDK language code. Multi-language templates only.  |


Example Request[](#example-request)
---------------------------------------

The following section shows an example request

    {
        "template": { },
        "options": { },
    }


Example Response[](#example-response)
-----------------------------------------

The following section shows an example response

           {
    	     "preheader": "Ready to Beefree a part of our user research project? Schedule your video call now!",
              "subject": "Beefree SDK: Let's Pollinate Ideas Together! 🐝🌼",
            "usage": {
                "prompt_tokens": 417,
                "completion_tokens": 48,
                "total_tokens": 465
            }
        }


Response Codes[](#response-codes)
-------------------------------------
-   **200 OK:** The request was successful, and the JSON was returned.

-   **400 Bad Request:** There was an issue with the request parameters.

-   **401 Unauthorized:** The API key is invalid or missing.

-   **500 Internal Server Error:** An unexpected server error occurred.

Error Handling
-------------------------
[Write any error handling considerations here if applicable.]

Additional Considerations
-------------------------
[Write any additional considerations here if applicable.]
