---
title: Energy performance diagnostic OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from energy performance diagnostics using our deep learning engine. It will work for any kind of EPD template. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 energy performance diagnostic images or pdfs to train your OCR.

Define your Energy performance diagnostic (DPE) use case
 

First, we’re going to define what fields we want to extract from your **energy performance diagnostic**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4a0dd58-capture-decran-2021-01-20-a-145306.png",
        "capture-decran-2021-01-20-a-145306.png",
        736,
        1052,
        "#e7e3e0"
      ],
      "caption": "Energy performance diagnostic key data extraction"
    }
  ]
}
[/block]
  * **Validation date**: 30/06/2022
  *  **Annual energy consumption** : 43430 KW/h
  *  **Habitation energy rating** : D
  *  **Address**: 12 Basse Rue, 85200 SAINT MARTIN DE FREIGNEAU
  *  **Annual energy price**: 3063€
  
 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘Create a new API’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/20/etiquette-energie-dpe.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/932e277-Capture_decran_2021-04-09_a_14.08.17.png",
        "Capture d’écran 2021-04-09 à 14.08.17.png",
        1123,
        446,
        "#f5f5f7"
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
        "https://files.readme.io/1f9171d-Capture_decran_2021-04-09_a_14.08.23.png",
        "Capture d’écran 2021-04-09 à 14.08.23.png",
        1123,
        446,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"FR\" } },\n          \"handwritten\": false,\n          \"name\": \"validation_date\",\n          \"public_name\": \"validation date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": 1 } },\n          \"handwritten\": false,\n          \"name\": \"annual_energy_consumption\",\n          \"public_name\": \"annual energy consumption\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"habitation_energy_rating\",\n          \"public_name\": \"Habitation energy rating\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"address\",\n          \"public_name\": \"address\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"annual_energy_price\",\n          \"public_name\": \"annual energy price\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"validation_date\",\n        \"annual_energy_consumption\",\n        \"habitation_energy_rating\",\n        \"address\",\n        \"annual_energy_price\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  *  **Validation date**: type Date in the European default format
  * **Annual energy consumption**: type Number/Integer
  * **Habitation energy rating**: type string contains only alpha characters
  * **Address**: type string with both numeric and alpha characters.
  * **Annual energy price**: Number type
  

 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8ec119d-Capture_decran_2021-04-09_a_14.09.43.png",
        "Capture d’écran 2021-04-09 à 14.09.43.png",
        1148,
        649,
        "#fbfbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 

 

## Train your custom energy performance diagnostic OCR API
 

 

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9970838-Capture_decran_2021-04-09_a_14.11.35.png",
        "Capture d’écran 2021-04-09 à 14.11.35.png",
        1318,
        768,
        "#e3e4e6"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your DPE deep learning model in the Training section of our API. 

 

You should get your first model trained in a few hours and you will be soon able to use your custom OCR API for parsing energy performance diagnostic in your application.


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!