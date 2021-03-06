---
title: Endpoints
excerpt: ''
next:
  pages:
    - prediction
    - annotation
  description: ''
hidden: false
---
Mindee's REST API endpoint are specific points of entry used to make requests.

## Endpoints
- [**Predictions**](https://developers.mindee.com/docs/prediction): this refers to the response or results that our APIs deliver on a given document. All our APIs offer a prediction endpoint.

- [**Annotations**](https://developers.mindee.com/docs/annotation): this refers to labels used to train your custom API. The annotation endpoint is only available for APIs built with API Builder.

## Base URL
Mindee provides off-the-shelf and custom APIs. To make a prediction or train an API, we use the REST interface where you can make requests over HTTPS protocol. Each URL starts with the same pattern: `https://api.mindee.net/v1/products/_<account_name>_/_<api_name>_/` where,

- **__<account_name>__**: refers to your username or organization name with which you signed up with.
- **__<api_name>__**: refers to the name of the API your are using.

## Authentication
Each request made to the Mindee REST API must be authenticated with an API key generated through Mindee. The API key is specific to the document parsing API you are working with. See [Authenticate your API calls](https://developers.mindee.com/docs/authentication#authenticate-your-api-calls) to understand how Mindee's document parsing API authentication works.

## JSON Response
When calling any Mindee's REST API endpoint, you will get a standardized JSON object as a response. This JSON object always have an **api_request** key that contains global information on the request you just made.

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
The other JSON keys depend on the resource you want to access, in the [Prediction JSON response](https://developers.mindee.com/docs/annotation) you will find information about what happened during your request.
