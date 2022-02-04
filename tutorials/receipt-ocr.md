---
title: Receipt OCR
excerpt: Automatically extract data from receipts and bills
---
Mindee’s receipt OCR API uses deep learning to automatically, accurately, and instantaneously parse your receipt details.

In under a second, the API extracts a set of data from your pdfs or photos of receipts, including:

> Total amount
> Receipt date
> Receipt time
> Merchant name
> Taxes details
> Locale & currency
> Expense category


API Prerequisites

>1. You’ll need a free Mindee account. [Sign up](https://platform.mindee.com/signup) and confirm your email to log in.
>2. A receipt.  Look in your bag/wallet for a recent one, or do a [Google Image search](https://www.google.com/search?q=cafe+receipt) for a receipt and download a few to test with.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1ff3082-4.1.jpg",
        "4.1.jpg",
        451,
        607,
        "#918983"
      ]
    }
  ]
}
[/block]
## Set up the API

Log into your Mindee account and access your Expense Receipt API environment by clicking the Expense Receipts card:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/73c998a-3.2.png",
        "3.2.png",
        429,
        308,
        "#d5e2ea"
      ],
      "sizing": "80",
      "border": false,
      "caption": "Mindee Expense receipt OCR API"
    }
  ]
}
[/block]
When clicking this card, you land on the dashboard page - where you can quickly see API usage (you have none right now, but that will change).  On the left navigation, there are links to “Documentation”, “API Keys” and “Live Interface”.  The docs tab has all of the technical details you’ll need to build for the receipts API endpoint, and the Live Interface is a cool interactive demo. 

Rather than try out the demo, we want to build with the API,  so click on **API Keys** to create an API token.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0ee3302-2.7.jpg",
        "2.7.jpg",
        1904,
        976,
        "#f9fafa"
      ]
    }
  ]
}
[/block]
Click on the **Create a new API key** button and name your API key:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/afdfde0-3.4.jpg",
        "3.4.jpg",
        1904,
        976,
        "#c5c9d0"
      ]
    }
  ]
}
[/block]
Now, we are ready to make an API call.  You can find sample codes for the most popular languages in the "Documentation" tab:

[block:code]
{
  "codes": [
    {
      "code": "curl -X POST \\\n  https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict \\\n  -H 'Authorization: Token my-api-key-here' \\\n  -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' \\\n  -F document=@/path/to/your/file.png",
      "language": "curl"
    },
    {
      "code": "import requests\n\nurl = \"https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict\"\n\nwith open(\"/path/to/my/file\", \"rb\") as myfile:\n    files = {\"document\": myfile}\n    headers = {\"Authorization\": \"Token my-api-key-here\"}\n    response = requests.post(url, files=files, headers=headers)\n    print(response.text)",
      "language": "python"
    },
    {
      "code": "// works for NODE > v10\nconst axios = require('axios');\nconst fs = require(\"fs\");\nconst FormData = require('form-data')\n\nasync function makeRequest() {\n    let data = new FormData()\n    data.append('document', fs.createReadStream('./file.jpg'))\n    const config = {\n        method: 'POST',\n        url: 'https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict',\n        headers: { \n          'Authorization':'Token my-api-key-here',\n          ...data.getHeaders()\n           },\n        data\n    }\n\n    try {\n      let response = await axios(config)\n      console.log(response.data);\n    } catch (error) {\n      console.log(error)\n    }\n\n}\n\nmakeRequest()",
      "language": "javascript",
      "name": "Node.js"
    },
    {
      "code": "# tested with Ruby 2.5\nrequire 'uri'\nrequire 'net/http'\nrequire 'net/https'\nrequire 'mime/types'\n\nurl = URI(\"https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict\")\nfile = \"/path/to/your/file.png\"\n\nhttp = Net::HTTP.new(url.host, url.port)\nhttp.use_ssl = true\nrequest = Net::HTTP::Post.new(url)\nrequest[\"Authorization\"] = 'Token my-api-key-here'\nrequest.set_form([['document', File.open(file)]], 'multipart/form-data')\n\nresponse = http.request(request)\nputs response.read_body",
      "language": "ruby"
    },
    {
      "code": "<form onsubmit=\"mindeeSubmit(event)\" >\n  <input type=\"file\" id=\"my-file-input\" name=\"file\" />\n  <input type=\"submit\" />\n</form>\n\n<script type=\"text/javascript\">\nconst mindeeSubmit = (evt) => {\n  evt.preventDefault()\n  let myFileInput = document.getElementById('my-file-input');\n  let myFile = myFileInput.files[0]\n  if (!myFile) { return }\n  let data = new FormData();\n  data.append(\"document\", myFile, myFile.name);\n\n  let xhr = new XMLHttpRequest();\n\n  xhr.addEventListener(\"readystatechange\", function () {\n    if (this.readyState === 4) {\n      console.log(this.responseText);\n    }\n  });\n\n  xhr.open(\"POST\", \"https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict\");\n  xhr.setRequestHeader(\"Authorization\", \"Token my-api-key-here\");\n  xhr.send(data);\n}\n</script>",
      "language": "html",
      "name": "HTML/JavaScript"
    }
  ]
}
[/block]
Simply replace {my-api-key-here} with your new API token and /path/to/your/file/png with the path to your receipt. 


[block:callout]
{
  "type": "info",
  "title": "You can also copy this code right from the documentation tab of the API with your API token inserted for you."
}
[/block]
In this example, we'll use this receipt:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ffc127d-sample_receipt.jpg",
        "sample_receipt.jpg",
        800,
        1066,
        "#bab8b1"
      ],
      "sizing": "original",
      "caption": "Receipt image"
    }
  ]
}
[/block]
Paste the cURL sample into your terminal, hit enter, and about a second later, you will receive a JSON response with the receipt details. Since the response is quite verbose, we will walk through the various fields section by section.

## API Response

Here is the full json response you get when you call the API:


[block:code]
{
  "codes": [
    {
      "code": "{\n  \"api_request\": {\n    \"error\": {},\n    \"resources\": [\n      \"document\"\n    ],\n    \"status\": \"success\",\n    \"status_code\": 201,\n    \"url\": \"http://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict\"\n  },\n  \"document\": {\n    \"annotations\": {\n      \"labels\": []\n    },\n    \"id\": \"cc875b84-e83e-4799-aabe-4b2c18f44b26\",\n    \"inference\": {\n      \"finished_at\": \"2021-05-06T16:37:29+00:00\",\n      \"pages\": [\n        {\n          \"id\": 0,\n          \"prediction\": {\n            \"category\": {\n              \"confidence\": 0.99,\n              \"value\": \"food\"\n            },\n            \"date\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.479,\n                  0.173\n                ],\n                [\n                  0.613,\n                  0.173\n                ],\n                [\n                  0.613,\n                  0.197\n                ],\n                [\n                  0.479,\n                  0.197\n                ]\n              ],\n              \"raw\": \"26-Feb-2016\",\n              \"value\": \"2016-02-26\"\n            },\n            \"locale\": {\n              \"confidence\": 0.82,\n              \"country\": \"GB\",\n              \"currency\": \"GBP\",\n              \"language\": \"en\",\n              \"value\": \"en-GB\"\n            },\n            \"orientation\": {\n              \"confidence\": 0.99,\n              \"degrees\": 0\n            },\n            \"supplier\": {\n              \"confidence\": 0.71,\n              \"polygon\": [\n                [\n                  0.394,\n                  0.068\n                ],\n                [\n                  0.477,\n                  0.068\n                ],\n                [\n                  0.477,\n                  0.087\n                ],\n                [\n                  0.394,\n                  0.087\n                ]\n              ],\n              \"value\": \"CLACHAN\"\n            },\n            \"taxes\": [\n              {\n                \"code\": null,\n                \"confidence\": 0.98,\n                \"polygon\": [\n                  [\n                    0.19,\n                    0.403\n                  ],\n                  [\n                    0.698,\n                    0.403\n                  ],\n                  [\n                    0.698,\n                    0.432\n                  ],\n                  [\n                    0.19,\n                    0.432\n                  ]\n                ],\n                \"rate\": 20.0,\n                \"value\": 1.7\n              }\n            ],\n            \"time\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.62,\n                  0.173\n                ],\n                [\n                  0.681,\n                  0.173\n                ],\n                [\n                  0.681,\n                  0.191\n                ],\n                [\n                  0.62,\n                  0.191\n                ]\n              ],\n              \"raw\": \"15:20\",\n              \"value\": \"15:20\"\n            },\n            \"total_incl\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.549,\n                  0.619\n                ],\n                [\n                  0.715,\n                  0.619\n                ],\n                [\n                  0.715,\n                  0.64\n                ],\n                [\n                  0.549,\n                  0.64\n                ]\n              ],\n              \"value\": 10.2\n            }\n          }\n        }\n      ],\n      \"prediction\": {\n        \"category\": {\n          \"confidence\": 0.99,\n          \"value\": \"food\"\n        },\n        \"date\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.479,\n              0.173\n            ],\n            [\n              0.613,\n              0.173\n            ],\n            [\n              0.613,\n              0.197\n            ],\n            [\n              0.479,\n              0.197\n            ]\n          ],\n          \"raw\": \"26-Feb-2016\",\n          \"value\": \"2016-02-26\"\n        },\n        \"locale\": {\n          \"confidence\": 0.82,\n          \"country\": \"GB\",\n          \"currency\": \"GBP\",\n          \"language\": \"en\",\n          \"value\": \"en-GB\"\n        },\n        \"supplier\": {\n          \"confidence\": 0.71,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.394,\n              0.068\n            ],\n            [\n              0.477,\n              0.068\n            ],\n            [\n              0.477,\n              0.087\n            ],\n            [\n              0.394,\n              0.087\n            ]\n          ],\n          \"value\": \"CLACHAN\"\n        },\n        \"taxes\": [\n          {\n            \"code\": null,\n            \"confidence\": 0.98,\n            \"page_id\": 0,\n            \"polygon\": [\n              [\n                0.19,\n                0.403\n              ],\n              [\n                0.698,\n                0.403\n              ],\n              [\n                0.698,\n                0.432\n              ],\n              [\n                0.19,\n                0.432\n              ]\n            ],\n            \"rate\": 20.0,\n            \"value\": 1.7\n          }\n        ],\n        \"time\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.62,\n              0.173\n            ],\n            [\n              0.681,\n              0.173\n            ],\n            [\n              0.681,\n              0.191\n            ],\n            [\n              0.62,\n              0.191\n            ]\n          ],\n          \"raw\": \"15:20\",\n          \"value\": \"15:20\"\n        },\n        \"total_incl\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.549,\n              0.619\n            ],\n            [\n              0.715,\n              0.619\n            ],\n            [\n              0.715,\n              0.64\n            ],\n            [\n              0.549,\n              0.64\n            ]\n          ],\n          \"value\": 10.2\n        }\n      },\n      \"processing_time\": 1.121,\n      \"product\": {\n        \"features\": [\n          \"locale\",\n          \"category\",\n          \"date\",\n          \"time\",\n          \"total_incl\",\n          \"taxes\",\n          \"supplier\",\n          \"orientation\"\n        ],\n        \"name\": \"Mindee-Demo/expense_receipts\",\n        \"type\": \"standard\",\n        \"version\": \"3.0\"\n      },\n      \"started_at\": \"2021-05-06T16:37:28+00:00\"\n    },\n    \"n_pages\": 1,\n    \"name\": \"sample_receipt.jpg\",\n    \"ocr\": {}\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]

### Extracted fields

Under the ```api_request``` key of the JSON response, you can find some metadata about the request.

What is probably most important to you is the extracted data. Under the ```document``` key, you can find a structure like this:
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"annotations\": {\n      \"labels\": []\n    },\n    \"id\": \"cc875b84-e83e-4799-aabe-4b2c18f44b26\",\n    \"inference\": {\n      \"finished_at\": \"2021-05-06T16:37:29+00:00\",\n      \"pages\": [\n        {\n          \"id\": 0,\n          \"prediction\": {\n            \"category\": {...},\n            \"date\": {...},\n            \"locale\": {...},\n            \"orientation\": {...},\n            \"supplier\": {...}\n        }\n      ],\n      \"prediction\": {\n        \"category\": {... },\n        \"date\": {...},\n        \"locale\": {...},\n        \"supplier\": {...},\n        \"taxes\": [...],\n        \"time\": {...},\n        \"total_incl\": {...},\n      \"processing_time\": 1.121,\n      \"product\": {\n        \"features\": [\n          \"locale\",\n          \"category\",\n          \"date\",\n          \"time\",\n          \"total_incl\",\n          \"taxes\",\n          \"supplier\",\n          \"orientation\"\n        ],\n        \"name\": \"Mindee-Demo/expense_receipts\",\n        \"type\": \"standard\",\n        \"version\": \"3.0\"\n      },\n      \"started_at\": \"2021-05-06T16:37:28+00:00\"\n    },\n    \"n_pages\": 1,\n    \"name\": \"sample_receipt.jpg\",\n    \"ocr\": {}\n  }",
      "language": "json"
    }
  ]
}
[/block]
The extracted data appears in two different elements of the list.

**Document-level prediction**: ```document > inference > prediction``` is the document level prediction. It contains the different fields extracted at the document level, meaning that for multi-pages pdfs, we reconstruct a single receipt object using all the pages.

**Page-level prediction**: ```document > inference > pages[] > prediction``` is an array, containing the extracted data from each page. For images, there is only one element on this array, but for pdfs, you can find the extracted data for each pdf page.

Each predicted field contains a **confidence_score** as well as a polygon when the information is located in the image. 

### Category
 
[block:code]
{
  "codes": [
    {
      "code": "\"category\": {\n\t\"confidence\": 0.99,\n\t\"value\": \"food\"\n}",
      "language": "json"
    }
  ]
}
[/block]
 
The API makes a prediction on the type of purchase.  In this case, it is 99% sure it is food.  The possible categories are [toll, food, parking, transport, accommodation, gasoline, miscellaneous].

 

### Date
 
Identified from the text on the receipt and converted into ISO format. This purchase was made on February 26, 2016, and the model is 99% confident in that choice.  The segmentation bounding box provides 4 (x,y) coordinates indicating where the data was pulled from the receipt [(0,0) is the upper left corner, (1,1) is the bottom right corner].

[block:code]
{
  "codes": [
    {
      "code": "\"date\": {\n    \"confidence\": 0.99,\n    \"page_id\": 0,\n    \"polygon\": [\n      [\n        0.479,\n        0.173\n      ],\n      [\n        0.613,\n        0.173\n      ],\n      [\n        0.613,\n        0.197\n      ],\n      [\n        0.479,\n        0.197\n      ]\n    ],\n    \"raw\": \"26-Feb-2016\",\n    \"value\": \"2016-02-26\"\n  }",
      "language": "json"
    }
  ]
}
[/block]
 

### Locale
 

Using data from the receipt, the API can predict where the purchase was made, the language, and the currency. Check the documentation for the latest support. At the time of writing, support is centered on Europe and North America.

[block:code]
{
  "codes": [
    {
      "code": "\"locale\": {\n  \"confidence\": 0.82,\n  \"country\": \"GB\",\n  \"currency\": \"GBP\",\n  \"language\": \"en\",\n  \"value\": \"en-GB\"\n}",
      "language": "json"
    }
  ]
}
[/block]
In the case of my receipt, it is 82% confident that the purchase is in GB, and in £.

 

### Merchant
[block:code]
{
  "codes": [
    {
      "code": "\"supplier\": {\n  \"confidence\": 0.71,\n    \"page_id\": 0,\n      \"polygon\": [\n        [\n          0.394,\n          0.068\n        ],\n        [\n          0.477,\n          0.068\n        ],\n        [\n          0.477,\n          0.087\n        ],\n        [\n          0.394,\n          0.087\n        ]\n      ],\n\t\"value\": \"CLACHAN\"\n}",
      "language": "json"
    }
  ]
}
[/block]
The API correctly predicted (it was 71% sure) that it was a CLACHAN store. Again, four (x,y) points mark the location of the text naming the Merchant on the image.

 

### Orientation
[block:callout]
{
  "type": "warning",
  "body": "This field is not extracted on the document-level prediction. Getting a document orientation is not possible as it depends on pages only."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "\"orientation\": {\n  \"confidence\": 0.99,\n  \"degrees\": 0\n}",
      "language": "json"
    }
  ]
}
[/block]

Did the document require rotation before parsing?  Measured in 90 degree increments [0.90.180.270]. In this case, it did not require any rotation.

 

### Taxes
 
[block:code]
{
  "codes": [
    {
      "code": "\"taxes\": [\n  {\n    \"code\": null,\n    \"confidence\": 0.98,\n    \"polygon\": [\n      [\n        0.19,\n        0.403\n      ],\n      [\n        0.698,\n        0.403\n      ],\n      [\n        0.698,\n        0.432\n      ],\n      [\n        0.19,\n        0.432\n      ]\n    ],\n    \"rate\": 20.0,\n    \"value\": 1.7\n  }\n]",
      "language": "json"
    }
  ]
}
[/block]
 

The API detects taxes from line items. It's then returned as an array of items. Each of those items contains:
- **value**: the amount of the tax line in the receipt currency
- **rate**: (optional) float between 0 and 1
- **code**: (optional) the tax code (HST, GST... for Canadian; City Tax, State tax for US, etc..)

 
### Time
 

[block:code]
{
  "codes": [
    {
      "code": "\"time\": {\n  \"confidence\": 0.99,\n    \"polygon\": [\n      [\n        0.62,\n        0.173\n      ],\n      [\n        0.681,\n        0.173\n      ],\n      [\n        0.681,\n        0.191\n      ],\n      [\n        0.62,\n        0.191\n      ]\n    ],\n  \"raw\": \"15:20\",\n  \"value\": \"15:20\"\n}",
      "language": "json"
    }
  ]
}
[/block]

Time the receipt was printed in HH:mm format.

 
### Total
 

Perhaps the most important part of the receipt, the total spent including taxes, along with confidence and the box indicating the location on the receipt.

[block:code]
{
  "codes": [
    {
      "code": "\"total_incl\": {\n  \"confidence\": 0.99,\n    \"polygon\": [\n      [\n        0.549,\n        0.619\n      ],\n      [\n        0.715,\n        0.619\n      ],\n      [\n        0.715,\n        0.64\n      ],\n      [\n        0.549,\n        0.64\n      ]\n    ],\n    \"value\": 10.2\n}",
      "language": "json"
    }
  ]
}
[/block]