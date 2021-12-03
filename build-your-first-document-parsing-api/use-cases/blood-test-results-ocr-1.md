---
title: Blood Test Results OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Blood Test Results using our deep learning engine. It will work for any document issued by any laboratory. 

 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Blood Test Results images or pdfs to train your OCR.
 

 

## Define your Blood Test Results use case
 

First, we’re going to define what fields we want to extract from your **Blood Test Results**. 

 

 
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4461f3f-q.png",
        "q.png",
        476,
        598,
        "#e3ebec"
      ],
      "caption": "Blood results key data extraction"
    }
  ]
}
[/block]
 

  * **Patient name**: The full name of the patient 
  * **Date of Report**: The date of the report creation
  * **ID Number**: The patient ID Number
  * **Sodium Results**: The amount of Sodium the patient has in his organism according to the blood test results. 
  * **Calcium Results**: The amount of Calcium the patient has in his organism according to the blood test results. 
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.

 

[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/21/blood-test.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/25c9584-Capture_decran_2021-04-08_a_12.59.02.png",
        "Capture d’écran 2021-04-08 à 12.59.02.png",
        1161,
        508,
        "#f7f8f9"
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
        "https://files.readme.io/981abb2-Capture_decran_2021-04-09_a_14.26.06.png",
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"patient_name\",\n          \"public_name\": \"Patient name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date_of_report\",\n          \"public_name\": \"Date of Report\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"id_number\",\n          \"public_name\": \"ID Number\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"sodium_results\",\n          \"public_name\": \"Sodium Results\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"calcium_results\",\n          \"public_name\": \"Calcium Results\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"patient_name\",\n        \"date_of_report\",\n        \"id_number\",\n        \"sodium_results\",\n        \"calcium_results\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:


  * **Patient name**: type String that never contains numeric characters.
  * **Date of Report**: type Date with US format.  
  * **ID Number**: type Number without specifications.
  * **Sodium Results**: type Number without specifications. 
  * **Calcium Results**: type Number without specifications. 

 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/598ae34-Capture_decran_2021-04-08_a_13.00.26.png",
        "Capture d’écran 2021-04-08 à 13.00.26.png",
        1161,
        593,
        "#fafbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Blood Test Results OCR
 

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a98666d-Capture_decran_2021-04-08_a_13.01.03.png",
        "Capture d’écran 2021-04-08 à 13.01.03.png",
        1366,
        782,
        "#e9ecef"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your Blood Test Results, deep learning model, in the Training section of our API. 

 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Blood Test Results in your application.

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!