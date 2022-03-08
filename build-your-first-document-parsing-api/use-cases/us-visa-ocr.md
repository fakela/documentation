---
title: US Visa OCR
excerpt: ''
hidden: false
---
This article walks you through the building process of an OCR API that extracts data from US Visas using our deep learning engine. It will work for any visa issued by the United States of America.  

 

 

**Prerequisites**
> 1. You’ll need a beta account. [Sign up](https://platform.mindee.com/signup)  and confirm your email to login.
> 2. You’ll need at least 20 US Visa images or pdfs to train your OCR.
 

 

## Define your US Visa use case
 

First, we’re going to define what fields we want to extract from your **US Visa**. 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d4743c8-capture-decran-2021-01-20-a-170254.png",
        "capture-decran-2021-01-20-a-170254.png",
        796,
        520,
        "#aea39b"
      ],
      "caption": "US Visa key data extraction"
    }
  ]
}
[/block]

 

 

  * **First name**: The first name of the visa holder (Happyperson)
  *  **Last name**: The last name of the visa holder (Traveler)
  *  **Passport number**: The passport number of the visa holder (AB1234567)
  *  **Control Number**:  The visa control number (20191234567890)
  *  **Visa type**: The visa type appearing on the US Visa (B1/B2)
  

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.

 


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/20/via.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/760d833-Capture_decran_2021-04-08_a_10.15.38.png",
        "Capture d’écran 2021-04-08 à 10.15.38.png",
        1067,
        505,
        "#eae9e9"
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
        "https://files.readme.io/967ddcc-Capture_decran_2021-04-08_a_10.15.44.png",
        "Capture d’écran 2021-04-08 à 10.15.44.png",
        1067,
        505,
        "#fafbfc"
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"first_name\",\n          \"public_name\": \"First name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"last_name\",\n          \"public_name\": \"Last Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"passport_number\",\n          \"public_name\": \"Passport Number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"control_number\",\n          \"public_name\": \"Control Number\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"visa_type\",\n          \"public_name\": \"Visa Type\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"first_name\",\n        \"last_name\",\n        \"passport_number\",\n        \"control_number\",\n        \"visa_type\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
 

**Or build your data model manually**
Using the interface, add up to your data model each field.

 In our example, here are the different field configurations we used:


  * **First name**: type String that never contains numeric characters.
  * **Last Name**: type String without specifications. 
  * **Passport Number**: type String without specifications.
  * **Control Number**: type Number without specifications. 
  * **Visa Type**: type String without specifications.
  
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f60e078-Capture_decran_2021-04-08_a_10.17.28.png",
        "Capture d’écran 2021-04-08 à 10.17.28.png",
        1067,
        640,
        "#fafbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

 

## Train your US Visa OCR
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0ae2281-Capture_decran_2021-04-08_a_10.18.19.png",
        "Capture d’écran 2021-04-08 à 10.18.19.png",
        1259,
        866,
        "#c5c7ca"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 


 

 

You’re all set! 

 

Now is the time to train your US Visa deep learning model in the Training section of our API. 

 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing US Visa in your application.

 

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any questions regarding your use case, feel free to reach out on our chat!