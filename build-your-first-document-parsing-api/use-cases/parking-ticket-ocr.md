---
title: Parking Ticket OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Parking Ticket using our deep learning engine.

 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Parking Ticket images or pdfs to train your OCR.
 

 

## Define your Parking Ticket use case
 

First, we’re going to define what fields we want to extract from your **Parking Ticket**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c46e094-parking_ticket.png",
        "parking ticket.png",
        399,
        597,
        "#7d7875"
      ],
      "caption": "Parking ticket key data extraction"
    }
  ]
}
[/block]
  * **Citation Number**: The citation identification number 
  *  **Date**: The date of the citation
  *  **Time**: The time it was when the citation was issued
  *  **Licence Number**: The licence number of the vehicle mentioned in the citation 
  *  **State**: The state in which the citation was delivered
  *  **Amount Due**: The total amount due by the vehicle's owner
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘Create a new API’ button.
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/22/parking-ticket.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/60fcb05-Capture_decran_2021-04-07_a_15.06.55.png",
        "Capture d’écran 2021-04-07 à 15.06.55.png",
        1391,
        516,
        "#e0e0e0"
      ],
      "caption": "Parking ticket API set up"
    }
  ]
}
[/block]
 
 

Once you’re ready, click on the “**next**” button. We are going to specify the data types for each of the fields we want our API to extract.



 


To move forward, you have two possibilities:

**Upload a json config**
Copy the following JSON into a file and upload it on the interface

 

 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"citation_number\",\n          \"public_name\": \"Citation Number\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date\",\n          \"public_name\": \"Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"time_issued\",\n          \"public_name\": \"Time issued\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"licence_number\",\n          \"public_name\": \"Licence Number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"state\",\n          \"public_name\": \"State\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"amount_due\",\n          \"public_name\": \"Amount Due\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"citation_number\",\n        \"date\",\n        \"time_issued\",\n        \"licence_number\",\n        \"state\",\n        \"amount_due\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9d34a72-Capture_decran_2021-04-07_a_15.07.05.png",
        "Capture d’écran 2021-04-07 à 15.07.05.png",
        1391,
        516,
        "#fbfbfd"
      ],
      "caption": "Define your parking ticket model"
    }
  ]
}
[/block]
In our example, here are the different field configurations we used:

  * **Citation Number**: type Number without specifications. 
  * **Date**: type Date with US format.
  * **Time issued**: type String without specifications. 
  * **Licence Number**: type String without specifications. 
  * **State**: type String that never contains numeric characters. 
  * **Amount Due**: type Number without specifications. 
  

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

 

 

## Train your Parking Ticket OCR
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fa37c59-Capture_decran_2021-04-08_a_09.51.17.png",
        "Capture d’écran 2021-04-08 à 09.51.17.png",
        1629,
        869,
        "#c3c4c7"
      ],
      "caption": "Training your parking ticket model"
    }
  ]
}
[/block]
 


 

 

You’re all set! 

 

Now is the time to train your Parking Ticket deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Parking Ticket in your application.

 

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!