---
title: W9 forms OCR
excerpt: ''
---
This article describes how to build an OCR API that extracts data from W9 forms using our deep learning engine. If you want to automate your bank workflow, this article is for you. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 W9 images or pdfs to train your OCR.

## Define your W9 use case
 

First, we’re going to define what fields we want to extract from your **W9**. 


![capture-decran-2021-01-25-a-120927.png](images/0807a15-capture-decran-2021-01-25-a-120927.png)
W9 form key data extraction

  * **Name**: The taxpayer's name. 
  *  **Address**: The taxpayer's mailing address (number, street, and apt)
  *  **City**: The taxpayer's city.
  *  **State**: The taxpayer's state. 
  *  **Zip Code**: The taxpayer's zip code.
  *  **Date**: The date the W9 was filled.
  *  **Employer ID**: The employer identification number.
 

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements. 

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract from your W9, head over to the platform and press the ‘**Create a new API**’ button.

 

<div class="magic-block-html">
    You land now on the setup page. <a 
      href="https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/25/w-9.png"
      target="_blank">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:
</div>


![Capture d’écran 2021-04-09 à 14.39.43.png](images/2323247-Capture_decran_2021-04-09_a_14.39.43.png)
Set up your model

Once you’re ready, click on the “**next**” button. We are going to specify the data types for each of the fields we want our API to extract.


![Capture d’écran 2021-04-09 à 14.39.48.png](images/c4174a1-Capture_decran_2021-04-09_a_14.39.48.png)
Define your model

To move forward, you have two possibilities:

**Upload a json config**
Copy the following JSON into a file and upload it on the interface


```json
{
  "problem_type_": {
    "classificator": { "features": [], "features_name": [] },
    "selector": {
      "features": [
        {
          "cfg": { "filter": { "alpha": -1, "numeric": 0 } },
          "handwritten": false,
          "name": "name",
          "public_name": "Name",
          "semantics": "word"
        },
        {
          "cfg": { "filter": { "alpha": -1, "numeric": -1 } },
          "handwritten": false,
          "name": "address",
          "public_name": "Address",
          "semantics": "word"
        },
        {
          "cfg": { "filter": { "alpha": -1, "numeric": 0 } },
          "handwritten": false,
          "name": "city",
          "public_name": "City",
          "semantics": "word"
        },
        {
          "cfg": { "filter": { "alpha": -1, "numeric": 0 } },
          "handwritten": false,
          "name": "state",
          "public_name": "State",
          "semantics": "word"
        },
        {
          "cfg": { "filter": { "is_integer": -1 } },
          "handwritten": false,
          "name": "zip_code",
          "public_name": "Zip Code",
          "semantics": "amount"
        },
        {
          "cfg": { "filter": { "convention": "US" } },
          "handwritten": false,
          "name": "date",
          "public_name": "Date",
          "semantics": "date"
        },
        {
          "cfg": { "filter": { "is_integer": -1 } },
          "handwritten": true,
          "name": "employer_id",
          "public_name": "Employer ID",
          "semantics": "amount"
        }
      ],
      "features_name": [
        "name",
        "address",
        "city",
        "state",
        "zip_code",
        "date",
        "employer_id"
      ]
    }
  }
}
```


**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

  *   **Name**: type String that never contains numeric characters. 
  * **Address**: type String without specifications.
  * **City**: type String that never contains numeric characters. 
  * **State**: type String that never contains numeric characters. 
  * **Zip Code**: type Number without specifications.
  * **Date**: type Date with US format. 
  * **Employer ID:** type Number without specifications. 
 
 

 

Once you’re done setting up your data model, press the **Start training your model** button at the top of the screen.

 

![Capture d’écran 2021-04-09 à 14.41.00.png](images/5ffd015-Capture_decran_2021-04-09_a_14.41.00.png)
Ready to train model

 
 
## Train your W9 OCR
 

 


 
![Capture d’écran 2021-04-09 à 14.42.35.png](images/0674e79-Capture_decran_2021-04-09_a_14.42.35.png)
Train your W9 model

 

You’re all set! 

 

Now is the time to train your W9 deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing W9 forms in your application.

 To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!