---
title: Test your API with Postman
excerpt: ''
hidden: false
---
## Test your document parsing API with Postman

### Objective
In this article, we'll learn how to test a Mindee document parsing API using Postman, a popular developer tool.



### Prerequisites


1. You must have set up a custom document parsing API at https://platform.mindee.com. If you don’t have one ready, set up the demo API using the US tax form W-9 described in [Build your document parsing API](doc:build-your-first-document-parsing-api) .

2. For a better developer experience, we recommend that you train your API model with at least 20 documents (as done in the tutorial mentioned above).

3. The Postman app running on your machine.


## Step 1: Set up Postman


Assuming you already have a data model ready to go, you can test it right away with Postman (or any other tool that understands the [OpenAPI v2 specification](https://swagger.io/specification/v2/) - fka Swagger v2.0).



To do so, head over the **Documentation** page of your Mindee API and select the *download openapi.json* link, as shown below:






[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/62084bb-screenshot-2021-05-02-at-192846.png",
        "screenshot-2021-05-02-at-192846.png",
        1440,
        498,
        "#f9f8f8"
      ]
    }
  ]
}
[/block]
If you didn't follow the tutorial, you can access the [JSON file](https://mindee-public-website.s3.amazonaws.com/blog/2021/05/02/openapi-us-w-9-forms-1.json) and continue along with the tutorial.



Next, open your Postman desktop client and import the json file using the Import menu:






[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/24ddb89-screenshot-2021-05-02-at-214852.png",
        "screenshot-2021-05-02-at-214852.png",
        1440,
        821,
        "#2c2b2a"
      ]
    }
  ]
}
[/block]
Once you have uploaded your file to Postman, you should see the following confirmation screen:






[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2e97e23-screenshot-2021-05-02-at-215123.png",
        "screenshot-2021-05-02-at-215123.png",
        1296,
        839,
        "#333232"
      ]
    }
  ]
}
[/block]
Press the *Import* button. Your w-9 Postman collection shows up in Postman, as follows:




[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/514f1ac-screenshot-2021-05-02-at-215338.png",
        "screenshot-2021-05-02-at-215338.png",
        662,
        526,
        "#323130"
      ]
    }
  ]
}
[/block]
Now, let’s generate an API key so we can test our API in Postman.




## Step 2: Generate an API key



Head over the **API Keys** page of your API Dashboard and press the Create new API key button:






[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/006c79f-screenshot-2021-05-02-at-215446.png",
        "screenshot-2021-05-02-at-215446.png",
        1000,
        422,
        "#f8f8f9"
      ]
    }
  ]
}
[/block]
Enter the name of the application that will use your API key (such as “Postman”) and press the *Create new API key* button. A page similar to the following screenshot appears below:



[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f2807ad-screenshot-2021-05-02-at-215540.png",
        "screenshot-2021-05-02-at-215540.png",
        1000,
        303,
        "#f7f7f8"
      ]
    }
  ]
}
[/block]
Next, copy the API key to your clipboard by pressing the copy icon. Paste this key right away into a text file, we’ll need it in the next step.



## Step 3: Configure Postman environment variables


Back in Postman, create an environment called W-9 and a variable called ```apiToken```:






[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/196150c-screenshot-2021-05-02-at-215926.png",
        "screenshot-2021-05-02-at-215926.png",
        1000,
        739,
        "#302e2e"
      ]
    }
  ]
}
[/block]
In the *Initial Value* column of the ```apiToken``` variable, paste the API key you generated in Step 2 and press the *Add* button.



Once you've added the environment, you can close the *Manage Environments* window. Now select the W-9s environment:





[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3dd1383-screenshot-2021-05-02-at-220319.png",
        "screenshot-2021-05-02-at-220319.png",
        1000,
        279,
        "#2e2c2b"
      ]
    }
  ]
}
[/block]
Congratulations! Your API is now properly configured in Postman.

In the next article, we’ll look at how you can use your API’s Predict endpoint.