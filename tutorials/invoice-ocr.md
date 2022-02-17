---
title: Invoice OCR
excerpt: Automatically extract data from unstructured invoices
---
Mindee’s Invoice OCR API uses deep learning to automatically, accurately, and instantaneously parse invoices in your applications. It takes the API a few seconds to extract data from your PDFs or photos of invoices. The API extracts data such as:

- Due date
- Invoice date
- Invoice number 
- Locale & currency
- Payment details (IBAN, Swift, Bic, Account number...) 
- Supplier identification number (SIRET, EIN, VAT number...)
- Supplier name
- Taxes details
- Total amount including taxes

## Set up the API
1. You'll need to get an invoice. This can be a recently received invoice or you can google for [free invoice samples](https://www.google.com/search?q=invoice) that you can download to test with. Alternatively, you can use the sample invoice provided below.
![sample invoice](https://files.readme.io/a74eaa5-c8e283b-sample_invoice.jpeg)

2. Log into your [Mindee account](https://platform.mindee.com/login) and access your Invoice API dashboard by clicking the **Invoice API** card.
![invoice receipts API card on the right](https://files.readme.io/f111f5b-Screenshot_2021-12-02_at_18.05.20.png "set up api")

3. On the left navigation, click on **API Keys** to create an API key.
![API key on the left nav](https://files.readme.io/e3f871c-image_5.png "set up api")

4. Click on the **Create API key** button and name your API key:
![create a new API key button](https://files.readme.io/13d2cca-image_6.png "set up api")

5. From the left navigation, go to **Documentation > API reference**, you'll find sample code in popular languages and command line. Copy and paste the sample code of your desired choice in your application, code environment, terminal etc.
![invoice api sample code in the api reference section](https://files.readme.io/c1a00b6-invoice-sample-code.png "set up api")

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

- Replace **my-api-key-here** with your new API key, or use the _"select an API key"_ feature and it will be filled automatically.
- Replace **/path/to/your/file/png** with the path to your invoice.

6. Run your code. You will receive a JSON response with the invoice details. 

## API Response
Below is the full sample JSON response you get when you call the API. Since the response is quite verbose, we will walk through the fields section by section.

```json
{
  "api_request": {
    "error": {},
    "resources": [
      "document"
    ],
    "status": "success",
    "status_code": 201,
    "url": "http://api.mindee.net/v1/products/mindee/invoices/v2/predict"
  },
  "document": {
    "annotations": {
      "labels": []
    },
    "id": "cbf37732-9570-4c77-a81f-82cb023aba7b",
    "inference": {
      "finished_at": "2021-05-26T12:18:50+00:00",
      "pages": [
        {
          "id": 0,
          "prediction": {
            "company_registration": [],
            "date": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.84,
                  0.305
                ],
                [
                  0.932,
                  0.305
                ],
                [
                  0.932,
                  0.318
                ],
                [
                  0.84,
                  0.318
                ]
              ],
              "value": "2018-09-25"
            },
            "document_type": {
              "value": "INVOICE"
            },
            "due_date": {
              "confidence": 0.86,
              "polygon": [
                [
                  0.841,
                  0.323
                ],
                [
                  0.941,
                  0.323
                ],
                [
                  0.941,
                  0.338
                ],
                [
                  0.841,
                  0.338
                ]
              ],
              "raw": "Upon receipt",
              "value": "2018-09-25"
            },
            "invoice_number": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.841,
                  0.264
                ],
                [
                  0.864,
                  0.264
                ],
                [
                  0.864,
                  0.279
                ],
                [
                  0.841,
                  0.279
                ]
              ],
              "value": "14"
            },
            "locale": {
              "confidence": 0.94,
              "currency": "CAD",
              "language": "en"
            },
            "orientation": {
              "confidence": 0.99,
              "degrees": 0
            },
            "payment_details": [],
            "supplier": {
              "confidence": 0.11,
              "polygon": [
                [
                  0.165,
                  0.089
                ],
                [
                  0.385,
                  0.089
                ],
                [
                  0.385,
                  0.145
                ],
                [
                  0.165,
                  0.145
                ]
              ],
              "value": "DESIGNS TURNPIKE CO"
            },
            "taxes": [
              {
                "confidence": 0.76,
                "polygon": [
                  [
                    0.784,
                    0.744
                  ],
                  [
                    0.965,
                    0.744
                  ],
                  [
                    0.965,
                    0.758
                  ],
                  [
                    0.784,
                    0.758
                  ]
                ],
                "rate": 8.0,
                "value": 193.2
              }
            ],
            "total_excl": {
              "confidence": 0.0,
              "polygon": [],
              "value": null
            },
            "total_incl": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.886,
                  0.839
                ],
                [
                  0.971,
                  0.839
                ],
                [
                  0.971,
                  0.858
                ],
                [
                  0.886,
                  0.858
                ]
              ],
              "value": 2608.2
            }
          }
        }
      ],
      "prediction": {
        "company_registration": [],
        "date": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.84,
              0.305
            ],
            [
              0.932,
              0.305
            ],
            [
              0.932,
              0.318
            ],
            [
              0.84,
              0.318
            ]
          ],
          "value": "2018-09-25"
        },
        "document_type": {
          "value": "INVOICE"
        },
        "due_date": {
          "confidence": 0.86,
          "page_id": 0,
          "polygon": [
            [
              0.841,
              0.323
            ],
            [
              0.941,
              0.323
            ],
            [
              0.941,
              0.338
            ],
            [
              0.841,
              0.338
            ]
          ],
          "raw": "Upon receipt",
          "value": "2018-09-25"
        },
        "invoice_number": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.841,
              0.264
            ],
            [
              0.864,
              0.264
            ],
            [
              0.864,
              0.279
            ],
            [
              0.841,
              0.279
            ]
          ],
          "value": "14"
        },
        "locale": {
          "confidence": 0.94,
          "currency": "CAD",
          "language": "en"
        },
        "payment_details": [],
        "supplier": {
          "confidence": 0.11,
          "page_id": 0,
          "polygon": [
            [
              0.165,
              0.089
            ],
            [
              0.385,
              0.089
            ],
            [
              0.385,
              0.145
            ],
            [
              0.165,
              0.145
            ]
          ],
          "value": "DESIGNS TURNPIKE CO"
        },
        "taxes": [
          {
            "confidence": 0.76,
            "page_id": 0,
            "polygon": [
              [
                0.784,
                0.744
              ],
              [
                0.965,
                0.744
              ],
              [
                0.965,
                0.758
              ],
              [
                0.784,
                0.758
              ]
            ],
            "rate": 8.0,
            "value": 193.2
          }
        ],
        "total_excl": {
          "confidence": 0.0,
          "page_id": null,
          "polygon": [],
          "value": null
        },
        "total_incl": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.886,
              0.839
            ],
            [
              0.971,
              0.839
            ],
            [
              0.971,
              0.858
            ],
            [
              0.886,
              0.858
            ]
          ],
          "value": 2608.2
        }
      },
      "processing_time": 1.114,
      "product": {
        "features": [
          "locale",
          "invoice_number",
          "date",
          "due_date",
          "total_incl",
          "total_excl",
          "taxes",
          "document_type",
          "payment_details",
          "company_registration",
          "supplier",
          "orientation"
        ],
        "name": "Mindee-Demo/invoices",
        "type": "standard",
        "version": "2.0"
      },
      "started_at": "2021-05-26T12:18:49+00:00"
    },
    "n_pages": 1,
    "name": "sample_invoice.jpg",
    "ocr": {}
  }
}
```

### Extracted fields
Under the `api_request` key of the JSON response, you can find some metadata about the request.

What is probably most important to you is the extracted data. Under the `document` key, you can find a structure like this:

```json
{
  "document": {
    "annotations": {
      "labels": []
    },
    "id": "cbf37732-9570-4c77-a81f-82cb023aba7b",
    "inference": {
      "finished_at": "2021-05-26T12:18:50+00:00",
      "pages": [
        {
          "id": 0,
          "prediction": {
            "company_registration": [],
            "date": {},
            "document_type": {},
            "due_date": {},
            "invoice_number": {},
            "locale": {},
            "orientation": {},
            "payment_details": [],
            "supplier": {},
            "taxes": [],
            "total_excl": {},
            "total_incl": {}
          }
        }
      ],
      "prediction": {
        "company_registration": [],
        "date": {},
        "document_type": {},
        "due_date": {},
        "invoice_number": {},
        "locale": {},
        "payment_details": [],
        "supplier": {},
        "taxes": [],
        "total_excl": {},
        "total_incl": {}
      },
      "processing_time": 1.114,
      "product": {
        "features": [
          "locale",
          "invoice_number",
          "date",
          "due_date",
          "total_incl",
          "total_excl",
          "taxes",
          "document_type",
          "payment_details",
          "company_registration",
          "supplier",
          "orientation"
        ],
        "name": "Mindee-Demo/invoices",
        "type": "standard",
        "version": "2.0"
      },
      "started_at": "2021-05-26T12:18:49+00:00"
    },
    "n_pages": 1
    "name": "sample_invoice.jpg",
    "ocr": {}
  }
}
```

The extracted data appears in two different elements on the list.

- **Document-level prediction**: The JSON response returns `document > inference > prediction`. This contains the different fields extracted at the document level, this implies that for multi-page pdfs, we reconstruct a single invoice object using all the pages.

- **Page-level prediction**: The JSON response returns `document > inference > pages[] > prediction`. Pages which is an array contains the extracted data from each page. For images, there is only one element on this array, but for multi-page pdfs, you can find the extracted data for each pdf page


#### Confidence Score and Polygon
Each predicted field contains a **confidence_score** and a **polygon** which is the box indicating the location of the properties extracted on the document.

```json
{
  "invoice_number": {
    "confidence": 0.99,
    "page_id": 0,
    "polygon": [
      [
        0.841,
        0.264
      ],
      [
        0.864,
        0.264
      ],
      [
        0.864,
        0.279
      ],
      [
        0.841,
        0.279
      ]
    ],
    "value": "14"
  }
}
```

### date
In the JSON response below, we have the value of the invoice date in an ISO format(yyyy-mm-dd).

```json
{
  "date": {
    "confidence": 0.99,
    "page_id": 0,
    "polygon": [
      [
        0.84,
        0.305
      ],
      [
        0.932,
        0.305
      ],
      [
        0.932,
        0.318
      ],
      [
        0.84,
        0.318
      ]
    ],
    "value": "2018-09-25"
  }
}
```

### due_date
In the JSON response below, we have the value of the invoice due_ date in an ISO format(yyyy-mm-dd).

```json
{
  "due_date": {
    "confidence": 0.86,
    "page_id": 0,
    "polygon": [
      [
        0.841,
        0.323
      ],
      [
        0.941,
        0.323
      ],
      [
        0.941,
        0.338
      ],
      [
        0.841,
        0.338
      ]
    ],
    "raw": "Upon receipt",
    "value": "2018-09-25"
  }
}
```

### total_incl
In the JSON response below, we have the value of the total amount including taxes.

```json
{
  "total_incl": {
    "confidence": 0.99,
    "page_id": 0,
    "polygon": [
      [
        0.886,
        0.839
      ],
      [
        0.971,
        0.839
      ],
      [
        0.971,
        0.858
      ],
      [
        0.886,
        0.858
      ]
    ],
    "value": 2608.2
  }
}
```

### total_excl
In the JSON response below, we have the value of the total amount excluding taxes.

```json
{
  "total_excl": {
    "confidence": 0.4,
    "page_id": 0,
    "polygon": [
      [
        0.886,
        0.839
      ],
      [
        0.971,
        0.839
      ],
      [
        0.971,
        0.858
      ],
      [
        0.886,
        0.858
      ]
    ],
    "value": 2608.2
  }
}
```

### taxes
In the JSON response below, we have the list of taxes detected in the invoice. Each tax item includes:
- **value**: the tax item amount in the invoice currency
- **rate**: the tax rate associated to the amount

```json
{
  "taxes": [
    {
      "confidence": 0.76,
      "page_id": 0,
      "polygon": [
        [
          0.784,
          0.744
        ],
        [
          0.965,
          0.744
        ],
        [
          0.965,
          0.758
        ],
        [
          0.784,
          0.758
        ]
      ],
      "rate": 8.0,
      "value": 193.2
    }
  ]
}
```

### payment_details
In the JSON response below, we have the list of all the suppliers' payment details.

> **Info** 📘 
>
> On some invoices, there are many payment details written such as account number, IBAN, routing number, BIC etc. Our Invoice OCR extracts all of them.

In the JSON response below, each item contains different fields and they are set to null or filled with the right value depending on the invoice:

```json
{
  "payment_details": [
    {
      "account_number": "XXXX",
      "confidence": 0.95,
      "iban": "XXXX",
      "page_id": 0,
      "polygon": [
        [ 0.075, 0.539 ],
        [ 0.312, 0.539 ],
        [ 0.312, 0.564 ],
        [ 0.075, 0.564 ]
      ],
      "routing_number": "XXX",
      "swift": "XXX"
    }
  ]
}
```

### company_registration
In the JSON response below, we have the list all of the company identifiers. Each item may contain:
- **value**: The company registration number value.
- **type**: This is generic and can include: 
    - COMPANY REGISTRATION NUMBER or country specific: TIN (United States), GST/HST (Canada), SIREN/SIRET (France), UEN (Singapore), STNR (Germany), KVK (NL), CIF (Spain), NIF (Portugal), CVR (Denmark), CF (Italy), DIC (Czech Republic), RFC (Mexico), GSTIN (India) ...etc
    -  TAX ID 
    - VAT NUMBER etc
  
```json
{
  "company_registration": [
    {
      "confidence": 0.99,
      "page_id": 0,
      "polygon": [
        [ 0.515, 0.962 ],
        [ 0.59, 0.962 ],
        [ 0.59, 0.973 ],
        [ 0.515, 0.973 ]
      ],
      "type": "SIRET",
      "value": "XXX81125600010"
    },
    {
      "confidence": 0.99,
      "page_id": 0,
      "polygon": [
        [ 0.658, 0.963 ],
        [ 0.729, 0.963 ],
        [ 0.729, 0.973 ],
        [ 0.658, 0.973 ]
      ],
      "type": "VAT NUMBER",
      "value": "FR44837811XXX"
    }
  ]
}
```


### supplier
In the JSON response below, we have the value of the supplier name as written in the invoice.

```json
{
  "supplier": {
    "confidence": 0.11,
    "page_id": 0,
    "polygon": [
      [
        0.165,
        0.089
      ],
      [
        0.385,
        0.089
      ],
      [
        0.385,
        0.145
      ],
      [
        0.165,
        0.145
      ]
    ],
    "value": "DESIGNS TURNPIKE CO"
  }
}
```

### locale
In the JSON response, we have the currency and language found on the invoice.

```json
{
  "locale": {
    "confidence": 0.94,
    "currency": "CAD",
    "language": "en"
  }
}
```
