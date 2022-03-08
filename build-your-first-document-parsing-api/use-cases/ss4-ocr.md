---
title: SS4 OCR
excerpt: ''
hidden: false
---
This article describes how to build an OCR API that extracts data from SS4 using our deep learning engine. If you want to automate your workflow, this article is for you. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 SS4 images or pdfs to train your OCR.

## Define your SS4 use case
 

First, we’re going to define what fields we want to extract from your **SS4**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7a51bae-capture-decran-2021-01-25-a-115136.png",
        "capture-decran-2021-01-25-a-115136.png",
        456,
        588,
        "#ebeaeb"
      ],
      "caption": "Set up your model"
    }
  ]
}
[/block]
  * **Entity Name**: The legal name of the entity. 
  *  **Address**: The entity's full address (mailing, city, state)
  *  **SSN**: The Social Security Number of the principal officer. 
  *  **Type of entity**: The type of entity. 
  *  **Reason for applying**: The reason why you apply for an employer identification number.
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements. 

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract from your SS4, head over to the platform and press the ‘**Create a new API**’ button.

 
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/25/sample-ein-ss4-application-form-2009-1-728.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/709115f-Capture_decran_2021-04-09_a_14.33.05.png",
        "Capture d’écran 2021-04-09 à 14.33.05.png",
        1116,
        451,
        "#f7f8f9"
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
        "https://files.readme.io/e9e00e8-Capture_decran_2021-04-09_a_14.33.09.png",
        "Capture d’écran 2021-04-09 à 14.33.09.png",
        1116,
        451,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"entity_name\",\n          \"public_name\": \"Entity Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"address\",\n          \"public_name\": \"Address\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": 0, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"ssn\",\n          \"public_name\": \"SSN\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"type_of_entity\",\n          \"public_name\": \"Type of entity\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"reason_for_applying\",\n          \"public_name\": \"Reason for applying\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"entity_name\",\n        \"address\",\n        \"ssn\",\n        \"type_of_entity\",\n        \"reason_for_applying\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Entity Name**: type String that never contains numeric characters. 
  * **Address**: type String without specifications. 
  * **SSN**: type String that never contains alpha characters. 
  * **Type of entity**: type String that never contains numeric characters. 
  * **Reason for applying**: type String that never contains numeric characters. 
  
 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d0d4473-Capture_decran_2021-04-09_a_14.34.12.png",
        "Capture d’écran 2021-04-09 à 14.34.12.png",
        1132,
        646,
        "#fbfbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your SS4 OCR
 

 


 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0515ef9-Capture_decran_2021-04-09_a_14.35.26.png",
        "Capture d’écran 2021-04-09 à 14.35.26.png",
        1317,
        770,
        "#e6e7ee"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
You’re all set! 

 

Now is the time to train your SS4 deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing SS4 in your application.

  

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!