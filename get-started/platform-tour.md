---
title: Platform tour
excerpt: ''
next:
  pages:
    - build-your-first-document-parsing-api
    - invoice-ocr
    - document-parsing-tutorials
  description: ''
---
## API Hub

When you [sign in](https://platform.mindee.com) to your account, you'll land on the APIs Hub page. Where you can find here off-the-shelf APIs in the APIs store as well as the APIs you have created yourself.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6afca95-Screenshot_2021-11-22_at_23.52.33.png",
        "Screenshot 2021-11-22 at 23.52.33.png",
        2842,
        1430,
        "#ededf0"
      ]
    }
  ]
}
[/block]

To use an API, click on the corresponding API card you want from the API store. If you can't find what you're looking for in the off-the-shelf API Store catalog, you can build it yourself by clicking the **Create a new API ** button. [Follow this tutorial to guide you through the API creation process.](https://developers.mindee.com/docs/build-your-first-document-parsing-api)


## API filtering by Locale

In the APIs store, you can filter your off-the-shelf APIs based on locations which makes it easier to sort the APIs you want to use. 
Some of the APIs listed are relevant only to a certain location, for example,  the French ID card API won't be that relevant to someone in the United States unless there is a specific need for it. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/72a17c0-Screenshot_2021-11-22_at_23.54.56.png",
        "Screenshot 2021-11-22 at 23.54.56.png",
        1362,
        998,
        "#dfdddf"
      ]
    }
  ]
}
[/block]
## API - Dashboard
 
From the dashboard section, you can monitor and manage your usage and your plan


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/24d3e27-2.1.jpg",
        "2.1.jpg",
        1904,
        976,
        "#f9fafb"
      ],
      "caption": "Mindee API dashboard"
    }
  ]
}
[/block]

### API Usage

You can view your current monthly plan and usage under the API usage section. Your default subscription is a free plan that renews automatically each month. To customize your subscription, click on the "Go unlimited" button. If your plan is active, it will be automatically renewed each month.


### API Metrics
In the API Metrics section you can view your:

- **Traffic**: Number of inputs processed (images and pdf pages).
- **Errors**: Number of HTTP errors.
- **Latency**: Average server-side computation time in milliseconds.



## API - Documentation

Whether it's an off-the-shelf API from the API Store or a custom-built API, you can access specific documentation to help you test and integrate easily.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fae4a9a-2.2.jpg",
        "2.2.jpg",
        1904,
        976,
        "#f9fafa"
      ],
      "caption": "Mindee APIs Documentation"
    }
  ]
}
[/block]
The documentation has different sections which are: API Reference, Response scheme, Limitations, Open API




### API Reference

From the API reference section you can view: 
- **HTTP Request**: This contains all the main information you need to make a request to your API, such as base URL, Content-type, Authentication headers, and form data.
- **Sample code**: Ready to use sample codes in different languages. Copy and paste in your environment.



[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c0af70e-2.3.jpg",
        "2.3.jpg",
        1540,
        694,
        "#f9fbfb"
      ],
      "caption": "API Reference"
    }
  ]
}
[/block]


### Response scheme

From the Response scheme section you can view: 
- **Response structure**: This is a full JSON response example along with a few details about how to access your document level predictions.
- **Extracted fields**: This provides details about every field extracted by the API within a document.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ff186fd-2.4.jpg",
        "2.4.jpg",
        1540,
        694,
        "#f9fbfa"
      ],
      "caption": "Response scheme"
    }
  ]
}
[/block]




### Limitations

From the limitations section you can view: 
- **Supported documents**: This contains details on the type of documents you can send to the API for parsing.
- **Rate limits**: Provides information on the rate limits of each API depending on your plan.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5883fa9-2.5.jpg",
        "2.5.jpg",
        1540,
        694,
        "#fbfcfc"
      ],
      "caption": "Limitations"
    }
  ]
}
[/block]



### Open API

You can find a swagger-like user interface to navigate through your API technical information. You can also download the Open API configuration of your API.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fc315f7-2.6.jpg",
        "2.6.jpg",
        1540,
        694,
        "#fafbfb"
      ],
      "caption": "Open API"
    }
  ]
}
[/block]



## API -  API Keys

In this section, you can create, retrieve, and delete your API keys. 


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/706254b-2.7.jpg",
        "2.7.jpg",
        1904,
        976,
        "#f9fafa"
      ],
      "caption": "Mindee API Keys"
    }
  ]
}
[/block]

You can also create multipe API keys according to your needs. Before deleting your API keys, keep in mind that it cannot be revoked. 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9a3fa30-Screenshot_2021-12-09_at_12.03.05.png",
        "Screenshot_2021-12-09_at_12.03.05.png",
        1904,
        976,
        "#f9fafa"
      ],
      "caption": "Mindee API Keys"
    }
  ]
}
[/block]




## API - Live interface

This is your home for no code testing.** Drag and drop your documents** to see the API in action. Quickly visualize all the extracted fields along with the raw API JSON response.
[block:callout]
{
  "type": "warning",
  "body": "For custom-built APIs, a first trained model is required before being able to use the live interface."
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7595d34-liveInterface.png",
        "liveInterface.png",
        1000,
        567,
        "#dbd8d3"
      ],
      "caption": "Mindee Live Interface"
    }
  ]
}
[/block]
## API -Models
[block:callout]
{
  "type": "info",
  "body": "This section appears only in the APIs you've built using the API Builder"
}
[/block]
This section allows you to keep track of your training progress in real-time to know when it's in progress, deployed, or canceled. 
## API [block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/58f6977-Screenshot_2021-11-24_at_14.24.01.png",
        "Screenshot 2021-11-24 at 14.24.01.png",
        2416,
        1274,
        "#f7f7f7"
      ]
    }
  ]
}
[/block]
- Training


[block:callout]
{
  "type": "info",
  "body": "This section appears only in the APIs you've built using the API Builder"
}
[/block]
This section allows you to train your custom-built API by annotating data.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1e9120c-2.9.jpg",
        "2.9.jpg",
        1893,
        1014,
        "#fbfbfc"
      ],
      "caption": "API builder training"
    }
  ]
}
[/block]
The left part of the Training interface is the viewer. You can drag and drop single documents or archives you want to annotate. 

The right part of the screen is your data model. Each field you've set up in your data model appears here.


## API - Settings

[block:callout]
{
  "type": "info",
  "body": "This section appears only in the APIs you've built using the API Builder"
}
[/block]
This section allows you to modify metadata about your API. 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fd7eec6-2.10.jpg",
        "2.10.jpg",
        1893,
        1014,
        "#f6f6f7"
      ]
    }
  ]
}
[/block]
In the **Actions** section, you can also:

- **Download your training data**: An email with your training data (raw files and annotations) will be sent to you and your account admins.
- **Download your data model config**: It's the json formatted data model of your API. Downloading this configuration file will help you duplicate your API if you want to create a similar one.
- **Delete your API**: You can delete your API, along with all its training data. This action is permanent and cannot be undone.
