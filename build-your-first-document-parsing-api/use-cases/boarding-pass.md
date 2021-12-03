---
title: Boarding Pass OCR
excerpt: ''
---
This article walks you through the building process of an OCR API that extracts data from Flight Boarding Passes using our deep learning engine. It will work for any airline company or boarding pass template. 

**Prerequisites** 
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Boarding Pass images or PDFs to train your OCR.

## Define your Boarding Pass use case
 

First, we’re going to define the fields we'd like to extract from a **Boarding Pass**. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/179518e-capture-decran-2021-01-20-a-143327.png",
        "capture-decran-2021-01-20-a-143327.png",
        779,
        405,
        "#e1c8c7"
      ],
      "caption": "Boarding pass key data extraction"
    }
  ]
}
[/block]
 

  *  **Passenger name**: The full name of the travelling passenger (John Doe)
  *  **Flight number**: The flight number for the boarding pass, including the airline's identification letters (AC 2505)
  *  **Date**: The date of departure in US format (10/12/2017)
  *  **Departure airport**: The airport of departure including the airport identification letters (New Delhi DEL)
  * **Destination airport**: The airport of destination including the airport identification letters (Los Angeles LAX)
  *   **Boarding Time**: The boarding time (07:45)

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

##Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**create a new API**’ button.
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/20/https___prodstatic9netau___media_2018_04_19_10_39_boardingpass.jpg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/788e675-Capture_decran_2021-03-29_a_13.53.25.png",
        "Capture d’écran 2021-03-29 à 13.53.25.png",
        1152,
        580,
        "#f3eff1"
      ],
      "caption": "Set up your API"
    }
  ]
}
[/block]
 Once you’re ready, press the “next” button, and let's specify the data types for each of the fields we want our API to extract.

To move forward, you have two possibilities:

**Upload a json config**
Copy the following JSON into a file and upload it on the interface
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"passenger_name\",\n          \"public_name\": \"Passenger Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"flight_number\",\n          \"public_name\": \"Flight number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date\",\n          \"public_name\": \"Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"departure_airport\",\n          \"public_name\": \"Departure airport\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"destination_airport\",\n          \"public_name\": \"Destination airport\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": 0, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"boarding_time\",\n          \"public_name\": \"Boarding Time\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"passenger_name\",\n        \"flight_number\",\n        \"date\",\n        \"departure_airport\",\n        \"destination_airport\",\n        \"boarding_time\"\n      ]\n    }\n  }\n}\n",
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
        "https://files.readme.io/9f39399-Capture_decran_2021-03-29_a_13.53.33.png",
        "Capture d’écran 2021-03-29 à 13.53.33.png",
        1152,
        580,
        "#fafbfc"
      ],
      "caption": "Build manually your data model"
    }
  ]
}
[/block]
> **Passenger name**: type String that never contains numeric characters.
> **Flight number**: type String without specifications. 
> **Date**: type Date with US format order.
> **Departure airport**: type String that never contains numeric characters.
> **Destination airport**: type String that never contains numeric characters.
> **Boarding Time**: type String that never contains alpha characters

 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7f7b56e-Capture_decran_2021-03-29_a_13.56.24.png",
        "Capture d’écran 2021-03-29 à 13.56.24.png",
        1153,
        673,
        "#f9fafc"
      ],
      "caption": "Data model ready"
    }
  ]
}
[/block]
 

## Train your Boarding Pass OCR model
 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/485c0e2-Capture_decran_2021-03-29_a_13.57.26.png",
        "Capture d’écran 2021-03-29 à 13.57.26.png",
        1380,
        933,
        "#cacace"
      ],
      "caption": "Data model training"
    }
  ]
}
[/block]
 

 

 

Now is the time to train your Boarding Pass deep learning model in the Training section of your API. 

 

 

In a few hours (minutes if you're expeditious), you’ll get your first model trained and will be able to use your custom OCR API for parsing Boarding Passes in your application.

 

To get more information about the training phase, please refer to the [Getting Started tutorial](doc:build-your-first-document-parsing-api).

If you have any questions regarding your use case, feel free to reach out on the chat!