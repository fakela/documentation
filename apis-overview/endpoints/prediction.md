---
title: Prediction
excerpt: ''
next:
  pages:
    - document-inputs
    - limitations
    - annotation
  description: ''
---
## URL
To make a prediction on a specific document extraction API, you must select your API version **__<api_version>__** and use this endpoint:

[block:code]
{
  "codes": [
    {
      "code": "https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict",
      "language": "http",
      "name": "POST"
    }
  ]
}
[/block]
## Account Name
The name of the account that created the API. For the off-the-shelf APIs, this will read 'mindee.'

## Versioning
A document extraction API is defined by a major or a minor version.

**Major versions**
Major version changes are not backward-compatible, with possibly a different output format.
Example of major versions: **v1**, **v2**

**Minor versions**
For each major version, a minor version is backward-compatible with the previous. They may contain performance updates or new extracted features with no changes with preexisting minor versions.
Example of minor versions: **v1.1**, **v1.2**
[block:callout]
{
  "type": "warning",
  "title": "Minor versions are only available through the API builder",
  "body": "* Off-the-shelf APIs do not have minor versions available.\n\n* When using the API builder, each training will create a new minor version of your document extraction API. You can simply use the major version **v1** to select the most up-to-date minor version."
}
[/block]
## Payload

### Send a binary file
Use multipart/form-data encoding to send your document
`document :  my_file`

Example:
[block:code]
{
  "codes": [
    {
      "code": "curl -X POST \\\n  https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict \\\n  -H 'Authorization: Token my-token' \\\n  -H 'content-type: multipart/form-data' \\\n  -F document=@my_file.png",
      "language": "curl"
    },
    {
      "code": "import requests\n\nurl = \"https://api.mindee.net/v1/products/teamMindee/azeaze/v1/predict\"\n\nwith open(\"/path/to/my/file\", \"rb\") as myfile:\n    files = {\"document\": myfile}\n    headers = {\"Authorization\": \"Token my-api-key-here\"}\n    response = requests.post(url, files=files, headers=headers)\n    print(response.text)",
      "language": "python"
    },
    {
      "code": "using System;\nusing System.IO;\nusing System.Net.Http;\nusing System.Net.Http.Headers;\n\nclass Program\n{\n    static void Main(string[] args)\n    {\n        var url = \"https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict\";\n        var filePath = @\"/path/to/my/file\";\n        var token = \"my-api-key-here\";\n\n        var file = File.OpenRead(filePath);\n        var streamContent = new StreamContent(file);\n        var imageContent = new ByteArrayContent(streamContent.ReadAsByteArrayAsync().Result);\n        imageContent.Headers.ContentType = MediaTypeHeaderValue.Parse(\"multipart/form-data\");\n\n        var form = new MultipartFormDataContent();\n        form.Add(imageContent, \"document\", Path.GetFileName(filePath));\n\n        var httpClient = new HttpClient();\n        httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue(\"Token\", token);\n        var response = httpClient.PostAsync(url, form).Result;\n        Console.WriteLine(response.Content.ReadAsStringAsync().Result);\n    }\n}",
      "language": "csharp",
      "name": "C# (.NET)"
    }
  ]
}
[/block]
### Send a base64 encoded file
Prepare a JSON payload with application/json encoding:
```
{
  "document": "/9j......"
}
```
Send your request:
[block:code]
{
  "codes": [
    {
      "code": "curl -X POST \\\n  https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict \\\n  -H 'Authorization: Token my-api-key-here' \\\n  -H 'content-type: application/json' \\\n  -d '{\"document\": \"/9j...\"}'",
      "language": "curl"
    }
  ]
}
[/block]
### Send a URL
Only public HTTPS URL accepted.

Prepare a JSON payload with application/json encoding:
```
{
  "document": "https://my_file.pdf
}
```
Send your request:
[block:code]
{
  "codes": [
    {
      "code": "curl -X POST \\\n  https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict \\\n  -H 'Authorization: Token my-token' \\\n  -H 'content-type: application/json' \\\n  -d '{\"document\": \"https://my_file.pdf\"}'",
      "language": "curl"
    }
  ]
}
[/block]
## JSON response
As stated in [Endpoints JSON Response](doc:endpoints#json-response), Mindee's REST API response format always contains an **api_request** key with general information about your request. When calling the prediction endpoint, the parsed information from your documents can be found in the **document** key.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"api_request\": {... }, \n  \"document\": {\n    \"id\": \"ac668055-e7db-48f2-b81f-e5ba9a6a6b8f\",\n    \"inference\": {\n      \"extras\": {},\n      \"finished_at\": \"\",\n      \"pages\": [\n        {\n          \"id\": 0,\n          \"prediction\": {}\n        },\n        {\n          \"id\": 1,\n          \"prediction\": {}\n        }\n      ],\n      \"prediction\": {},\n      \"processing_time\": 0.44,\n      \"product\": {},\n      \"started_at\": \"\",\n    },\n    \"n_pages\": 2,\n    \"name\": \"myfile.pdf\",\n  }\n}",
      "language": "json",
      "name": null
    }
  ]
}
[/block]
In the *document* values, you'll find some  basic information about your document,  including the number of pages **n_pages**, its filename **name** and an unique 36 characters long identifier **id**.
The most important part of this response is the **inference** key you can find nested inside the **document** key.
This **inference** key contains information about Mindee's processing of your document: **started_at**, **finished_at** and **processing_time**. It also contains a **product** key giving insights about the document parsing API you used, and an **extras** key that can contains additional information.

If you want to retrieve your document prediction, you can choose whether you want a prediction per page or a single prediction for your whole document:
- document level predictions can be found in the **prediction** key: `document > inference > prediction`
- predictions per page can be found in the **pages** key. **pages** is a list of JSON objects containing both an **id** and a **prediction** key: `document > inference > pages[] > prediction`
[block:callout]
{
  "type": "success",
  "body": "To know more about your document parsing API response, especially the **prediction** object's structure, you can access the Documentation part of your API on Mindee's platform.",
  "title": "Prediction structure"
}
[/block]
## Get candidates for annotation

When training via API, you must flag your document as a document for training using the `training=true` parameter. This will make sure we save the document in order to use it later for training.
However, even for non-training requests, you can add the `candidates=true` query parameters to retrieve the candidates of your document.
[block:code]
{
  "codes": [
    {
      "code": "https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict?training=true&candidates=true",
      "language": "http",
      "name": "POST"
    }
  ]
}
[/block]
When doing so, you'll get in the **extras** key of your **document**'s **inference** object a new **candidates** key.
[block:code]
{
  "codes": [
    {
      "code": "...\n  \"extras\": {\n    \"candidates\": {\n      \"extraction\": {\"pages\": [...]},\n      \"classification\": {}\n    }\n  }\n...",
      "language": "json",
      "name": "Example extras key"
    }
  ]
}
[/block]
In this candidates key, you can find both the `extraction` and `classification` candidates.
For **extraction**, there is a **pages** list. For each page of your uploaded document, you will get all of your candidates for each extraction field of your API.
For classification feature, since classification is done as the document level, there is no page dimension.
[block:code]
{
  "codes": [
    {
      "code": "{\n \"pages\": [\n   {\n     \"my_first_field\": [\n       {\n         \"content\": \"xxx\",\n         \"key\": \"abcdefgh\",\n         \"polygon\": [],\n       }\n     ],\n     \"my_second_field\": [...]\n   }\n ] \n}",
      "language": "json",
      "name": "Example extraction candidates"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"my_first_classification_field\": [\"class1\", \"class2\"],\n  \"my_second_classification_field\": [...]\n}",
      "language": "json",
      "name": "Example classification candidates"
    }
  ]
}
[/block]
Each **extraction** candidate is represented by a **content** a **key** and a **polygon**. You will use the **key** when annotating your document, while the **content** is the text our models found in the box and **polygon** is a list of absolute coordinates to find your box on your original document.