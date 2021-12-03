---
title: Delivery Note OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Delivery Note using our deep learning engine. It will work for any bank company or bank statement template. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Delivery Note images or pdfs to train your OCR.

## Define your Delivery Note use case
 

First, we’re going to define what fields we want to extract from your **Delivery Note. 
**

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/13604c5-rr.png",
        "rr.png",
        460,
        598,
        "#f6f6f6"
      ],
      "caption": "Delivery note key data extraction"
    }
  ]
}
[/block]
  * **Entity Name**: The full name of the entity 
  *  **Code**: The delivery code
  *  **Shipping Method**: The shipping Method's code
  *  **Sales Person**: The full name of the salesperson 
  *  **Order Number**: The order number
  
 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘Create a new API’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/21/delivery-note.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4787cca-Capture_decran_2021-04-09_a_10.45.53.png",
        "Capture d’écran 2021-04-09 à 10.45.53.png",
        1117,
        445,
        "#f8f9fb"
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
        "https://files.readme.io/3a93bfc-Capture_decran_2021-04-09_a_10.46.02.png",
        "Capture d’écran 2021-04-09 à 10.46.02.png",
        1117,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"entity_name\",\n          \"public_name\": \"Entity name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"code\",\n          \"public_name\": \"Code\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"shipping_method\",\n          \"public_name\": \"Shipping Method\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"salesperson\",\n          \"public_name\": \"Salesperson\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"order_number\",\n          \"public_name\": \"Order Number\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"entity_name\",\n        \"code\",\n        \"shipping_method\",\n        \"salesperson\",\n        \"order_number\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Entity name:** type String that never contains numeric characters.
  * **Code**: type String without specifications. 
  * **Shipping Method:** type String that never contains numeric characters. 
  * **Salesperson**: type String that never contains numeric characters.  
  * **Order Number**: type String without specifications. 


 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/47cd1cf-Capture_decran_2021-04-09_a_10.47.16.png",
        "Capture d’écran 2021-04-09 à 10.47.16.png",
        1137,
        650,
        "#fbfbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Delivery Note OCR
 

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ae64382-Capture_decran_2021-04-09_a_10.47.53.png",
        "Capture d’écran 2021-04-09 à 10.47.53.png",
        1318,
        770,
        "#edeef1"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your Delivery Note deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Delivery Note in your application.


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!