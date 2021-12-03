---
title: Getting started
excerpt: ''
next:
  pages:
    - python-receipt-ocr
    - python-passport-ocr
    - python-invoice-ocr
  description: ''
---
Get started with Mindee's python SDK.

[block:callout]
{
  "type": "warning",
  "body": "The python SDK supports Invoice, Passport and Receipt OCR APIs. To create a Python SDK for a custom-built API from the API Builder, please [Follow this guide](doc:generate-your-clients).",
  "title": ""
}
[/block]
 

## Install the mindee python helper library

 

Install from PyPi using pip, a package manager for Python.
 

[block:code]
{
  "codes": [
    {
      "code": "pip install mindee",
      "language": "shell"
    }
  ]
}
[/block]
 

Don't have pip installed? Try installing it, by running this from the command line:
[block:code]
{
  "codes": [
    {
      "code": "$ curl https://bootstrap.pypa.io/get-pip.py | python",
      "language": "shell"
    }
  ]
}
[/block]
 

Getting started with the Mindee API couldn't be easier. Create a Client and you're ready to go.

 

## Instantiate your Client
 

The mindee.Client needs your API credentials. You can either pass these directly to the constructor (see the code below) or via environment variables.

 

Depending on what type of document you want to parse, you need to add specifics auth token for each endpoint.

 
[block:code]
{
  "codes": [
    {
      "code": "from mindee import Client\n\nmindee_client = Client(\n    expense_receipt_token=\"your_expense_receipts_api_token_here\",\n    invoice_token=\"your_invoice_api_token_here\",\n    passport_token=\"your_passport_api_token_here\",\n    raise_on_error=True\n)",
      "language": "python"
    }
  ]
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Parameters",
    "h-1": "Details",
    "0-0": "expense_receipt_token",
    "1-0": "invoice_token",
    "2-0": "passport_token",
    "3-0": "raise_on_error",
    "3-1": "**(boolean, default True) **Specify whether or not to raise an Exception when HTTP errors occur.",
    "0-1": "(string) API key for [Receipt OCR API](doc:receipt-ocr)",
    "1-1": "(string) API key for [Invoice OCR API](doc:invoice-ocr)",
    "2-1": "(string) API key for [Passport OCR API](doc:passport-ocr)"
  },
  "cols": 2,
  "rows": 4
}
[/block]
We suggest storing your credentials as environment variables. Why? You'll never have to worry about committing your credentials and accidentally posting them somewhere public.

 

## Parse a document
[block:code]
{
  "codes": [
    {
      "code": "from mindee import Client\n\nmindee_client = Client(\n    expense_receipt_token=\"your_expense_receipts_api_token_here\",\n    invoice_token=\"your_invoice_api_token_here\",\n    passport_token=\"your_passport_api_token_here\",\n    raise_on_error=True\n)\n\n# Parse a receipt\nreceipt_data = mindee_client.parse_receipt(\"/path/to/file\")\n\n# Parse an invoice\ninvoice_data = mindee_client.parse_invoice(\"/path/to/file\")\n\n# Parse a passport\npassport_data = mindee_client.parse_passport(\"/path/to/file\")\n",
      "language": "python"
    }
  ]
}
[/block]
## Input types
 

You can pass your input file in three ways:

**From file path**

 
[block:code]
{
  "codes": [
    {
      "code": "receipt_data = mindee_client.parse_receipt('/path/to/file', input_type=\"path\")",
      "language": "python"
    }
  ]
}
[/block]
** From a file object**


[block:code]
{
  "codes": [
    {
      "code": "with open('/path/to/file', 'rb') as fp:\n     receipt_data = mindee_client.parse_receipt(fp, input_type=\"file\")\n ",
      "language": "python"
    }
  ]
}
[/block]
**From a base64**
 
[block:code]
{
  "codes": [
    {
      "code": "receipt_data = mindee_client.parse_receipt(base64_string, input_type=\"base64\")",
      "language": "python"
    }
  ]
}
[/block]