---
title: Invoice API
excerpt: ''
---

## Invoice data structure

```python
from mindee import Client

mindee_client = Client().config_invoice("invoice-api-key")
invoice_data = mindee_client.doc_from_path("/path/to/file").parse("invoice")
```

### Document level prediction

The document attribute is the Invoice object constructed by gathering all the pages into a single document.
[block:code]
{
  "codes": [
    {
      "code": "invoice_data.invoice # returns a unique object from class Invoice",
      "language": "python"
    }
  ]
}
[/block]

### Page level prediction

For multi-pages pdf, the 'pages' attribute is a list of document objects, each object is constructed using a unique page of the pdf.
[block:code]
{
  "codes": [
    {
      "code": "invoice_data.invoices # [Invoice, Invoice ...] ",
      "language": "python"
    }
  ]
}
[/block]
### Raw HTTP response
[block:code]
{
  "codes": [
    {
      "code": "invoice_data.http_response # full HTTP request object ",
      "language": "python"
    }
  ]
}
[/block]
Contains the full Mindee API HTTP response object in JSON format


## Extracted invoice fields

Each invoice object contains a set of different fields.


To access an invoice object, you need to create a **mindee.Client **and call the Client.parse_invoice method:
[block:code]
{
  "codes": [
    {
      "code": "from mindee import Client\n\n# Instantiate your client\nmindee_client = Client(invoice_token=\"your_api_key_here\")\n\n# Call the Mindee invoice endpoint and parse the result\ninvoice_data = mindee_client.parse_invoice(\"/path/to/my/file\")",
      "language": "python"
    }
  ]
}
[/block]
Each field contains the four following attributes:


> **value**: (Str or Float depending on the field type), corresponds to the field value. Set to None if the >field was not extracted.
> **probability**: (Float), the confidence score of the field prediction.
> **bbox**: (Array[Float]), contains the relative vertices coordinates of the bounding box containing the > field in the image. If the field is not written, the bbox is an empty array. 
> **reconstructed**: (Bool), True if the field was reconstructed using other fields.

Depending on the Field type, there can be extra attributes.


### Total amounts
 

 **Invoice.total_incl**: Total amount including taxes

[block:code]
{
  "codes": [
    {
      "code": "# To get the total amount including taxes value (float), ex: 14.24\ntotal_incl = invoice_data.invoice.total_incl.value",
      "language": "python"
    }
  ]
}
[/block]
 

 **Invoice.total_excl**: Total amount excluding taxes

[block:code]
{
  "codes": [
    {
      "code": "# To get the total amount excluding taxes value (float), ex: 10.21\ntotal_excl = invoice_data.invoice.total_excl.value",
      "language": "python"
    }
  ]
}
[/block]
 

**Invoice.total_tax**: Total tax value reconstructed from tax lines


[block:code]
{
  "codes": [
    {
      "code": "# To get the total tax amount value (float), ex: 8.42\ntotal_tax = invoice_data.invoice.total_tax.value",
      "language": "python"
    }
  ]
}
[/block]
 
### Taxes
 

**invoice.taxes**: Array of Tax fields

Each of the tax fields has two extra attributes:


> **code**: (String), Optional tax code. (HST, GST... for Canadian; City Tax, State tax for US, etc..)
> **rate**: (Float), Optional tax rate.

[block:code]
{
  "codes": [
    {
      "code": "# To get the list of taxes\ntaxes = invoice_data.invoice.taxes\n\n# Loop on each Tax field\nfor tax in taxes:\n   # To get the tax amount\n   tax_amount = tax.value\n\n   # To get the tax code for from a tax object\n   tax_code = tax.code\n  \n   # To get the tax rate\n   tax_rate = tax.rate",
      "language": "python"
    }
  ]
}
[/block]
### Dates
 

Each date field comes with an extra attribute:

> **date_object**: (Datetime), datetime object from python datetime.date library
 

 **invoice.invoice_date**: Date of issuance of the invoice

[block:code]
{
  "codes": [
    {
      "code": "# To get the invoice date of issuance (string)\ninvoice_date = invoice_data.invoice.invoice_date.value",
      "language": "python"
    }
  ]
}
[/block]
 

**invoice.due_date**: Payment due date of the invoice

[block:code]
{
  "codes": [
    {
      "code": "# To get the invoice due date (string)\ndue_date = invoice_data.invoice.invoice_date.value",
      "language": "python"
    }
  ]
}
[/block]
### Supplier information
 

 **Invoice.supplier**: Supplier name as written in the invoice (logo or supplier Infos
[block:code]
{
  "codes": [
    {
      "code": "# To get the supplier name\nsupplier_name = invoice_data.invoice.supplier.value",
      "language": "python"
    }
  ]
}
[/block]
 

**Invoice.payment_details**: List of invoice's supplier payment details information.

Each object in the list contains extra attributes:

> **iban**: (String)
> **swift**: (String)
> **routing_number**: (String)
> **account_number**: (String)
[block:code]
{
  "codes": [
    {
      "code": "# To get the list of payment details\npayment_details = invoice_data.invoice.payment_details\n\n# Loop on each object\nfor payment_detail in payment_details:\n   # To get the IBAN\n   iban = payment_details.iban\n\n   # To get the swift\n   swift = payment_details.swift\n\n   # To get the routing number\n   routing_number = payment_details.routing_number\n\n   # To get the account_number\n   account_number = payment_details.account_number\n",
      "language": "python"
    }
  ]
}
[/block]
**Invoice.company_number**:  List of detected company registration number.

Each object in the list contains an extra attribute:

> **type**: (String), Generic: VAT NUMBER, TAX ID, GST NUMBER, COMPANY REGISTRATION NUMBER > or country specific: TIN (United States), GST/HST (Canada), SIREN/SIRET (France), UEN (Singapore), 
> STNR (Germany), KVK (NL), CIF (Spain), NIF (Portugal), CVR (Denmark), CF (Italy), DIC (Czech Republic), > RFC (Mexico), GSTIN (India) ...etc
[block:code]
{
  "codes": [
    {
      "code": "\n# To get the list of company numbers\ncompany_registration_numbers = invoice_data.invoice.company_number\n\n# Loop on each object\nfor company_number in company_registration_numbers:\n   # To get the type of number\n   company_number_type = company_number.type\n\n   # To get the company number\n   company_number_value = company_number.value\n \n",
      "language": "python"
    }
  ]
}
[/block]
### Locale and currency
 

**invoice_data.locale**: Language ISO code

Contains an extra attribute:
> **currency**: (String), ISO currency code

[block:code]
{
  "codes": [
    {
      "code": "# To get the total language code\nlanguage = invoice_data.invoice.locale.value\n\n# To get the invoice currency code\ncurrency = invoice_data.invoice.locale.currency",
      "language": "python"
    }
  ]
}
[/block]