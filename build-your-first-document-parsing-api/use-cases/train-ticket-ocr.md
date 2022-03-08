---
title: Train Ticket OCR
excerpt: ''
hidden: false
---
This article shows you how to build an OCR API that extracts data from train tickets (or eTickets) using our deep learning engine. It will work for any train ticket format or template, paper or digital. Improve your workflow by extracting data directly from your train ticket documents. 

 

 

**Prerequisites**
> 1. You’ll need a free account.  [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 train ticket images or PDFs to train your OCR.
 

 

## Define your Train Ticket use case
 

First, we’re going to define the fields we'd like to extract from our **train tickets**. 



[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e466d43-aaa.png",
        "aaa.png",
        761,
        444,
        "#e7e8e8"
      ],
      "caption": "Train ticket key data extraction"
    }
  ]
}
[/block]

  * **Passenger name**: The full name of the passenger traveling (Jane Martin)
  *  **Reservation number**: The reservation number of your train ticket  (925D90)
  *  **Departure Date**: The date of departure 
  *  **Departure station code**: The 3 letters identification code for your departure station  (WAS)
  *  **Arrival station code**: The 3 letters identification code for your arrival station  (NYP)
  *  **Departure Time**: The train departure time from the departure station (01:50 PM)

 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements.

## Deploy your API
 

Once you have defined all of the fields you want to extract, head over to the platform and press the ‘**create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/20/train-ticket.jpeg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/facee82-Capture_decran_2021-03-29_a_14.04.34.png",
        "Capture d’écran 2021-03-29 à 14.04.34.png",
        1149,
        559,
        "#f5f6f8"
      ],
      "caption": "Set up your model"
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
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"passenger_name\",\n          \"public_name\": \"Passenger name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"reservation_number\",\n          \"public_name\": \"Reservation number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"departure_date\",\n          \"public_name\": \"Departure Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"departure_station_code\",\n          \"public_name\": \"Departure Station Code\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"arrival_station_code\",\n          \"public_name\": \"Arrival Station Code\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"departure_time\",\n          \"public_name\": \"Departure Time\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"passenger_name\",\n        \"reservation_number\",\n        \"departure_date\",\n        \"departure_station_code\",\n        \"arrival_station_code\",\n        \"departure_time\"\n      ]\n    }\n  }\n}\n",
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
        "https://files.readme.io/638a683-capture-decran-2021-03-29-a-135333.png",
        "capture-decran-2021-03-29-a-135333.png",
        1152,
        580,
        "#fafbfc"
      ],
      "caption": "Define your model"
    }
  ]
}
[/block]
  *  **Passenger name**: String type that never contains numeric characters.
  *  **Reservation number**: String type without specifications. 
  *  **Departure Date**: Date type with US format.
  *  **Departure Station** Code: String type that never contains numeric characters.
  *  **Arrival Station** Code: type String that never contains numeric characters.
  *  **Departure Time**: type String without specifications.
  

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ff197b3-Capture_decran_2021-03-29_a_14.07.47.png",
        "Capture d’écran 2021-03-29 à 14.07.47.png",
        1157,
        677,
        "#f9fafc"
      ],
      "caption": "Data model ready to train"
    }
  ]
}
[/block]
## Train your Boarding Pass OCR
 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/83378ba-Capture_decran_2021-03-29_a_14.09.41.png",
        "Capture d’écran 2021-03-29 à 14.09.41.png",
        1369,
        989,
        "#c9cdd2"
      ],
      "caption": "Train your train ticket OCR"
    }
  ]
}
[/block]
 

 

 

You’re all set! 

 

Now is the time to train your train ticket deep learning model in the Training section of your API. 

 

In a few hours (minutes if you're swift), you’ll get your first model trained and will be able to use your custom OCR API for parsing train tickets in your application.

 

To get more information about the training phase, please refer to the [Getting Started tutorial](doc:build-your-first-document-parsing-api).

If you have any questions regarding your use case, feel free to reach out on the chat!