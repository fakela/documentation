---
title: 1040 Forms OCR
excerpt: ''
hidden: false
---
This article describes how to build an OCR API that extracts data from 1040 Forms using our deep learning engine. If you want to automate your workflow, this article is for you. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 1040 Form images or pdfs to train your OCR.

## Define your 1040 Forms use case
 

First, we’re going to define what fields we want to extract from your **1040 Forms. **

 

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/741658c-capture-decran-2021-01-25-a-144018.png",
        "capture-decran-2021-01-25-a-144018.png",
        448,
        591,
        "#e0ebeb"
      ],
      "caption": ""
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/502df61-capture-decran-2021-01-25-a-144023.png",
        "capture-decran-2021-01-25-a-144023.png",
        448,
        591,
        "#e3eeed"
      ],
      "caption": "1040 form key data extraction"
    }
  ]
}
[/block]
 

  * **First Name**: The First name and middle name initial of the taxpayer. 
  *  **Last Name**: The Last name of the taxpayer. 
  * **Spouse First Name**: The First name and middle name initial of the taxpayer's spouse. 
  *  **Spouse Last Name**: The Last name of the taxpayer's spouse. 
  *  **SSN**: The Social Security Number of the taxpayer. 
  *  **Spouse SSN**: The Social Security Number of the taxpayer's spouse. 
  *  **Salary**: The taxpayer's wages, salaries, tips, etc.
  *  **Ordinary Dividends**: The taxpayer's ordinary dividends (3b)
  *  **Occupation**: The taxpayer's occupation. 
  *  **Spouse Occupation**: The taxpayer's spouse's occupation. 
  *  **Identity Protection PIN**: The taxpayer's identity protection PIN provided by the IRS.
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements. 

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract from your 1040 forms, head over to the platform and press the ‘**Create a new API**’ button.
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/25/2020-form-1040.pdf\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e7c72eb-Capture_decran_2021-04-09_a_14.47.42.png",
        "Capture d’écran 2021-04-09 à 14.47.42.png",
        1124,
        452,
        "#f2f6f7"
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
        "https://files.readme.io/1ba314b-Capture_decran_2021-04-09_a_14.47.47.png",
        "Capture d’écran 2021-04-09 à 14.47.47.png",
        1124,
        452,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"first_name\",\n          \"public_name\": \"First Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"last_name\",\n          \"public_name\": \"Last Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"spouse_first_name\",\n          \"public_name\": \"Spouse First Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"spouse_last_name\",\n          \"public_name\": \"Spouse Last Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"ssn\",\n          \"public_name\": \"SSN\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"spouse_ssn\",\n          \"public_name\": \"Spouse SSN\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"salary\",\n          \"public_name\": \"Salary\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"ordinary_dividends\",\n          \"public_name\": \"Ordinary Dividends\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"occupation\",\n          \"public_name\": \"Occupation\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"spouse_occupation\",\n          \"public_name\": \"Spouse Occupation\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"identity_protection_pin\",\n          \"public_name\": \"Identity Protection PIN\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"first_name\",\n        \"last_name\",\n        \"spouse_first_name\",\n        \"spouse_last_name\",\n        \"ssn\",\n        \"spouse_ssn\",\n        \"salary\",\n        \"ordinary_dividends\",\n        \"occupation\",\n        \"spouse_occupation\",\n        \"identity_protection_pin\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **First Name**: type String that never contains numeric characters. 
  * **Last Name**: type String that never contains numeric characters. 
  * **Spouse First Name**: type String that never contains numeric characters. 
  * **Spouse Last Name**: type String that never contains numeric characters. 
  * **SSN**: type Number without specifications. 
  * **Spouse SSN**: type Number without specifications. 
  * **Salary**: type Number without specifications. 
  * **Ordinary Dividends**: type Number without specifications. 
  * **Occupation**: type String that never contains numeric characters. 
  * **Spouse Occupation**: type String that never contains numeric characters. 
  * **Identity Protection PIN**: type Number without specifications. 
  

 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a535bcd-Capture_decran_2021-04-09_a_14.49.44.png",
        "Capture d’écran 2021-04-09 à 14.49.44.png",
        1130,
        636,
        "#fbfbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 


 
 
## Train your 1040 forms OCR
 

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3b808d2-Capture_decran_2021-04-09_a_14.51.29.png",
        "Capture d’écran 2021-04-09 à 14.51.29.png",
        1315,
        769,
        "#eff3f4"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

Now is the time to train your 1040 form deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing 1040 forms in your application.

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!