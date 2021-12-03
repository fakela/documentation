---
title: DS 2019 OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from the DS 2019 form using our deep learning engine. It will work for any airline company or boarding pass template. 

 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 DS 2019 form images or pdfs to train your OCR.
 

 

## Define your DS 2019 use case
 

First, we’re going to define what fields we want to extract from your **DS 2019 form. **

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/adb045c-capture-decran-2021-01-20-a-180213.png",
        "capture-decran-2021-01-20-a-180213.png",
        465,
        601,
        "#eeeeed"
      ],
      "caption": "DS 2019 key data extraction"
    }
  ]
}
[/block]
 
  * **First Name**: The first name of the DS 2019 holder
  * **Family Name**: The last name of the DS 2019 holder
  * **Gender**: The DS 2019 holder gender 
  * **Visa type**: The visa type linked to the DS 2019 form
  * **End of cover period**: The ending date of the DS 2019 cover period
  

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.

 
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/20/ds-2019.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2c3de84-Capture_decran_2021-04-08_a_10.32.29.png",
        "Capture d’écran 2021-04-08 à 10.32.29.png",
        1159,
        501,
        "#f7f8fa"
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
        "https://files.readme.io/db5355d-Capture_decran_2021-04-08_a_10.32.39.png",
        "Capture d’écran 2021-04-08 à 10.32.39.png",
        1159,
        501,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"first_name\",\n          \"public_name\": \"First name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"family_name\",\n          \"public_name\": \"Family name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"gender\",\n          \"public_name\": \"Gender\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"visa_type\",\n          \"public_name\": \"Visa Type\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"end_of_cover_period\",\n          \"public_name\": \"End of cover period\",\n          \"semantics\": \"date\"\n        }\n      ],\n      \"features_name\": [\n        \"first_name\",\n        \"family_name\",\n        \"gender\",\n        \"visa_type\",\n        \"end_of_cover_period\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
 
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **First name**: type String that never contains numeric characters.
  * **Family name**: type String that never contains numeric characters.
  * **Gender**: type String that never contains numeric characters.  
  * **Visa Type**: type String without specifications.
  * **End of cover period**: type Date in US format.


Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9a51dd0-Capture_decran_2021-04-08_a_10.34.13.png",
        "Capture d’écran 2021-04-08 à 10.34.13.png",
        1183,
        663,
        "#fafbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]

 
 
## Train your DS 2019 form OCR
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4d585a0-Capture_decran_2021-04-08_a_10.44.08.png",
        "Capture d’écran 2021-04-08 à 10.44.08.png",
        1372,
        879,
        "#f3f3f5"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]


 

 

You’re all set! 

 

Now is the time to train your DS 2019 deep learning model in the Training section of our API. 

 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing DS 2019 form in your application.

 

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!