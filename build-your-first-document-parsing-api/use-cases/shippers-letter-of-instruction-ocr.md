---
title: Shipper's Letter of Instruction OCR
excerpt: ''
hidden: false
---
This article walks you through the building process of an OCR API that extracts data from Shipper's letter of Instruction using our deep learning engine. This API works with any letter template. 

  

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Shipper's letter of Instruction images or pdfs to train your OCR.

## Define your Shipper's letter of Instruction use case
 

First, we’re going to define what fields we want to extract from your **Shipper's letter of Instruction**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2a101bb-ba.png",
        "ba.png",
        424,
        596,
        "#e6e6e7"
      ],
      "caption": "Shipper's letter of instruction key data extraction"
    }
  ]
}
[/block]
  *  Shipper: The shipper's full name 
  *  Consignee: The consignee's full name 
  *  Forwarding Agent: The forwarding agent's full name 
  *  Reference: The Shipper's letter of an Instruction reference number
  *  Declared Value: The declared value of shipped goods
  *  Date of issue: The issue date of Shipper's letter of Instruction
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract from your letter of instruction, head over to the platform and press the ‘**Create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/22/shippers-letter-of-instruction.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b76842f-Capture_decran_2021-04-09_a_10.26.34.png",
        "Capture d’écran 2021-04-09 à 10.26.34.png",
        1122,
        449,
        "#f6f7f9"
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
        "https://files.readme.io/0983ddb-Capture_decran_2021-04-09_a_10.26.41.png",
        "Capture d’écran 2021-04-09 à 10.26.41.png",
        1122,
        449,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"shipper\",\n          \"public_name\": \"Shipper\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"consignee\",\n          \"public_name\": \"Consignee\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"forwarding_agent\",\n          \"public_name\": \"Forwarding Agent\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"reference\",\n          \"public_name\": \"Reference\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"declared_value\",\n          \"public_name\": \"Declared Value\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date_of_issue\",\n          \"public_name\": \"Date of Issue\",\n          \"semantics\": \"date\"\n        }\n      ],\n      \"features_name\": [\n        \"shipper\",\n        \"consignee\",\n        \"forwarding_agent\",\n        \"reference\",\n        \"declared_value\",\n        \"date_of_issue\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Shipper**: type String that never contains numeric characters.
  * **Consignee**: type String that never contains numeric characters.
  * **Forwarding Agent**: type String that never contains numeric characters.
  * **Reference**: type Number without specifications. 
  * **Declared Value**: type Number without specifications. 
  * **Date of Issue**: type Date with US format. 


 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f95a287-Capture_decran_2021-04-09_a_10.28.11.png",
        "Capture d’écran 2021-04-09 à 10.28.11.png",
        1144,
        583,
        "#fafbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 

## Train your Shipper's letter of Instruction OCR


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2f32e7e-Capture_decran_2021-04-09_a_10.29.03.png",
        "Capture d’écran 2021-04-09 à 10.29.03.png",
        1309,
        772,
        "#e4e6e8"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
You’re all set! 

 

Now is the time to train your Shipper's letter of Instruction deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Shipper's letter of Instruction in your application.

 To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!