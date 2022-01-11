---
title: Welcome to Mindee Documentation
excerpt: ''
next:
  pages:
    - setup-your-account
    - build-your-first-document-parsing-api
    - invoice-ocr
  description: ''
---

## What is Mindee?
Mindee is a powerful OCR software and an API-first platform that helps developers automate applications' workflows by standardizing the document processing layer through data recognition for key information using computer vision and machine learning.

In addition to easily detecting and extracting key information using our pre-trained data models for common documents (e.g., invoices, receipts, passports, etc.), developers can easily build their own document parsing API, thereby enabling any type of business to solve all document-based use cases quickly and easily.

Our mission is to provide real-time, human-level accuracy in data extraction from paper and digital documents for our customers.

## Who is Mindee For?
Mindee has a developer-first mindset and strives to provide robust document parsing APIs that developers may use to solve their issues. Mindee eliminates the need for manual data entry. This results in:

- increased efficiency,
- fewer errors during data extraction, and,
- it enables individuals to concentrate on more essential tasks.

Mindee can be used for a variety of purposes, some of which are listed below:

- if you are dealing with a lot of documents that aren't very organized, like invoices, receipts, forms, and so on.
- need high-quality data extracted.
- need data to be retrieved quickly, etc.

## What Mindee Offers
1. **Key information extraction**: This refers to extracting a set of specific information from documents. This is done by specifying the set of fields that you wish to extract from documents so that you may automate a process based on this data whenever a new document is created or updated.

![A LinkedIn receipt example on the left with the detected and extracted fields on the right, including their values](https://files.readme.io/09f8748-invoice_article2_bis.jpeg "Invoice OCR API key information extraction")

Let's take a look at the **Invoice OCR example** above. For many accounting use cases such as accounts payable automation, you may need to extract key information from invoices such as:
 - Due date
 - Invoice date
 - Invoice number
 - Merchant name
 - Taxes
 - Total amount

This is where our off-the-shelf APIs comes into play to make your life easier. You can extract those different fields automatically using our [Invoice OCR API](https://developers.mindee.com/docs/invoice-ocr). This API has been trained to provide you with a precise and accurate solution. 

2. **Extracting key information from your own document type**: We frequently release new off-the-shelf APIs, but if you have a use case or documents that have not yet been released in our APIs store, you can build your own API in minutes. Using our API Builder, you can define your own list of key information you need from your documents and train the API to extract those fields by annotating a few dozen example files. Our users have already built and deployed into production many different document parsing APIs. The possibilities are infinite: here is a [non-exhaustive list](https://developers.mindee.com/docs/use-cases) of what we have seen so far.

3. **Document classification**: Sometimes, you need to classify documents automatically in your code. One reason could be that you want to make your users' lives easier, and let them upload several different types of documents at once, which means you definitely need to identify which is which. Perhaps they upload a single pdf with many different document types in it. Based on our experience, it can be very tricky to automate this depending on your use case. Well not anymore, cause with our API builder [document classification](https://developers.mindee.com/docs/document-classification) you can train a powerful document classification API in minutes, using your own class definitions.

![Document classification in Mindee classifying the different documents to their various types](https://files.readme.io/c53e825-1.1.png "Document classification")

## Mindee's Products

### Off-the-shelf APIs
Our off-the-shelf APIs are ready-to-use data extraction solutions: it is as easy as calling the API for the specific document you want to get information from. We meticulously crafted the data model specific to each use cases. These are trained using hundreds of thousands of documents to provide you with the most robust and accurate parsing solution. We are currently working on adding more options for users, however, here are the region specific off-the-shelf APIs currently available:

#### Globally
- [Invoice OCR API](https://developers.mindee.com/docs/invoice-ocr).
- [Receipt OCR API](https://developers.mindee.com/docs/receipt-ocr).
- [Passport OCR API](https://developers.mindee.com/docs/passport-ocr).

#### Europe
- [License Plates](https://blog.mindee.com/extending-license-plate-extraction/).

#### France
> _These are not documented yet (working on it), but if you use any other off-the-shelf API, you should be able to use them without any issues. If you need any help, feel free to ask on our [Slack community](https://slack.mindee.com)_
- Carte Nationale d'Identité.
- Carte Vitale.

**Note**: You can use all these available off-the-shelf API no matter your location.

### API Builder
[Mindee API Builder](https://developers.mindee.com/docs/build-your-first-document-parsing-api) is our battle-tested deep learning OCR algorithm that allows users to design and train an API to extract the data they need from any type of document.

