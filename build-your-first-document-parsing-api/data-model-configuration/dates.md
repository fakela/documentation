---
title: Dates
excerpt: ''
hidden: false
---
## Set up a date field


You want to extract a date from your documents?



You can do that with the API Builder by creating a **Date** field in the [Data model configuration](doc:data-model-configuration) step.



This section will walk you through the implications of setting up a **Date** field.



### Prerequisites


You’ll need a free platform account. [Sign up](https://platform.mindee.com) and confirm your email to login.


### Let’s get started! 



After giving a name, description and cover image to your new API, you should land on the following page



[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/75fcd86-e26135d-screenshot-2021-04-25-at-193740.png",
        "e26135d-screenshot-2021-04-25-at-193740.png",
        1000,
        465,
        "#fbfcfd"
      ]
    }
  ]
}
[/block]
Build a Date field by selecting “Date” in the right side menu.



### Additional parameters

If you have additional context about this specific field or how the information is usually displayed in your documents, you can specify it during the field set up.


#### Feed parameters through UI


Through the UI, you may specify a date format between:

* US (mm/dd/yyyy)
* EU (dd/mm/yyyy)


This format should be the format is which most dates are displayed on your documents.


[block:callout]
{
  "type": "warning",
  "body": "This format is not to be interpreted as the date format you want to have in the API response scheme."
}
[/block]
### Impact for training and making predictions


#### Candidates


By specifying the data type as Date, you will force the engine to only consider words and series of words that can be interpreted as a date as eligible candidates.


[block:callout]
{
  "type": "warning",
  "body": "This means that, for this specific field, we will never be able to extract any information in your document that cannot be interpreted as a date."
}
[/block]

#### Text parsed


Anything that can be read as a date including:

* **Standard formats** : “12/08/1980” or “1/1/19”
* **Alpha characters for months** : “December, 8th 1980”
* **Dates missing the day information** : “January 2019”


If the date you are looking for is sometimes displayed in another way, you should use a String field.