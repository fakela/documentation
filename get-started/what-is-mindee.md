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

[Mindee](https://mindee.com) is an API first platform that helps developers automate applications' workflows by standardizing the documents processing layer using computer vision and machine learning. In addition to easily detecting and extracting information using pre-trained data models for common documents (e.g., invoices, receipts, passports...), developers can easily build their own documents parsing API, thereby enabling any type of business to solve all document-based use cases quickly. 
Our mission is to help developers automate paperwork in their applications in real-time, with human-level accuracy.

## Who is Mindee for?
Mindee have a developer first mindset – we build powerful document parsing APIs that developers can utilize to solve their problems. Also, Mindee can be used if: 

- You are dealing with a lot of documents that aren't very organized, like invoices, receipts, forms, and so on.
- You need high-quality data extracted.
- You need data to be retrieved quickly. 

## Mindee Products

- **Off-the-shelf APIs**: With the Off-the-shelf APIs, you can integrate our data extraction APIs with no coding!. This can easily be used only in the browser for non technical people. Each of our off-the-shelf APIs (Passport OCR API, Receipt OCR API, Invoice OCR API etc) have been trained using hundreds of thousands of documents to provide you with the most robust and accurate parsing solution.
- **API Builder**: Mindee APi builder is our battle-tested deep learning OCR algorithms that allows users to design and train an API  to extract the data you need. from any type of document
- **docTR**: docTR which is also known as (Document Text Recognition) - is a seamless, high-performing & accessible library for OCR-related tasks powered by Deep Learning.

## What Mindee offers

### Key information extraction

Extracting a set of specific information from documents is also called **Key information extraction**. The goal is to define a list of fields you want to extract from documents, so you are able to automate a workflow based on this data when a new document comes up.

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

Let's take a look at this example: **Invoice OCR example**. 
For many accounting use cases such as accounts payable automation, you need to extract key information from invoices such as:
 - Due date
 - Total amount
 - Invoice date
 - Invoice number
 - Merchant name
 - Taxes
 - Total amount

You can extract those different fields automatically using our [Invoice OCR API](doc:invoice-ocr). This API has been trained to provide you with a precise and accurate solution.

### Extracting key information from your own document type

If you need an API that has not yet been released in our catalog, you can build your own in minutes.

Using our [API Builder](https://developers.mindee.com/docs/build-your-first-document-parsing-api), you can define your own list of key information and train an API to extract those fields by annotating a few dozen example files. Our users have already built and deployed into production many different document parsing APIs, you can find a non-exhaustive list [here](https://developers.mindee.com/docs/use-cases).


## Document classification

Sometimes, you need to classify documents automatically in your code. One reason can be that your users upload several different types of documents at once, and you need to identify which is which. Perhaps they upload a single pdf including many different documents. It can be very tricky to automate this depending on your use case.


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
[Using our API builder](doc:document-classification), you can train a powerful document classification API in minutes, using your own class definitions.

## Key concepts

