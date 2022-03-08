---
title: Medical prescription OCR
excerpt: ''
hidden: false
---
Reading this article you'll be able to build an OCR API that extracts data from medical prescriptions using our deep learning engine.

 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 different medical prescription images or pdfs to train your OCR model
 

 

## Define your medical prescription use case

 
First, we’re going to define what fields we want to extract from your **medical prescription**.

Here is the list of fields we are going to extract using our OCR API:

 

  * **Date**
  * **Doctor's name** 
  * **Patient's name**
  * **Address**: Of the medical center
  * **Phone number**: Of the medical center
 

 



 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

 

## Deploy your API
 
Once you have defined what fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.


You land now on the setup page. You can use any image you want for setting up the API, my setup looks like this:
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4bc70cf-Capture_decran_2021-04-08_a_18.24.34.png",
        "Capture d’écran 2021-04-08 à 18.24.34.png",
        1105,
        502,
        "#f7f9fb"
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
        "https://files.readme.io/b64fb51-Capture_decran_2021-04-08_a_18.24.42.png",
        "Capture d’écran 2021-04-08 à 18.24.42.png",
        1105,
        502,
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"FR\" } },\n          \"handwritten\": false,\n          \"name\": \"date\",\n          \"public_name\": \"Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"doctor_s_name\",\n          \"public_name\": \"Doctor's name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"patient_s_name\",\n          \"public_name\": \"Patient's name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"medical_center_s_address\",\n          \"public_name\": \"Medical center's address\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"handwritten\": false,\n          \"name\": \"medical_center_s_phone_number\",\n          \"public_name\": \"Medical center's phone number\",\n          \"semantics\": \"phone\"\n        }\n      ],\n      \"features_name\": [\n        \"date\",\n        \"doctor_s_name\",\n        \"patient_s_name\",\n        \"medical_center_s_address\",\n        \"medical_center_s_phone_number\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:


  * **Date**: in European format
  * **Doctor's name**: A name never contains numeric characters
  * **Patient's name**: A name never contains numeric characters
  * **Medical center's address**: an address may contain both numeric and alpha characters
  * **Medical center's phone number**


 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e46e4b6-Capture_decran_2021-04-08_a_18.26.58.png",
        "Capture d’écran 2021-04-08 à 18.26.58.png",
        1114,
        581,
        "#fafafc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 

## Train your medical prescription OCR
 

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/24f2dc6-Capture_decran_2021-04-08_a_18.28.18.png",
        "Capture d’écran 2021-04-08 à 18.28.18.png",
        1304,
        771,
        "#e8eaee"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

 

You’re all set! 

 

 

Now is the time to train your medical prescription deep learning model in the Training section of our API. You will soon be able to use your custom OCR API for medical prescriptions! When you will reach at least 20 documents to train your model you will receive a confirmation email allowing your model to make predictions. 

 

 

To get more information about the training phase, please refer to the [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any questions regarding your use case, feel free to reach out on our chat!