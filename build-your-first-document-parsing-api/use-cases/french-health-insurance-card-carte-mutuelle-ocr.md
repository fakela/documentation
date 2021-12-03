---
title: French health insurance card OCR
excerpt: ''
---
This article explains how to extract all the relevant data from French health insurance cards (carte mutuelle tiers payant) using our deep learning OCR engine.


**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Health insurance card images or pdfs to train your OCR.
 
 

## Define the data you need from Health insurance cards
 

We need first to set up our use case by defining what fields we want to extract from your **health insurance cards.
**
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2911615-image-61.png",
        "image-61.png",
        1095,
        399,
        "#efd6d7"
      ],
      "caption": "French health insurance key data extraction"
    }
  ]
}
[/block]
 

 

In this article, we are going to set up an API for extracting the following fields:

 

  * **AMC Number**: The AMC number of the cardholder
  * **Member identification number**: The unique member identification number (numéro adhérent)
  * **Teletransmission number**
  * **Insured full name**: Full name of the first insured. You can add more fields of this type if you want to extract more of them.
  * **Insured social security number**: SSN of the first insured.
  * **Validity start date**
  * **Validity end date**
 

You can add as many fields as you want to fit your requirements.

 

 

## Deploy your Health Insurance card API
 

The field list was defined and we are now going to set up our API. Head over to the platform and press the ‘**Create a new API**’ button.

 
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/18/tiers-payant-recto-jpg.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ba33fda-Capture_decran_2021-04-08_a_12.48.38.png",
        "Capture d’écran 2021-04-08 à 12.48.38.png",
        1161,
        507,
        "#f6f3f4"
      ],
      "caption": "Set up your API"
    }
  ]
}
[/block]
 

Click on the “**next**” button. You land on a new page where we are going to add the technical definitions of the fields we defined above.

 
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6486c3b-Capture_decran_2021-04-08_a_12.48.49.png",
        "Capture d’écran 2021-04-08 à 12.48.49.png",
        1161,
        507,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": 0, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"amc_number\",\n          \"public_name\": \"AMC Number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": 0, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"member_identification_number\",\n          \"public_name\": \"Member identification number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": 0, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"teletransmission_number\",\n          \"public_name\": \"Teletransmission number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"insured_full_name\",\n          \"public_name\": \"Insured full name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"insured_social_security_number\",\n          \"public_name\": \"Insured social security number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"FR\" } },\n          \"handwritten\": false,\n          \"name\": \"validity_start_date\",\n          \"public_name\": \"Validity start date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"FR\" } },\n          \"handwritten\": false,\n          \"name\": \"validity_end_date\",\n          \"public_name\": \"Validity end date\",\n          \"semantics\": \"date\"\n        }\n      ],\n      \"features_name\": [\n        \"amc_number\",\n        \"member_identification_number\",\n        \"teletransmission_number\",\n        \"insured_full_name\",\n        \"insured_social_security_number\",\n        \"validity_start_date\",\n        \"validity_end_date\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
 **Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **AMC Number**: type String with no alpha characters
  * **Member identification number**: type String with no alpha characters
  * **Teletransmission number**: type String with no alpha characters
  * **Insured full name**: type String with no numeric characters
  * **Insured social security number**: type String without any specification
  * **Validity start date**: type Date
  * **Validity end date**: type Date

 

That's it for the setup phase. Let's deploy your OCR.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7cee149-Capture_decran_2021-04-08_a_12.50.39.png",
        "Capture d’écran 2021-04-08 à 12.50.39.png",
        1157,
        624,
        "#fafbfc"
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
        "https://files.readme.io/6f06e2f-Capture_decran_2021-04-08_a_12.51.36.png",
        "Capture d’écran 2021-04-08 à 12.51.36.png",
        1370,
        776,
        "#c6c7cc"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

Your setup is done. You can now deploy your API and train your deep learning OCR to extract data from your health insurance cards using the API.

 


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!