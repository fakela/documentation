---
title: Medical Certificate OCR
excerpt: ''
hidden: false
---
This article walks you through the building process of an OCR API that extracts data from Medical Certificates using our deep learning engine. 

 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Medical Certificate images or pdfs to train your OCR.
 

 

## Define your Medical Certificate use case
 

First, we’re going to define what fields we want to extract from your **Medical Certificate**. 

 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7cd6ff6-aaaa.png",
        "aaaa.png",
        792,
        561,
        "#dfe4e7"
      ],
      "caption": "Medical certificate key data extraction"
    }
  ]
}
[/block]
 

 

  * **Student Name**: The name of the certificate holder
  * **Student Number**: The student identification number 
  * **Student School**: The student's school for which the certificate was issued
  * **Address**: The medical examination center address 
  * **Medical center name**: The name of the medical center where the examination was performed
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.

 

[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/22/medical-certificate.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/35fcf32-Capture_decran_2021-04-08_a_16.48.53.png",
        "Capture d’écran 2021-04-08 à 16.48.53.png",
        1155,
        504,
        "#f8f9fb"
      ],
      "caption": "Set up your API"
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
        "https://files.readme.io/dcf9a0a-Capture_decran_2021-04-08_a_16.49.01.png",
        "Capture d’écran 2021-04-08 à 16.49.01.png",
        1155,
        504,
        "#fafbfd"
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"student_name\",\n          \"public_name\": \"Student Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"student_number\",\n          \"public_name\": \"Student Number\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"student_school\",\n          \"public_name\": \"Student School\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"address\",\n          \"public_name\": \"Address\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"medical_center\",\n          \"public_name\": \"Medical Center\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"student_name\",\n        \"student_number\",\n        \"student_school\",\n        \"address\",\n        \"medical_center\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
 **Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Student Name**: type String that never contains numeric characters.
  * **Student Number**: type Number without specifications.  
  * **Student School**: type String that never contains alpha characters. 
  * **Address**: type String without specifications. 
  * **Medical Center**: type String that never contains alpha characters. 

 


 

Once you’re done setting up your data model, press the Start training your model button at the bottom of the screen.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8b2a216-Capture_decran_2021-04-08_a_16.51.23.png",
        "Capture d’écran 2021-04-08 à 16.51.23.png",
        1164,
        606,
        "#fafbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
## Train your Medical Certificate OCR API

 
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4bfeb28-Capture_decran_2021-04-08_a_16.52.50.png",
        "Capture d’écran 2021-04-08 à 16.52.50.png",
        1373,
        777,
        "#d7dbe0"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 


 

 

You’re all set! 

 

Now is the time to train your Medical Certificate deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Medical Certificate in your application.


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!