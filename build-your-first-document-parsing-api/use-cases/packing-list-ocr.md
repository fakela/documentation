---
title: Packing List OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Packing List forms using our deep learning engine. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Packing List images or pdfs to train your OCR.

## Define your Packing List use case
 

First, we’re going to define what fields we want to extract from your **Packing List**. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fbd28c2-iiii.png",
        "iiii.png",
        428,
        596,
        "#eeeded"
      ],
      "caption": "Packing list key data extraction"
    }
  ]
}
[/block]
  *  **Exporter**: The name of the exporter
  *  **Exporter address**: The exporter's address 
  *  **Consignee**: The consignee's name
  *  **Consignee Address**: The consignee's address where the package must be delivered
  *  **Consignee Phone Number**: The consignee's phone number
  *  **Method of dispatch**: how the package is carried (sea)
  *  **Export Invoice Date**: Issue date of the export invoice
  *  **Export Invoice Number**: Identification number of the export invoice
  *  **Country of Origin**: where the package comes from 
  *  **Country of Final Destination**: the package final destination 
  *  **Total Weight**: total weight of package carried 
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/22/packing-list.png\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cb318d7-Capture_decran_2021-04-09_a_10.35.53.png",
        "Capture d’écran 2021-04-09 à 10.35.53.png",
        1125,
        447,
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
        "https://files.readme.io/4e4cc88-Capture_decran_2021-04-09_a_10.36.01.png",
        "Capture d’écran 2021-04-09 à 10.36.01.png",
        1125,
        447,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"exporter_name\",\n          \"public_name\": \"Exporter Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"exporter_address\",\n          \"public_name\": \"Exporter Address\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"consignee_name\",\n          \"public_name\": \"Consignee Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"consignee_address\",\n          \"public_name\": \"Consignee Address\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"handwritten\": false,\n          \"name\": \"consignee_phone_number\",\n          \"public_name\": \"Consignee phone number\",\n          \"semantics\": \"phone\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"method_of_dispatch\",\n          \"public_name\": \"Method of Dispatch\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"export_invoice_date\",\n          \"public_name\": \"Export Invoice Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"export_invoice_number\",\n          \"public_name\": \"Export Invoice Number\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"country_of_origin\",\n          \"public_name\": \"Country of Origin\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"country_of_final_destination\",\n          \"public_name\": \"Country of Final Destination\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"total_weight\",\n          \"public_name\": \"Total Weight\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"exporter_name\",\n        \"exporter_address\",\n        \"consignee_name\",\n        \"consignee_address\",\n        \"consignee_phone_number\",\n        \"method_of_dispatch\",\n        \"export_invoice_date\",\n        \"export_invoice_number\",\n        \"country_of_origin\",\n        \"country_of_final_destination\",\n        \"total_weight\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

 

  * **Exporter Name**: type String that never contains numeric characters.
  * **Exporter Address**: type String without specifications.  
  * **Consignee Name**: type String that never contains alpha characters. 
  * **Consignee Address**: type String without specifications. 
  * **Consignee phone number**: type Phone Number. 
  * **Method of Dispatch**: type String that never contains alpha characters. 
  * **Export Invoice Date**: type Date with US format. 
  * **Export Invoice Number**: type Number without specifications
  * **Country of Origin**: type String that never contains numeric characters. 
  * **Country of Final Destination**: type String that never contains numeric characters. 
  * **Total Weight**: type Number without specifications. 
  

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/73fa9de-Capture_decran_2021-04-09_a_10.38.34.png",
        "Capture d’écran 2021-04-09 à 10.38.34.png",
        1142,
        646,
        "#fbfbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Packing List OCR
 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3ffb428-Capture_decran_2021-04-09_a_10.40.02.png",
        "Capture d’écran 2021-04-09 à 10.40.02.png",
        1320,
        769,
        "#e7e8ea"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

You’re all set! 

 

Now is the time to train your Packing List deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Packing List in your application.


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!