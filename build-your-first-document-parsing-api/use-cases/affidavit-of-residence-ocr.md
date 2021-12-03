---
title: Affidavit of Residence OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Affidavits of Residence using our deep learning engine. 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Affidavit of Residence images or pdfs to train your OCR.

## Define your Affidavit of Residence use case
 

First, we’re going to define what fields we want to extract from your **Affidavit of Residence**.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f385093-capture-decran-2021-01-20-a-191923.png",
        "capture-decran-2021-01-20-a-191923.png",
        446,
        453,
        "#f8f8f8"
      ],
      "caption": "Affidavit of residence key data extraction"
    }
  ]
}
[/block]
  * **Full name**: The full name of the resident
  *  **Current Address**: The current address of the citizen
  *  **Date**: The letter date
  
 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/20/affidavit-of-residence.jpeg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4e70d08-Capture_decran_2021-04-09_a_13.43.58.png",
        "Capture d’écran 2021-04-09 à 13.43.58.png",
        1131,
        440,
        "#f9fafb"
      ],
      "caption": "Set up your model"
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
        "https://files.readme.io/70abc31-Capture_decran_2021-04-09_a_13.44.08.png",
        "Capture d’écran 2021-04-09 à 13.44.08.png",
        1131,
        440,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"full_name\",\n          \"public_name\": \"Full name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"current_address\",\n          \"public_name\": \"Current Address\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date\",\n          \"public_name\": \"Date\",\n          \"semantics\": \"date\"\n        }\n      ],\n      \"features_name\": [\"full_name\", \"current_address\", \"date\"]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Full name**: type String that never contains numeric characters.
  * **Current Address**: type String without specifications. 
  * **Date**: type String with no specifications. 
  
 

 

Once you’re done setting up your data model, press the **Start training your model**  button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d9c1d26-Capture_decran_2021-04-09_a_13.45.18.png",
        "Capture d’écran 2021-04-09 à 13.45.18.png",
        1141,
        647,
        "#fbfcfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Affidavit of Residence OCR
 

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9435808-Capture_decran_2021-04-09_a_13.46.42.png",
        "Capture d’écran 2021-04-09 à 13.46.42.png",
        1324,
        772,
        "#eeeff1"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your Affidavit of Residence deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Affidavit of Residence in your application.

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!