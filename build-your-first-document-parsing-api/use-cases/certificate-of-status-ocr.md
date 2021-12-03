---
title: Certificate of Status OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Certificate of Status using our deep learning engine. It will work for any bank company or bank statement template. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Certificate of Status images or pdfs to train your OCR.

## Define your Certificate of Status use case
 

First, we’re going to define what fields we want to extract from your **Certificate of Status**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f0c5847-ii.png",
        "ii.png",
        464,
        591,
        "#d6d5d5"
      ],
      "caption": "Certificate of status key data extraction"
    }
  ]
}
[/block]
  * **Entity name**: The full name of the entity 
  *  **File Number**: The file number of your certificate of status
  *  **Formation date**: The creation date of your entity
  *  **Type**: The type of entity
  *  **Jurisdiction**: The jurisdiction that your entity depends on
  *  **Status**: The status of your entity
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/21/certificate-of-status.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/75c9680-Capture_decran_2021-04-09_a_10.18.29.png",
        "Capture d’écran 2021-04-09 à 10.18.29.png",
        1122,
        455,
        "#f2f3f4"
      ],
      "caption": "Set up your certificate of status API"
    }
  ]
}
[/block]
Once you’re ready, click on the “**next**” button. We are going to specify the data types for each of the fields we want our API to extract.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/85f789c-Capture_decran_2021-04-09_a_10.18.42.png",
        "Capture d’écran 2021-04-09 à 10.18.42.png",
        1122,
        455,
        "#fbfbfd"
      ],
      "caption": "Define your model"
    }
  ]
}
[/block]
To move forward, you have two possibilities:

**Upload a json config**
Copy the following JSON into a file and upload it on the interface

[block:code]
{
  "codes": [
    {
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"entity_name\",\n          \"public_name\": \"Entity name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"file_number\",\n          \"public_name\": \"File Number\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"formation_date\",\n          \"public_name\": \"Formation Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"type\",\n          \"public_name\": \"Type\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"jurisdiction\",\n          \"public_name\": \"Jurisdiction\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"status\",\n          \"public_name\": \"Status\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"entity_name\",\n        \"file_number\",\n        \"formation_date\",\n        \"type\",\n        \"jurisdiction\",\n        \"status\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Entity name**: type String that never contains numeric characters.
  * **File Number**: type Number without specifications. 
  * **Formation Date**: type Date with US format.
  * **Type**: type String that never contains numeric characters. 
  * **Jurisdiction**: type String that never contains numeric characters. 
  * **Status**: type String that never contains numeric characters. 
  
 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ac35313-Capture_decran_2021-04-09_a_10.20.24.png",
        "Capture d’écran 2021-04-09 à 10.20.24.png",
        1132,
        575,
        "#fafbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
## Train your Certificate of Status OCR
 

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bac85ec-Capture_decran_2021-04-09_a_10.21.05.png",
        "Capture d’écran 2021-04-09 à 10.21.05.png",
        1311,
        770,
        "#e5e6e8"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your Certificate of Status deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Certificate of Status in your application.

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!