---
title: Train using the annotation endpoint
excerpt: ''
hidden: false
---
When using the API, you can correct and upload the results back into the model to continue training. However, not every prediction is 100% accurate, so you may need to provide corrections. To get additional potential results, add the **annotations=true** URL parameter to the prediction API:

[block:code]
{
  "codes": [
    {
      "code": "curl -X POST 'https://api.mindee.net/v1/products/doug1/us_w9/v1/predict?annotations=true'    -H 'Authorization: Token f7d710e56f215512f9fb4de536d5af8a'     -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' -F document=@harry_potter.pdf   ",
      "language": "shell"
    }
  ]
}
[/block]
This tells the API to provide alternative candidates for each prediction. Each prediction and candidate will now have a **candidate_key** that can be returned for training.
[block:code]
{
  "codes": [
    {
      "code": "\"city\": {\n\t\"confidence\": 0.7,\n\t\"values\": [\n\t\t{\n\t\t\t\"candidate_key\": \"0151bc9f\",\n\t\t\t\"confidence\": 0.62,\n\t\t\t\"content\": \",\",\n\t\t\t\"polygon\": [[0.204,0.347],[0.207,0.347],[0.207,0.362],[0.204,0.362]\n\t\t\t]\n\t\t},\n\t\t{\n\t\t\t\"candidate_key\": \"8d26e17e\",\n\t\t\t\"confidence\": 0.79,\n\t\t\t\"content\": \"CA\",\n\t\t\t\"polygon\": [[0.212,0.347],[0.23,0.347],[0.23,0.362],[0.212,0.362]\n\t\t\t]\n\t\t}\n\t]\n},\n\"name\": {\n\t\"confidence\": 0.98,\n\t\"values\": [\n\t\t{\n\t\t\t\"candidate_key\": \"e02bb231\",\n\t\t\t\"confidence\": 1.0,\n\t\t\t\"content\": \"Harry\",\n\t\t\t\"polygon\": [[0.1,0.12],[0.133,0.12],[0.133,0.133],[0.1,0.133]\n\t\t\t]\n\t\t},",
      "language": "json"
    }
  ]
}
[/block]
In the example above, the name "Harry" is correct, so we can return the *candidate_key* back with the label "name".  However the city value of ", CA" is incorrect, and we must find the correct words from the extracted set. 

The JSON response has  set of assets “OCR ->Candidates” available for each page and each element that is detected. In this case of the city, we are looking for:

[block:code]
{
  "codes": [
    {
      "code": "\"content\": \"Little\",\n\"key\": \"7832ef34\",\n\"polygon\": [\n\t[0.098, 0.347],\n\t[0.13, 0.347],\n\t[0.13, 0.362],\n\t[0.098, 0.362]\n]\n}, {\n\t\"content\": \"Whinging\",\n\t\"key\": \"6495fd94\",\n\t\"polygon\": [\n\t\t[0.136, 0.347],\n\t\t[0.202, 0.347],\n\t\t[0.202, 0.362],\n\t\t[0.136, 0.362]\n\t]\n     ...",
      "language": "json"
    }
  ]
}
[/block]
We can use these keys in the annotation response to Mindee.
[block:api-header]
{
  "title": "Annotation endpoint: POST"
}
[/block]
Now we can build the annotation update to Mindee for future training to improve the model. The documentId in the URL is provided in the JSON response, so the API knows which file the training is being improved for. Each label is named, and the candidate keys are submitted in the "selected" array:

[block:code]
{
  "codes": [
    {
      "code": "curl -X POST 'https://api.mindee.net/v1/products/doug1/us_w9/documents/<document_id>/annotations  -H 'Authorization: Token {apikey}     -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' -D  {\n\t\n\t\"labels\": [\n\t\t{\n\t\t\t\"page_id\":0,\n\t\t\t\"feature\": \"name\",\n\t\t\t\"selected\": [\"e02bb231\", \"89202491\"]\n\t\t},\n\t\t{\n\t\t\t\"page_id\":0,\n\t\t\t\"feature\": \"city\",\n\t\t\t\"selected\": [\"7832ef34\", \"6495fd94\"]\n\t\t},\n\t\t{\n\t\t\t\"page_id\":0,\n\t\t\t\"feature\": \"ssn\",\n\t\t\t\"selected\": [\"7dc15c77\", \"c48edb4a\", \"cd75f470\", \"d31e5e04\", \"dd411217\", \"8bebe180\"]\n\t\t},\n\t\t{\n\t\t\t\"page_id\":0,\n\t\t\t\"feature\": \"state\",\n\t\t\t\"selected\": [\"8d26e17e\"]\n\t\t},\n\t\t{\n\t\t\t\"page_id\":0,\n\t\t\t\"feature\": \"street_address\",\n\t\t\t\"selected\": [\"7ea04e96\", \"01abf396\", \"448cd325\"]\n\t\t},\n\t\t{\n\t\t\t\"page_id\":0,\n\t\t\t\"feature\": \"street_address\",\n\t\t\t\"selected\": [\"48804de1\"]\n\t\t}\n\t\t\n\t]\n\t\n}\n",
      "language": "shell"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Annotation endpoint: PUT"
}
[/block]
Using the same format as the POST above, the PUT replaces/updates any previous annotation made for the document.
[block:api-header]
{
  "title": "Annotation endpoint: DELETE"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "curl -X DELETE 'https://api.mindee.net/v1/products/doug1/us_w9/documents/<document_id>/annotations  ",
      "language": "text"
    }
  ]
}
[/block]
Used to delete the annotations made for a document from the training data set.
[block:callout]
{
  "type": "info",
  "title": "Annotation endpoint",
  "body": "See  [Annotation](doc:annotation) to get some more details on how to use Mindee's REST API's annotation endpoint."
}
[/block]