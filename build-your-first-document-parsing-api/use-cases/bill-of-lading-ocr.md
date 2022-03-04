---
title: Bill of Lading OCR
excerpt: ''
hidden: false
---
This article walks you through the building process of an OCR API that extracts data from Bills of Lading using our deep learning engine. It will work for any bank company or bank statement template. 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Bill of Lading images or pdfs to train your OCR.

## Define your Bill of Lading use case
 

First, we’re going to define what fields we want to extract from your **Bill of Lading. 
**

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6c99c7a-a.png",
        "a.png",
        626,
        597,
        "#ebeaea"
      ],
      "caption": "Bill of Lading key data extraction"
    }
  ]
}
[/block]

  * **Shipper's name**: The full name of the company shipping products 
  *  **Consignee's name**: The full name of the company receiving products
  *  **Ship Date**: Represents the date when the shipper sent listed products 
  *  **Due Date**: Represents the estimated date of delivery to the consignee
  *  **Carrier**: The name of the company carrying listed products from shipper to consignee
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/21/bill-of-lading.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/62770b8-Capture_decran_2021-04-09_a_10.53.00.png",
        "Capture d’écran 2021-04-09 à 10.53.00.png",
        1119,
        445,
        "#f7f8fa"
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
        "https://files.readme.io/dbc8719-Capture_decran_2021-04-09_a_10.53.08.png",
        "Capture d’écran 2021-04-09 à 10.53.08.png",
        1119,
        445,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"shipper_s_name\",\n          \"public_name\": \"Shipper's name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"consignee_s_name\",\n          \"public_name\": \"Consignee's Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"ship_date\",\n          \"public_name\": \"Ship Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"due_date\",\n          \"public_name\": \"Due Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"carrier\",\n          \"public_name\": \"Carrier\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"shipper_s_name\",\n        \"consignee_s_name\",\n        \"ship_date\",\n        \"due_date\",\n        \"carrier\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Shipper's name**: type String that never contains numeric characters.
  * **Consignee's Name**: type String that never contains numeric characters.
  * **Ship Date**: type Date with US format. 
  * **Due Date**: type Date with US format. 
  * **Carrier**: type String that never contains numeric characters. 


 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f9cb2fa-Capture_decran_2021-04-09_a_10.55.08.png",
        "Capture d’écran 2021-04-09 à 10.55.08.png",
        1131,
        638,
        "#fafbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Bill of Lading OCR
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7e6cccd-Capture_decran_2021-04-09_a_10.55.43.png",
        "Capture d’écran 2021-04-09 à 10.55.43.png",
        1315,
        771,
        "#e4e5eb"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 


 

 

You’re all set! 

 

Now is the time to train your Bill of Lading deep learning model in the Training section of our API. 

 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Bills of Lading in your application.


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!