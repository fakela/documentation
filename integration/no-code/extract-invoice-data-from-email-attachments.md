---
title: 'Zapier: Invoice OCR Extraction'
excerpt: ''
---
One of the most common ways we receive invoices for services rendered is via email.  The invoices are typically PDF files attached to the email.

In a typical expense process, invoices that are emailed to your company will have to be saved locally to a computer, and then re-uploaded into an invoicing system.  Maybe, even worse, the document must be opened and the details manually entered into the system.

In this post, we’ll build an invoice processing system: invoices that arrive via email will be automatically extracted, and all the data inserted into a Google Sheet.  

The best part: No coding required!  It will “just work” and will be completely “hands-free” - all the work will be done automatically!  If a Google Sheet is not your desired outcome - there are thousands of apps connected with Zapier, so this tutorial can be easily modified to interact with any other application.

The tools required:

1. A Gmail based email account.  
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
        "https://files.readme.io/9e5a045-Screenshot_2021-10-06_at_19.32.06.png",
        "Screenshot 2021-10-06 at 19.32.06.png",
        666,
        834,
        "#e3e1e1"
      ]
    }
  ]
}
[/block]
The first step in creating the Zap is creating the trigger - which will be the new email arriving in your Gmail account:


## Trigger Creation

The trigger we want is an email arriving into a Gmail account.  Search the “App events” for Gmail (it is often also right in the list of top apps):

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/98ee99f-Screenshot_2021-10-06_at_19.32.54.png",
        "Screenshot 2021-10-06 at 19.32.54.png",
        1516,
        1252,
        "#f5d9cf"
      ]
    }
  ]
}
[/block]
We want Gmail to trigger the Zap when a new attachment arrives:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d5b3242-Screenshot_2021-10-06_at_19.34.17.png",
        "Screenshot 2021-10-06 at 19.34.17.png",
        1870,
        1036,
        "#e4ecf8"
      ]
    }
  ]
}
[/block]
The next step asks you to connect your Gmail account to Zapier.  In an ideal world, you’d set up an address like ```invoices@<yourcompany>.com```.  For this demo, I used my Mindee email account.  The next step allows you to filter the emails based on the Gmail label or search string.  Here is where I am able to isolate to just emails with invoices:  

```
to:doug+invoice@mindee.co  has:attachment 
```

Here I am using a Gmail trick to ensure that only invoices emailed to me are parsed by the Zap.  With Gmail - you can add any value after the + and it acts as a unique email address - but arrives in the same inbox. 

The search also requires that there is an attachment in addition to being sent to my email address.

Now Zapier will test this trigger to find an email in the account that matches your search query (so now - quickly send an email -with an invoice attachment- to the Gmail account you’ve chosen, so that the search query succeeds).

Hopefully, your test will succeed, and you'll get a success message like below:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3b4dc17-Screenshot_2021-10-06_at_19.39.25.png",
        "Screenshot 2021-10-06 at 19.39.25.png",
        1968,
        1042,
        "#f8f8f8"
      ]
    }
  ]
}
[/block]
## Action time!

Now we will create an action, and we will use the Mindee OCR Invoice Parsing API. Search for Mindee in the action search bar:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2787e13-Screenshot_2021-10-06_at_19.40.22.png",
        "Screenshot 2021-10-06 at 19.40.22.png",
        1848,
        1168,
        "#f6d9cd"
      ]
    }
  ]
}
[/block]
Choose the Mindee OCR, and then select the action for invoice parsing:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3b104e0-Screenshot_2021-10-06_at_19.42.19.png",
        "Screenshot 2021-10-06 at 19.42.19.png",
        1980,
        1112,
        "#f5f6f7"
      ]
    }
  ]
}
[/block]
Next you’ll be asked to sign in to Mindee.  A popup will open with a form.  We have 3 endpoints featured in our Zapier integration, and using the dropdown, you’ll want to pick the invoice endpoint.  Once you select this, you’ll have to add an API Key.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a2f151a-Screenshot_2021-10-06_at_19.44.16.png",
        "Screenshot 2021-10-06 at 19.44.16.png",
        1750,
        1192,
        "#eff2f3"
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
        "https://files.readme.io/f275e19-Screenshot_2021-10-06_at_19.44.44.png",
        "Screenshot 2021-10-06 at 19.44.44.png",
        1482,
        1040,
        "#eff0f1"
      ]
    }
  ]
}
[/block]
Get your API key from https://platform.mindee.com/apishub/products/mindee/invoices?setup=default#tokens  You’ll need to sign in to your Mindee account, and then create or use one of your existing API keys

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ae490a8-Screenshot_2021-10-06_at_19.45.52.png",
        "Screenshot 2021-10-06 at 19.45.52.png",
        1210,
        1214,
        "#f9f9fa"
      ]
    }
  ]
}
[/block]
Insert your API key and Zapier will authenticate your account with Mindee.

Now we need to set up the action to send the attached document from your email message to Mindee.  Set the document field to be populated with the file attached to your email:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e09c8b7-Screenshot_2021-10-06_at_19.50.10.png",
        "Screenshot 2021-10-06 at 19.50.10.png",
        2068,
        1184,
        "#e8eef6"
      ]
    }
  ]
}
[/block]
Next - Zapier will test your document with the Mindee Invoice API, and you should see a success code, and a long JSON export showing all the details of the Mindee data extraction.

## Zapier gets excited.

Now that you have a trigger and an action set up, Zapier really wants to turn on the Zap.  We’re not quite ready for that, we want to add a second action to the Zap - to take the extracted fields and put them into a Google Sheet.. So, close the dialog to turn on the Zap, and add another action by pressing the + at the bottom of the screen.

This is confusing, so if you accidentally turn on your Zap - just go back into the edit mode, and you can add another step.

## Step 3 Google Sheet

WE've extracted the data from the Gmail attachment - now we want to do something with that attachment.  In this example, we'll add a row in a Google Sheet with all the details from the invoice:

We’ve created an [invoice demo google sheet](https://docs.google.com/spreadsheets/d/1akRuxXM104pXTrQlBVFTkFaerV75xOGcXz5soREJ4E4/edit?usp=sharing)  Open this google sheet and make a copy into your account (File-> make a copy).

The sheet looks like this: It may have data from a few invoices in it.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f486c7c-Screenshot_2021-10-06_at_19.53.26.png",
        "Screenshot 2021-10-06 at 19.53.26.png",
        1918,
        530,
        "#f7f7f7"
      ]
    }
  ]
}
[/block]
We will fill in a row of this spreadsheet with the data from the Mindee OCR extraction (and if you run it again - fill the next row with new data)

Now back in Zapier add Google Sheets as your 3rd action, and the events ill be to create a Spreadsheet row:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/73cc62a-Screenshot_2021-10-06_at_19.55.19.png",
        "Screenshot 2021-10-06 at 19.55.19.png",
        2098,
        1050,
        "#e7edf7"
      ]
    }
  ]
}
[/block]
Connect your Google Sheets account. Next you'll be asked to find a spreadhseet to connect to. If you've saved a copy of the spreadsheet above in your Google Account, you should be able to find it.  We’ll add a row into Sheet1.

You'll notice that Zapier finds the column names to help you figure out which elements you'd like to add to the sheet row:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9450b40-Screenshot_2021-10-06_at_19.57.38.png",
        "Screenshot 2021-10-06 at 19.57.38.png",
        1898,
        2394,
        "#f6f6f6"
      ]
    }
  ]
}
[/block]
Now we need to tell Zapier what data to place into each column of the row we are adding.  for simplicity, we'll just list the value to search for

* **Email From**: In the Gmail list find the “From” attribute. This will add the email address of who sent you the invoice.

* **Supplier**: in Mindee - search for “Document Inference Prediction Supplier Value”  
* **Date**: in Mindee - search for “Document Inference Prediction Date Value”
* **Due date**: in Mindee - search for “Document Inference Prediction  Due Date Value”
* **Total (before tax)**: in Mindee - search for “Document Inference Prediction  Total Excl Value”
* **Tax**: in Mindee - search for “Document Inference Prediction  Tax Value”
* **Total (incl tax)**: in Mindee - search for “Document Inference Prediction  Total Incl Value”
* **Currency**: in Mindee - search for “Document Inference Prediction  Locale Currency"

When you've completed this, the fields will look something like this:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0cb523b-Screenshot_2021-10-06_at_20.04.49.png",
        "Screenshot 2021-10-06 at 20.04.49.png",
        982,
        1252,
        "#f1f0f0"
      ]
    }
  ]
}
[/block]
Once you select the fields, you can test, and see that the correct rows are populated with the correct values. That’s it. Now you can name your Zap and turn it on for use!

## Testing your Zap

Now you can test your Zap by sending another email to your account with an invoice, and after a few minutes - you’ll see the values appear in your spreadsheet automatically from the Zap.

You can try it out the Zap created in this demo by emailing an invoice to doug+invoice@mindee.co, and it will appear in the Google Sheet listed above.  Do note that even with the +invoice, your email will go into my inbox, and the data will be in a publicly viewable spreadsheet so don’t send anything you don’t the world to see.

## No coding with Mindee

With just a few minutes of work (and with zero coding), we have build a fully functional invoice processing system - invoices sent as email attachments are automatically identified, extracted, and the results are placed in a Google Sheet.

We're very excited about the possible opportunities that no-coding options can bring to the Mindee Community!