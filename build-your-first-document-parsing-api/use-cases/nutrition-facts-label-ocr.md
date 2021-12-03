---
title: Nutrition Facts label OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Nutrition Facts labels using our deep learning engine. It will work for any food brand or label template. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 nutrition facts labels or pdfs to train your OCR.

## Define your Nutrition fact label use case
 

First, we’re going to define what fields we want to extract from your **Nutrition fact label. * 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5e34b1a-capture-decran-2021-01-21-a-110415.png",
        "capture-decran-2021-01-21-a-110415.png",
        1148,
        1052,
        "#46413c"
      ],
      "caption": "Nutrition facts label key data extraction"
    }
  ]
}
[/block]
  *  **Serving size**: 170 gram 
  *  **Total fat gram**: 2 gram
  * **Total fat daily value** : 3%
  * **Calories per serving**: 150
  
 

That’s it for our use case. Remember this is an example feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.

 
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/21/foodlabel012120crop.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4ed1175-Capture_decran_2021-04-09_a_14.16.39.png",
        "Capture d’écran 2021-04-09 à 14.16.39.png",
        1125,
        448,
        "#dbdada"
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
        "https://files.readme.io/07b4302-Capture_decran_2021-04-09_a_14.16.45.png",
        "Capture d’écran 2021-04-09 à 14.16.45.png",
        1125,
        448,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": 1 } },\n          \"handwritten\": false,\n          \"name\": \"serving_size\",\n          \"public_name\": \"Serving size\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"total_fat_gram\",\n          \"public_name\": \"Total fat gram\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": 0, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"total_fat_daily_value\",\n          \"public_name\": \"Total fat daily value\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": 1 } },\n          \"handwritten\": false,\n          \"name\": \"calories_per_serving\",\n          \"public_name\": \"Calories per serving\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"serving_size\",\n        \"total_fat_gram\",\n        \"total_fat_daily_value\",\n        \"calories_per_serving\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Serving size**: type Integer 
  * **Total fat gram**: type Number
  * **Total fat daily value**: type String that never contains alpha characters
  * **Calories per serving**: type Integer

 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/29958a3-Capture_decran_2021-04-09_a_14.17.52.png",
        "Capture d’écran 2021-04-09 à 14.17.52.png",
        1132,
        640,
        "#fbfbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Nutrition facts labels OCR
 

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/39bc65c-Capture_decran_2021-04-09_a_14.18.46.png",
        "Capture d’écran 2021-04-09 à 14.18.46.png",
        1316,
        768,
        "#babcbe"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your nutrition facts to train deep learning model in the Training section of our API. 

 

After 20 annotated data, your first model is trained and you're now able to use your custom OCR API for parsing nutrition facts labels in your application.


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!