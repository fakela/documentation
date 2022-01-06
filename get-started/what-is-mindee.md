---
title: Welcome to our Developer Portal
excerpt: ''
next:
  pages:
    - setup-your-account
    - build-your-first-document-parsing-api
    - invoice-ocr
  description: ''
---

## What is Mindee?

[Mindee](https://mindee.com) is an API-first platform that helps developers automate applications' workflows by standardizing the document processing layer using computer vision and machine learning. In addition to easily detecting and extracting information using pre-trained data models for common documents (e.g., invoices, receipts, passports, etc.), developers can easily build their own document parsing API, thereby enabling any type of business to solve all document-based use cases quickly. 

Our mission is to help developers automate paperwork in their applications in real-time, with human-level accuracy.

## Who is Mindee for?

Mindee has a developer-first mindset and aims to build powerful document parsing APIs that developers can utilize to solve their problems. Mindee can be used if you are:

- dealing with a lot of documents that aren't very organized, like invoices, receipts, forms, and so on.
- need high-quality data extracted.
- need data to be retrieved quickly. 

## Mindee Products

- **Off-the-shelf APIs**: With off-the-shelf APIs, you don't have to write any code to use our data extraction APIs. This can be used only in the browser. Each of our off-the-shelf APIs (Passport OCR API, Receipt OCR API, Invoice OCR API, etc.) has been trained using hundreds of thousands of documents to provide you with the most robust and accurate parsing solution.

- **API Builder**: [Mindee API Builder](https://mindee.com/lp/ocr-document-learning) is our battle-tested deep learning OCR algorithm that allows users to design and train an API to extract the data they need from any type of document.

- **docTR**: [Document Text Recognition](https://github.com/mindee/doctr) is a seamless, high-performing, and easily accessible library for OCR-related tasks powered by Deep Learning.

## What Mindee offers

1. **Key information extraction**: This refers to extracting a set of specific information from documents. This is done by specifying the set of fields that you wish to extract from documents so that you may automate a process based on this data whenever a new document is created or updated.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/09f8748-invoice_article2_bis.jpeg",
        "invoice_article2_bis.jpeg",
        1195,
        660,
        "#f8f9fc"
      ],
      "caption": "Invoice OCR API key information extraction"
    }
  ]
}
[/block]

Let's take a look at this example: **Invoice OCR example**. For many accounting use cases such as accounts payable automation, you need to extract key information from invoices such as:
 - Due date
 - Total amount
 - Invoice date
 - Invoice number
 - Merchant name
 - Taxes
 - Total amount

You can extract those different fields automatically using our [Invoice OCR API](doc:invoice-ocr). This API has been trained to provide you with a precise and accurate solution.

2. **Extracting key information from your own document type**: If you need an API that has not yet been released in our APIs Store, you can build your own in minutes. Using our [API Builder] (https://developers.mindee.com/docs/build-your-first-document-parsing-api), you can define your own list of key information and train an API to extract those fields by annotating a few dozen example files. Our users have already built and deployed into production many different document parsing APIs. You can find a non-exhaustive list [here] (https://developers.mindee.com/docs/use-cases).


3. **Document classification**: Sometimes, you need to classify documents automatically in your code. One reason can be that your users upload several different types of documents at once, and you need to identify which is which. Perhaps they upload a single pdf including many different documents. It can be very tricky to automate this depending on your use case. [Using our API builder](doc:document-classification), you can train a powerful document classification API in minutes, using your own class definitions.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c53e825-1.1.png",
        "1.1.png",
        726,
        623,
        "#f6f6f6"
      ],
      "caption": "Document classification"
    }
  ]
}
[/block]


## Key concepts

You will frequently encounter these concepts throughout this docs as Mindee is centred around them

- **Models**. A model is a machine learning file that can be trained to carry out specific tasks such as extracting capturing the total amount info from receipts.
- **Documents**. A semi-structured document like an invoice, receipt, ID document, W9-forms, train-ticket etc. in a PDF or image format.
- **Annotation**. Annotation is the process of labelling data to show the outcome you want your machine learning model to predict.
- **Predictions**. Prediction refers to the output of an algorithm after it has been trained on a dataset and applied to new data this occurs when your model has finished training your documents
