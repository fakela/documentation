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

## What is Prediction
Prediction refers to the response or results that our APIs deliver on a given document. All our APIs offer a prediction endpoint.

## Prediction URL
To make a prediction on your API, you must select your API version **__<api_version>__** and use the endpoint `predict`, you'll find this in _Documentation > API Reference_:

```http
https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict
```
- **account_name**: refers to the username or organization name of the account that created the API. For the off-the-shelf APIs, this will read as 'mindee'. 
- **api_name**: refers to the name of your document parsing API. 
- **api_version**: Mindee APIs are defined by both major or minor version.

### Major Versions
Major version changes are not backward-compatible and they have different output format. 
Example of major versions: **v1**, **v2**

### Minor Versions
A minor version is always backward-compatible with the previous ones within the same major version. They may contain performance updates or new extracted features with no changes with preexisting minor versions. Example of minor versions: **v1.1**, **v1.2**.

> 📘 **Info**
> 
> Minor versions are only available for custom APIs built using the API builder while major versions are available for both off-the-shelf and custom APIs. When using the API builder, each training will create a new minor version of your document extraction API. You can simply use the major version v1 to select the most up-to-date minor version.

## Payload
A payload refers to the data that you submit to the Mindee server when you are making an API request. There are three main forms of data that you can send:
- a binary file
- a base64 encoded File
- a public https url

### Send a Binary File
Use a `multipart/form-data` encoding to send your document

Example:

[block:code]
{
  "codes": [
    {
      "code": "curl -X POST \\\n  https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict \\\n  -H 'Authorization: Token my-token' \\\n  -H 'content-type: multipart/form-data' \\\n  -F document=@/path/to/your/file.png",
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

> 📘 **Info**
>
> The `@` in the `curl` command is very important as it tells curl that you aren’t passing a data but a file. 

### Send a Base64 Encoded File
Prepare a JSON payload with application/json encoding:
```json
{
  "document": "/9j......"
}
```
Send your request:

```shell
curl -X POST \
  https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict \
  -H 'Authorization: Token my-api-key-here' \
  -H 'Content-Type: application/json' \
  -d 'document="/9j..."'
```

### Send a URL
Only public HTTPS URL accepted.

Prepare a JSON payload with application/json encoding:
```json
{
  "document": "https://my_file.pdf"
}
```
Send your request:

```shell
curl -X POST \
  https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict \
  -H 'Authorization: Token my-token' \
  -H 'Content-Type: application/json' \
  -d 'document="https://my_file.pdf"'
```

## JSON Response
As stated in [Endpoints JSON response](https://developers.mindee.com/docs/endpoints#json-response), Mindee's REST API response format always contain an **api_request** key with general information about your request. When calling the prediction endpoint, the parsed information from your documents can be found in the **document** key.
```json
{
  "api_request": {... }, 
  "document": {
    "id": "ac668055-e7db-48f2-b81f-e5ba9a6a6b8f",
    "inference": {
      "extras": {},
      "finished_at": "",
      "pages": [
        {
          "id": 0,
          "prediction": {}
        },
        {
          "id": 1,
          "prediction": {}
        }
      ],
      "prediction": {},
      "processing_time": 0.44,
      "product": {},
      "started_at": "",
    },
    "n_pages": 2,
    "name": "myfile.pdf",
  }
}
```
In the document values, you'll find some  basic information about your document which includes
- the number of pages **n_pages**,
- its filename **name** and,
- an unique 36 characters long identifier **id**.

The most important part of this response is the **inference** key you can find nested inside the **document** key. The **inference** key contains information about the processing of your document which includes:
- **started_at**,
- **finished_at** and,
- **processing_time**. 

It also contains a **product** key giving insights about the document parsing API you used, and an **extras** key that contains additional information. 

## Prediction Level
To retrieve your document prediction, you can choose whether you want a prediction per page or a single prediction for your whole document. 

```json
{
 "document": {
   "n_pages": 2,
   "inference": {
     "prediction": {
       ...
     },
     "extras": {
       "candidates": {
         "classification": {
           ...
         }
       }
     },
     "pages": [
       {
         "id": 0,
         "prediction": {
           ...
         },
         "extras": {
           "candidates": {
             "extraction": {
               ...
             }
           }
         }
       },
       {
         "id": 1,
         "prediction": {
           ...
         },
         "extras": {
           "candidates": {
             "extraction": {
               ...
             }
           }
         }
       }
     ]
   }
 }
}
```

- **Document level predictions**: To get a single prediction for each field on your whole document, the JSON response returns `response> document > inference > prediction`. At the document level, we have `inference.extras.candidates`. The `extras.candidates` key contains only classification candidates.

```json
{
 "document": {
   "n_pages": 2,
   "inference": {
     "prediction": {
       ...
     },
     "extras": {
       "candidates": {
         "classification": {
           ...
         }
       }
     },
```

- **Predictions per page**: To get a prediction for each field among all your document pages, the JSON response returns `response > document > inference > pages[] > prediction`. Pages which is a list of JSON objects contains both **id** and a **prediction** key. At the page level, each `inference.pages` object will contain an `extras.candidates` key, containing the extraction candidates. 

```json
"pages": [
       {
         "id": 0,
         "prediction": {
           ...
         },
         "extras": {
           "candidates": {
             "extraction": {
               ...
             }
           }
         }
       }
     ]
```   

> 👍 **Success**
> 
> To know more about your document parsing API response, especially the prediction object's structure, you can access the [Documentation part of your API](https://developers.mindee.com/docs/platform-tour#api---documentation) on Mindee's platform.

## Get Candidates for Annotation
When training your API, you must flag your document as a document for training using the `training=true` parameter. This will make sure we save the document in order to use it later for training. However, even for non-training requests, you can add the `with_candidates=true` query parameters to retrieve the candidates of your document.

```html
https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict?training=true&with_candidates=true
```
While doing so, in the **extras** key of your **document**'s **inference** object you'll get a new **candidates** key. In the document level you'll get a classification candidate and in the page level, you'll get an extraction candidate.


- **Extraction candidate**: In extraction candidate, for each page of your uploaded document, you will get all of your candidates for each extraction field of your API. Below is an example of extraction output (page level) with two extraction fields `my_text_field` and `my_number_field`

```json
{
 "extraction": {
   "my_text_field": [
     {
       "content": "Bob",
       "key": "d3fb58c1",
       "polygon": [[0.518, 0.077], [0.415, 0.075], [0.416, 0.067], [0.518, 0.062]]
     },
     ...
   ],
   "my_number_field": [
     {
       "content": 105.87,
       "key": "c7ba79d2",
       "polygon": [[0.241, 0.063], [0.334, 0.064], [0.334, 0.073], [0.242, 0.072]]
     },
     ...
   ],
   ...
 }
}
```

Each **extraction** candidate is represented by a **content**, a **key** and a **polygon**. You will use the **key** when annotating your document, while the **content** is the text our models found in the box and **polygon** is a list of absolute coordinates to find your box on your original document.

- **Classification candidate**: For classification candidate, since classification is done at the document level, there is no page dimension. Below is an example of classification output (document level) with two classification fields color and size

```json
{
 "color": ["red", "green", "blue"],
 "size": ["short", "medium", "large"]
}
```
