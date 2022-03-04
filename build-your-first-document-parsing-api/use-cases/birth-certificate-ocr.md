---
title: Birth Certificate OCR
excerpt: ''
hidden: false
---
This article walks you through the building process of an OCR API that extracts data from Birth certificates using our deep learning engine. It will work for any document issued in the United States.  

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Birth Certificate images or pdfs to train your OCR.


##Define your Birth Certificate use case

First, we’re going to define what fields we want to extract from your **Birth Certificate**.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1e3b847-birth.png",
        "birth.png",
        461,
        597,
        "#d5dedd"
      ],
      "caption": "Birth certificate key data extraction"
    }
  ]
}
[/block]
  * **First name**: The first name of the birth certificate holder 
  *  **Last Name**: The last name of the birth certificate holder
  *  **Birth Date**: The date of birth of the birth certificate holder
  *  **City of Birth**: The city of birth of the birth certificate holder
  *  **Certificate Number**: The certificate Number 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/21/birth-certificate.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f7db5d4-Capture_decran_2021-04-08_a_18.12.33.png",
        "Capture d’écran 2021-04-08 à 18.12.33.png",
        1099,
        494,
        "#f0f3f4"
      ],
      "caption": "Set up your birth certificate model"
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
        "https://files.readme.io/a6ad125-Capture_decran_2021-04-08_a_18.24.42.png",
        "Capture d’écran 2021-04-08 à 18.24.42.png",
        1105,
        502,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"first_name\",\n          \"public_name\": \"First name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"last_name\",\n          \"public_name\": \"Last Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"birth_date\",\n          \"public_name\": \"Birth Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"city_of_birth\",\n          \"public_name\": \"City of Birth\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"certificate_number\",\n          \"public_name\": \"Certificate Number\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"first_name\",\n        \"last_name\",\n        \"birth_date\",\n        \"city_of_birth\",\n        \"certificate_number\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **First name**: type String that never contains numeric characters.
  * **Last Name**: type String that never contains numeric characters. 
  * **Birth Date**: type Date with US format. 
  * **City of Birth**: type String that never contains numeric characters. 
  * **Certificate Number**: type Number without specifications. 

Once you’re done setting up your data model, press the Start training your model button at the bottom of the screen.
 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0b41fff-Capture_decran_2021-04-08_a_18.14.21.png",
        "Capture d’écran 2021-04-08 à 18.14.21.png",
        1152,
        610,
        "#fafbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
## Train your Birth Certificate OCR
 

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/08a6cce-Capture_decran_2021-04-08_a_18.15.18.png",
        "Capture d’écran 2021-04-08 à 18.15.18.png",
        1314,
        831,
        "#eaeef0"
      ],
      "caption": "Train your birth certificate OCR"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your Birth Certificate deep learning model in the Training section of our API. 

 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Birth Certificate in your application.

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!