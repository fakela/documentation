---
title: Rent Receipt OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Rent Receipt using our deep learning engine.

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Rent Receipt images or pdfs to train your OCR.

## Define your Rent Receipt use case
 

First, we’re going to define what fields we want to extract from your **Rent Receipt**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4574829-ab.png",
        "ab.png",
        793,
        564,
        "#f4f4f3"
      ],
      "caption": "Rent receipt key data extraction"
    }
  ]
}
[/block]
  * **Name**: The landlord's full name 
  *  **Date**: The date of the receipt
  *  **Rent Amount**: The collected rent amount 
  *  **Rent collection date**: The rent collection date 
  *  **Rented good**: The description of rented good
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘Create a new API’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/22/rent-receipt.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6f1ea4e-Capture_decran_2021-04-09_a_13.33.08.png",
        "Capture d’écran 2021-04-09 à 13.33.08.png",
        1120,
        442,
        "#f8f9fb"
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
        "https://files.readme.io/7c9470c-Capture_decran_2021-04-09_a_13.35.02.png",
        "Capture d’écran 2021-04-09 à 13.35.02.png",
        1120,
        442,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"name\",\n          \"public_name\": \"Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date\",\n          \"public_name\": \"Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"rent_amount\",\n          \"public_name\": \"Rent Amount\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"rent_collection_date\",\n          \"public_name\": \"Rent collection date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"rented_good_description\",\n          \"public_name\": \"Rented Good Description\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"name\",\n        \"date\",\n        \"rent_amount\",\n        \"rent_collection_date\",\n        \"rented_good_description\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  *   **Name **: type String that never contains numeric characters.
  * **Date**: type Date with US format.  
  * **Rent Amount**: type Number without specifications.
  * **Rent collection date**: type Date with US format.
  * **Rented Good Description**: type String that never contains numeric characters. 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1ae32d5-Capture_decran_2021-04-09_a_13.36.20.png",
        "Capture d’écran 2021-04-09 à 13.36.20.png",
        1156,
        643,
        "#fbfbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Rent Receipt OCR
 

 


 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f288020-Capture_decran_2021-04-09_a_13.37.02.png",
        "Capture d’écran 2021-04-09 à 13.37.02.png",
        1325,
        777,
        "#d9dce0"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

You’re all set! 

 

Now is the time to train your Rent Receipt deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Rent Receipt in your application.

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!