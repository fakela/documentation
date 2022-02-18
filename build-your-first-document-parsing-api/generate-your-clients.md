---
title: Generate your clients
excerpt: ''
---
​
## Generate your client from Swagger json
 

 

In this tutorial, you'll learn how to generate your client library using an Open API configuration. We're going to generate a python client but you can use the same library to generate your client in many languages.

 

### Code generation
 
#### Python

First you will need to download the latest swagger-codegen-cli version from maven central : 

https://repo1.maven.org/maven2/io/swagger/swagger-codegen-cli/.

 

Make sure to have java installed in your computer by running the following command :

 
```
foo@bar:~$ java -version

openjdk version "11.0.9.1" 2020-11-04
OpenJDK Runtime Environment (build 11.0.9.1+1-Ubuntu-0ubuntu1.18.04)
OpenJDK 64-Bit Server VM (build 11.0.9.1+1-Ubuntu-0ubuntu1.18.04, mixed mode, sharing)
```
 

Download the `open_api.json` file from the documentation page of your Mindee project (in your project click the "Documentation" tab:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2e4a2db-CleanShot_2021-09-21_at_11.02.552x.png",
        "CleanShot 2021-09-21 at 11.02.55@2x.png",
        3010,
        1682,
        "#f8f7f8"
      ]
    }
  ]
}
[/block]
 
Run this command to generate the code by replacing `openapi.json` with the name of the JSON file you just downloaded.

```
foo@bar:~$ java -jar swagger-codegen-cli-version.jar generate -i openapi.json -l python -o your_api_client
```
 
 

You can now install your python sdk client :

 

>Create a virtual env :
```
foo@bar:~$ python3 -m venv python_sdk_client_venv
foo@bar:~$ source python_sdk_client_venv/bin/activate
```

You can ignore this step if you are already using your own python3 virtual env.

 
> Install your python sdk client via setuptools:

```
(python_sdk_client_venv) foo@bar:~$ cd your_api_client/
(python_sdk_client_venv) foo@bar:~$ python setup.py install
```
 

 

**You are all set and ready to use your Python SDK client.**

 
 
#### Python Usage
 

Create your api key from the API Keys page of your Mindee project: 

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0dcd81a-usage.png",
        "usage.png",
        1844,
        816,
        "#f6f6f7"
      ]
    }
  ]
}
[/block]
 

#### Using the predict endpoint
 
```
import swagger_client
from swagger_client.rest import ApiException
# replace XXX by your public api name in camel-case/ 
# for example, if your api is named api_name, replace XXXApi() by ApiNameApi()
api_instance = swagger_client.XXXApi()
authorization = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" # your api key
version = "v1" # choose your version
file = "path/to/your/file"
feedback = "true"

try:
    api_response = api_instance.upload_file(
        authorization, version, file, feedback=feedback
    )
except ApiException as e:
    raise e
```

 
 

* **api_response** is an object of type swagger_client.models.api_predict_response.ApiPredictResponse.

 
```
api_response.input_uuid # if you set feedback to 'true'
api_response.pages
api_response.predictions
```
 

* **api_response.pages.features** is a list containing all the candidates the API found for each field. Each item of the list corresponds to a page:

 
```
{
  'pages': {
    'candidates': [
      {
        'feature_1': [
          {
            'content': 'xxxx',
            'key': 'f0311d47',
            'segmentation': {
              'bounding_box': [
                [
                  0.2891,
                  0.0264
                ],
                [
                  0.4479,
                  0.0215
                ],
                [
                  0.4505,
                  0.0635
                ],
                [
                  0.2917,
                  0.0684
                ]
              ]
            }
          ]
          }
]
          ....
        ],
        'feature_2': ....

        
      }
    }


```

 

* **api_response.predictions** is a dict: containing the model's predictions for each feature. Note that if you're using the v0 version of your API, this object will be set to None as there is no trained model yet.

``` 

{
    'feature_1': [
                    {'content': 'xxx',
                     'key': 'c5d1daf7',
                     'page_id': 0,
                     'relative_vertices': [[0.0898, 0.0693],
                                           [0.2708, 0.0635],
                                           [0.2734, 0.1035],
                                           [0.0924, 0.1094]]
                    }, ....
                 ]
    'feature_2': ....
}

 
```
