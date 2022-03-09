---
title: Getting started
excerpt: ''
next:
  pages:
    - nodejs-invoice-ocr
    - nodejs-receipt-ocr
    - generate-your-clients
  description: ''
hidden: false
---
Get started with Mindee's Node.js SDK.


[block:callout]
{
  "type": "warning",
  "body": "The Node.js SDK supports Invoice and Receipt OCR APIs. To create a Node.js SDK for a custom-built API from the API Builder, please [follow this guide](doc:generate-your-clients)."
}
[/block]
## Install the mindee node.js helper library
 

The easiest way to install the mindee node.js helper is from NPM. You can run the command below from your project directory to install the library:
[block:code]
{
  "codes": [
    {
      "code": "npm install mindee",
      "language": "shell"
    }
  ]
}
[/block]
 

## Instantiate your Client
 

The mindee.Client needs your API credentials. You can either pass these directly to the constructor (see the code below) or via environment variables.

[block:code]
{
  "codes": [
    {
      "code": "const { Client } = require(\"mindee\");\n\nconst mindeeClient = new Client({\n  invoiceToken: \"yourInvoiceApiKey\",\n  receiptToken: \"yourReceiptApiKey\",\n});",
      "language": "javascript"
    }
  ]
}
[/block]
 

The mindee.Client can take multiple parameters. Some of those parameters can also be set using environment variables. For any parameter, if the env variable and the parameter are both defined, the parameter used will be the one set in the mindee.Client. This is the list of the different parameters:
[block:parameters]
{
  "data": {
    "h-0": "Parameters",
    "h-1": "Environment variable",
    "0-0": "invoiceToken",
    "1-0": "receiptToken",
    "4-0": "debug",
    "3-0": "debug",
    "2-0": "throwOnError",
    "h-2": "Details",
    "0-1": "MINDEE_INVOICE_TOKEN",
    "1-1": "MINDEE_RECEIPT_TOKEN",
    "3-1": "MINDEE_DEBUG",
    "3-2": "false by default) If true, logging will be in debug mode",
    "2-2": "(true by default) If true, the SDK will throw an error when the API response status is different from 200",
    "0-2": "Invoice API key",
    "1-2": "Receipt API key"
  },
  "cols": 3,
  "rows": 4
}
[/block]
We suggest storing your credentials as environment variables. Why? You'll never have to worry about committing your credentials and accidentally posting them somewhere public.

## Parse a document
[block:code]
{
  "codes": [
    {
      "code": "const { Client } = require(\"mindee\");\n\nconst mindeeClient = new Client({\n  invoiceToken: \"yourInvoiceApiKey\",\n  receiptToken: \"yourReceiptApiKey\"\n});\n\nmindeeClient.invoice.parse(\n    {\n        input : \"invoice.pdf\",\n        inputType : 'path'\n    }\n)\n    .then((res) => {\n        console.log(res.invoice);\n    })\n    .catch((err) => {\n        console.error(err);\n    });\n\nmindeeClient.receipt.parse(\n    {\n        input : \"receipt.jpg\",\n        inputType : 'path',\n    }\n)\n    .then((res) => {\n        console.log(res.receipt);\n    })\n    .catch((err) => {\n        console.error(err);\n    });",
      "language": "javascript"
    }
  ]
}
[/block]
## Input types

You can pass your input file in three ways:

### From file path

[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n    {\n        input : \"invoice.pdf\",\n        inputType : 'path',\n    }\n)\n    .then((res) => {\n        console.log(res.invoice);\n    })\n    .catch((err) => {\n        console.error(err);\n    });",
      "language": "javascript"
    }
  ]
}
[/block]
### From a file object

[block:code]
{
  "codes": [
    {
      "code": "const fs = require(\"fs\");\n\nconst file = fs.createReadStream(\"./path/to/img/or/pdf\");\n\nmindeeClient.invoice.parse(\n    {\n        input : file,\n        inputType : 'stream',\n    }\n)\n    .then((res) => {\n        console.log(res.invoice);\n    })\n    .catch((err) => {\n        console.error(err);\n    });",
      "language": "javascript"
    }
  ]
}
[/block]
### From a base64
[block:code]
{
  "codes": [
    {
      "code": "const base64 = fs.readFileSync(\"./inv.pdf\", {\n  encoding: \"base64\",\n});\n\nmindeeClient.invoice.parse(\n    {\n        input : base64,\n        inputType : 'base64',\n    }\n)\n    .then((res) => {\n        console.log(res.invoice);\n    })\n    .catch((err) => {\n        console.error(err);\n    });",
      "language": "javascript"
    }
  ]
}
[/block]