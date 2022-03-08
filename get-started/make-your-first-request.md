---
title: Make your first request
excerpt: ''
hidden: false
---

This guide will walk you through the fundamental processes of making API calls and queries using our document parsing APIs.

## Prerequisites
For the following, you'll need a Mindee account. For more information on how to create an account, see [Setup your account section](https://developers.mindee.com/docs/setup-your-account).

## Create an API Key
Once you are logged in, you'll land on the APIs hub page where you can see **Your APIs** which will be empty at the beginning and the off-the-shelf APIs at the **APIs Store**. 

![APIs hub page with Your APIs section on the left and API store section on the right](https://files.readme.io/6345e3a-api-hub-page.png "create an api key")

To create an API key: 

1. Click on any of the API cards on the APIs Store, for this example, we will click on the **Expense Receipts** card. 

![Expense receipts API card on the right](https://files.readme.io/f111f5b-Screenshot_2021-12-02_at_18.05.20.png "create an api key")

2. You'll land on the Expense receipt API dashboard. On the left side menu, click on **API Keys**.

![Expense receipt API dashboard on the right and menu for API keys on the left](https://files.readme.io/6c0cb60-api-dashboard1.png "api dashboard")

3. Click on **Create a new API key** button.

![Button for creating new expense receipt API Key](https://files.readme.io/86f4f94-Screenshot_2021-12-02_at_18.19.19.png "api keys")

4. Give your API key a desired name, for example, _"My First API Key"_ and click on **Create API key**.

![Dialog box for adding a API key name](https://files.readme.io/42c7047-api-key-name.png "api keys")

5. Your API key will be created showing the date and time it was created.

![Section showing the created API key with date and time](https://files.readme.io/7a51fcd-created-api.png "created api keys")

## Get Your Sample Code
![Mindee Sample code located under the API reference tab on the right](https://files.readme.io/424a9f3-expense-reciept-sample-code.png "sample code")

Sample code in several languages and command line tools are provided by Mindee, and they are ready to use by simply copying and pasting them into your coding environments, applications, or command line tools. To make use of this:

1. On the left side of the screen, click on **Documentation**.
2. Under the **API Reference** tab, you'll find the **Sample code** section in a number of popular languages or command line tool. Select according to your desired needs.
3. Select the API key you wish to use.
4. Copy and paste the code below into your applications, coding environments or command line interface. You're ready to go!

## Live Interface
![Live interface section located on the right with extracted fields](https://files.readme.io/2e3e774-Screenshot_2022-01-08_at_01.02.01.png "live interface")

This is your home for no code testing. It is a graphical user interface that allows you to view the file you've uploaded as well as see all of the extracted information including the raw API JSON response in one location. To make use of this feature, on the left side menu, Click on **Live Interface**. There are two approaches to use the Live Interface feature:
- Uploading a **New document**, or
- Making use of the **Use my camera** feature

### Uploading A New Document
With the **New document** feature located at the bottom of the live Interface, you can upload the documents that you want to the Live Interface and this will appear below. To do this, click on the **New document button** and select on the image document you want. You can only upload one document at a time. However, to make uploads faster, you can drag and drop an image document in the image frame.

### Making Use Of The Use My Camera Feature
With the **Use my camera** feature located at the bottom of the live Interface, you can take pictures of your documents. You'll need to allow your browser or web cam to use your camera, otherwise, you won't be able to take a picture of your document. 

### Extracted Fields
You can click on each of the files below to view the extracted fields for each document you have uploaded. Once your document is shown on the live interface, it automatically extracts fields from the document and highlights them. There are two different formats in which the results are shown:
- Expected fields
- API response fields

#### Expected Fields
You can examine the extracted fields using the **Expected fields** column. This is a subset of what the API will return.

![Expected fields column with extracted fields](https://files.readme.io/8a451d6-expected-field.png "extracted fields")

#### API Response
The API response gives a raw JSON of the extracted fields. It is the same response you will get from using the API in your application. There is more detailed information about the extracted data here than in the expected fields. You can easily download it with the arrow button at the top

![API response column with extracted fields](https://files.readme.io/5891586-api-response.png "extracted fields")

