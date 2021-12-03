---
title: French Payslips OCR
excerpt: ''
---
This article explains how to build an OCR API that automatically extracts data from French payslips (bulletins de salaire). 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 French payslips images or PDFs to train your OCR.

## Define your French payslips use case
 

First, we need to specify the fields we want to extract from our payslips.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/95d02b5-image-44.png",
        "image-44.png",
        536,
        791,
        "#edede2"
      ],
      "caption": "French payslip key data extraction"
    }
  ]
}
[/block]

For our example, we are going to extract the following list of fields from our French payslips:

 

  *  **Employee full name**: First and last names of the employee
  *  **Employee SSN**: Employee social security number
  *  **Employer SIRET**: Employer SIRET number 
  *  **Payslip period**:  Payslip month and year 
  *  **Net paid**: Total net paid 
  *  **Gross salary**: Total gross salary before taxes
 

Feel free to add any data you'd like the OCR to extract.


## Deploy your API
 

Once you have defined the fields you want to extract, head over to the platform and press the ‘**create a new API**’ button.

 
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/18/fiche-de-paie-2020.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/430b439-Capture_decran_2021-03-29_a_13.37.19.png",
        "Capture d’écran 2021-03-29 à 13.37.19.png",
        1123,
        557,
        "#f5f6f8"
      ],
      "caption": "Setup your model"
    }
  ]
}
[/block]
 

We're ready! Press the “**next**” button. We are going to build our data model in the next section.


 

To move forward, you have two possibilities:

**Upload a json config**
Copy the following JSON into a file and upload it on the interface

 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"employee_full_name\",\n          \"public_name\": \"Employee Full Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"employee_ssn\",\n          \"public_name\": \"Employee SSN\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"company_siret\",\n          \"public_name\": \"Company SIRET\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"FR\" } },\n          \"handwritten\": false,\n          \"name\": \"payslip_period\",\n          \"public_name\": \"Payslip period\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"net_paid\",\n          \"public_name\": \"Net Paid\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"gross_salary\",\n          \"public_name\": \"Gross salary\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"employee_full_name\",\n        \"employee_ssn\",\n        \"company_siret\",\n        \"payslip_period\",\n        \"net_paid\",\n        \"gross_salary\"\n      ]\n    }\n  }\n}\n",
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
        "https://files.readme.io/6c553db-Capture_decran_2021-03-29_a_13.37.30.png",
        "Capture d’écran 2021-03-29 à 13.37.30.png",
        1123,
        557,
        "#fafafc"
      ],
      "caption": "Upload JSON or manually set up your API"
    }
  ]
}
[/block]
 
In our example, here are the different field configurations we used:


  *  **Employee full name**: type String with no numeric characters
  *  **Employee SSN**: type String. Note that we haven't checked the "It never contains alpha characters" as social security numbers can contain 'a' or 'b' for Corsican.
  *  **Employer company SIRET**: type String that never contains alpha characters.
  *  **Payslip period**: type Date 
  *  **Net paid**: type Amount
  *  **Gross salary**: type Amount



You are now ready to train your model!

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/de94b6b-Capture_decran_2021-03-29_a_13.41.38.png",
        "Capture d’écran 2021-03-29 à 13.41.38.png",
        1133,
        797,
        "#fafbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Payslip OCR
 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f95859a-Capture_decran_2021-03-29_a_13.42.51.png",
        "Capture d’écran 2021-03-29 à 13.42.51.png",
        1376,
        997,
        "#edeef1"
      ],
      "caption": "Training your payslip API"
    }
  ]
}
[/block]
 

You’re all set! 

 

Now is the time to train your custom Payslip deep learning model. To get more information about the training phase, please refer to the [Getting Started tutorial](doc:build-your-first-document-parsing-api). And if you have any questions regarding your use case, feel free to reach out to us on our chat!