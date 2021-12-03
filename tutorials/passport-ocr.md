---
title: Passport OCR
excerpt: Automatically extracts data from passports
---
Many on-boarding processes in mobile or web apps require to extract some data from ID documents. Using Mindee's Passport API, you can automatically extract data from passports to offer to your users the best on-boarding experience.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4a16b1d-passport_pic.jpg",
        "passport_pic.jpg",
        401,
        560,
        "#ccd1c9"
      ]
    }
  ]
}
[/block]
The API extracts: 

> **country**: Passport's country of issuance
> **id_number**: Passport's number
> **given_names**: Holder's given names
> **surname**: Holder's surname
> **birth_date**: Holder's date of birth
> **birth_place**: Holder's birth place
> **gender**: Holder's gender
> **issuance_date**: ISO formatted passport's date of issuance
> **expiry_date**: ISO formatted passport's expiry date
> **mrz1**: Passport's machine readable zone line 1
> **mrz2**: Passport's machine readable zone line 2

**API Prerequisites**

1. You’ll need a free Mindee account. Sign up and confirm your email to log in.
2. A picture of a passport.  You can use yours safely as data protection is one of our priority and we won't send your images to any third party application. You can also download the following fake one:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f100914-fake_passport.jpeg",
        "fake_passport.jpeg",
        800,
        1113,
        "#d0d4ca"
      ]
    }
  ]
}
[/block]
## Set up the API

Log into your Mindee account and access your International Passport API environment by clicking the Passport API card:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/68c04be-image_7.png",
        "image (7).png",
        428,
        304,
        "#817c86"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]
When clicking this card, you land on the dashboard page - where you can quickly see API usage (you have none right now, but that will change). 

On the left navigation, there are links to “Documentation”, “API Keys” and “Live Interface”. The docs tab has all of the technical details you’ll need to build for the invoice API.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7a87c4d-image_8.png",
        "image (8).png",
        1920,
        894,
        "#f8f8f8"
      ]
    }
  ]
}
[/block]
Click on the Create a **new API key** button and name your API key:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/33cf503-image_9.png",
        "image (9).png",
        1920,
        894,
        "#c5c9cf"
      ]
    }
  ]
}
[/block]
Now, we are ready to make an API call. You can find sample codes for the most popular languages in the "Documentation" tab:


[block:code]
{
  "codes": [
    {
      "code": "curl -X POST \\\n  https://api.mindee.net/v1/products/mindee/passport/v1/predict \\\n  -H 'Authorization: Token my-api-key-here' \\\n  -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' \\\n  -F document=@/path/to/your/file.png",
      "language": "curl"
    },
    {
      "code": "import requests\n\nurl = \"https://api.mindee.net/v1/products/mindee/passport/v1/predict\"\n\nwith open(\"/path/to/my/file\", \"rb\") as myfile:\n    files = {\"document\": myfile}\n    headers = {\"Authorization\": \"Token my-api-key-here\"}\n    response = requests.post(url, files=files, headers=headers)\n    print(response.text)",
      "language": "python"
    },
    {
      "code": "// works for NODE > v10\nconst axios = require('axios');\nconst fs = require(\"fs\");\nconst FormData = require('form-data')\n\nasync function makeRequest() {\n    let data = new FormData()\n    data.append('document', fs.createReadStream('./file.jpg'))\n    const config = {\n        method: 'POST',\n        url: 'https://api.mindee.net/v1/products/mindee/passport/v1/predict',\n        headers: { \n          'Authorization':'Token my-api-key-here',\n          ...data.getHeaders()\n           },\n        data\n    }\n\n    try {\n      let response = await axios(config)\n      console.log(response.data);\n    } catch (error) {\n      console.log(error)\n    }\n\n}\n\nmakeRequest()",
      "language": "javascript",
      "name": "Node.js"
    },
    {
      "code": "<form onsubmit=\"mindeeSubmit(event)\" >\n  <input type=\"file\" id=\"my-file-input\" name=\"file\" />\n  <input type=\"submit\" />\n</form>\n\n<script type=\"text/javascript\">\nconst mindeeSubmit = (evt) => {\n  evt.preventDefault()\n  let myFileInput = document.getElementById('my-file-input');\n  let myFile = myFileInput.files[0]\n  if (!myFile) { return }\n  let data = new FormData();\n  data.append(\"document\", myFile, myFile.name);\n\n  let xhr = new XMLHttpRequest();\n\n  xhr.addEventListener(\"readystatechange\", function () {\n    if (this.readyState === 4) {\n      console.log(this.responseText);\n    }\n  });\n\n  xhr.open(\"POST\", \"https://api.mindee.net/v1/products/mindee/passport/v1/predict\");\n  xhr.setRequestHeader(\"Authorization\", \"Token my-api-key-here\");\n  xhr.send(data);\n}\n</script>",
      "language": "html",
      "name": "HTML/JavaScript"
    },
    {
      "code": "# tested with Ruby 2.5\nrequire 'uri'\nrequire 'net/http'\nrequire 'net/https'\nrequire 'mime/types'\n\nurl = URI(\"https://api.mindee.net/v1/products/mindee/passport/v1/predict\")\nfile = \"/path/to/your/file.png\"\n\nhttp = Net::HTTP.new(url.host, url.port)\nhttp.use_ssl = true\nrequest = Net::HTTP::Post.new(url)\nrequest[\"Authorization\"] = 'Token my-api-key-here'\nrequest.set_form([['document', File.open(file)]], 'multipart/form-data')\n\nresponse = http.request(request)\nputs response.read_body",
      "language": "ruby"
    }
  ]
}
[/block]
Replace {my-api-key-here} with your new API key, and /path/to/your/file/png with the path to your passport image or pdf.

Paste the cURL sample into your terminal, hit enter, and about a second later, you will receive a JSON response with the passport details. Since the response is quite verbose, we will walk through the fields section by section.

## API Response
Here is the full JSON response you get when you call the API:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"api_request\": {\n    \"error\": {},\n    \"resources\": [\n      \"document\"\n    ],\n    \"status\": \"success\",\n    \"status_code\": 201,\n    \"url\": \"https://api.mindee.net/v1/products/mindee/passport/v1/predict\"\n  },\n  \"document\": {\n    \"annotations\": {\n      \"labels\": []\n    },\n    \"id\": \"c2651887-85f0-4890-88a1-55d1acbe1263\",\n    \"inference\": {\n      \"finished_at\": \"2021-06-01T10:27:52+00:00\",\n      \"pages\": [\n        {\n          \"id\": 0,\n          \"prediction\": {\n            \"birth_date\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.5172,\n                  0.081\n                ],\n                [\n                  0.9155,\n                  0.7614\n                ],\n                [\n                  0.5103,\n                  0.3545\n                ],\n                [\n                  0.0073,\n                  0.6564\n                ]\n              ],\n              \"value\": \"2001-08-25\"\n            },\n            \"birth_place\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.7475,\n                  0.7026\n                ],\n                [\n                  0.0837,\n                  0.6433\n                ],\n                [\n                  0.772,\n                  0.8915\n                ],\n                [\n                  0.2545,\n                  0.1172\n                ]\n              ],\n              \"value\": \"string\"\n            },\n            \"country\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.3263,\n                  0.6623\n                ],\n                [\n                  0.4642,\n                  0.4185\n                ],\n                [\n                  0.3179,\n                  0.8991\n                ],\n                [\n                  0.4653,\n                  0.9794\n                ]\n              ],\n              \"value\": \"string\"\n            },\n            \"expiry_date\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.0719,\n                  0.7544\n                ],\n                [\n                  0.0987,\n                  0.3772\n                ],\n                [\n                  0.8204,\n                  0.3824\n                ],\n                [\n                  0.6437,\n                  0.7535\n                ]\n              ],\n              \"value\": \"2023-04-12\"\n            },\n            \"gender\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.4187,\n                  0.6225\n                ],\n                [\n                  0.7608,\n                  0.3195\n                ],\n                [\n                  0.2222,\n                  0.8163\n                ],\n                [\n                  0.5484,\n                  0.586\n                ]\n              ],\n              \"value\": \"string\"\n            },\n            \"given_names\": [\n              {\n                \"confidence\": 0.99,\n                \"polygon\": [\n                  [\n                    0.892,\n                    0.1198\n                  ],\n                  [\n                    0.8429,\n                    0.3504\n                  ],\n                  [\n                    0.4408,\n                    0.4322\n                  ],\n                  [\n                    0.2926,\n                    0.2348\n                  ]\n                ],\n                \"value\": \"string\"\n              }\n            ],\n            \"id_number\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.8481,\n                  0.0496\n                ],\n                [\n                  0.5729,\n                  0.4031\n                ],\n                [\n                  0.4119,\n                  0.0891\n                ],\n                [\n                  0.0492,\n                  0.3859\n                ]\n              ],\n              \"value\": \"string\"\n            },\n            \"issuance_date\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.708,\n                  0.5445\n                ],\n                [\n                  0.8973,\n                  0.375\n                ],\n                [\n                  0.9134,\n                  0.8104\n                ],\n                [\n                  0.827,\n                  0.3991\n                ]\n              ],\n              \"value\": \"2019-08-03\"\n            },\n            \"mrz1\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.5703,\n                  0.3335\n                ],\n                [\n                  0.4427,\n                  0.1992\n                ],\n                [\n                  0.0419,\n                  0.3303\n                ],\n                [\n                  0.0059,\n                  0.65\n                ]\n              ],\n              \"value\": \"string\"\n            },\n            \"mrz2\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.3573,\n                  0.7532\n                ],\n                [\n                  0.9437,\n                  0.9827\n                ],\n                [\n                  0.5973,\n                  0.1705\n                ],\n                [\n                  0.538,\n                  0.8355\n                ]\n              ],\n              \"value\": \"string\"\n            },\n            \"orientation\": {\n              \"confidence\": 0.99,\n              \"degrees\": 270\n            },\n            \"surname\": {\n              \"confidence\": 0.99,\n              \"polygon\": [\n                [\n                  0.5189,\n                  0.9896\n                ],\n                [\n                  0.3264,\n                  0.3849\n                ],\n                [\n                  0.9078,\n                  0.1242\n                ],\n                [\n                  0.8757,\n                  0.085\n                ]\n              ],\n              \"value\": \"string\"\n            }\n          }\n        }\n      ],\n      \"prediction\": {\n        \"birth_date\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.246,\n              0.2646\n            ],\n            [\n              0.9535,\n              0.65\n            ],\n            [\n              0.1072,\n              0.5242\n            ],\n            [\n              0.201,\n              0.7183\n            ]\n          ],\n          \"value\": \"2001-08-25\"\n        },\n        \"birth_place\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.263,\n              0.6665\n            ],\n            [\n              0.1728,\n              0.9879\n            ],\n            [\n              0.7359,\n              0.16\n            ],\n            [\n              0.6487,\n              0.9166\n            ]\n          ],\n          \"value\": \"string\"\n        },\n        \"country\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.5038,\n              0.3721\n            ],\n            [\n              0.8746,\n              0.9776\n            ],\n            [\n              0.3966,\n              0.9076\n            ],\n            [\n              0.2861,\n              0.1554\n            ]\n          ],\n          \"value\": \"string\"\n        },\n        \"expiry_date\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.3412,\n              0.7005\n            ],\n            [\n              0.4965,\n              0.6171\n            ],\n            [\n              0.1555,\n              0.7132\n            ],\n            [\n              0.7421,\n              0.6633\n            ]\n          ],\n          \"value\": \"2023-04-12\"\n        },\n        \"gender\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.5592,\n              0.5758\n            ],\n            [\n              0.2672,\n              0.0716\n            ],\n            [\n              0.9684,\n              0.6278\n            ],\n            [\n              0.2855,\n              0.1543\n            ]\n          ],\n          \"value\": \"string\"\n        },\n        \"given_names\": [\n          {\n            \"confidence\": 0.99,\n            \"page_id\": 0,\n            \"polygon\": [\n              [\n                0.5765,\n                0.6945\n              ],\n              [\n                0.1599,\n                0.7222\n              ],\n              [\n                0.3402,\n                0.1705\n              ],\n              [\n                0.755,\n                0.371\n              ]\n            ],\n            \"value\": \"string\"\n          }\n        ],\n        \"id_number\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.4431,\n              0.1359\n            ],\n            [\n              0.339,\n              0.6333\n            ],\n            [\n              0.9366,\n              0.5534\n            ],\n            [\n              0.3192,\n              0.9519\n            ]\n          ],\n          \"value\": \"string\"\n        },\n        \"issuance_date\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.6635,\n              0.6699\n            ],\n            [\n              0.0262,\n              0.938\n            ],\n            [\n              0.6887,\n              0.7021\n            ],\n            [\n              0.2226,\n              0.7361\n            ]\n          ],\n          \"value\": \"2019-08-03\"\n        },\n        \"mrz1\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.2724,\n              0.1524\n            ],\n            [\n              0.6602,\n              0.949\n            ],\n            [\n              0.6035,\n              0.8488\n            ],\n            [\n              0.8763,\n              0.5025\n            ]\n          ],\n          \"value\": \"string\"\n        },\n        \"mrz2\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.7596,\n              0.8019\n            ],\n            [\n              0.4068,\n              0.5756\n            ],\n            [\n              0.0751,\n              0.086\n            ],\n            [\n              0.5724,\n              0.5922\n            ]\n          ],\n          \"value\": \"string\"\n        },\n        \"surname\": {\n          \"confidence\": 0.99,\n          \"page_id\": 0,\n          \"polygon\": [\n            [\n              0.0798,\n              0.3528\n            ],\n            [\n              0.4076,\n              0.5601\n            ],\n            [\n              0.9134,\n              0.0295\n            ],\n            [\n              0.9604,\n              0.5395\n            ]\n          ],\n          \"value\": \"string\"\n        }\n      },\n      \"processing_time\": 0.52,\n      \"product\": {\n        \"features\": [\n          \"country\",\n          \"id_number\",\n          \"given_names\",\n          \"surname\",\n          \"birth_date\",\n          \"birth_place\",\n          \"gender\",\n          \"issuance_date\",\n          \"expiry_date\",\n          \"orientation\",\n          \"mrz1\",\n          \"mrz2\"\n        ],\n        \"name\": \"mindee/International Passports\",\n        \"version\": \"1.0\"\n      },\n      \"started_at\": \"2021-06-01T10:27:52+00:00\"\n    },\n    \"n_pages\": 1,\n    \"name\": \"myfile.jpg\",\n    \"ocr\": {}\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
**To access the page-level prediction:** document > inference > pages[] > prediction is an array, containing the extracted data from each page. For images, there is only one element on this array, but for pdfs, you can find the extracted data for each pdf page.

Each predicted field contains a confidence_score as well as a polygon when the information is located in the image.

### country
Passport's country ISO 3166-1 alpha-3 code (3 letters format)
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"country\": {\n    \"confidence\": 1,\n    \"polygon\": [\n      [\n        0.508,\n        0.547\n      ],\n      [\n        0.559,\n        0.547\n      ],\n      [\n        0.559,\n        0.568\n      ],\n      [\n        0.508,\n        0.568\n      ]\n    ],\n    \"value\": \"GBR\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]

### id_number
Passport's number
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"id_number\": {\n    \"confidence\": 1,\n    \"polygon\": [\n      [\n        0.723,\n        0.547\n      ],\n      [\n        0.899,\n        0.547\n      ],\n      [\n        0.899,\n        0.569\n      ],\n      [\n        0.723,\n        0.569\n      ]\n    ],\n    \"value\": \"707797979\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### given_names
List of holder's given names

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"given_names\": [\n    {\n      \"confidence\": 0.99,\n      \"polygon\": [\n        [\n          0.341,\n          0.617\n        ],\n        [\n          0.435,\n          0.617\n        ],\n        [\n          0.435,\n          0.638\n        ],\n        [\n          0.341,\n          0.638\n        ]\n      ],\n      \"value\": \"HENERT\"\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
### surname
Holder's surname

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"surname\": {\n    \"confidence\": 0.99,\n    \"polygon\": [\n      [\n        0.34,\n        0.581\n      ],\n      [\n        0.473,\n        0.581\n      ],\n      [\n        0.473,\n        0.604\n      ],\n      [\n        0.34,\n        0.604\n      ]\n    ],\n    \"value\": \"PUDARSAN\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### birth_date
ISO formatted holder's date of birth

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"birth_date\": {\n    \"confidence\": 1,\n    \"polygon\": [\n      [\n        0.341,\n        0.689\n      ],\n      [\n        0.571,\n        0.689\n      ],\n      [\n        0.571,\n        0.714\n      ],\n      [\n        0.341,\n        0.714\n      ]\n    ],\n    \"value\": \"1995-05-20\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### birth_place
Holder's birth place

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"birth_place\": {\n    \"confidence\": 0.9,\n    \"polygon\": [\n      [\n        0.441,\n        0.724\n      ],\n      [\n        0.556,\n        0.724\n      ],\n      [\n        0.556,\n        0.744\n      ],\n      [\n        0.441,\n        0.744\n      ]\n    ],\n    \"value\": \"CAMTETH\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### gender
Holder's gender

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"gender\": {\n    \"confidence\": 1,\n    \"polygon\": [\n      [\n        0.054,\n        0.919\n      ],\n      [\n        0.928,\n        0.919\n      ],\n      [\n        0.928,\n        0.945\n      ],\n      [\n        0.054,\n        0.945\n      ]\n    ],\n    \"value\": \"M\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### issuance_date
ISO formatted passport's date of issuance

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"issuance_date\": {\n    \"confidence\": 1,\n    \"polygon\": [\n      [\n        0.34,\n        0.763\n      ],\n      [\n        0.565,\n        0.763\n      ],\n      [\n        0.565,\n        0.788\n      ],\n      [\n        0.34,\n        0.788\n      ]\n    ],\n    \"value\": \"2012-04-23\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### expiry_date
ISO formatted passport's expiry date

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"expiry_date\": {\n    \"confidence\": 1,\n    \"polygon\": [\n      [\n        0.34,\n        0.796\n      ],\n      [\n        0.576,\n        0.796\n      ],\n      [\n        0.576,\n        0.82\n      ],\n      [\n        0.34,\n        0.82\n      ]\n    ],\n    \"value\": \"2017-04-22\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### mrz1
Passport's machine readable zone line 1
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"mrz1\": {\n    \"confidence\": 0.99,\n    \"polygon\": [\n      [\n        0.055,\n        0.882\n      ],\n      [\n        0.926,\n        0.882\n      ],\n      [\n        0.926,\n        0.911\n      ],\n      [\n        0.055,\n        0.911\n      ]\n    ],\n    \"value\": \"P<GBRPUDARSAN<<HENERT<<<<<<<<<<<<<<<<<<<<<<<\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]
### mrz2
Passport's machine readable zone line 2

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"mrz2\": {\n    \"confidence\": 1,\n    \"polygon\": [\n      [\n        0.054,\n        0.919\n      ],\n      [\n        0.928,\n        0.919\n      ],\n      [\n        0.928,\n        0.945\n      ],\n      [\n        0.054,\n        0.945\n      ]\n    ],\n    \"value\": \"7077979792GBR9505209M1704224<<<<<<<<<<<<<<00\"\n  }\n}",
      "language": "json"
    }
  ]
}
[/block]