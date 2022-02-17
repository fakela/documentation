---
title: Passport OCR
excerpt: Automatically extracts data from passports
---
Many on-boarding processes in mobile or web apps require to extract some data from ID documents. Using Mindee's Passport API, you can automatically extract data from passports to offer to your users the best on-boarding experience. The API extracts: 

- **birth_date**: Holder's date of birth
- **birth_place**: Holder's birth place
- **country**: Passport's country of issuance
- **expiry_date**: ISO formatted passport's expiry date
- **gender**: Holder's gender
- **given_names**: Holder's given names
- **id_number**: Passport's number
- **issuance_date**: ISO formatted passport's date of issuance
- **mrz1**: Passport's machine readable zone line 1
-  **mrz2**: Passport's machine readable zone line 2
- **surname**: Holder's surname

## Set up the API
1. You'll need to get a picture of a passport. You can use this fake one below.

![sample fake passport](https://files.readme.io/4a16b1d-passport_pic.jpg "set up apo")

2. Log into your [Mindee account](https://platform.mindee.com/login) and access your Passport API dashbboard by clicking the **International Passport** card.
![International Passports API card on the right](https://files.readme.io/f111f5b-Screenshot_2021-12-02_at_18.05.20.png "set up api")

3. On the left navigation, click on **API Keys** to create an API key.
![API key on the left nav](https://files.readme.io/7ada39c-api-passport-api-key.png "set up api")

4. Click on the **Create API key** button and name your API key.
![create a new API key button](https://files.readme.io/33cf503-image_9.png "set up api")

5. From the left navigation, go to **Documentation > API reference**, you'll find sample code in popular languages and command line. Copy and paste the sample code of your desired choice in your application, code environment, terminal etc.
![passport api sample code in the api reference section](https://files.readme.io/3ccc2e4-passport-sample-code.png "set up api")

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

- Replace **my-api-key-here** with your new API key, or use the _"select an API key"_ feature and it will be filled automatically.
- Replace **/path/to/your/file/png** with the path to your passport.

6. Run your code. You will receive a JSON response with the passport details. 

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
    "url": "https://api.mindee.net/v1/products/mindee/passport/v1/predict"
  },
  "document": {
    "annotations": {
      "labels": []
    },
    "id": "c2651887-85f0-4890-88a1-55d1acbe1263",
    "inference": {
      "finished_at": "2021-06-01T10:27:52+00:00",
      "pages": [
        {
          "id": 0,
          "prediction": {
            "birth_date": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.5172,
                  0.081
                ],
                [
                  0.9155,
                  0.7614
                ],
                [
                  0.5103,
                  0.3545
                ],
                [
                  0.0073,
                  0.6564
                ]
              ],
              "value": "2001-08-25"
            },
            "birth_place": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.7475,
                  0.7026
                ],
                [
                  0.0837,
                  0.6433
                ],
                [
                  0.772,
                  0.8915
                ],
                [
                  0.2545,
                  0.1172
                ]
              ],
              "value": "string"
            },
            "country": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.3263,
                  0.6623
                ],
                [
                  0.4642,
                  0.4185
                ],
                [
                  0.3179,
                  0.8991
                ],
                [
                  0.4653,
                  0.9794
                ]
              ],
              "value": "string"
            },
            "expiry_date": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.0719,
                  0.7544
                ],
                [
                  0.0987,
                  0.3772
                ],
                [
                  0.8204,
                  0.3824
                ],
                [
                  0.6437,
                  0.7535
                ]
              ],
              "value": "2023-04-12"
            },
            "gender": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.4187,
                  0.6225
                ],
                [
                  0.7608,
                  0.3195
                ],
                [
                  0.2222,
                  0.8163
                ],
                [
                  0.5484,
                  0.586
                ]
              ],
              "value": "string"
            },
            "given_names": [
              {
                "confidence": 0.99,
                "polygon": [
                  [
                    0.892,
                    0.1198
                  ],
                  [
                    0.8429,
                    0.3504
                  ],
                  [
                    0.4408,
                    0.4322
                  ],
                  [
                    0.2926,
                    0.2348
                  ]
                ],
                "value": "string"
              }
            ],
            "id_number": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.8481,
                  0.0496
                ],
                [
                  0.5729,
                  0.4031
                ],
                [
                  0.4119,
                  0.0891
                ],
                [
                  0.0492,
                  0.3859
                ]
              ],
              "value": "string"
            },
            "issuance_date": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.708,
                  0.5445
                ],
                [
                  0.8973,
                  0.375
                ],
                [
                  0.9134,
                  0.8104
                ],
                [
                  0.827,
                  0.3991
                ]
              ],
              "value": "2019-08-03"
            },
            "mrz1": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.5703,
                  0.3335
                ],
                [
                  0.4427,
                  0.1992
                ],
                [
                  0.0419,
                  0.3303
                ],
                [
                  0.0059,
                  0.65
                ]
              ],
              "value": "string"
            },
            "mrz2": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.3573,
                  0.7532
                ],
                [
                  0.9437,
                  0.9827
                ],
                [
                  0.5973,
                  0.1705
                ],
                [
                  0.538,
                  0.8355
                ]
              ],
              "value": "string"
            },
            "orientation": {
              "confidence": 0.99,
              "degrees": 270
            },
            "surname": {
              "confidence": 0.99,
              "polygon": [
                [
                  0.5189,
                  0.9896
                ],
                [
                  0.3264,
                  0.3849
                ],
                [
                  0.9078,
                  0.1242
                ],
                [
                  0.8757,
                  0.085
                ]
              ],
              "value": "string"
            }
          }
        }
      ],
      "prediction": {
        "birth_date": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.246,
              0.2646
            ],
            [
              0.9535,
              0.65
            ],
            [
              0.1072,
              0.5242
            ],
            [
              0.201,
              0.7183
            ]
          ],
          "value": "2001-08-25"
        },
        "birth_place": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.263,
              0.6665
            ],
            [
              0.1728,
              0.9879
            ],
            [
              0.7359,
              0.16
            ],
            [
              0.6487,
              0.9166
            ]
          ],
          "value": "string"
        },
        "country": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.5038,
              0.3721
            ],
            [
              0.8746,
              0.9776
            ],
            [
              0.3966,
              0.9076
            ],
            [
              0.2861,
              0.1554
            ]
          ],
          "value": "string"
        },
        "expiry_date": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.3412,
              0.7005
            ],
            [
              0.4965,
              0.6171
            ],
            [
              0.1555,
              0.7132
            ],
            [
              0.7421,
              0.6633
            ]
          ],
          "value": "2023-04-12"
        },
        "gender": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.5592,
              0.5758
            ],
            [
              0.2672,
              0.0716
            ],
            [
              0.9684,
              0.6278
            ],
            [
              0.2855,
              0.1543
            ]
          ],
          "value": "string"
        },
        "given_names": [
          {
            "confidence": 0.99,
            "page_id": 0,
            "polygon": [
              [
                0.5765,
                0.6945
              ],
              [
                0.1599,
                0.7222
              ],
              [
                0.3402,
                0.1705
              ],
              [
                0.755,
                0.371
              ]
            ],
            "value": "string"
          }
        ],
        "id_number": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.4431,
              0.1359
            ],
            [
              0.339,
              0.6333
            ],
            [
              0.9366,
              0.5534
            ],
            [
              0.3192,
              0.9519
            ]
          ],
          "value": "string"
        },
        "issuance_date": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.6635,
              0.6699
            ],
            [
              0.0262,
              0.938
            ],
            [
              0.6887,
              0.7021
            ],
            [
              0.2226,
              0.7361
            ]
          ],
          "value": "2019-08-03"
        },
        "mrz1": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.2724,
              0.1524
            ],
            [
              0.6602,
              0.949
            ],
            [
              0.6035,
              0.8488
            ],
            [
              0.8763,
              0.5025
            ]
          ],
          "value": "string"
        },
        "mrz2": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.7596,
              0.8019
            ],
            [
              0.4068,
              0.5756
            ],
            [
              0.0751,
              0.086
            ],
            [
              0.5724,
              0.5922
            ]
          ],
          "value": "string"
        },
        "surname": {
          "confidence": 0.99,
          "page_id": 0,
          "polygon": [
            [
              0.0798,
              0.3528
            ],
            [
              0.4076,
              0.5601
            ],
            [
              0.9134,
              0.0295
            ],
            [
              0.9604,
              0.5395
            ]
          ],
          "value": "string"
        }
      },
      "processing_time": 0.52,
      "product": {
        "features": [
          "country",
          "id_number",
          "given_names",
          "surname",
          "birth_date",
          "birth_place",
          "gender",
          "issuance_date",
          "expiry_date",
          "orientation",
          "mrz1",
          "mrz2"
        ],
        "name": "mindee/International Passports",
        "version": "1.0"
      },
      "started_at": "2021-06-01T10:27:52+00:00"
    },
    "n_pages": 1,
    "name": "myfile.jpg",
    "ocr": {}
  }
}
```

### Extracted fields
Under the `api_request` key of the JSON response, you can find some metadata about the request. 

What is probably most important to you is the extracted data. Under the `document` key, you can find a structure like this:

```json
  "document": {
    "annotations": {
      "labels": []
    },
    "id": "c2651887-85f0-4890-88a1-55d1acbe1263",
    "inference": {
      "finished_at": "2021-06-01T10:27:52+00:00",
      "pages": [
        {
          "id": 0,
          "prediction": {
            "birth_date": {},
            "birth_place": {},
            "country": {},
            "expiry_date": {},
            "gender": {},
            "given_names": [],
            "id_number": {},
            "issuance_date": {},
            "mrz1": {},
            "mrz2": {},
            "orientation": {},
            "surname": {}
          }
        }
      ],
      "prediction": {
        "birth_date": {},
        "birth_place": {},
        "country": {},
        "expiry_date": {},
        "gender": {},
        "given_names": [],
        "id_number": {},
        "issuance_date": {},
        "mrz1": {},
        "mrz2": {},
        "surname": {},
      "processing_time": 0.52,
      "product": {
        "features": [
          "country",
          "id_number",
          "given_names",
          "surname",
          "birth_date",
          "birth_place",
          "gender",
          "issuance_date",
          "expiry_date",
          "orientation",
          "mrz1",
          "mrz2"
        ],
        "name": "mindee/International Passports",
        "version": "1.0"
      },
      "started_at": "2021-06-01T10:27:52+00:00"
    },
    "n_pages": 1,
    "name": "myfile.jpg",
    "ocr": {}
  }
}
```
The extracted data appears in two different elements on the list.

- **Document-level prediction**: The JSON response returns `document > inference > prediction`. This contains the different fields extracted at the document level, this implies that for multi-page pdfs, we reconstruct a single invoice object using all the pages.

- **Page-level prediction**: The JSON response returns `document > inference > pages[] > prediction`. Pages which is an array contains the extracted data from each page. For images, there is only one element on this array, but for multi-page pdfs, you can find the extracted data for each pdf page.


#### Confidence Score and Polygon
Each predicted field contains a **confidence_score** and a **polygon** which is the box indicating the location of the properties extracted on the document.

```json
 {
  "birth_date": {
    "confidence": 0.99,
    "polygon": [
      [
        0.5172,
        0.081
      ],
      [
        0.9155,
        0.7614
      ],
      [
        0.5103,
        0.3545
      ],
      [
        0.0073,
        0.6564
      ]
    ],
    "value": "2001-08-25"
  }
} 
```

### country
In the JSON response below, we have the value of the passport's country in ISO 3166-1 alpha-3 code format (three-letter country codes).

```json
{
  "country": {
    "confidence": 1,
    "polygon": [
      [
        0.508,
        0.547
      ],
      [
        0.559,
        0.547
      ],
      [
        0.559,
        0.568
      ],
      [
        0.508,
        0.568
      ]
    ],
    "value": "GBR"
  }
}
```

### id_number
In the JSON respone below, the value ID number is the passport's number.

```json
{
  "id_number": {
    "confidence": 1,
    "polygon": [
      [
        0.723,
        0.547
      ],
      [
        0.899,
        0.547
      ],
      [
        0.899,
        0.569
      ],
      [
        0.723,
        0.569
      ]
    ],
    "value": "707797979"
  }
}
```

### given_names
In the JSON response below, we have the value of holder's given names.

```json
{
  "given_names": [
    {
      "confidence": 0.99,
      "polygon": [
        [
          0.341,
          0.617
        ],
        [
          0.435,
          0.617
        ],
        [
          0.435,
          0.638
        ],
        [
          0.341,
          0.638
        ]
      ],
      "value": "HENERT"
    }
  ]
}
```

### surname
In the JSON response below, we have the value of the holder's surname.

```json
{
  "surname": {
    "confidence": 0.99,
    "polygon": [
      [
        0.34,
        0.581
      ],
      [
        0.473,
        0.581
      ],
      [
        0.473,
        0.604
      ],
      [
        0.34,
        0.604
      ]
    ],
    "value": "PUDARSAN"
  }
}
```

### birth_date
In the JSON response below, we have the value of the holder's birth date in ISO format(yyyy-mm-dd).

```json
{
  "birth_date": {
    "confidence": 1,
    "polygon": [
      [
        0.341,
        0.689
      ],
      [
        0.571,
        0.689
      ],
      [
        0.571,
        0.714
      ],
      [
        0.341,
        0.714
      ]
    ],
    "value": "1995-05-20"
  }
}
```

### birth_place
In the JSON response below, we have the value of the holder's birth place.

```json
{
  "birth_place": {
    "confidence": 0.9,
    "polygon": [
      [
        0.441,
        0.724
      ],
      [
        0.556,
        0.724
      ],
      [
        0.556,
        0.744
      ],
      [
        0.441,
        0.744
      ]
    ],
    "value": "CAMTETH"
  }
}
```

### gender
In the JSON response below, we have the value of the holder's gender.

```json
{
  "gender": {
    "confidence": 1,
    "polygon": [
      [
        0.054,
        0.919
      ],
      [
        0.928,
        0.919
      ],
      [
        0.928,
        0.945
      ],
      [
        0.054,
        0.945
      ]
    ],
    "value": "M"
  }
}
```

### issuance_date
In the JSON response below, we have the value of the passport's date of issuance in ISO format(yyyy-mm-dd).

```json
{
  "issuance_date": {
    "confidence": 1,
    "polygon": [
      [
        0.34,
        0.763
      ],
      [
        0.565,
        0.763
      ],
      [
        0.565,
        0.788
      ],
      [
        0.34,
        0.788
      ]
    ],
    "value": "2012-04-23"
  }
}
```

### expiry_date
In the JSON response below, we have the value of the passport's expiry date in ISO format(yyyy-mm-dd).

```json
{
  "expiry_date": {
    "confidence": 1,
    "polygon": [
      [
        0.34,
        0.796
      ],
      [
        0.576,
        0.796
      ],
      [
        0.576,
        0.82
      ],
      [
        0.34,
        0.82
      ]
    ],
    "value": "2017-04-22"
  }
}
```

### mrz1
In the JSON response below, we have the value of the passport's machine readable zone line 1.

```json
{
  "mrz1": {
    "confidence": 0.99,
    "polygon": [
      [
        0.055,
        0.882
      ],
      [
        0.926,
        0.882
      ],
      [
        0.926,
        0.911
      ],
      [
        0.055,
        0.911
      ]
    ],
    "value": "P<GBRPUDARSAN<<HENERT<<<<<<<<<<<<<<<<<<<<<<<"
  }
}
```

### mrz2
In the JSON response below, we have the value of the passport's machine readable zone line 2.

```json
{
  "mrz2": {
    "confidence": 1,
    "polygon": [
      [
        0.054,
        0.919
      ],
      [
        0.928,
        0.919
      ],
      [
        0.928,
        0.945
      ],
      [
        0.054,
        0.945
      ]
    ],
    "value": "7077979792GBR9505209M1704224<<<<<<<<<<<<<<00"
  }
}
```
