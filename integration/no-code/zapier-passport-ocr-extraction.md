---
title: 'Zapier: Passport OCR Extraction'
excerpt: ''
---
Every time you plan an international trip, you are asked for  your passport number, date of birth, country of citizenship, so that you can prove who you are.

What if the airlines had a specialized tool to extract this information from an official document like a passport?  You could simply upload an image, and the'd extract the data, and enter it into their database.

With Mindee's Passport OCR API it is possible... using Mindee and Zapier - you can do it with no code!

All you need is 

1. A Google account 
2. A free [Zapier account](https://zapier.com)
3. A free [Mindee API key](https://platform.mindee.com/apishub/products/mindee/passport?setup=default#tokens)

To do this work with no coding at all, we'll use Zapier.  Zapier is a no code service that connects different tools with a secure no-code interface.  They call the connections “Zaps.”  Each Zap has a “trigger” an event that starts the process, and an "action" that occurs after the trigger has fired.

In the case of the Zap we are building, you will need a premium account ($29.95/ month). If you are a new user (or if you have a new Zapier account), you'll have free premium access for a week (but your Zap will turn off when the trial ends).

## Our Zap Trigger

We'll create a simple Google Form that will ask for a passport image.  When the form is submitted, it is saved in Google Drive.  Our Zap will be triggered by "New File in Google Drive."

### Creating a Google Form

From your Google account - you can create a form at [Google Forms](https://docs.google.com/forms). We've created a simple form that only asks for a file upload for a passport:



[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a7d6fda-Screenshot_2021-10-13_at_17.48.55.png",
        "Screenshot 2021-10-13 at 17.48.55.png",
        1584,
        980,
        "#f0edf6"
      ]
    }
  ]
}
[/block]
You can try this form out [yourself](https://docs.google.com/forms/d/e/1FAIpQLSdycYuOhjMAXY85CeFZQu7RiL6-EUThOzSqy6jM4sx6U4JGjg/viewform). Please don't send real passport photos, that is not really a secure way to handle private information.

Now, all the files uploaded will appear in a folder in my Google Drive. This is what will trigger our zap.  At Zapier.com, click the "Create Zap" button


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3ddc05d-Screenshot_2021-10-13_at_17.54.04.png",
        "Screenshot 2021-10-13 at 17.54.04.png",
        952,
        660,
        "#e6e6e7"
      ]
    }
  ]
}
[/block]
Our Trigger will be from Google Drive.  We want to trigger whenever there is a new file in a folder (note that the file upload folder may be 2 layers deep in your Google Drive):

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/50454d9-Screenshot_2021-10-13_at_21.26.06.png",
        "Screenshot 2021-10-13 at 21.26.06.png",
        2560,
        1710,
        "#f4f5f5"
      ]
    }
  ]
}
[/block]
You'll be asked to sign into Google, and to share your Drive access to Zapier.  The next steps are share the folder, and to choose the folder.  Google Drive names the folder with the name of the Google Form, which is handy for finding the correct content.

Now, to test this trigger, you must upload a passport using the form, so that Zapier can find a file.  I recommend the [Isabel Santos](https://drive.google.com/file/d/1i4-fhncwKfTJIdqwjuM0y-pmn0yL0tf0/view?usp=sharing) fake passport (Google it, it's a bit of a ride - and the Bruce Lee signature is the pièce de résistance).

## Adding an Action

The Zap will Trigger when a new file lands in Google Drive. Now the Action to undertake is to parse the passport photo with Mindee, and add it to a database.  This is actually 2 actions: Mindee OCR extraction and then depositing the extracted results.  First, of course is to add the Mindee Passport Action:



[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9a07584-Screenshot_2021-10-13_at_21.28.22.png",
        "Screenshot 2021-10-13 at 21.28.22.png",
        2128,
        1346,
        "#f3f4f5"
      ]
    }
  ]
}
[/block]
You'll be asked to sign in to a Mindee account.  This is the third tutorial in our Zapier suite, so we have logged in for Invoices and Receipts - but we need to connect a new account for the Passport endpoint:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/37ee3ba-Screenshot_2021-10-13_at_21.29.47.png",
        "Screenshot 2021-10-13 at 21.29.47.png",
        2058,
        1306,
        "#e7e7e8"
      ]
    }
  ]
}
[/block]
Choose the Passport API, and add an API key from your [Mindee Dashboard](https://platform.mindee.com/apishub/products/mindee/passport?setup=default#tokens) (this is a fake API key - no security issues here)
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1faa832-Screenshot_2021-10-13_at_21.31.59.png",
        "Screenshot 2021-10-13 at 21.31.59.png",
        1422,
        976,
        "#eceded"
      ]
    }
  ]
}
[/block]
The document to send to Mindee is clearly the document that was uploaded to Google drive (but you have to tell Zapier that):


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a0832df-Screenshot_2021-10-13_at_21.35.23.png",
        "Screenshot 2021-10-13 at 21.35.23.png",
        2254,
        1274,
        "#eaecf4"
      ]
    }
  ]
}
[/block]
You can test this Action, and you should get a 201 response from Mindee with the extracted data.

Now, we have the data, let's place it in a database.  there are a lot of databases in Zapier, but we'll use everyone's favourite - a Google Sheet :)

We create a [Sheet](https://docs.google.com/spreadsheets/d/1h217kAVWFrRnsQn6unD_B-gfFmeX9FaZzSddyBJj4YQ/edit?usp=sharing) in our Google account, naming columns to associate with passport data, and link to it in Zapier:





[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bb3b316-Screenshot_2021-10-13_at_21.41.42.png",
        "Screenshot 2021-10-13 at 21.41.42.png",
        2104,
        2380,
        "#eeeff4"
      ]
    }
  ]
}
[/block]
We fill in the predicted values from Mindee into the columns that Zapier extracted from the spreadsheet, and when we test the Zap, the values are added into our 'database':
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/26b5585-Screenshot_2021-10-13_at_21.44.39.png",
        "Screenshot 2021-10-13 at 21.44.39.png",
        1924,
        610,
        "#f2f2f2"
      ]
    }
  ]
}
[/block]
And thats all there is to it.  We've build a sample app that an airline could use to simplify the data entry for international travel - with just a few clicks and using no code!

> Clearly this is a sample app - as this sort of data does require more security than storing in a Google account.  But as a proof of concept, it shows the process that one could follow.  

there are thousands of applications already set up in Zapier - and we're excited to see what sorts of apps can be built with Mindee.