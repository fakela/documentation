---
title: Invoice OCR
excerpt: Automatically extract data from unstructured invoices
---
Mindee’s receipt OCR API uses deep learning to automatically, accurately, and instantaneously parse invoices in your applications.

In a few seconds, the API extracts a set of data from your pdfs or photos of invoices:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1c5f149-1_7wcPoKrXNYBZYTvDcHxhhA.png",
        "invoice_cover.jpeg",
        504,
        660,
        "#fafafa"
      ]
    }
  ]
}
[/block]
> Total amount including taxes
> Total amount excluding taxes
> Invoice number
> Invoice date
> Due date
> Supplier name
> Supplier identification number (SIRET, EIN, VAT number...)
> Taxes details
> Locale & currency
> Payment details (IBAN, Swift, Bic, Account number...)



API Prerequisites

>1. You’ll need a free Mindee account. [Sign up](https://platform.mindee.net/signup) and confirm your email to log in.
>2. An invoice.  Use a recently received invoice, or do a [Google Image search](https://www.google.com/search?q=invoice) for an invoice and download a few to test with.



## Set up the API

Log into your Mindee account and access your Expense Receipt API environment by clicking the Invoice API card:



[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0ea3678-invoice_card.jpg",
        "invoice_card.jpg",
        705,
        631,
        "#fbfcfb"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]
When clicking this card, you land on the dashboard page - where you can quickly see API usage (you have none right now, but that will change).  On the left navigation, there are links to “Documentation”, “API Keys” and “Live Interface”.  The docs tab has all of the technical details you’ll need to build for the invoice API. 

Rather than try out the demo, we want to build with the API,  so click on **API Keys** to create an API key.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e3f871c-image_5.png",
        "image (5).png",
        2880,
        1316,
        "#f9f9fa"
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
        "https://files.readme.io/13d2cca-image_6.png",
        "image (6).png",
        2880,
        1420,
        "#c2c6ce"
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
      "code": "curl -X POST \\\n  https://api.mindee.net/v1/products/mindee/invoices/v2/predict \\\n  -H 'Authorization: Token my-api-key-here' \\\n  -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' \\\n  -F document=@/path/to/your/file.png",
      "language": "curl"
    },
    {
      "code": "import requests\n\nurl = \"https://api.mindee.net/v1/products/mindee/invoices/v2/predict\"\n\nwith open(\"/path/to/my/file\", \"rb\") as myfile:\n    files = {\"document\": myfile}\n    headers = {\"Authorization\": \"Token my-api-key-here\"}\n    response = requests.post(url, files=files, headers=headers)\n    print(response.text)",
      "language": "python"
    },
    {
      "code": "// works for NODE > v10\nconst axios = require('axios');\nconst fs = require(\"fs\");\nconst FormData = require('form-data')\n\nasync function makeRequest() {\n    let data = new FormData()\n    data.append('document', fs.createReadStream('./file.jpg'))\n    const config = {\n        method: 'POST',\n        url: 'https://api.mindee.net/v1/products/mindee/invoices/v2/predict',\n        headers: { \n          'Authorization':'Token my-api-key-here',\n          ...data.getHeaders()\n           },\n        data\n    }\n\n    try {\n      let response = await axios(config)\n      console.log(response.data);\n    } catch (error) {\n      console.log(error)\n    }\n\n}\n\nmakeRequest()",
      "language": "javascript",
      "name": "Node.js"
    },
    {
      "code": "# tested with Ruby 2.5\nrequire 'uri'\nrequire 'net/http'\nrequire 'net/https'\nrequire 'mime/types'\n\nurl = URI(\"https://api.mindee.net/v1/products/mindee/invoices/v2/predict\")\nfile = \"/path/to/your/file.png\"\n\nhttp = Net::HTTP.new(url.host, url.port)\nhttp.use_ssl = true\nrequest = Net::HTTP::Post.new(url)\nrequest[\"Authorization\"] = 'Token my-api-key-here'\nrequest.set_form([['document', File.open(file)]], 'multipart/form-data')\n\nresponse = http.request(request)\nputs response.read_body",
      "language": "ruby"
    },
    {
      "code": "<form onsubmit=\"mindeeSubmit(event)\" >\n  <input type=\"file\" id=\"my-file-input\" name=\"file\" />\n  <input type=\"submit\" />\n</form>\n\n<script type=\"text/javascript\">\nconst mindeeSubmit = (evt) => {\n  evt.preventDefault()\n  let myFileInput = document.getElementById('my-file-input');\n  let myFile = myFileInput.files[0]\n  if (!myFile) { return }\n  let data = new FormData();\n  data.append(\"document\", myFile, myFile.name);\n\n  let xhr = new XMLHttpRequest();\n\n  xhr.addEventListener(\"readystatechange\", function () {\n    if (this.readyState === 4) {\n      console.log(this.responseText);\n    }\n  });\n\n  xhr.open(\"POST\", \"https://api.mindee.net/v1/products/mindee/invoices/v2/predict\");\n  xhr.setRequestHeader(\"Authorization\", \"Token my-api-key-here\");\n  xhr.send(data);\n}\n</script>",
      "language": "html",
      "name": "HTML/JavaScript"
    }
  ]
}
[/block]
Replace **{my-api-key-here}** with your new API key, and **/path/to/your/file/png** with the path to your invoice.

For our example, we'll use this fake photo of invoice:
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c8e283b-sample_invoice.jpg",
        "sample_invoice.jpg",
        824,
        1064,
        "#f9f9f9"
      ]
    }
  ]
}
[/block]
Paste the cURL sample into your terminal, hit enter, and about a second later, you will receive a JSON response with the invoice details. Since the response is quite verbose, we will walk through the fields section by section.


## API Response

Here is the full JSON response you get when you call the API:


[block:code]
{
  "codes": [
    {
      "code": "{\n  \"api_request\": {\n    \"error\": {},\n    \"resources\": [\n      \"document\"\n    ],\n    \"status\": \"success\",\n    \"status_code\": 201,\n    \"url\": \"http://api.mindee.net/v1/products/mindee/invoices/v2/predict\"\n  },\n  \"document\": {\n    \"annotations\": {\n      \"labels\": []\n    },\n    \"id\": \"cbf37732-9570-4c77-a81f-82cb023aba7b\",\n    \"inference\": {\n      \"finished_at\": \"2021-05-26T12:18:50+00:00\",\n      \"pages\": [\n        {\n          \"id\": 0,\n          \"prediction\": {\n            \"company_registration\": [],\n            \"date\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.84,\n                  0.305\n                ],\n                [\n                  0.932,\n                  0.305\n                ],\n                [\n                  0.932,\n                  0.318\n                ],\n                [\n                  0.84,\n                  0.318\n                ]\n              ],\n              \"value\": \"2018-09-25\"\n            },\n            \"document_type\": {\n              \"value\": \"INVOICE\"\n            },\n            \"due_date\": {\n              \"confidence\": 0.86,\n              \"polygon\": [\n                [\n                  0.841,\n                  0.323\n                ],\n                [\n                  0.941,\n                  0.323\n                ],\n                [\n                  0.941,\n                  0.338\n                ],\n                [\n                  0.841,\n                  0.338\n                ]\n              ],\n              \"raw\": \"Upon receipt\",\n              \"value\": \"2018-09-25\"\n            },\n            \"invoice_number\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.841,\n                  0.264\n                ],\n                [\n                  0.864,\n                  0.264\n                ],\n                [\n                  0.864,\n                  0.279\n                ],\n                [\n                  0.841,\n                  0.279\n                ]\n              ],\n              \"value\": \"14\"\n            },\n            \"locale\": {\n              \"confidence\": 0.94,\n              \"currency\": \"CAD\",\n              \"language\": \"en\"\n            },\n            \"orientation\": {\n              \"confidence\": 0.99,\n              \"degrees\": 0\n            },\n            \"payment_details\": [],\n            \"supplier\": {\n              \"confidence\": 0.11,\n              \"polygon\": [\n                [\n                  0.165,\n                  0.089\n                ],\n                [\n                  0.385,\n                  0.089\n                ],\n                [\n                  0.385,\n                  0.145\n                ],\n                [\n                  0.165,\n                  0.145\n                ]\n              ],\n              \"value\": \"DESIGNS TURNPIKE CO\"\n            },\n            \"taxes\": [\n              {\n                \"confidence\": 0.76,\n                \"polygon\": [\n                  [\n                    0.784,\n                    0.744\n                  ],\n                  [\n                    0.965,\n                    0.744\n                  ],\n                  [\n                    0.965,\n                    0.758\n                  ],\n                  [\n                    0.784,\n                    0.758\n                  ]\n                ],\n                \"rate\": 8.0,\n                \"value\": 193.2\n              }\n            ],\n            \"total_excl\": {\n              \"confidence\": 0.0,\n              \"polygon\": [],\n              \"value\": null\n            },\n            \"total_incl\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.886,\n                  0.839\n                ],\n                [\n                  0.971,\n                  0.839\n                ],\n                [\n                  0.971,\n                  0.858\n                ],\n                [\n                  0.886,\n                  0.858\n                ]\n              ],\n              \"value\": 2608.2\n            }\n          }\n        }\n      ],\n      \"prediction\": {\n        \"company_registration\": [],\n        \"date\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.84,\n              0.305\n            ],\n            [\n              0.932,\n              0.305\n            ],\n            [\n              0.932,\n              0.318\n            ],\n            [\n              0.84,\n              0.318\n            ]\n          ],\n          \"value\": \"2018-09-25\"\n        },\n        \"document_type\": {\n          \"value\": \"INVOICE\"\n        },\n        \"due_date\": {\n          \"confidence\": 0.86,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.841,\n              0.323\n            ],\n            [\n              0.941,\n              0.323\n            ],\n            [\n              0.941,\n              0.338\n            ],\n            [\n              0.841,\n              0.338\n            ]\n          ],\n          \"raw\": \"Upon receipt\",\n          \"value\": \"2018-09-25\"\n        },\n        \"invoice_number\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.841,\n              0.264\n            ],\n            [\n              0.864,\n              0.264\n            ],\n            [\n              0.864,\n              0.279\n            ],\n            [\n              0.841,\n              0.279\n            ]\n          ],\n          \"value\": \"14\"\n        },\n        \"locale\": {\n          \"confidence\": 0.94,\n          \"currency\": \"CAD\",\n          \"language\": \"en\"\n        },\n        \"payment_details\": [],\n        \"supplier\": {\n          \"confidence\": 0.11,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.165,\n              0.089\n            ],\n            [\n              0.385,\n              0.089\n            ],\n            [\n              0.385,\n              0.145\n            ],\n            [\n              0.165,\n              0.145\n            ]\n          ],\n          \"value\": \"DESIGNS TURNPIKE CO\"\n        },\n        \"taxes\": [\n          {\n            \"confidence\": 0.76,\n            \"page_id\": 0,\n            \"polygon\": [\n              [\n                0.784,\n                0.744\n              ],\n              [\n                0.965,\n                0.744\n              ],\n              [\n                0.965,\n                0.758\n              ],\n              [\n                0.784,\n                0.758\n              ]\n            ],\n            \"rate\": 8.0,\n            \"value\": 193.2\n          }\n        ],\n        \"total_excl\": {\n          \"confidence\": 0.0,\n          \"page_id\": null,\n          \"polygon\": [],\n          \"value\": null\n        },\n        \"total_incl\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.886,\n              0.839\n            ],\n            [\n              0.971,\n              0.839\n            ],\n            [\n              0.971,\n              0.858\n            ],\n            [\n              0.886,\n              0.858\n            ]\n          ],\n          \"value\": 2608.2\n        }\n      },\n      \"processing_time\": 1.114,\n      \"product\": {\n        \"features\": [\n          \"locale\",\n          \"invoice_number\",\n          \"date\",\n          \"due_date\",\n          \"total_incl\",\n          \"total_excl\",\n          \"taxes\",\n          \"document_type\",\n          \"payment_details\",\n          \"company_registration\",\n          \"supplier\",\n          \"orientation\"\n        ],\n        \"name\": \"Mindee-Demo/invoices\",\n        \"type\": \"standard\",\n        \"version\": \"2.0\"\n      },\n      \"started_at\": \"2021-05-26T12:18:49+00:00\"\n    },\n    \"n_pages\": 1,\n    \"name\": \"sample_invoice.jpg\",\n    \"ocr\": {}\n  }\n}",
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
      "code": "{\n  \"document\": {\n    \"annotations\": {\n      \"labels\": []\n    },\n    \"id\": \"cbf37732-9570-4c77-a81f-82cb023aba7b\",\n    \"inference\": {\n      \"finished_at\": \"2021-05-26T12:18:50+00:00\",\n      \"pages\": [\n        {\n          \"id\": 0,\n          \"prediction\": {\n            \"company_registration\": [],\n            \"date\": {},\n            \"document_type\": {},\n            \"due_date\": {},\n            \"invoice_number\": {},\n            \"locale\": {},\n            \"orientation\": {},\n            \"payment_details\": [],\n            \"supplier\": {},\n            \"taxes\": [],\n            \"total_excl\": {},\n            \"total_incl\": {}\n          }\n        }\n      ],\n      \"prediction\": {\n        \"company_registration\": [],\n        \"date\": {},\n        \"document_type\": {},\n        \"due_date\": {},\n        \"invoice_number\": {},\n        \"locale\": {},\n        \"payment_details\": [],\n        \"supplier\": {},\n        \"taxes\": [],\n        \"total_excl\": {},\n        \"total_incl\": {}\n      },\n      \"processing_time\": 1.114,\n      \"product\": {\n        \"features\": [\n          \"locale\",\n          \"invoice_number\",\n          \"date\",\n          \"due_date\",\n          \"total_incl\",\n          \"total_excl\",\n          \"taxes\",\n          \"document_type\",\n          \"payment_details\",\n          \"company_registration\",\n          \"supplier\",\n          \"orientation\"\n        ],\n        \"name\": \"Mindee-Demo/invoices\",\n        \"type\": \"standard\",\n        \"version\": \"2.0\"\n      },\n      \"started_at\": \"2021-05-26T12:18:49+00:00\"\n    },\n    \"n_pages\": 1,\n    \"name\": \"sample_invoice.jpg\",\n    \"ocr\": {}\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]

The extracted data appears in two different elements of the list.

**Document-level prediction**: ```document > inference > prediction``` is the document level prediction. It contains the different fields extracted at the document level, meaning that for multi-pages pdfs, we reconstruct a single invoice object using all the pages.

**Page-level prediction**: ```document > inference > pages[] > prediction``` is an array, containing the extracted data from each page. For images, there is only one element on this array, but for pdfs, you can find the extracted data for each pdf page.

Each predicted field contains a **confidence_score** as well as a polygon when the information is located in the image. 

### invoice_number
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"invoice_number\": {\n    \"confidence\": 0.99,\n    \"page_id\": 0,\n    \"polygon\": [\n      [\n        0.841,\n        0.264\n      ],\n      [\n        0.864,\n        0.264\n      ],\n      [\n        0.864,\n        0.279\n      ],\n      [\n        0.841,\n        0.279\n      ]\n    ],\n    \"value\": \"14\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]

### date
ISO formatted invoicing date.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"date\": {\n    \"confidence\": 0.99,\n    \"page_id\": 0,\n    \"polygon\": [\n      [\n        0.84,\n        0.305\n      ],\n      [\n        0.932,\n        0.305\n      ],\n      [\n        0.932,\n        0.318\n      ],\n      [\n        0.84,\n        0.318\n      ]\n    ],\n    \"value\": \"2018-09-25\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### due_date
ISO formatted invoice due date
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"due_date\": {\n    \"confidence\": 0.86,\n    \"page_id\": 0,\n    \"polygon\": [\n      [\n        0.841,\n        0.323\n      ],\n      [\n        0.941,\n        0.323\n      ],\n      [\n        0.941,\n        0.338\n      ],\n      [\n        0.841,\n        0.338\n      ]\n    ],\n    \"raw\": \"Upon receipt\",\n    \"value\": \"2018-09-25\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### total_incl
Total amount including taxes.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"total_incl\": {\n    \"confidence\": 0.99,\n    \"page_id\": 0,\n    \"polygon\": [\n      [\n        0.886,\n        0.839\n      ],\n      [\n        0.971,\n        0.839\n      ],\n      [\n        0.971,\n        0.858\n      ],\n      [\n        0.886,\n        0.858\n      ]\n    ],\n    \"value\": 2608.2\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### total_excl
Total amount excluding taxes.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"total_excl\": {\n    \"confidence\": 0.4,\n    \"page_id\": 0,\n    \"polygon\": [\n      [\n        0.886,\n        0.839\n      ],\n      [\n        0.971,\n        0.839\n      ],\n      [\n        0.971,\n        0.858\n      ],\n      [\n        0.886,\n        0.858\n      ]\n    ],\n    \"value\": 2608.2\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### taxes
List of taxes detected in the invoice. Each tax item includes:
> **value**: tax item amount in the invoice currency
> **rate**:  tax rate associated to the amount
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"taxes\": [\n    {\n      \"confidence\": 0.76,\n      \"page_id\": 0,\n      \"polygon\": [\n        [\n          0.784,\n          0.744\n        ],\n        [\n          0.965,\n          0.744\n        ],\n        [\n          0.965,\n          0.758\n        ],\n        [\n          0.784,\n          0.758\n        ]\n      ],\n      \"rate\": 8.0,\n      \"value\": 193.2\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
### payment_details
List of supplier's payment details. Supports IBAN, BIC and routing numbers.
[block:callout]
{
  "type": "info",
  "title": "Why a list?",
  "body": "On some invoices, there are many payment details written. Our Invoice OCR extracts all of them."
}
[/block]
Each item contains different fields, set to null or filled with the right value depending on the invoice:
> **account_number**
> **iban**
> **routing_number**
> **bic** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"payment_details\": [\n    {\n      \"account_number\": \"XXXX\",\n      \"confidence\": 0.95,\n      \"iban\": \"XXXX\",\n      \"page_id\": 0,\n      \"polygon\": [\n        [ 0.075, 0.539 ],\n        [ 0.312, 0.539 ],\n        [ 0.312, 0.564 ],\n        [ 0.075, 0.564 ]\n      ],\n      \"routing_number\": \"XXX\",\n      \"swift\": \"XXX\"\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
### company_registration
List of company identifier. Each item contains:
> **value**: the company registration number value
> **type**: Generic: VAT NUMBER, TAX ID, COMPANY REGISTRATION NUMBER or country specific: TIN (United States), GST/HST (Canada), SIREN/SIRET (France), UEN (Singapore), STNR (Germany), KVK (NL), CIF (Spain), NIF (Portugal), CVR (Denmark), CF (Italy), DIC (Czech Republic), RFC (Mexico), GSTIN (India) ...etc
[block:callout]
{
  "type": "info",
  "title": "Why a list?",
  "body": "The API extract all the supplier identifiers in the invoice, along with the corresponding type."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"company_registration\": [\n    {\n      \"confidence\": 0.99,\n      \"page_id\": 0,\n      \"polygon\": [\n        [ 0.515, 0.962 ],\n        [ 0.59, 0.962 ],\n        [ 0.59, 0.973 ],\n        [ 0.515, 0.973 ]\n      ],\n      \"type\": \"SIRET\",\n      \"value\": \"XXX81125600010\"\n    },\n    {\n      \"confidence\": 0.99,\n      \"page_id\": 0,\n      \"polygon\": [\n        [ 0.658, 0.963 ],\n        [ 0.729, 0.963 ],\n        [ 0.729, 0.973 ],\n        [ 0.658, 0.973 ]\n      ],\n      \"type\": \"VAT NUMBER\",\n      \"value\": \"FR44837811XXX\"\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
### supplier
Supplier name as written in the invoice.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"supplier\": {\n    \"confidence\": 0.11,\n    \"page_id\": 0,\n    \"polygon\": [\n      [\n        0.165,\n        0.089\n      ],\n      [\n        0.385,\n        0.089\n      ],\n      [\n        0.385,\n        0.145\n      ],\n      [\n        0.165,\n        0.145\n      ]\n    ],\n    \"value\": \"DESIGNS TURNPIKE CO\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### locale
Currency and language of the invoice.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"locale\": {\n    \"confidence\": 0.94,\n    \"currency\": \"CAD\",\n    \"language\": \"en\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]