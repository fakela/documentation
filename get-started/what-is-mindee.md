---
title: Welcome to Mindee Documentation
excerpt: ''
next:
  pages:
    - setup-your-account
    - build-your-first-document-parsing-api
    - invoice-ocr
  description: 'Getting started with Mindee'
---

## About Mindee
[Mindee](https://mindee.com) is an API-first platform that helps developers automate applications' workflows by standardizing the document processing layer using computer vision and machine learning. In addition to easily detecting and extracting information using pre-trained data models for common documents (e.g., invoices, receipts, passports, etc.), developers can easily build their own document parsing API, thereby enabling any type of business to solve all document-based use cases quickly and easily. 

Our mission is to help developers automate paperwork in their applications in real-time, with human-level accuracy.

## Who is Mindee For?
Mindee has a developer-first mindset and aims to build powerful document parsing APIs that developers can utilize to solve their problems. Mindee can be used if you are:

- dealing with a lot of documents that aren't very organized, like invoices, receipts, forms, and so on.
- need high-quality data extracted.
- need data to be retrieved quickly. 

## Mindee's Products
- **Off-the-shelf APIs**: With [off-the-shelf APIs](), you don't have to write any code to use our data extraction APIs. Although, this can be used only in the browser, each of our off-the-shelf APIs ([Passport OCR API](https://developers.mindee.com/docs/passport-ocr), [Receipt OCR API](https://developers.mindee.com/docs/receipt-ocr), [Invoice OCR API](https://developers.mindee.com/docs/invoice-ocr), etc.) has been trained using hundreds of thousands of documents to provide you with the most robust and accurate parsing solution.

- **API Builder**: [Mindee API Builder](https://mindee.com/lp/ocr-document-learning) is our battle-tested deep learning OCR algorithm that allows users to design and train an API to extract the data they need from any type of document.

- **docTR**: [Document Text Recognition](https://github.com/mindee/doctr) is a seamless, high-performing, and easily accessible library for OCR-related tasks powered by Deep Learning.

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

2. **Extracting key information from your own document type**: We frequently release new off-the-shelf APIs, but if you have an use case or documents that has not yet been released in our APIs store, you can build your own API in minutes. Using our [API Builder](https://developers.mindee.com/docs/build-your-first-document-parsing-api), you can define your own list of key information you need from your documents and train the API to extract those fields by annotating a few dozen example files. Our users have already built and deployed into production many different document parsing APIs. The possibilities are infinite: here is a [non-exhaustive list](https://developers.mindee.com/docs/use-cases) of what we have seen so far.

3. **Document classification**: Sometimes, you need to classify documents automatically in your code. One reason can be that you want to make your users' life easier, and let them upload several different types of documents at once which means you definitely need to identify which is which. Perhaps they upload a single pdf including many different document types in it. Based on our experience, it can be very tricky to automate this depending on your use case. Not anymore with the API builder [document classification](https://developers.mindee.com/docs/document-classification) you can train a powerful document classification API in minutes, using your own class definitions.

![](https://files.readme.io/c53e825-1.1.png "Document classification")
