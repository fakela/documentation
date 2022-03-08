---
title: Bank Checks OCR
excerpt: ''
hidden: false
---
This article describes how to build an OCR API that extracts data from Bank Checks using our deep learning engine. If you want to automate your bank workflow, this article is for you. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Bank Checks images or pdfs to train your OCR.

## Define your Bank Checks use case
 

First, we’re going to define what fields we want to extract from your **Bank Checks**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2059ad6-capture-decran-2021-01-25-a-111852.png",
        "capture-decran-2021-01-25-a-111852.png",
        811,
        366,
        "#e7ebe3"
      ],
      "caption": "Bank checks key data extraction"
    }
  ]
}
[/block]
  * **Issuer**: The bank check's issuer's full name.
  *  **Recipient**: The bank check's recipient's full name.
  *  **Amount**: The bank check amount transferred from the issuer to the recipient.
  *  **Date**: The date the bank check was written. 
  *  **Check Number**: The bank check Number (top hand right corner)
  

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements. 

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract from your Bank Checks, head over to the platform and press the ‘**Create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/25/check_1.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cf18f3d-Capture_decran_2021-04-09_a_14.25.59.png",
        "Capture d’écran 2021-04-09 à 14.25.59.png",
        1125,
        454,
        "#f6f8f8"
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
        "https://files.readme.io/71b9479-Capture_decran_2021-04-09_a_14.26.06.png",
        "Capture d’écran 2021-04-09 à 14.26.06.png",
        1125,
        454,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"issuer\",\n          \"public_name\": \"Issuer\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": true,\n          \"name\": \"recipient\",\n          \"public_name\": \"Recipient\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": true,\n          \"name\": \"amount\",\n          \"public_name\": \"Amount\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date\",\n          \"public_name\": \"Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"check_number\",\n          \"public_name\": \"Check Number\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\"issuer\", \"recipient\", \"amount\", \"date\", \"check_number\"]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Issuer**: type String that never contains numeric characters. 
  * **Recipient**: type String that never contains numeric characters and that is mostly handwritten. 
  * **Amount**: type Number that is mostly handwritten. 
  * **Date**: type Date with US format that is mostly handwritten.
  * **Check Number**: type Number without specifications. 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/10828a4-Capture_decran_2021-04-09_a_14.27.16.png",
        "Capture d’écran 2021-04-09 à 14.27.16.png",
        1137,
        635,
        "#fbfbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Bank Checks OCR
 

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1f1a99b-Capture_decran_2021-04-09_a_14.27.57.png",
        "Capture d’écran 2021-04-09 à 14.27.57.png",
        1324,
        768,
        "#c8ccd0"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your Bank Checks deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Bank Checks in your application.

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!