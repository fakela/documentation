---
title: Bus Ticket OCR
excerpt: ''
hidden: false
---
This article walks you through the building process of an OCR API that extracts data from Bus Ticket using our deep learning engine. It will work for any bus company.

 

 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Bus Ticket images or pdfs to train your OCR.
 

 

## Define your Bus Ticket use case
 

First, we’re going to define what fields we want to extract from your **Bus Ticket**. 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/39a80f3-capture-decran-2021-01-20-a-172506.png",
        "capture-decran-2021-01-20-a-172506.png",
        422,
        467,
        "#dcdbe0"
      ],
      "caption": "Bus ticket key data extraction"
    }
  ]
}
[/block]

  *  **Bus Company**: The name of the company that sold the ticket (megabus.com)
  *  **Reservation Number**: The reservation number that will be asked when you board the bus (67-2722-033018-M10R-1415-LAS-ANA)
  *  **Date**: The date of departure (March 30, 2018)
  *  **Departure city**: The city of departure for your travel by bus (Las Vegas)
  *  **Arrival city**: The city of destination (Anaheim)
  *  **Departure Time**: The bus departure time from the departure city (2:15 PM)
  *  **Price**: The total amount paid for the bus ticket ($41,75)
 

 

That’s it for our use case, but you are free to add any other relevant data to fit your requirements.

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract, head over to the platform and press the ‘**create a new API**’ button.

 
[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/20/megabus.jpeg\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d660c46-Capture_decran_2021-04-07_a_14.49.55.png",
        "Capture d’écran 2021-04-07 à 14.49.55.png",
        1635,
        519,
        "#f9fafb"
      ],
      "caption": "Set up your API"
    }
  ]
}
[/block]
Once you’re ready, click on the “**next**” button. We are going to specify the data types for each of the fields we want our API to extract from your bus ticket.

 


 

To move forward, you have two possibilities:

**Upload a json config**
Copy the following JSON into a file and upload it on the interface

 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"bus_company\",\n          \"public_name\": \"Bus company\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"reservation_number\",\n          \"public_name\": \"Reservation number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date\",\n          \"public_name\": \"Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"departure_city\",\n          \"public_name\": \"Departure city\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"arrival_city\",\n          \"public_name\": \"Arrival city\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"departure_time\",\n          \"public_name\": \"Departure Time\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"price\",\n          \"public_name\": \"Price\",\n          \"semantics\": \"amount\"\n        }\n      ],\n      \"features_name\": [\n        \"bus_company\",\n        \"reservation_number\",\n        \"date\",\n        \"departure_city\",\n        \"arrival_city\",\n        \"departure_time\",\n        \"price\"\n      ]\n    }\n  }\n}\n",
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
        "https://files.readme.io/976e6de-Capture_decran_2021-04-07_a_14.50.07.png",
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
  *  **Bus company**: type String that never contains numeric characters.
  *  **Reservation number**: type String without specifications. 
  *  **Date**: type String without specifications.
  *  **Departure city**: type String that never contains numeric characters.
  *  **Arrival city**: type String that never contains numeric characters.
  *  **Departure Time**: type String without specifications. 
  *  **Price**: type Number without specifications. 



 

Once you’re done setting up your bus ticket data model, press the **Start training your model** button at the bottom of the screen.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/889ee92-Capture_decran_2021-04-07_a_14.54.59.png",
        "Capture d’écran 2021-04-07 à 14.54.59.png",
        1198,
        613,
        "#fafbfc"
      ],
      "caption": "Model ready to train"
    }
  ]
}
[/block]
 
## Train your Bus Ticket OCR
 

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/deff4c7-Capture_decran_2021-04-07_a_14.56.55.png",
        "Capture d’écran 2021-04-07 à 14.56.55.png",
        1639,
        924,
        "#e0e2e5"
      ],
      "caption": "Training your model"
    }
  ]
}
[/block]

 

You’re all set! 

 

Now is the time to train your Bus ticket deep learning model in the Training section of our API. 

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing Bus Ticket in your application.

To get more information about the training phase, please refer to the [Getting Started tutorial](doc:build-your-first-document-parsing-api).

If you have any questions regarding your use case, feel free to reach out via our chat!