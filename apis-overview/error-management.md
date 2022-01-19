---
title: Error management
excerpt: ''
---

## Mindee REST API Status and Error Codes
To indicate successful execution or when error occur, we utilize standard HTTP codes. In the case of errors, the response will contain extra information about the error with an error code.

## JSON Response
Mindee REST APIs return either 200 (OK) or 201 (Created) when an API request successfully runs to completion. Status codes in the 400-500 range indicate failures.

## Successful Execution
Those operations that complete successfully will return 2xx status codes in addition to the API response status information in the response body. 
```
{
  "api_request": 
  {
    "error": {}, 
    "resources": ["document"], 
    "status": "success", 
    "status_code": 201, 
    "url": "https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict"
  }, 
  "document": {...}
}
```

The table below shows the typical response codes supported by Mindee API.

| Operation | Response code  | HTTP status code  | Possible response  |
|:---    | :---  |  :----:  |     ---: |
| `GET` | OK | 200 | Request succeeds  |
|`POST` | Success | 201 | API created |


## Error Handling
If an error occurs when calling Mindee's REST API because of an issue with the client's input (such as incorrect data), the standard error code 4xx is used. If an operation fails because of an issue with the Mindee server, a 5xx error code will be returned. 

In the JSON format you will find a **code** in the **error** response key that gives a description of the error that occurred.

```
{
  "api_request": {
    "status": "failure",
    "status_code": 401,
    "resources": [],
    "url": "https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict",
    "error": {
      "details": "No token provided",
      "message": "Authorization required",
      "code": "Unauthorized",
     },
   }
}
```

Errors happening can be split in two main parts:

### 4xx Errors - Client Errors

| Error code | HTTP status code    | Possible reasons |
|:---    | :---        |    :----:   | 
| BadRequest | 400  |<ul><li>**Wrong file type**: file types allowed: png, jpg, webp, pdf.</li><li>**Missing input file**: see how to manage input data.</li><li>**Too many pages in pdf**: APIs have a maximum limit of pages allowed for pdf files.</li></ul>|
|Unauthorized  | 401  | **Bad token**: you didn’t provide the authentication header or the token is wrong. | 
|Forbidden  | 403  | **Inference is blocked**: your API access has been blocked. | 
|NotFound  | 404  |<ul><li>**Wrong endpoint**: provided endpoint doesn't match any product.</li> <li>**Wrong version**: wrong version in base URL.</li></ul>     | 
|FileTooLarge | 413  | **File is too big**: APIs have a maximum file size allowed.      | 
|TooManyRequests  |429 | <ul><li>**Plan limit reached**: you have reached your maximum number of requests.</li> <li>**Too high frequency**: number of requests over time is limited. See [Technical limitations documentation](https://developers.mindee.com/docs/limitations)</li></ul>.| 

### 5xx Errors - Server Errors
| Error code | HTTP status code    | Possible reasons |
|:---    | :---        |    :----:   | 
|ServerError| 500 | An unknown error occurred during the processing of your request.|
|RequestTimeout| 504| The request takes too much time to be processed.|
