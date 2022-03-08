---
title: Predict Endpoint
excerpt: ''
hidden: false
---
## How to use the Predict endpoint with Postman
 

### Objective
In the previous article, we reviewed how to set up Postman to use a Mindee API Builder API. Each custom API you build and deploy with Mindee has one endpoint: ```/predict```.

 

### Prerequisites
See previous article

 

### Endpoint overview
 

The ```/predict``` endpoint takes a document as an input and returns predictions (made by the backing machine learning model) of all fields as defined in your API data model.

 

### Calling the Predict endpoint
 

Let's set up the predict endpoint in Postman.  We'll begin by working our way across the various fields that must be populated. 

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6710a79-screenshot-2021-05-06-at-193435.png",
        "screenshot-2021-05-06-at-193435.png",
        1000,
        400,
        "#332d2c"
      ]
    }
  ]
}
[/block]
 

In the url Params section, we must add the version of the API.  On your Mindee dashboard, you'll see the API url has two version numbers.  For example:

```
https://api.mindee.net/v1/products/doug1/us_w_9_forms/v1/predict
```

The first v1 is the API version - this is version 1 of the document builder API.  The second version tells you the number of trainings that have occurred for this specific API: in this case one training has completed, so it is version 1 of the w-9 API.

 

In the params section of Postman, enter the version number of your training, In this case it is v1


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/008b490-screenshot-2021-05-06-at-194209.png",
        "screenshot-2021-05-06-at-194209.png",
        1000,
        389,
        "#2c2c2c"
      ]
    }
  ]
}
[/block]
The next section to populate is Authorization.  Here we'll choose "API Key" and enter a key we generated from our dashboard:

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9dade14-screenshot-2021-05-06-at-194836.png",
        "screenshot-2021-05-06-at-194836.png",
        1000,
        342,
        "#2f2e2e"
      ]
    }
  ]
}
[/block]
 

We will skip the header section, and move to the Body of the request.  Instead of "Text" we change the request to "File":

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d0fa0a5-screenshot-2021-05-06-at-205431.png",
        "screenshot-2021-05-06-at-205431.png",
        1000,
        347,
        "#302f30"
      ]
    }
  ]
}
[/block]
 

And then we'll pick a file that we'd like to test with, in this case the W-9 for Sirius Black:

 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3162a35-screenshot-2021-05-06-at-205726.png",
        "screenshot-2021-05-06-at-205726.png",
        1000,
        323,
        "#2f3133"
      ]
    }
  ]
}
[/block]
 

### You are set to test!
We've now set up our Postman instance to test and predict W-9 tax forms.  Clicking submit sends the W-9 to Mindee, and the result will contain the predictions:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d091b72-screenshot-2021-05-06-at-210502.png",
        "screenshot-2021-05-06-at-210502.png",
        1000,
        489,
        "#2c2c2c"
      ]
    }
  ]
}
[/block]
 



In the above screenshot, we see a 201 "Success" message, telling us that this JSON will have the w-9 predictions.

 

### Structure of the /predict endpoint response

To save space, we will not paste the entire response for the predict endpoint. The endpoint will make predictions for each page of the document (in this case, just one page) and then return the prediction:

 ```

"document": {

"annotations": {

"labels": []

},

"id": "c3b8d42c-8237-4ab1-a7e2-adb56115f750",

"inference": {

"finished_at": "2021-05-07T00:59:12+00:00",

"pages": [

{

"id": 0,

"prediction": {

  <the prediction for page 0>


}

],

"prediction": {

 < the predictions for the entire document>

} 
```

### Parameter predictions

Each parameter will have a prediction.  In this case, let's look at the name attribute:

 
```
"name": {
                    "confidence": 1.0,
                    "page_id": 0,
                    "values": [
                        {
                            "confidence": 1.0,
                            "content": "SIRIUS",
                            "polygon": [
                                [
                                    0.094,
                                    0.122
                                ],
                                [
                                    0.145,
                                    0.122
                                ],
                                [
                                    0.145,
                                    0.133
                                ],
                                [
                                    0.094,
                                    0.133
                                ]
                            ]
                        },
                        {
                            "confidence": 1.0,
                            "content": "BLACK",
                            "polygon": [
                                [
                                    0.154,
                                    0.122
                                ],
                                [
                                    0.202,
                                    0.122
                                ],
                                [
                                    0.202,
                                    0.133
                                ],
                                [
                                    0.154,
                                    0.133
                                ]
                            ]
                        }
                    ]
                },
```

 In the case of the name, the API found 2 words that fit the model, the words "Sirius" and "Black" (which is the correct response for this file.

 

Each value is given a confidence interval (both are 1.0 in this case, meaning that the model is 100% confident); the content value; and a polygon of 4 (x,y) coordinates that define the location in the document.

### Conclusion
We've now used our Postman instance of our Document Builder API to successfully test the API.  We submitted a document, and received a response back with the correctly extracted terms. Now we can use this Postman instance to quickly test and run our API.