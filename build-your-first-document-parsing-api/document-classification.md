---
title: Document classification
excerpt: ''
next:
  pages:
    - build-your-first-document-parsing-api
    - training-interface
  description: ''
---
Workflows often involve document processing. And sometimes, you need to classify those documents automatically in your software. One reason can be that your users upload a bunch of different data in a unique flow, or they upload a single pdf including many different documents. It can be very tricky to automate this depending on your use case.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c28c68d-1.1.png",
        "1.1.png",
        726,
        623,
        "#f6f6f6"
      ]
    }
  ]
}
[/block]
In this article, we’ll show you how to build an accurate document classification API that fits exactly your needs. In minutes, you’ll get your API up and running and you’ll be able to process millions of documents synchronously.

 

## Example use case
 
Let’s take an example where your users are uploading documents on a single endpoint of your backend, and you want to classify them into 5 categories:

> * W9
> * 1040 Forms
> * Invoices
> * Payslips
> * Other


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/84516a8-1.2.png",
        "1.2.png",
        905,
        289,
        "#f0f1f1"
      ]
    }
  ]
}
[/block]



 

## Create your classification document API

Sign in to the platform and click on the **Create a new API **button.

Fill out a few information about your API. Give it a name, a description, and a cover image if you want.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4c9c208-1.3.png",
        "1.3.png",
        1600,
        818,
        "#fcfcfc"
      ]
    }
  ]
}
[/block]
Then click **Next**


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/92a96d5-1.4.png",
        "1.4.png",
        1600,
        821,
        "#fbfcfd"
      ]
    }
  ]
}
[/block]
This is where we define our document data model. We are going to define our different classes within a classification field.

Add a Classification field:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/199dc9e-1.5.png",
        "1.5.png",
        125,
        101,
        "#f9f7f8"
      ],
      "sizing": "original"
    }
  ]
}
[/block]
A popup will show up, we need now to input our different possible classes. Let’s fill the form with the classes defined earlier.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/780434c-1.6.png",
        "1.6.png",
        1600,
        819,
        "#c9cfd6"
      ]
    }
  ]
}
[/block]
Once you click the **Add this classification field** button, we are all set. You can now click the **Start training your model** button.

## Train your document classifier API

Your API was just deployed! Now we need to train the model.

To do so, we’ll need data, **15 samples for each type should be enough to get very high performances**, but it’s up to you to train with more if you want to. It’s going to take you no more than 10 minutes to annotate your data once it’s uploaded.
 

The training interface looks like this:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/775818a-1.8.png",
        "1.8.png",
        1600,
        821,
        "#fdfdfd"
      ]
    }
  ]
}
[/block]
On the left part of the screen, you can upload images, pdf, or zip archives. If you have all your training data in a folder on your laptop, just zip it and drag and drop it on the upload interface. You can mix pdfs and images, it’s not a problem as our backend will take care of this.

Gathering your samples for training is actually the most boring part of the process.

In my example, I have a total of 90 data, equally distributed. As it’s a dummy example, I’ve put random documents for the “other” class, but in your real-world use case, it’s better to use real data from your flow that you’d consider as “other”.

Our zip file is ready. When we drag and drop the file on the left part of the screen, the data management pane opens:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ab6a011-1.9.png",
        "1.9.png",
        1600,
        822,
        "#e6e7ea"
      ]
    }
  ]
}
[/block]
Each data will appear automatically in the pane when it’s ready for annotation. 

To make the annotation process easier, click on the **Setting icon in the header,** and check the automatic data loading:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9a0a5c7-1.10.png",
        "1.10.png",
        1600,
        821,
        "#c5cbd2"
      ]
    }
  ]
}
[/block]
Let’s start annotating the data.

Click on **Your data set** on the left part of the screen, and click on the first document you see in the list.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0c84dca-1.11.png",
        "1.11.png",
        1600,
        820,
        "#e4e5e8"
      ]
    }
  ]
}
[/block]
Now, it’s very simple. Click on the desired class for each data on the right part of the interface:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c596bf3-1.12.png",
        "1.12.png",
        784,
        147,
        "#f3f6fa"
      ]
    }
  ]
}
[/block]
**Validate,  and repeat.**

In our example, it took 5 minutes to annotate 89 data.

A model is trained every 20 data, and each of them is automatically deployed on your API under new versions:

* V1.0 = no model
* V1.1 = 1st model (20 data)
* V1.2 = 2nd model (40 data)
* …
 

You get an email when a model is deployed. My last model was deployed 15 minutes after I finished my 89 annotations. The first one was ready before I finished.

To know the performances or your model, ask the chat, we’ll give you the accuracy of your model. I got an overall accuracy of 96%, with confusion coming from invoices being classified as others. Adding a few more invoices and other documents would fix this.

 

## Use the API

Your API is now ready to be used in your code.

Once your first model is deployed you can test it right away with new data.

Hit the **Live interface** button on the sidebar, drag and drop a document. You should see something like this:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/895fc83-1.13.png",
        "1.13.png",
        1600,
        813,
        "#4f5f71"
      ]
    }
  ]
}
[/block]
The latest version of your API (i.e the latest trained model) is automatically set for the live interface. 

To integrate your API in your application, you can now hit the **Documentation** button in the sidebar.