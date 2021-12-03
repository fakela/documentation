---
title: Emails
excerpt: ''
---
## Set up an Email Address field


You want to extract an email address from your documents?

You can do that with the API Builder by creating an Email Address field in the Data Model configuration step.

This section will walk you through the implications of setting up a Email Address field.

### Prerequisites


You’ll need a free account. [Sign up](https://platform.midee.com) and confirm your email to login.


### Let’s get started! 


After giving a name, description and cover image to your new API, you should land on the following page


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/85f0509-e26135d-screenshot-2021-04-25-at-193740.png",
        "e26135d-screenshot-2021-04-25-at-193740.png",
        1000,
        465,
        "#fbfcfd"
      ]
    }
  ]
}
[/block]
Build an Email Address field by selecting “Email address” from the right side of the menu.



### Additional parameter

There is no additional parameter to be fed to the engine regarding email addresses.




### Impact for training and making predictions


#### Candidates


By specifying the data type as Email Address, you will force the engine to only consider words and series of words that can be interpreted as an email address as eligible candidates.


[block:callout]
{
  "type": "warning",
  "body": "This means that, for this specific field, we will never be able to extract any information in your document that cannot be interpreted as an email address."
}
[/block]