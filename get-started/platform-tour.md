---
title: Platform tour
excerpt: ''
next:
  pages:
    - build-your-first-document-parsing-api
    - invoice-ocr
  description: ''
---

This section provides an insight into the basics of Mindee UI. It describes all the features and its function.

## API Hub
![Mindee API Store on the left and Your APIs on the right](https://files.readme.io/6345e3a-api-hub-page.png "API hub")

When you create an account at Mindee, you'll land on the APIs Hub. There are two sections on this page: The [**Off-the-shelf APIs**](https://developers.mindee.com/docs/what-is-off-the-shelf-api) in the APIs store and **Your APIs** which are off-the-shelf APIs currently in use and custom generated APIs.

To use an API, click on the corresponding API card you want from the API store. If you can't find what you're looking for in the off-the-shelf API Store, you can build it yourself by clicking on the **Create a new API** button. [Follow this tutorial to guide you through the process of creating your own API.](https://developers.mindee.com/docs/build-your-first-document-parsing-api)

## API Filtering by Location
![API filtering by location showing the different country](https://files.readme.io/72a17c0-Screenshot_2021-11-22_at_23.54.56.png "API filter")

You can filter your off-the-shelf APIs in the APIs store by location; this makes it easier to find the APIs you wish to use. However, regardless of your location, you will be able have access to all available off-the-shelf APIs.

Some of the APIs listed are relevant only to a certain location; for example, the French ID card API won't be that relevant to someone in the United States unless there is a specific need for it.

Here are the region specific off-the-shelf APIs currently available:

#### Globally
- [Invoice OCR API](https://developers.mindee.com/docs/invoice-ocr).
- [Receipt OCR API](https://developers.mindee.com/docs/receipt-ocr).
- [Passport OCR API](https://developers.mindee.com/docs/passport-ocr). 
#### Europe
- [License Plates](https://blog.mindee.com/extending-license-plate-extraction/)

#### France
> _These are not documented yet (working on it), but if you use any other off-the-shelf API, you should be able to use them without any issues. If you need any help, feel free to ask on our [Slack community](https://slack.mindee.com)_
- Carte Nationale d'Identité.
- Carte Vitale.

**Note**: You can use all these available off-the-shelf API no matter your location.

## API - Dashboard
![Mindee API dashboard with the different section](https://files.readme.io/24d3e27-2.1.jpg "dashboard")
 
From the dashboard, you can monitor and manage your usage and your plan. The dashboard has two main sections: 
- API usage section
- API metrics section

### API Usage
![Dashboard API usage](https://files.readme.io/e4efcf0-api_usage.jpg "api usage")

You can view your current monthly plan and usage under the API usage. The default subscription is a free plan that renews automatically each month. To customize your subscription, click on the **Go unlimited** button. If your plan is active, it will be automatically renewed each month.

### API Metrics
![Dashboard API metrics](https://files.readme.io/ee66585-api_metric.jpg "api metrics")

In the API Metrics section you can view your:
- **Traffic**: Number of inputs processed (images and pdf pages).
- **Errors**: Number of HTTP errors.
- **Latency**: Average server-side computation time in milliseconds.

## API - Documentation
![Mindee APIs documentation with the different section](https://files.readme.io/fae4a9a-2.2.jpg "documentation")

Whether it's an [off-the-shelf](https://developers.mindee.com/docs/what-is-off-the-shelf-api) API from the API Store or a custom-built API, you can access the specific documentation to help you test and integrate easily. The documentation has different sections which are: 
- API Reference
- Response scheme
- Limitations
- Open API

### API Reference
![API reference section with its sub-section](https://files.readme.io/c0af70e-2.3.jpg "api reference")

From the API reference section you can view: 
- **HTTP Request**: This contains all the main information you need to make a request to your API, such as base URL, Content-type, Authentication headers, and form data.
- **Sample code**: This contains ready to use sample codes in different languages which you can copy and paste in your environment.

### Response scheme
![Response scheme section with its sub-section](https://files.readme.io/ff186fd-2.4.jpg "response scheme")

From the Response scheme section you can view: 
- **Response structure**: This contains a full JSON response example along with a few details about how to access your document level predictions.
- **Extracted fields**: This provides details about every field extracted by the API within a document.

### Limitations
![Limitations section with its sub-section](https://files.readme.io/5883fa9-2.5.jpg "limitation")

From the limitations section you can view: 
- **Supported documents**: This contains details on the type of documents you can send to the API for parsing.
- **Rate limits**: This provides information on the rate limits of each API depending on your plan.

### Open API
![Open API swagger-like interface section](https://files.readme.io/fc315f7-2.6.jpg "open api")

The OpenAPI section is a swagger-like user interface that allows you to navigate through your API technical information. You can also download the OpenAPI definition of your API.

## API -  API Keys
![Mindee API Keys](https://files.readme.io/706254b-2.7.jpg "api keys")

With the API keys section, you can create numerous API keys according to your needs, retrieve, and delete your API keys. Follow these [steps listed here](https://developers.mindee.com/docs/make-your-first-request#create-an-api-key) to create an API key. 

To delete an API key:
1. Click on the trash icon located on the left.
![API key with trash icon on the left](https://files.readme.io/7a51fcd-created-api.png)
2. A dialog box will pop out, type the name of your API key and click on the **Delete API** button.

![Mindee Delete API Keys](https://files.readme.io/0499e65-delete-api-key.png "api keys")

**Note**: It is important to note that if you delete your API keys, it cannot be revoked. 

## API - Live interface
![Mindee API live interface section](https://files.readme.io/7595d34-liveInterface.png "live interface")

This is your home for no code testing. In our graphical user interface, you can drag and drop your documents to see the API in action. You can also see all of the extracted information, as well as the raw API JSON response in one location. For custom-built APIs, a trained model is required before the live interface can be used.

## API - Models
![Mindee API Models section](https://files.readme.io/602f837-unnamed_1.png "api model")
    
This section is only available for custom APIs built using the API Builder. You can monitor the status of your training in real time, informing you when it is in progress, deployed, or canceled.

## API - Training
![Mindee API Training section](https://files.readme.io/1e9120c-2.9.jpg "api training")

This section is only available for custom APIs built using the API Builder. In this section, you can train your custom-built API by annotating data. The left part of the Training interface is the viewer. You can drag and drop single documents or archives you want to annotate.  The right part of the screen is your data model. Each field you've set up in your data model appears here.

## API - Settings
![Mindee API settings section](https://files.readme.io/fd7eec6-2.10.jpg "api setting")

This section is only available for custom APIs built using the API Builder. In this section, you can modify the metadata about your API. In the **Actions** section, you can also:

- **Download your training data**: An email with your training data (raw files and annotations) will be sent to you and your account admins.
- **Download your data model config**: It's the json formatted data model of your API. Downloading this configuration file will help you duplicate your API if you want to create a similar one.
- **Delete your API**: You can delete your API, along with all its training data. This action is permanent and cannot be undone.

