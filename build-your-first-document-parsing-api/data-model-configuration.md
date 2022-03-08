---
title: Data model configuration
excerpt: ''
hidden: false
---
​
## Define your custom Data Model
 

In order to train your custom parsing API, you need to define a data model, i.e. a list of fields and their corresponding data types you want to extract from your documents.

This tutorial will walk you through the steps of defining such a Data Model.


For further information on specific data types, see arborescence on the left.


### Prerequisites

You’ll need a free Mindee account. [Sign up](https://platform.mindee.com/) and confirm your email to login.
 


### Let’s get started! 


After giving a name, description and cover image to your new API, you should land on the following page

 ![](https://mindee-public-website.s3.amazonaws.com/blog/2021/04/25/screenshot-2021-04-25-at-193740.png)



From there you have two options:


1. Manually add fields one by one by filling the form on the right side of the screen

2.  Upload a Data Model config file


Let’s start with the manual option.


### Manually add a field to your Data Model
 

You can add a new field by filling in the right-side form with the following information:

 
**Field Name**: The straightforward name that will appear on the annotation interface later on. Use a name that means something to you when reading it


**API response key**: The name of the key used in the API response scheme


**Field type**: The Field Type specifies the type of information we are going to look for on the document and defines the data type that will be returned in the API response.

 

You can choose among a drop-down list of pre-built data types between :


```
String
Number
Date
Email address
Phone number
Url
```

 

### Update or Delete a field
 

Now that you’ve created you first field, you should see something like this

 ![](https://mindee-public-website.s3.amazonaws.com/blog/2021/04/25/screenshot-2021-04-25-at-194651.png)



 

From there you can: 

 

* **Add a field** : Manually add a new field to your Data Model following the same process. You can repeat this step as many times as you want, there is no limit is the number of fields you can extract from a document.
* **Edit a field** : Edit a specific field. You can change its Field name, API response key and Field type
* **Delete a field** : Delete a specific field from your data model
* **Start training** : When your Data Model is ready. Click here to automatically deploy your API and start training it. 
 

 

### Upload a Data Model file config  
 

Alternatively, you can create a whole set of fields at once by uploading a config json file in the left-side section. 

 ![](https://mindee-public-website.s3.amazonaws.com/blog/2021/04/25/screenshot-2021-04-25-at-194905.png)



 

 

For instance, with our started example, the config json file looks like this

```
{
	"problem_type": {
		"classificator": {
			"features": [

			],
			"features_name": [

			]
		},
		"selector": {
			"features": [
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
				},
				{
					"cfg": {
						"filter": {
							"is_integer": -1
						}
					},
					"handwritten": false,
					"name": "number",
					"public_name": "number",
					"semantics": "amount"
				},
				{
					"cfg": {
						"filter": {
							"convention": "US"
						}
					},
					"handwritten": false,
					"name": "date",
					"public_name": "date",
					"semantics": "date"
				},
				{
					"handwritten": false,
					"name": "email",
					"public_name": "email",
					"semantics": "email"
				},
				{
					"handwritten": false,
					"name": "url",
					"public_name": "url",
					"semantics": "url"
				},
				{
					"handwritten": false,
					"name": "phone",
					"public_name": "phone",
					"semantics": "phone"
				}
			],
			"features_name": [
				"name",
				"number",
				"date",
				"email",
				"url",
				"phone"
			]
		}
	}
}
```
 

Each field is introduce by a cfg key and has the following attributes:

 

* **handwritten**: is entry handwritten or not. Mandatory

* **name**: the API response key. Mandatory.

* **public_name**: the Field Name. Mandatory.

* **semantics**: the Field Type. Mandatory.

* **cfg**: An object of additional data constraints depending on the Field Type.

 

 

The possible parameters for the **cfg** object are all mandatory and are the following:

 

####semantics = word (String):

* **alpha**: Does it contain alpha characters. -1 = sometimes, 0 = never, 1 = always. Default value = -1

* **numeric**: Does it contain numeric characters. -1 = sometimes, 0 = never, 1 = always. Default value = -1

 

####semantics = amount :

* **is_integer**: Is it an INT. -1 = sometimes, 1 = always. Default value = -1

​