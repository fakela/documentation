---
title: Endpoints
excerpt: ''
next:
  pages:
    - prediction
    - annotation
  description: ''
---
## Base URL
Mindee provides several document extraction APIs, whether off-the-shelf or trainable by the user. To make a prediction or train an API, we use a REST interface where you can make requests over HTTP protocol. Each URL starts with the same pattern: **api.mindee.net/v1/products/_<account_name>_/_<api_name>_/**

where **__<account_name>__** is your user name or organization name
and **__<api_name>__** the name of your document extraction API.

## Authentication
Each request made to the REST API must be authenticated with an API key generated via the platform. The API key is specific to the document parsing API you are working with.

Read [this article](doc:authentication) to understand how Mindee's document extraction APIs authentication works.

## Endpoints
[**Predictions**](doc:prediction) - make a prediction from your document parsing API. All our APIs offer a prediction endpoint.

[**Annotations**](doc:annotation) - send labels to train your document parsing API. The annotation endpoint is only available for APIs built with API Builder.

## JSON Response
When calling any Mindee's REST API endpoint, you will get a standardized JSON object as a response. This JSON object always have an **api_request** key that contains global information on the request you just made.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"api_request\": \n  {\n    \"error\": {}, \n    \"resources\": [\"document\"], \n    \"status\": \"success\", \n    \"status_code\": 201, \n    \"url\": \"https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict\"\n  }, \n  \"document\": {...}\n}",
      "language": "json",
      "name": "Example structure of JSON response"
    }
  ]
}
[/block]
The other JSON keys depend on the resource you want to access: this is where you will find information about what happened during your request. For example, see [Prediction JSON Response](doc:prediction#json-response).