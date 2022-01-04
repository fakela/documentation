---
title: Training
excerpt: ''
---
## How it works
 

 
[block:callout] { "type": "info", "body": "This section describes the training cycle of your deep learning algorithm." } [/block] 

### Create a dummy API 
 

First, we’re going to create a dummy API that illustrates the main phases of the training cycle.

1. Log in on the [Mindee-platform](https://platform.mindee.com). You'll land on the APIs hub page.
2. Click the **Create a new API** button. 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/69c0bd2-Screenshot_2021-12-22_at_05.05.22.png",
        "Screenshot_2021-12-22_at_05.05.22.png",
        1000,
        375,
        "#f5f8fa"
      ]
    }
  ]
}
[/block]

3. You'll land on the setup page. Here is the [train ticket](https://mindee-public-website-dev.s3.amazonaws.com/blog/2021/01/20/train-ticket.jpeg) used for setting up the API, and it looks like this:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8e140ab-train-setup.png",
        "train-setup.png",
        1000,
        375,
        "#f5f8fa"
      ]
    }
  ]
}
[/block]
 

4. Click on **Next**. We'll use the JSON upload to create the API. 

 [block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/da153c5-json-upload.png",
        "json-upload.png",
        1000,
        375,
        "#f5f8fa"
      ]
    }
  ]
}
[/block]

Copy the following JSON into a file and upload it on the interface.

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

Alternatively, you can build the data model manually:

- **Passenger name**: String type that never contains numeric characters.
- **Reservation number**: String type without specifications.
- **Departure Date**: Date type with US format (MM-DD-YYYY).
- **Departure Station Code**: String type that never contains numeric characters.
- **Arrival Station Code**: type String that never contains numeric characters.
- **Departure Time**: type String without specifications.


In this model, we have set up a field for each type. Once it’s done, it should looks like this

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4a95a22-rent1.png",
        "rent1.png",
        1000,
        450,
        "#fbfcfd"
      ]
    }
  ]
}
[/block]
 


5. Click on the **start training your model** button to begin the training phase.

 


## Training phase
 

Our API was deployed, and you land now on the training section.

 

Upload the [sample invoice image](https://mindee-public-website.s3.amazonaws.com/blog/2021/01/14/all_fields.jpg) into the document area:

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/dde4f40-screenshot-2021-04-25-at-212029.png",
        "screenshot-2021-04-25-at-212029.png",
        1000,
        546,
        "#d8dfe6"
      ]
    }
  ]
}
[/block]

 

Click on any field input in the form, you should see the blue boxes on your document changing.

 

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e540f4c-screen_recording_2021-04-25_at_212331_ketuqi-1.gif",
        "screen_recording_2021-04-25_at_212331_ketuqi-1.gif",
        1000,
        563,
        "#e3e9f0"
      ]
    }
  ]
}
[/block]
 

 

The blue boxes displayed on the document for each field are actually the *fields candidates*. For each field you set up in your data model, our engine will parse the potential candidates so that a user, you, or an automatic script can tell the model what candidate was actually the one you are looking for.

 

That’s what happens when you click on the validate button.

 

For example, let’s assume we are looking for the total amount of the invoice. 

 

When you hit the blue box corresponding to the total amount in the document, the color changes and the amount is filled in the field.

 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c13b265-screenshot-2021-04-25-at-215420.png",
        "screenshot-2021-04-25-at-215420.png",
        1000,
        592,
        "#dee5ec"
      ]
    }
  ]
}
[/block]
 



 

When you are going to press “validate”, you are going to tell the deep learning model that this green box was the one corresponding to the total amount. In other words, you are **teaching the model which candidate** is the total amount, and he’s going to learn to extract the right one on new samples.

 

At the very beginning, there is no trained model and calling the /predict endpoint will give you only the candidates for each field, no predictions.

 

Without any prediction, the /predict endpoint and the training cycle looks like this:

 

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ec0b526-pasted_image_0_1.png",
        "pasted image 0 (1).png",
        1279,
        571,
        "#eff6fa"
      ]
    }
  ]
}
[/block]
 

 

The /annotations endpoint is automatically called within the interface, but you can also use the API if you want to do this on your own interface.


 

### Model training
 

Once there are 20 data sent to the annotations endpoint, the training of your first model will start.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5015005-models.gif",
        "models.gif",
        1200,
        628,
        "#dadfe6"
      ]
    }
  ]
}
[/block]
 

Our deep learning engine will automatically generate and train a model based on the data you send, and a lot of extra features based on computer visions and natural language processing embeddings.

 

In a nutshell, the algorithm will take as inputs the image of each document as well as the whole text. It’s then going to be train based on your annotations to extract the right candidates for each field.

 

Once the model is trained, it’s going to be automatically deployed in your API, and you will see a **v1.1 ** version of your API appear in the documentation. A new [minor version](doc:prediction#versioning) is released every time a new model is deployed.

 

When you call the predict endpoint with a trained model, it will perform an inference before sending back the response:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/befbcf3-pasted_image_0_2.png",
        "pasted image 0 (2).png",
        1401,
        555,
        "#eef5f9"
      ]
    }
  ]
}
[/block]
 



 

 

If you want to dive deeper into our product, feel free to reach out to our data scientist team: contact@mindee.com
