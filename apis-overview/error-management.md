---
title: Error management
excerpt: ''
---
## JSON Response

If an error occurs when calling Mindee's REST API, you will always get the same JSON response format:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"api_request\": {\n    \"status\": \"failure\",\n    \"status_code\": 401,\n    \"resources\": [],\n    \"url\": \"https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict\",\n    \"error\": {\n      \"details\": \"No token provided\",\n      \"message\": \"Authorization required\",\n      \"code\": \"Unauthorized\",\n     },\n   }\n}",
      "language": "json"
    }
  ]
}
[/block]
You will find a **code** in the **error** response key that defines the error that occurred.

## Possible Errors

Errors happening can be split in two main parts:

**4xx errors - Client Errors**
[block:parameters]
{
  "data": {
    "h-0": "Error code",
    "h-1": "HTTP status code",
    "0-0": "**BadRequest**",
    "1-0": "**Unauthorized**",
    "2-0": "**Forbidden**",
    "3-0": "**NotFound**",
    "0-1": "400",
    "1-1": "401",
    "2-1": "403",
    "3-1": "404",
    "4-0": "**FileTooLarge**",
    "4-1": "413",
    "5-0": "**TooManyRequests**",
    "5-1": "429",
    "h-2": "Possible reasons",
    "0-2": "**Wrong file type**: file types allowed:  png, jpg, webp, pdf\n**Missing input file**: see how to manage input data documentation\n**Too many pages in pdf**: APIs have a maximum limit of pages allowed for pdf files",
    "1-2": "**Bad token**: you didn’t provide the authentication header or the token is wrong.",
    "2-2": "**Inference is blocked**: your API access has been blocked.",
    "3-2": "**Wrong endpoint**: provided endpoint doesn't match any product\n**Wrong version**: wrong version in base URL",
    "4-2": "**File is too big**: APIs have a maximum file size allowed",
    "5-2": "**Plan limit reached**: you have reached your maximum number of requests.\n**Too high frequency**: number of requests over time is limited. See Authentication documentation"
  },
  "cols": 3,
  "rows": 6
}
[/block]
**5xx errors - Server Errors**
[block:parameters]
{
  "data": {
    "h-0": "Error code",
    "h-1": "HTTP status code",
    "h-2": "Possible reasons",
    "0-0": "**ServerError**",
    "0-1": "500",
    "1-0": "**RequestTimeout**",
    "1-1": "504",
    "0-2": "An unknown error occurred during the processing of your request",
    "1-2": "The request takes too much time to be processed"
  },
  "cols": 3,
  "rows": 2
}
[/block]