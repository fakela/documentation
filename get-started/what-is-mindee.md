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
[Mindee](https://mindee.com) is a developer platform that enables you to **extract key information from any type of document with your code**. Our mission is to help developers automate paperwork in their applications in real-time, with human-level accuracy.

## What does Mindee offer?

## Who is Minder for?
Mindee is a powerful document parsing API built for developers and performs best if:

- You are dealing with a lot of documents that aren't very organized, like invoices, receipts, forms, and so on.
- You need high-quality data extracted.
- You need data to be retrieved quickly.

## Mindee Products

- Off-the-shelf APIs
- API Builder
- docTR

## Key information extraction
## Key concepts

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
### Invoice OCR example

For many accounting use cases such as accounts payable automation, you need to extract key information from invoices such as:
> * Total amount
> * Invoice date
> * Due date
> * Merchant name
> * Taxes
> * Invoice number
> * ...

You can extract those different fields automatically using our [Invoice OCR API](doc:invoice-ocr).

Each of our off-the-shelf APIs have been trained using hundreds of thousands of documents to provide you with the most robust and accurate parsing solution. We frequently release off-the-shelf APIs such as our [Receipt OCR API](doc:receipt-ocr) or [Passport OCR API](doc:passport-ocr). Feel free to ask us about our roadmap to see what is coming next.

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
