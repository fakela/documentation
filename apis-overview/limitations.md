---
title: Technical limitations
excerpt: ''
---

A set of limits are enforced to ensure the safety of Mindee's parsing document APIs. An API may have additional limits depending on its plan. An API call that causes any of these limits to be exceeded will be rejected with an error. You can find limits specific to your API in the documentation tab.

> **Info**📘
>
>If you have needs beyond these limits then get in touch with the sales team and we'll work something out.

## Rate Limits
Here are the default values of the rate limits in Mindee.
![Rate limits part of Mindee's platform documentation tab](https://files.readme.io/56777aa-ratelimits.png "rate limits")

### Documents
- Maximum file size(image and PDF): 10 MB.
- Maximum number of pages for PDF: 
    - Off-the-shelves: 5-10 pages(depending on the product) .
    - API builder: 5 pages.
    
### API Calls
We have three plans that are available for our customers depending on the number of API calls they want to make.
- Developer plan,
- Pay as you go, and,
- Enterprise.

More information can be seen on our [pricing page](https://mindee.com/pricing)

### Requests
- Maximum request throughput per second: 4 requests
- Maximum request throughput per minute: 75 requests

### Data model 
If your data model contains more than 50 properties, we cannot guarantee an optimal experience. 
Please get in touch with the support team, so we can further discuss the situation with you.

### Payload
Payload in Mindee refers to the data that you send to the server when you make an API request .

## Accepted document files

| Type    | MIME Type       | Extensions  |
| ------------- |:-------------:| -----:|
| Image JPEG     | image/jpeg |jpeg, jpg |
| Image Portable Network Graphics     | image/png     |   png|
| Image WEBP |  image/webp     |    webp |
| Adobe Portable Document Format | 	application/pdf | pdf|
