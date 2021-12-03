---
title: Electricity Bill OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Electricity Bills using our deep learning engine. It will work for any bank company or bank statement template. 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Electricity Bill images or pdfs to train your OCR.

## Define your Electricity Bill use case
 

First, we’re going to define what fields we want to extract from your **Electricity Bill**. 



 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c52acfc-jjj.png",
        "jjj.png",
        463,
        596,
        "#ebeef0"
      ],
      "caption": "Electricity bill key data extraction"
    }
  ]
}
[/block]
  *  **Electricity Provider**: The electricity provider name
  *  **Customer Name**: The full name of the customer 
  *  **Account Number**: The account number of the client  
  *  **Bill Date**: The bill issued date 
  *  **Amount**: The total due for this month 
  *  **Phone number**: The customer's phone number
  *  **Service Address**: The customer's address related to the electricity bill
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.

 
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/21/electricity-bill.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7664f2e-Capture_decran_2021-04-09_a_11.00.36.png",
        "Capture d’écran 2021-04-09 à 11.00.36.png",
        1130,
        450,
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
        "https://files.readme.io/a815aec-Capture_decran_2021-04-09_a_11.00.43.png",
        "Capture d’écran 2021-04-09 à 11.00.43.png",
        1130,
        450,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"electricity_provider\",\n          \"public_name\": \"Electricity provider\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"customer_name\",\n          \"public_name\": \"Customer name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": 0, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"account_number\",\n          \"public_name\": \"Account Number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"bill_date\",\n          \"public_name\": \"Bill Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"amount_due\",\n          \"public_name\": \"Amount Due\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"handwritten\": false,\n          \"name\": \"phone_number\",\n          \"public_name\": \"Phone Number\",\n          \"semantics\": \"phone\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"service_address\",\n          \"public_name\": \"Service address\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"electricity_provider\",\n        \"customer_name\",\n        \"account_number\",\n        \"bill_date\",\n        \"amount_due\",\n        \"phone_number\",\n        \"service_address\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Electricity provider**: type String that never contains numeric characters.
  * **Customer name**: type String that never contains numeric characters.
  * **Account Number**: type String that never contains alpha characters. 
  * **Bill Date**: type Date with US format.  
  * **Amount Due**: type Number without specifications. 
  * **Phone Number**: type Phone Number. 
  * **Service address**: type String without specifications. 
  
 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7e2d3a0-Capture_decran_2021-04-09_a_11.02.12.png",
        "Capture d’écran 2021-04-09 à 11.02.12.png",
        1136,
        649,
        "#fbfbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Electricity Bill OCR
 

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2039c75-Capture_decran_2021-04-09_a_11.05.09.png",
        "Capture d’écran 2021-04-09 à 11.05.09.png",
        1324,
        776,
        "#ebedf0"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your Electricity Bill deep learning model in the Training section of our API. 

 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Electricity Bill in your application.

 

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!