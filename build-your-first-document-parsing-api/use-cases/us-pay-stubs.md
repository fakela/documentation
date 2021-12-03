---
title: US Pay Stubs OCR
excerpt: ''
---
This article lays out the process recommended to build an OCR API that extracts data from US pay stubs using Mindee's deep learning engine.

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 US pay stubs (images or PDFs) to train your OCR.
 
## Define your Pay Stub use case
 

You might need to automatically extract data from pay stubs to improve your user experience in payroll or loan eligibility workflows. This article will guide you over the few steps required to deploy your Pay Stubs data extraction API.

First, we’re going to define the fields we want to extract from your pay stubs.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/81108d3-pay_stub.png",
        "pay stub.png",
        696,
        766,
        "#f6f6f5"
      ],
      "caption": "Pay Stub key data extraction"
    }
  ]
}
[/block]
 

Here is the list of fields we are going to extract using our OCR API:


  *  **Employer**: The full name of the employer issuing the pay stub
  *  **Net pay**: Total net paid to the employee
  *  **Pay date**: Date of wage payment
  *  **Period beginning**: Pay stub start date
  *  **Period ending**: Pay stub end date
  *  **Gross pay**: Total gross pay before taxes and deductions
  *  **Total tax**: Total tax deducted
 
You can add as many relevant fields as you need to better fit your requirements.

## Deploy your API
 

Once you have defined what fields you want to extract, head over to the platform and press the ‘**create a new API**’ button.
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/18/pay_stub_example.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c5b2ca6-Capture_decran_2021-03-29_a_12.56.41.png",
        "Capture d’écran 2021-03-29 à 12.56.41.png",
        1146,
        556,
        "#f8f9fb"
      ],
      "caption": "Setup your model"
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"employer\",\n          \"public_name\": \"Employer\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"net_pay\",\n          \"public_name\": \"Net Pay\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"pay_date\",\n          \"public_name\": \"Pay Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": {} },\n          \"handwritten\": false,\n          \"name\": \"period_beg\",\n          \"public_name\": \"Period beg\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"period_end\",\n          \"public_name\": \"Period end\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"gross_pay\",\n          \"public_name\": \"Gross Pay\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"total_tax\",\n          \"public_name\": \"Total tax \",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"employer\",\n        \"net_pay\",\n        \"pay_date\",\n        \"period_beg\",\n        \"period_end\",\n        \"gross_pay\",\n        \"total_tax\"\n      ]\n    }\n  }\n}\n",
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
        "https://files.readme.io/e1f5cb2-Capture_decran_2021-03-29_a_13.00.38.png",
        "Capture d’écran 2021-03-29 à 13.00.38.png",
        1146,
        556,
        "#fafafc"
      ],
      "caption": "Manually set up your API"
    }
  ]
}
[/block]
In our example, here are the different field configurations we used:

  * **Employer**: type String 
  *  **Net pay**: type Amount
  *  **Pay date**: type Date
  *  **Period beginning**: type Date 
  *  **Period ending**: type Date
  *  **Gross pay**: type Amount
  *  **Total tax:** Total tax deducted

Your model is now ready to start training. 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/711ae02-Capture_decran_2021-03-29_a_13.04.31.png",
        "Capture d’écran 2021-03-29 à 13.04.31.png",
        1147,
        588,
        "#fbfbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 

 

## Train your Pay Stub OCR
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4aead70-Capture_decran_2021-03-29_a_13.12.35.png",
        "Capture d’écran 2021-03-29 à 13.12.35.png",
        1892,
        997,
        "#eff0f2"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]


 

You’re all set! 

 

Now is the time to train your US Pay Stub deep learning model in the Training section of your API. 

 

To get more information about the training phase, please refer to the [Getting Started tutorial](doc:build-your-first-document-parsing-api) .

If you have any questions regarding your use case, feel free to reach out on the chat!