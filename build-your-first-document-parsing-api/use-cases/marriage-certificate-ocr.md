---
title: Marriage Certificate OCR
excerpt: ''
hidden: false
---
This article walks you through the building process of an OCR API that extracts data from Marriage Certificates using our deep learning engine. It will work for any bank company or bank statement template. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Marriage Certificate images or pdfs to train your OCR.

## Define your Marriage Certificate use case
 

First, we’re going to define what fields we want to extract from your **Marriage Certificate**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c06c446-marriage_certif.png",
        "marriage certif.png",
        671,
        598,
        "#e4e2d9"
      ],
      "caption": "Marriage certificate key data extraction"
    }
  ]
}
[/block]
  * **Issuer Name:** The name of the marriage certificate issuer
  *  **Issued date**: The date of issue of the marriage certificate 
  *  **Husband's Name**: The husband's name
  *  **Wife's name**: The wife's name
  *  **Clerk information**: The clerk address information
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.

 
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/21/marriage-certificate.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f7e87e1-Capture_decran_2021-04-08_a_21.20.32.png",
        "Capture d’écran 2021-04-08 à 21.20.32.png",
        1100,
        500,
        "#f4f5f5"
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
        "https://files.readme.io/e06dfb7-Capture_decran_2021-04-08_a_16.49.01.png",
        "Capture d’écran 2021-04-08 à 16.49.01.png",
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"issuer_name\",\n          \"public_name\": \"Issuer Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"issued_date\",\n          \"public_name\": \"Issued Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"husband_s_name\",\n          \"public_name\": \"Husband's Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"wife_s_name\",\n          \"public_name\": \"Wife's name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"clerk_information\",\n          \"public_name\": \"Clerk Information\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"issuer_name\",\n        \"issued_date\",\n        \"husband_s_name\",\n        \"wife_s_name\",\n        \"clerk_information\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Issuer Name**: type String that never contains numeric characters.
  * **Issued Date**: type Date with US format.  
  * **Husband's Name**: type String that never contains numeric characters. 
  * **Wife's name**: type String that never contains numeric characters. 
  * **Clerk Information**: type String that never contains numeric characters. 


Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ac2a38f-Capture_decran_2021-04-08_a_21.21.56.png",
        "Capture d’écran 2021-04-08 à 21.21.56.png",
        1114,
        714,
        "#fafbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
## Train your Marriage Certificate OCR
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/55ff571-Capture_decran_2021-04-08_a_21.23.28.png",
        "Capture d’écran 2021-04-08 à 21.23.28.png",
        1310,
        780,
        "#e0e2e5"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
You’re all set! 

 

Now is the time to train your Marriage Certificate deep learning model in the Training section of our API. 

 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Marriage Certificate in your application.


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!