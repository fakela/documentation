---
title: 'Zapier: Receipt OCR Extraction'
excerpt: ''
---
Have you ever been out at a business meal, and collected the receipt, but before you could submit your expense, you lost the receipt? With Mindee's receipt parsing API, you can take a photo, and we'll extract all the details from the receipt.

The trick is developing a tool that is easy to use from your phone to take the image and do the processing.

In this post, well use the Mindee Receipt OCR extraction inside our no-code Zapier integration.  We'll have a working demo up in minutes without writing a single line of code.

We'll use a dedicated Discord channel to upload the receipts, and then we'll send the image, and the data pulled form the receipt to a second discord channel - where you can see all of your receipts for the week (when it is time to do expense reporting). 

Zapier offers thousands of applications to integrate with - you might even find your expense reporting software  is supported - so the data can be sent right into a new expense report!

The tools required:

1. A Discord account with a channel you can use for uploading receipts.
2. A free Zapier account (sign up at [Zapier.com](https://zapier.com))
3. A [Mindee account](https://platform.mindee.com) with an Invoice parsing API key.

## Zapier

Zapier is a no code service that connects different tools with a secure no-code interface.  They call the connections “Zaps.”  Each Zap has a “trigger” an event that starts the process, and an "action" that occurs after the trigger has fired.

In the case of the Zap we are building, you will need a premium account ($29.95/ month). If you are a new user (or if you have a new Zapier account), you'll have free premium access for a week (but your Zap will turn off when the trial ends).

Once you have created a Zapier account, you’ll land at the app dashboard.  Click the black “Create Zap” button:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/34d360c-Screenshot_2021-10-06_at_19.32.06.png",
        "Screenshot 2021-10-06 at 19.32.06.png",
        666,
        834,
        "#e3e1e1"
      ]
    }
  ]
}
[/block]
The first step in creating the Zap is creating the trigger - which will be a new message (with an attachment) being posted in a Discord channel:


## Trigger Creation

The trigger we want is a new message (with an attachment) being posted in a Discord channel.  Search the “App events” for Discord:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c7340ed-Screenshot_2021-10-07_at_21.34.35.png",
        "Screenshot 2021-10-07 at 21.34.35.png",
        2066,
        1376,
        "#f2e0da"
      ]
    }
  ]
}
[/block]
The trigger is a new message appearing in a channel:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/569e7d9-Screenshot_2021-10-07_at_21.35.09.png",
        "Screenshot 2021-10-07 at 21.35.09.png",
        1992,
        1090,
        "#e7ebf5"
      ]
    }
  ]
}
[/block]
Log in to your Discord account, and pick the channel you're going to upload receipts to.  In this case, we have created a (creatively named) "#upload-receipts" channel.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0abf854-Screenshot_2021-10-07_at_21.37.25.png",
        "Screenshot 2021-10-07 at 21.37.25.png",
        1840,
        1100,
        "#e8ebf6"
      ]
    }
  ]
}
[/block]
In the next step, Zapier will test the trigger, so make sure you have a message in your channel (it will be a lot easier if there is a receipt connected to the message).  So if you have not sent a message with a receipt to the channel, do that before you test the Trigger.

## Action time!

Now we will create an action, and we will use the Mindee OCR Invoice Parsing API. Search for Mindee in the action search bar:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9a82d87-Screenshot_2021-10-06_at_19.40.22.png",
        "Screenshot 2021-10-06 at 19.40.22.png",
        1848,
        1168,
        "#f6d9cd"
      ]
    }
  ]
}
[/block]
We want to use the Receipt endpoint from Mindee:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/549805c-Screenshot_2021-10-12_at_20.22.23.png",
        "Screenshot 2021-10-12 at 20.22.23.png",
        1896,
        1216,
        "#f4f5f6"
      ]
    }
  ]
}
[/block]
If you have followed the other tutorials on Invoice or Passport OCR demos, you may have already logged in., but we need to create a new connection to the Receipt endpoint (each endpoint currently has separate API keys). to do this, we'll click "Connect a new account"
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7a8650d-Screenshot_2021-10-12_at_20.23.26.png",
        "Screenshot 2021-10-12 at 20.23.26.png",
        2000,
        1196,
        "#f2f2f3"
      ]
    }
  ]
}
[/block]
Next you'll choose the Receipt API endpoint, and enter an API key (retrievable at [platform.mindee.com](https://platform.mindee.com/apishub/products/mindee/expense_receipts?setup=default#tokens)
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b27a244-Screenshot_2021-10-12_at_20.23.26.png",
        "Screenshot 2021-10-12 at 20.23.26.png",
        2000,
        1196,
        "#f2f2f3"
      ]
    }
  ]
}
[/block]
We'll set the action to test the attachment that was sent into the discord channel. We do this by specifying the URL where Mindee can retrieve the image.  Finally, we'll test the Mindee action:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f620fae-Screenshot_2021-10-12_at_20.39.40.png",
        "Screenshot 2021-10-12 at 20.39.40.png",
        1846,
        1214,
        "#f6f6f7"
      ]
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/24c9f3b-Screenshot_2021-10-12_at_20.40.41.png",
        "Screenshot 2021-10-12 at 20.40.41.png",
        1948,
        1530,
        "#f8f8f7"
      ]
    }
  ]
}
[/block]
In the response, we can see the 201 response with the parsed information from the receipt.  Now that we have extracted all this data, we can send a message in Discord to the "results" channel with all the receipt details.  You could do one of thousands of actions with this data. but for demo purposes, we'll just use the same Discord account. 

We'll pick the channel to send the results to, and then format the results:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1da8d4c-Screenshot_2021-10-12_at_20.51.38.png",
        "Screenshot 2021-10-12 at 20.51.38.png",
        2032,
        2068,
        "#f2f2f2"
      ]
    }
  ]
}
[/block]
The channel message will extract the time from the Discord message, and then pull Mindee receipt data: 
Date
Category
Total
Taxes
Currency
Country

There is text added to format the message nicely, and when you test this, a message will appear in the Discord channel with your parsed receipt.

we'll name the messenger the "Mindee Bot" and use the Mindee logo.  the final step before activating our zap is to run the final test, and this message appears in Discord:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1b14e37-Screenshot_2021-10-12_at_20.52.42.png",
        "Screenshot 2021-10-12 at 20.52.42.png",
        1214,
        1048,
        "#4e4e4f"
      ]
    }
  ]
}
[/block]


In this demo - we've sent a receipt to a Discord channel. Zapier retrieve the URL of the attachment, and sends it to Mindee's Receipt API to parse the data. When the extraction is complete, a formatted message containing the extracted data, and a picture of the receipt is posted to a 2nd Discord channel.