---
title: Cropper
excerpt: ''
---

## What is Cropper?
Cropper enables users to retrieve the coordinates of cropped images from a document through our APIs.

## How it Works
The cropper feature can be used on any API on the prediction route:

```http
https://api.mindee.net/v1/products/<account_name>/<api_name>/<api_version>/predict?cropper=true
```
 
`?cropper=true` which is the additional parameter

## Cropper Output
The cropper results are located at the [page level](https://developers.mindee.com/docs/prediction#predictions-per-page) when retrieving document prediction. The cropper results are returned in the following JSON object `document.inference.pages[].extras.cropper.cropping[].xxxxxx`. Most of the time, taking the first element of the cropper output is sufficient for most use case.

The results show the polygon vertices at the page level, for each possible cropped document within the image:

- **bounding_box**: straight rectangle (always inside canvas).
- **rectangle**: rectangle that may be oriented (can go beyond the canvas, ie. vertices coordinate < 0 and > 1).
- **quadrangle**: free polygon with 4 vertices (always inside canvas).
- **polygon**: free polygon with up to 30 vertices (always inside canvas).

The Vertices format are a list of (x, y) relative coordinates, always in clockwise order. Starting vertex may not be fixed (depends if this is a rectangle or a free polygon).

Example: 
```json
[[0.143, 0.002], 
[0.727, 0.002], 
[0.727, 0.996], 
[0.143, 0.996]].
```

### Example With Receipts V3
Using this [sample receipt document](https://files.readme.io/1ff3082-4.1.jpg)

- [Set up your API Key](https://developers.mindee.com/docs/receipt-ocr#set-up-the-api)
- From the left navigation, go to **Documentation > API reference**, you'll find sample code in popular languages and command lines.
- Copy and paste the sample code of your desired choice in your application, code environment, terminal, etc.

In our request, the cropper additional param `?cropper=true` is added to the receipts API.

[block:code]
{
  "codes": [
    {
      "code": "curl -X POST \n  https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict?cropper=true\n  -H 'Authorization: Token my-token' \n  -F document=@/path/to/your/file.png",
      "language": "curl"
    },
    {
      "code": "import requests\n\nurl = \"https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict?cropper=true\"\n\nwith open(\"/path/to/my/file\", \"rb\") as myfile:\n    files = {\"document\": myfile}\n    headers = {\"Authorization\": \"Token my-api-key-here\"}\n    response = requests.post(url, files=files, headers=headers)\n    print(response.text)",
      "language": "python"
    },
    {
      "code": "// works for NODE > v10\nconst axios = require('axios');\nconst fs = require(\"fs\");\nconst FormData = require('form-data')\n\nasync function makeRequest() {\n    let data = new FormData()\n    data.append('document', fs.createReadStream('./file.jpg'))\n    const config = {\n        method: 'POST',\n        url: 'https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict?cropper=true',\n        headers: { \n          'Authorization':'Token my-api-key-here',\n          ...data.getHeaders()\n           },\n        data\n    }\n\n    try {\n      let response = await axios(config)\n      console.log(response.data);\n    } catch (error) {\n      console.log(error)\n    }\n\n}\n\nmakeRequest()",
      "language": "javascript",
      "name": "Node.js"
    },
    {
      "code": "# tested with Ruby 2.5\nrequire 'uri'\nrequire 'net/http'\nrequire 'net/https'\nrequire 'mime/types'\n\nurl = URI(\"https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict?cropper=true\")\nfile = \"/path/to/your/file.png\"\n\nhttp = Net::HTTP.new(url.host, url.port)\nhttp.use_ssl = true\nrequest = Net::HTTP::Post.new(url)\nrequest[\"Authorization\"] = 'Token my-api-key-here'\nrequest.set_form([['document', File.open(file)]], 'multipart/form-data')\n\nresponse = http.request(request)\nputs response.read_body",
      "language": "ruby"
    },
    {
      "code": "<form onsubmit=\"mindeeSubmit(event)\" >\n  <input type=\"file\" id=\"my-file-input\" name=\"file\" />\n  <input type=\"submit\" />\n</form>\n\n<script type=\"text/javascript\">\nconst mindeeSubmit = (evt) => {\n  evt.preventDefault()\n  let myFileInput = document.getElementById('my-file-input');\n  let myFile = myFileInput.files[0]\n  if (!myFile) { return }\n  let data = new FormData();\n  data.append(\"document\", myFile, myFile.name);\n\n  let xhr = new XMLHttpRequest();\n\n  xhr.addEventListener(\"readystatechange\", function () {\n    if (this.readyState === 4) {\n      console.log(this.responseText);\n    }\n  });\n\n  xhr.open(\"POST\", \"https://api.mindee.net/v1/products/mindee/expense_receipts/v3/predict?cropper=true\");\n  xhr.setRequestHeader(\"Authorization\", \"Token my-api-key-here\");\n  xhr.send(data);\n}\n</script>",
      "language": "javascript",
      "name": "HTML/Javascript"
    }
  ]
}
[/block]
**Output**: Our result shows the different polygon vertices (bounding_box, rectangle, quadrangle, polygon) at the page level.

```json
{
  ...
      "pages": [
        {
          "extras": {
            "cropper": {
              "cropping": [
                {
                  "bounding_box": [
                    [
                      0.121,
                      0
                    ],
                    [
                      0.787,
                      0
                    ],
                    [
                      0.787,
                      0.998
                    ],
                    [
                      0.121,
                      0.998
                    ]
                  ],
                  "polygon": [
                    [
                      0.152,
                      0.416
                    ],
                    [
                      0.16,
                      0.186
                    ],
                    [
                      0.172,
                      0.02
                    ],
                    [
                      0.211,
                      0.006
                    ],
                    [
                      0.357,
                      0.006
                    ],
                    [
                      0.592,
                      0.006
                    ],
                    [
                      0.656,
                      0.023
                    ],
                    [
                      0.775,
                      0.043
                    ],
                    [
                      0.789,
                      0.055
                    ],
                    [
                      0.756,
                      0.549
                    ],
                    [
                      0.756,
                      0.637
                    ],
                    [
                      0.736,
                      0.955
                    ],
                    [
                      0.719,
                      0.994
                    ],
                    [
                      0.607,
                      0.996
                    ],
                    [
                      0.197,
                      0.996
                    ],
                    [
                      0.131,
                      0.994
                    ],
                    [
                      0.123,
                      0.982
                    ],
                    [
                      0.125,
                      0.855
                    ],
                    [
                      0.139,
                      0.668
                    ],
                    [
                      0.139,
                      0.584
                    ]
                  ],
                  "quadrangle": [
                    [
                      0.173,
                      0
                    ],
                    [
                      0.786,
                      0.012
                    ],
                    [
                      0.737,
                      0.994
                    ],
                    [
                      0.122,
                      0.996
                    ]
                  ],
                  "rectangle": [
                    [
                      0.172,
                      -0.019
                    ],
                    [
                      0.785,
                      0.012
                    ],
                    [
                      0.735,
                      1.027
                    ],
                    [
                      0.121,
                      0.996
                    ]
                  ]
                }
              ]
            }
          }
        ...
```