---
title: US Employment Authorization OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from US Employment Authorization using our deep learning engine. 

 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 US Employment Authorization images or pdfs to train your OCR.
 

 

## Define your US Employment Authorization use case
 

First, we’re going to define what fields we want to extract from your **US Employment Authorization**. 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/52ffcb6-capture-decran-2021-01-20-a-173525.png",
        "capture-decran-2021-01-20-a-173525.png",
        794,
        510,
        "#928990"
      ],
      "caption": "US Employment Authorization key data extraction"
    }
  ]
}
[/block]

 

  * **Surname**: The last name of the work permit holder 
  * **Given Name**: The first name of the work permit holder 
  * **Category**: The US Employment Authorization category  
  * **Valid from**: The starting date of the validity of your US employment authorization card 
  * **Card expires**: The expiration date of your US employment authorization card
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.

 

[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/20/work-permit.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c869edf-Capture_decran_2021-04-08_a_12.21.52.png",
        "Capture d’écran 2021-04-08 à 12.21.52.png",
        1161,
        513,
        "#e2e3e6"
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
        "https://files.readme.io/9d12f7e-Capture_decran_2021-04-08_a_12.22.53.png",
        "Capture d’écran 2021-04-08 à 12.22.53.png",
        1161,
        513,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"surname\",\n          \"public_name\": \"Surname\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"given_name\",\n          \"public_name\": \"Given Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"category\",\n          \"public_name\": \"Category\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"valid_from\",\n          \"public_name\": \"Valid from\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"card_expires\",\n          \"public_name\": \"Card expires\",\n          \"semantics\": \"date\"\n        }\n      ],\n      \"features_name\": [\n        \"surname\",\n        \"given_name\",\n        \"category\",\n        \"valid_from\",\n        \"card_expires\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
 
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used: 

  * **Surname**: type String that never contains numeric characters.
  * **Given Name**: type String that never contains numeric characters.  
  * **Category**: type String without specifications. 
  * **Valid from**: type Date in US format. 
  * **Card expires:** type Date in US format.

 

Once you’re done setting up your data model, press the **Start training your model** button.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/07b79f1-Capture_decran_2021-04-08_a_12.24.34.png",
        "Capture d’écran 2021-04-08 à 12.24.34.png",
        1158,
        613,
        "#fafbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
## Train your US Employment Authorization OCR
 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f44cdab-Capture_decran_2021-04-08_a_12.25.05.png",
        "Capture d’écran 2021-04-08 à 12.25.05.png",
        1366,
        834,
        "#c4c5ca"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]

 

You’re all set! 

 

Now is the time to train your US Employment Authorization deep learning model in the Training section of our API. 

 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing US Employment Authorization in your application.

 


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!