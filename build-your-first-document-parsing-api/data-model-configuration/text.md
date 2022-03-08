---
title: Text
excerpt: ''
hidden: false
---
## Set up a text field




You want to extract text fields from your documents (full name, addresses, place..) ?



You can do that with the API Builder by creating a text field in the Data Model configuration step. [Data model configuration](doc:data-model-configuration) 




This section will walk you through the implications of setting up a string field and the different parameters you can specify.





### Prerequisites


1. You’ll need a free platform account. [Sign up](https://platform.mindee.com) and confirm your email to login.


### Let’s get started! 


After giving a name, description and cover image to your new API, you should land on the following page:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e26135d-screenshot-2021-04-25-at-193740.png",
        "screenshot-2021-04-25-at-193740.png",
        1000,
        465,
        "#fbfcfd"
      ]
    }
  ]
}
[/block]



Build a text field by selecting the Text field image from the choices on the right.


### Additional parameters

If you have additional context about this specific field and how the information is usually displayed in your documents, you can specify it during the field set up.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/aa79a51-screenshot-2021-04-25-at-202328.png",
        "screenshot-2021-04-25-at-202328.png",
        1000,
        1167,
        "#bec8d3"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]
#### Feed parameters through UI


Through the UI, you may check two different checkboxes:

* **It never contains any alpha characters**. By checking this, the engine will never be able to predict a word or a list of words containing alpha characters as the correct value for this field.
* **It never contains any numeric characters**. By checking this, the engine will never be able to predict a word or a list of words containing numeric characters as the correct value for this field.



#### Feed parameters through config.json file


You may want to create a String field through by uploading a config.json file. (See Data Model tutorial for more info)[https://mindee.com/documentation/api-builder/data-model]


Doing this, you have access to more possible parameters for this String field than the two checkboxes on the UI. To do that, fill in the cfg objects in your config.json file with the following parameters:



**alpha**: Does it contain alpha characters

* possible values: -1 means sometimes;  0 means never; 1 means always.
* default value: -1



**numeric**: Does it contain numeric characters

* possible values: -1 means sometimes;  0 means never; 1 means always.
* default value: -1



A valid entry for a String field in a config.json should look like this:

```
				{
					"cfg": {
						"filter": {
							"alpha": 0,
							"numeric": 0
						}
					},
					"handwritten": false,
					"name": "name",
					"public_name": "name",
					"semantics": "word"
				}
```

### Impact for training and making predictions


By default, a Text field allows every information read on the document to be considered as an eligible candidate.

Specifying the different parameters will have consequences for you in the training phase and when making predictions later on.



Basically, it provides the engine with **a list of criteria that a word or a list of words should match** in order to be considered as a valid candidate or an eligible possible correct answer.

[block:callout]
{
  "type": "warning",
  "title": "",
  "body": "Warning: This means that, for this specific field, we will never be able to extract any information in your document that does not match these criteria."
}
[/block]




This field type should be your go-to data type if you do not have sufficient context about your documents or if the information you are looking for is displayed in inconsistent ways between different documents.