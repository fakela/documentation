---
title: Diploma OCR
excerpt: ''
---
Reading this article you'll be able to build an OCR API that extracts data from diploma using our deep learning engine.


**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 different diploma images or pdfs to train your OCR model

## Define your diploma prescription use case
 
First, we’re going to define what fields we want to extract from your **diploma**.

 

Here is the list of fields we are going to extract using our OCR API:

  * **Date**
  * **University name**: String which contains both numeric and alpha characters 
  * **Graduate name**: String which Only contains alpha characters
  * **Major**: String which only contains alpha characters
  * **Diploma number**: Amount 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f36d8ae-diplome-2.jpeg",
        "diplome-2.jpeg",
        3928,
        2704,
        "#bcb6a7"
      ],
      "caption": "Diploma key data extraction"
    }
  ]
}
[/block]
 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 
Once you have defined what fields you want to extract, head over to the platform and press the ‘**Create a new API**’ button.


 
You land now on the setup page. You can use any image you want for setting up the API, my setup looks like this:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9ac3638-Capture_decran_2021-04-08_a_21.42.02.png",
        "Capture d’écran 2021-04-08 à 21.42.02.png",
        941,
        471,
        "#f4f6f8"
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
        "https://files.readme.io/8c43f55-Capture_decran_2021-03-29_a_13.53.33.png",
        "Capture d’écran 2021-03-29 à 13.53.33.png",
        1152,
        580,
        "#fafbfc"
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date\",\n          \"public_name\": \"Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"university_name\",\n          \"public_name\": \"University Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"graduate_name\",\n          \"public_name\": \"Graduate Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"major\",\n          \"public_name\": \"Major\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"diploma_number\",\n          \"public_name\": \"Diploma Number\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"date\",\n        \"university_name\",\n        \"graduate_name\",\n        \"major\",\n        \"diploma_number\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  * **Date**: in European format
  * **University name**: String which contains both numeric and alpha characters
  * **Graduate name**: A name never contains numeric characters
  * **Major**: String which only contains alpha characters
  * **Diploma number**: Amount


Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a65d817-Capture_decran_2021-04-08_a_21.46.37.png",
        "Capture d’écran 2021-04-08 à 21.46.37.png",
        1013,
        570,
        "#f9fbfd"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 



 
 
## Train your diploma OCR
 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7c1e613-Capture_decran_2021-04-08_a_21.51.40.png",
        "Capture d’écran 2021-04-08 à 21.51.40.png",
        1203,
        595,
        "#dbdcdc"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

Now is the time to train your diploma deep learning model in the Training section of our API. You will soon be able to use your custom OCR API for diplomas! When you will reach at least 20 documents to train your model you will receive a confirmation email allowing your model to make predictions. 

To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!