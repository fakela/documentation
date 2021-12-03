---
title: Certificate of Origin OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Certificate of Origin using our deep learning engine. It will work for any bank company or bank statement template. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Certificate of Origin images or pdfs to train your OCR.

## Define your Certificate of Origin use case
 

First, we’re going to define what fields we want to extract from your **Certificate of Origin**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/10955e2-aa.png",
        "aa.png",
        432,
        556,
        "#e6e6e6"
      ],
      "caption": "Certificate of origin key data extraction"
    }
  ]
}
[/block]
  * **Agent Name**: The full name of the agent 
  *  **Name and Address of shipper**: The full name and address of the shipper  
  *  **Name and Address of consignee**: The full name and address of the consignee  
  *  **Package Weight**: The total package weight
  *  **Package Description**: The package description
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/21/certificate-of-origin.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/41237c6-Capture_decran_2021-04-08_a_22.02.31.png",
        "Capture d’écran 2021-04-08 à 22.02.31.png",
        904,
        445,
        "#f6f7f8"
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
        "https://files.readme.io/2b3c661-Capture_decran_2021-04-07_a_14.50.07.png",
        "Capture d’écran 2021-04-07 à 14.50.07.png",
        1635,
        519,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"agent_name\",\n          \"public_name\": \"Agent Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"name_and_address_of_shipper\",\n          \"public_name\": \"Name and Address of shipper\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"name_and_address_of_consignee\",\n          \"public_name\": \"Name and Address of consignee\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"package_weight\",\n          \"public_name\": \"Package weight\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"package_description\",\n          \"public_name\": \"Package Description\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"agent_name\",\n        \"name_and_address_of_shipper\",\n        \"name_and_address_of_consignee\",\n        \"package_weight\",\n        \"package_description\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Agent name**: type String that never contains numeric characters.
  * **Name and Address of shipper**: type String without specifications. 
  * **Name and Address of consignee**: type String without specifications. 
  * **Package weight**: type Number without specifications. 
  * **Package Description**: type String without specifications. 
  
 

 

Once you’re done setting up your data model, press the **Start training your model**  button at the bottom of the screen.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a0342f8-Capture_decran_2021-04-08_a_22.04.10.png",
        "Capture d’écran 2021-04-08 à 22.04.10.png",
        916,
        513,
        "#f9fafc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
## Train your Certificate of Origin OCR
 

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ec11106-Capture_decran_2021-04-08_a_22.06.32.png",
        "Capture d’écran 2021-04-08 à 22.06.32.png",
        1079,
        595,
        "#e3e4e8"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your Certificate of Origin deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Certificate of Origin in your application.

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!