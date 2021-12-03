---
title: Python Receipt OCR
excerpt: ''
---
## Receipt data structure
[block:code]
{
  "codes": [
    {
      "code": "from mindee import Client\n\nmindee_client = Client(\n    expense_receipt_token=\"your_expense_receipts_api_key_here\",\n)\n\nreceipt_data = mindee_client.parse_receipt('/path/to/file', input_type=\"path\")",
      "language": "python"
    }
  ]
}
[/block]
### Document level prediction

The receipt_data object returned by the **parse_receipt** method contains the following elements:
[block:code]
{
  "codes": [
    {
      "code": "receipt_data.receipt # returns a unique object from class Receipt",
      "language": "python"
    }
  ]
}
[/block]
The receipt attribute is the Receipt object constructed by gathering all the pages into a single document. The method used for creating a single receipt object with multiple pages relies on field confidence scores. Basically, we iterate over each page, and for each field, we keep the one that has the highest probability.

### Page level prediction
[block:code]
{
  "codes": [
    {
      "code": "receipt_data.receipts # [Receipt, Receipt ...] ",
      "language": "python"
    }
  ]
}
[/block]
For multi-pages pdf, the receipts attribute contains one receipt object per input. For a single-page pdf or an image, the list will only contain 1 item, and for a multi-page pdf, it will contain one item per page.

 
### Raw HTTP Response

[block:code]
{
  "codes": [
    {
      "code": "receipt_data.http_response # full HTTP request object ",
      "language": "python"
    }
  ]
}
[/block]
Contains the full Mindee API HTTP response object in JSON format

 

 ## Extracted receipt fields
 

Each receipt object contains a set of different fields.


To access a receipt object, you need to create a mindee.Client and call the Client.parse_receipt method:
[block:code]
{
  "codes": [
    {
      "code": "from mindee import Client\n\n# Instantiate your client\nmindee_client = Client(expense_receipts_token=\"your_api_key_here\")\n\n# Call the Mindee expense receipts endpoint and parse the result\nreceipt_data = mindee_client.parse_receipt(\"/path/to/my/file\")",
      "language": "python"
    }
  ]
}
[/block]
 

Whatever the field type, each of them contains the four following attributes:

 

> **value**: (Str or Float depending on the field type), corresponds to the field value. Set to None if the >field was not extracted.
> **probability**: (Float), confidence score of the field prediction.
> **bbox**: (Array[Float]), contains the relative vertices coordinates of the bounding box containing the > field in the image. If the field is not written, the bbox is an empty array. 
>r **econstructed**: (Bool), True if the field was reconstructed using other fields.
 

Depending on the Field type, there can be extra attributes.


### Total amounts
 

**receipt.total_incl:** Total amount including taxes

[block:code]
{
  "codes": [
    {
      "code": "# To get the total amount including taxes value (float), ex: 14.24\ntotal_incl = receipt_data.receipt.total_incl.value",
      "language": "python"
    }
  ]
}
[/block]
 

**receipt.total_excl**: Total amount excluding taxes

[block:code]
{
  "codes": [
    {
      "code": "# To get the total amount excluding taxes value (float), ex: 10.21\ntotal_excl = receipt_data.receipt.total_excl.value",
      "language": "python"
    }
  ]
}
[/block]
 

**receipt.total_tax**: Total tax value reconstructed from tax lines
[block:code]
{
  "codes": [
    {
      "code": "# To get the total tax amount value (float), ex: 8.42\ntotal_tax = receipt_data.receipt.total_tax.value",
      "language": "python"
    }
  ]
}
[/block]
 

 

### Taxes
 

**receipt.taxes**: Array of Tax fields

Each of the tax field has two extra attributes:

> **code**: (String), Optional tax code. (HST, GST... for canadian; City Tax, State tax for US etc..)
> **rate**: (Float), Optional tax rate.
 

[block:code]
{
  "codes": [
    {
      "code": "# To get the list of taxes\ntaxes = receipt_data.receipt.taxes\n\n# Loop on each Tax field\nfor tax in taxes:\n   # To get the tax amount\n   tax_amount = tax.value\n\n   # To get the tax code for from a tax object\n   tax_code = tax.code\n  \n   # To get the tax rate\n   tax_rate = tax.rate",
      "language": "python"
    }
  ]
}
[/block]

 

### Dates
 

Each date field comes with an extra attribute:


> **date_object**: (Datetime), datetime object from python datetime.date library
 

 **receipt.date**: Payment date related to the receipt

[block:code]
{
  "codes": [
    {
      "code": "# To get the receipt date of issuance (string)\nreceipt_date = receipt_data.receipt.value",
      "language": "python"
    }
  ]
}
[/block]
 

### Supplier informations
 

**receipt.supplier**: Supplier name as written in the receipt (logo)
[block:code]
{
  "codes": [
    {
      "code": "# To get the supplier name\nsupplier_name = receipt_data.receipt.supplier.value",
      "language": "python"
    }
  ]
}
[/block]
### Locale and currency


**locale**: Language ISO code

Contains an extra attribute:

**currency**: (String), ISO currency code
 
[block:code]
{
  "codes": [
    {
      "code": "# To get the total language code\nlanguage = receipt_data.receipt.locale.value\n\n# To get the receipt currency code\ncurrency = receipt_data.receipt.locale.currency",
      "language": "python"
    }
  ]
}
[/block]
### Category
 

**category**: Receipt category among the list:  toll, food, parking, transport, accommodation, gasoline, miscellaneous

[block:code]
{
  "codes": [
    {
      "code": "# To get the category\ncategory = receipt_data.receipt.category.value",
      "language": "python"
    }
  ]
}
[/block]
### Time
 

**time**: Time of purchase with 24 hours formatting (hh:mm)


[block:code]
{
  "codes": [
    {
      "code": "# To get the category\ncategory = receipt_data.receipt.time.value",
      "language": "python"
    }
  ]
}
[/block]