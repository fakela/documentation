---
title: Traffic Ticket OCR
excerpt: ''
hidden: false
---
This article describes how to build an OCR API that extracts data from Traffic ticket using our deep learning engine. If you want to automate your traffic ticket workflow, this article is for you. 

 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Traffic ticket images or pdfs to train your OCR.
 

 

## Define your Traffic ticket use case
 

First, we’re going to define what fields we want to extract from your **Traffic ticket**. 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fd32014-capture-decran-2021-01-21-a-163834.png",
        "capture-decran-2021-01-21-a-163834.png",
        794,
        596,
        "#e9e9e9"
      ],
      "caption": "Traffic ticket key data extraction"
    }
  ]
}
[/block]

  * **Date**: The date of the offence
  * **Time**: The time of the offence
  * **Description**: The description of the violation
  * **Place of occurrence**: The place where the violation occurred
  * **Badge**: The badge number
 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements. For example, you could add the county, the arrest type, or anything else you want really. 

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract from your traffic ticket document, head over to the platform and press the ‘**Create a new API**’ button.

 
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/22/proces-verbal.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6c556a9-Capture_decran_2021-04-08_a_10.01.35.png",
        "Capture d’écran 2021-04-08 à 10.01.35.png",
        1394,
        508,
        "#f7f8f9"
      ],
      "caption": "Set up your  Traffic Ticket OCR"
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
        "https://files.readme.io/694e27e-Capture_decran_2021-04-08_a_10.01.47.png",
        "Capture d’écran 2021-04-08 à 10.01.47.png",
        1394,
        508,
        "#fbfcfd"
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date_of_offence\",\n          \"public_name\": \"Date of Offence\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"time\",\n          \"public_name\": \"Time\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"description_of_violation\",\n          \"public_name\": \"Description of Violation\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"place_of_occurrence\",\n          \"public_name\": \"Place of Occurrence\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"badge_number\",\n          \"public_name\": \"Badge Number\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"date_of_offence\",\n        \"time\",\n        \"description_of_violation\",\n        \"place_of_occurrence\",\n        \"badge_number\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  
  * **Date of Offence**: type Date with US format
  * **Time**: type String without specifications. 
  * **Description of Violation**: type String without specifications. 
  * **Place of Occurrence**: type String without specifications. 
  * **Badge Number**: type Number without specifications. 

 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6af0efa-Capture_decran_2021-04-08_a_10.03.32.png",
        "Capture d’écran 2021-04-08 à 10.03.32.png",
        989,
        643,
        "#fafbfc"
      ],
      "caption": "Ready to train traffic ticket OCR"
    }
  ]
}
[/block]
 
 
## Train your Traffic ticket OCR
 

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e6756d7-Capture_decran_2021-04-08_a_10.04.30.png",
        "Capture d’écran 2021-04-08 à 10.04.30.png",
        1275,
        872,
        "#d4d7db"
      ],
      "caption": "Train your traffic ticket OCR"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your Traffic ticket deep learning model in the Training section of our API. 

 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Traffic ticket in your application.

 

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!