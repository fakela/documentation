---
title: Medicare health insurance card OCR
excerpt: ''
hidden: false
---
This article explains how to quickly build and deploy an accurate OCR API that extracts data from US Medicare health insurance cards using our deep learning engine. It can be adapted to any type of health insurance card from other providers.

 

 

**Prerequisites**
You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
You’ll need at least 20 Health insurance card images or pdfs to train your OCR.
 

 

 

## Define your Health Insurance card data model
 

First, we’re going to define what fields we want to extract from your **health insurance cards**.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e32d3b2-image-54.png",
        "image-54.png",
        698,
        437,
        "#d9d1d6"
      ],
      "caption": "Health insurance key data extraction"
    }
  ]
}
[/block]
 

 

 

Here is the field list we want our algorithm to look for in your documents:

 

  * **Card owner**: The full name card owner
  * **ID Number**: The unique identifier claim number
  * **Sex**: Gender of the card owner
  * **Hospital effective date**: Start date of the hospital coverage 
  * **Medical effective date**: Start date of the medical coverage
 

If you're following this article for other types of health insurance cards, feel free to add as many as you want.

 

 

## Deploy your API
 

Once you have defined the field list, head over to the platform and press the ‘**Create a new API**’ button.
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/18/image-52.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/60a1924-Capture_decran_2021-04-08_a_12.39.22.png",
        "Capture d’écran 2021-04-08 à 12.39.22.png",
        1155,
        504,
        "#f1f2f5"
      ],
      "caption": "Set up your API"
    }
  ]
}
[/block]
 

 

Once you’re ready, click on the “**next**” button. You land on a new page where we are going to define more technically the required field we want to extract in our new OCR API.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2c716fa-Capture_decran_2021-04-08_a_12.39.43.png",
        "Capture d’écran 2021-04-08 à 12.39.43.png",
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"cardholder\",\n          \"public_name\": \"Cardholder\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"id_number\",\n          \"public_name\": \"ID Number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"sex\",\n          \"public_name\": \"Sex\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"hospital_effective_date\",\n          \"public_name\": \"Hospital effective date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"medical_effective_date\",\n          \"public_name\": \"Medical  effective date\",\n          \"semantics\": \"date\"\n        }\n      ],\n      \"features_name\": [\n        \"cardholder\",\n        \"id_number\",\n        \"sex\",\n        \"hospital_effective_date\",\n        \"medical_effective_date\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
 **Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Cardholder**: type String. The cardholder name never contains numeric characters, you can specify this by clicking the corresponding checkbox
  * **ID Number**: type String. It's composed of both alpha and numeric characters so we don't put any specification for the claim number.
  * **Sex**: type String. Like cardholder, there are no numeric characters for this one.
  * **Hospital effective date**: type Date
  * **Medical  effective date**: type Date


Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bd49427-Capture_decran_2021-04-08_a_12.41.14.png",
        "Capture d’écran 2021-04-08 à 12.41.14.png",
        1160,
        589,
        "#fafbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]

 
 
 
## Train your health insurance card model
 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2b14018-Capture_decran_2021-04-08_a_12.42.02.png",
        "Capture d’écran 2021-04-08 à 12.42.02.png",
        1376,
        775,
        "#d3d4d8"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

Your setup is done. You can now deploy your API and train your model for automatically extracting data from your health insurance cards using the API.

 

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!