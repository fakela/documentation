---
title: Numbers
excerpt: ''
---
## Set up a number field
 

You want to extract either an amount, a float number or a list of numeric characters from your documents?

 

You can do that with the API Builder by creating a number field in the Data Model configuration step. 
[Data model configuration](doc:data-model-configuration) 
 

This section will walk you through the implications of setting up a number field and the different parameters you can specify.

 

### Prerequisites


1. You’ll need a free platform account. [Sign up](https://platform.mindee.com) and confirm your email to login.


### Let’s get started! 


After giving a name, description and cover image to your new API, you should land on the following page:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ddfea62-e26135d-screenshot-2021-04-25-at-193740.png",
        "e26135d-screenshot-2021-04-25-at-193740.png",
        1000,
        465,
        "#fbfcfd"
      ]
    }
  ]
}
[/block]
 


Build a number field by selecting the number icon on the right side of the screen.

 

### Additional parameters


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/de9fc91-numbers.png",
        "numbers.png",
        1000,
        1138,
        "#c0c6d0"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]
If you have additional context about this specific field or how the information is usually displayed in your documents, you can specify it during the field set up.

 

#### Feed parameters through UI
 

Through the UI, you may enable a checkbox:

 
* **It is always an integer**. By checking this, the engine will never be able to predict as a correct value a number that cannot be parsed as an integer
 
 
#### Feed parameters through config.json file
 

You may want to create a number field through by uploading a config.json file. 

 

You may fill in the cfg objects in your config.json file with the following parameter:



**is_integer** : Is the number or amount an integer

* possible values: -1 means sometimes; 1 means always

* default value: -1

 

A valid entry for a number field in a config.json should look like this:

 
```
{
  "cfg": {
    "is_integer": -1
  },
  "handwritten": false,
  "name": "rating",
  "semantics": "amount",
  "public_name": "rating"
}
```
 
 

### Impact for training and making predictions
 


By specifying the data type as Number, you will force the engine to only consider words and series of words that can be interpreted as numbers or amounts as eligible candidates.

 
[block:callout]
{
  "type": "warning",
  "body": "This means that, for this specific field, we will never be able to extract any information in your document that cannot be interpreted as an amount or a number."
}
[/block]


 

#### Text parsed
 

Anything that can be read an amount or a number.

 

Ex: “1,000,876.93”, “12” and “$98.78” are Numbers

 

Amounts or numbers written with alpha characters are not parsed as Numbers.

 

Ex: “fifteen” or “two hundred and twelve” are not parsed as Numbers.

 

If the information you are looking for is sometimes displayed as such, you should use a String field.

​