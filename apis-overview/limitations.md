---
title: Technical limitations
excerpt: ''
---

A set of limits are enforced to ensure the safety of Mindee's parsing document APIs. A project may have additional limits depending on its plan. An API call that causes any of these limits to be exceeded will be rejected with an error. You can find these limits in the documentation tab of your API.

> **Info**📘
>
>If you have needs beyond these limits then get in touch with the support team and we'll work something out.

![Rate limits part of Mindee's platform documentation tab](https://files.readme.io/56777aa-ratelimits.png)

The rate limits are entirely customizable but here are the default values for self-serve:

## Documents
- Maximum file size(image and PDF): 10 MB.
- Maximum number of pages for PDF: 
    - Off-the-shelves: 5-10 pages(depending on the product) .
    - API builder: 5 pages.
    
## API Calls
- **Free Plan**: Maximum number of API calls: 
    - Off-the-shelves: 250 calls. 
    - API builder: 500 calls.
- **Unlimited Plan**: No limits.

**Note**: 250 free calls refers to the number of pages/documents i.e a single call, with a 2 pages pdf, will decrease your quota by two times.

## Requests
- Maximum request throughput per second: 4 requests
- Maximum request throughput per minute: 75 requests

## Data model 
If your data model contains more than 50 properties, we cannot guarantee an optimal experience. 
Please get in touch with the support team, so we can further discuss the situation with you.

## Payload
Payload in Mindee refers to the data that you send to the server when you make an API request .

## Accepted document files

| Type    | MIME Type       | Extensions  |
| ------------- |:-------------:| -----:|
| Image JPEG     | image/jpeg |jpeg, jpg |
| Image Portable Network Graphics     | image/png     |   png|
| Image WEBP |  image/webp     |    webp |
| Adobe Portable Document Format | 	application/pdf | pdf|

Document types that will be supported soon:


| Type    | MIME Type       | Extensions  |
| ------------- |:-------------:| -----:|
| High Efficiency Image File Format     | image/heif  | heic, heif |
|Tagged Image File Format     | image/tiff     |   tiff, tif |

