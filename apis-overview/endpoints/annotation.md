---
title: Annotation
excerpt: ''
next:
  pages:
    - limitations
  description: ''
hidden: false
---
## Train your document parsing API
When using the API builder, you train with your own documents your API. You can choose to use Mindee Platform to annotate your documents, or you can use the endpoint Annotation to send the labels found on the candidate boxes.

[block:callout]
{
  "type": "warning",
  "title": "Prediction candidates",
  "body": "You need to make a prediction with the annotation enabled to start annotating your documents.\nSee [Get prediction candidates](doc:prediction#get-candidates-for-annotation)"
}
[/block]

## Send your labels
After making your prediction as explained before, you'll find a 36 characters long **id** in the **document** key of your JSON response:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"api_request\": {...},\n  \"document\": {\n    \"id\": \"696da711-1c86-4a28-a14a-3f5dddd92d7c\",\n    ...\n  },\n}\n",
      "language": "json"
    }
  ]
}
[/block]
As we saw in the  [Get annotation candidates](doc:prediction#get-candidates-for-annotation) section, you can also retrieve candidates from your prediction request's JSON response. Using these candidates, you can then annotate your document, to improve your model performances. 

When annotating a document, you have access to the annotating endpoint, which comes with 3 different HTTP methods depending on what you want to achieve on the document:

[block:code]
{
  "codes": [
    {
      "code": "https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_main_version>/documents/<document_id>/annotations",
      "language": "http",
      "name": null
    }
  ]
}
[/block]
* **POST** - submits the labels for training. 
* **PUT** - update previously submitted training
* **DELETE** - removes all training data for this document

Note that for now, API made using our API builder only supports main_version 1.

When using either the **POST** or **PUT** method, you need to send your annotations in the body of your HTTP request. The required body needs to contain a single **labels** key.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"labels\": []\n}",
      "language": "json",
      "name": "Example annotation body"
    }
  ]
}
[/block]
This **labels** key must be a list containing valid JSON objects whose format depends on the type of feature you are annotating.

**Selector features**

For selector features, a label contains 3 keys:
**page_id** - the id of the page you found your annotation candidate in.
**feature** - the name of the feature you are annotating.
**selected** - an array of selected candidate keys you found in your prediction request.  If the prediction was correct, you must still submit the candidate keys for the correctly identified candidate.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"page_id\": 0,\n  \"feature\": \"first_name\",\n  \"selected\": [\"abcdefg\"]\n}",
      "language": "json",
      "name": "Example selector label"
    }
  ]
}
[/block]

**Classificator features**

For selector features, a label contains only 2 keys:
**feature** - the name of the feature you are annotating.
**class** - the associated class for your document.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"feature\": \"yes_or_no\",\n  \"class\": \"yes\"\n}",
      "language": "json",
      "name": "Example classificator label"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "When annotating a document, you need to send all your fields' labels at once. For example, if your API contains two fields, one selector and one classificator, your body should look like this:",
  "title": "Annotating multiple fields"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"labels\": [\n    {\n      \"page_id\": 0,\n      \"feature\": \"first_name\",\n      \"selected\": [\"abcdefg\"]\n    },\n    {\n      \"feature\": \"yes_or_no\",\n      \"class\": \"yes\"\n    }\n  ]\n}",
      "language": "json",
      "name": "Full JSON body example"
    }
  ]
}
[/block]

If your feature has more than one candidate key (for example the address "123 Main Street" will have three keys representing "123" "Main" and "Street"), all three candidate keys should be added to the selected array.