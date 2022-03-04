---
title: Bank Statement OCR
excerpt: ''
hidden: false
---
This article walks you through the building process of an OCR API that extracts data from Bank Statements using our deep learning engine. It will work for any bank company or bank statement template. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Bank Statement images or pdfs to train your OCR.

## Define your Bank Statement use case
 

First, we’re going to define what fields we want to extract from your **Bank Statement**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bdbc346-capture-decran-2021-01-20-a-193616.png",
        "capture-decran-2021-01-20-a-193616.png",
        493,
        598,
        "#e9e9e9"
      ],
      "caption": "Bank Statement key data extraction"
    }
  ]
}
[/block]
  * **Full name**: The full name of the client 
  *  **Address**: The address of the client  
  *  **Account Number**: The account number 
  *  **Opening Balance**: The opening balance of the account at the beginning of the month 
  *  **Closing Balance**: The closing balance of the account at the end of the month
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/20/bank-details-us-2.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9a87315-Capture_decran_2021-04-09_a_13.51.20.png",
        "Capture d’écran 2021-04-09 à 13.51.20.png",
        1117,
        447,
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
        "https://files.readme.io/5ce3010-Capture_decran_2021-04-09_a_10.53.08.png",
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"full_name\",\n          \"public_name\": \"Full name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"address\",\n          \"public_name\": \"Address\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": 0, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"account_number\",\n          \"public_name\": \"Account Number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"opening_balance\",\n          \"public_name\": \"Opening Balance\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"closing_balance\",\n          \"public_name\": \"Closing Balance\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"full_name\",\n        \"address\",\n        \"account_number\",\n        \"opening_balance\",\n        \"closing_balance\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Full name**: type String that never contains numeric characters.
  * **Address**: type String without specifications. 
  * **Account Number**: type String with no alpha characters.
  * **Opening Balance**: type Number without specifications. 
  * **Closing Balance**: type Number without specifications. 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1fd90d2-Capture_decran_2021-04-09_a_13.59.21.png",
        "Capture d’écran 2021-04-09 à 13.59.21.png",
        1123,
        640,
        "#fbfbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Bank Statement OCR
 

 


 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7a704b3-Capture_decran_2021-04-09_a_13.55.35.png",
        "Capture d’écran 2021-04-09 à 13.55.35.png",
        1303,
        767,
        "#eeeff1"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
You’re all set! 

 

Now is the time to train your Bank Statement deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Bank statements in your application.


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!