---
title: URLs
excerpt: ''
---
## Set up an URL Address field


You want to extract an url from your documents?


You can do that with the API Builder by creating an URL field in the Data Model configuration step. This section will walk you through the implications of setting up a URL field.



### Prerequisites


You’ll need a free account. [Sign up](https://platform.mindee.com) and confirm your email to login.


### Let’s get started! 

After giving a name, description and cover image to your new API, you should land on the following page


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8f8f2a6-e26135d-screenshot-2021-04-25-at-193740.png",
        "e26135d-screenshot-2021-04-25-at-193740.png",
        1000,
        465,
        "#fbfcfd"
      ]
    }
  ]
}
[/block]
Build an URL field by selecting “URL” from the right side of the menu.



#### Additional parameters

There is no additional parameter to be fed to the engine regarding URLs.




### Impact for training and making predictions


#### Candidates


By specifying the data type as URLs, you will force the engine to only consider words and series of words that can be interpreted as an URL as eligible candidates.


[block:callout]
{
  "type": "warning",
  "body": "This means that, for this specific field, we will never be able to extract any information in your document that cannot be interpreted as an URL."
}
[/block]