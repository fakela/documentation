---
title: Node.js invoice OCR
excerpt: ''
---
## Invoice data structure


To access an invoice object, you need to create a **mindee.Client **and call the **Client.invoice.parse** method:
[block:code]
{
  "codes": [
    {
      "code": "const { Client } = require(\"mindee\");\n\nconst mindeeClient = new Client({\n  invoiceToken: \"yourInvoiceToken\"\n});\n\nmindeeClient.invoice.parse(\n  {\n    input : \"invoice.pdf\",\n    inputType : 'path',\n    filename : undefined,\n    cutPdf : true,\n    includeWords : false\n  }\n)\n  .then((res) => {\n    console.log(res.invoice);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]

### Client.invoice.parse parameters
[block:parameters]
{
  "data": {
    "h-0": "Parameter name",
    "h-1": "Description",
    "h-2": "Default value",
    "0-0": "input",
    "1-0": "inputType",
    "2-0": "cutPdf",
    "3-0": "includeWords",
    "0-1": "Document object",
    "1-1": "**path**: File path\n**stream**: From file object\n**base64**: From a base64 encoded file",
    "1-2": "path",
    "2-1": "(Boolean) If set to **true**, when sending a multi pages pdf of more than 5 pages, the library create a new pdf by concatenating the first 4 pages and the last page.",
    "2-2": "true",
    "4-0": "filename",
    "4-1": "(String) Specify a filename of your input.",
    "4-2": "undefined",
    "3-2": "false",
    "3-1": "(Boolean) If set to **true**, the raw_http response will include all the words in the document associated to their positions."
  },
  "cols": 3,
  "rows": 5
}
[/block]
### Document level prediction

```res.invoice```

The document attribute is the Invoice object constructed by gathering all the pages into a single document.


[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n  {\n    input : \"invoice.pdf\",\n    inputType : 'path',\n    cutPdf : true,\n    includeWords : false\n  }\n)\n  .then((res) => {\n    console.log(res.invoice);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]
### Page level prediction

```res.invoices```

For multi-pages pdf, the 'pages' attribute is a list of document objects, each object is constructed using a unique page of the pdf.


[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n  {\n    input : \"invoice.pdf\",\n    inputType : 'path',\n    cutPdf : true,\n    includeWords : false\n  }\n)\n  .then((res) => {\n    console.log(res.invoices);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]
### Raw HTTP response

Get the full API response as a Node.js HTTP Response object
[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n {\n   input : \"invoice.pdf\",\n   inputType : 'path',\n   cutPdf : true,\n   includeWords : false\n }\n)\n  .then((res) => {\n    console.log(res.httpResponse);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]

## Extracted invoice fields

Each invoice object contains a set of different fields.

Most fields contain the following attributes:

>**value**: (Str or Float depending on the field type), corresponds to the field value. Set to None if the field was not extracted. For reconstructed fields, the value attribute might not be present in the field (this will be changed in a later version of the node.js SDK)
>**probability**: (Float), the confidence score of the field prediction.
>**bbox**:(Array[Float]), contains the relative vertices coordinates of the bounding box containing the field in the image. If the field is not written, the bbox is an empty array. 
>**reconstructed**: (Bool), True if the field was reconstructed using other fields.
>**pageNumber**: (int), the page number of the extracted field
 

Depending on the Field type, there can be extra attributes.

### Total amounts

invoice.totalIncl: Total amount including taxes
invoice.totalExcl: Total amount excluding taxes
invoice.totalTax: Total tax value reconstructed from tax lines

[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n {\n   input : \"invoice.pdf\",\n   inputType : 'path',\n }\n)\n  .then((res) => {\n    console.log(res.invoice.totalIncl);\n    console.log(res.invoice.totalExcl);\n    console.log(res.invoice.totalTax);\n  })\n  .catch((err) => {\n    console.error(err);\n  });\n ",
      "language": "javascript"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  value: 38.92,\n  probability: 0.99,\n  bbox: [\n    [ 0.865, 0.641 ],\n    [ 0.955, 0.641 ],\n    [ 0.955, 0.675 ],\n    [ 0.865, 0.675 ]\n  ]\n}\n{\n  pageNumber: 0,\n  reconstructed: false,\n  value: 36.72,\n  probability: 0.99,\n  bbox: [\n    [ 0.898, 0.709 ],\n    [ 0.955, 0.709 ],\n    [ 0.955, 0.734 ],\n    [ 0.898, 0.734 ]\n  ]\n}\n{\n  pageNumber: 0,\n  reconstructed: true,\n  value: 2.2,\n  probability: 0.9801,\n  bbox: []\n}",
      "language": "json"
    }
  ]
}
[/block]
 

### Taxes
 

invoice.taxes: Array of Tax fields


Each the tax field has an extra attributes:

> **rate**: (Float), Optional tax rate.
 

[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n {\n   input : \"invoice.pdf\",\n   inputType : 'path',\n }\n)\n  .then((res) => {\n    console.log(res.invoice.taxes);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "[\n  {\n    pageNumber: 0,\n    reconstructed: false,\n    value: 1.7,\n    probability: 1,\n    bbox: [ [Array], [Array], [Array], [Array] ],\n    rate: 20\n  }\n]",
      "language": "json"
    }
  ]
}
[/block]
 

 

### Dates
  

invoice.invoiceDate: Issuance date of the invoice

invoice.dueDate: Due date of payment of the invoice


Each date field comes with an extra attribute:

> **dateObject**:: (Datetime), DateTime object 
 
 

[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n {\n   input : \"invoice.pdf\",\n   inputType : 'path',\n }\n)\n  .then((res) => {\n    console.log(res.invoice.invoiceDate);\n    console.log(res.invoice.dueDate);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  value: '2021-01-28',\n  probability: 0.99,\n  bbox: [\n    [ 0.395, 0.448 ],\n    [ 0.474, 0.448 ],\n    [ 0.474, 0.462 ],\n    [ 0.395, 0.462 ]\n  ],\n  dateObject: '2021-01-28T00:00:00.000Z'\n}\n{\n  pageNumber: 0,\n  reconstructed: false,\n  value: '2021-01-28',\n  probability: 0.94,\n  bbox: [\n    [ 0.394, 0.448 ],\n    [ 0.474, 0.448 ],\n    [ 0.474, 0.464 ],\n    [ 0.394, 0.464 ]\n  ],\n  dateObject: '2021-01-28T00:00:00.000Z'\n}",
      "language": "json"
    }
  ]
}
[/block]
 
### Supplier information
 

invoice.supplier: Supplier name as written in the invoice
invoice.paymentDetails: List of Supplier's payment details written in the invoice
invoice.companyNumber: Supplier's company number


Each payment details object contains extra attributes:

> **iban**: (String)
> **swift**: (String)


Each company number object contains an extra attribute:

> **type**: (String), Generic: VAT NUMBER, TAX ID, GST NUMBER, COMPANY REGISTRATION NUMBER or country-specific: TIN (United States), GST/HST (Canada), SIREN/SIRET (France), UEN (Singapore), STNR (Germany), KVK (NL), CIF (Spain), NIF (Portugal), CVR (Denmark), CF (Italy), DIC (Czech Republic), RFC (Mexico), GSTIN (India) ...etc
[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n {\n   input : \"invoice.pdf\",\n   inputType : 'path',\n }\n)\n  .then((res) => {\n    console.log(res.invoice.supplier);\n    console.log(res.invoice.paymentDetails);\n    console.log(res.invoice.companyNumber);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  value: 'Google',\n  probability: 0.18,\n  bbox: [\n    [ 0.125, 0.074 ],\n    [ 0.172, 0.074 ],\n    [ 0.172, 0.083 ],\n    [ 0.125, 0.083 ]\n  ]\n}\n[\n  {\n    pageNumber: 0,\n    reconstructed: false,\n    value: 'EE657700xxxxxx265345',\n    probability: 0.97,\n    bbox: [ [Array], [Array], [Array], [Array] ],\n    iban: 'EE6xxxxxxxxxx345',\n    swift: 'LxxxxxE22'\n  }\n]\n[\n  {\n    pageNumber: 0,\n    reconstructed: false,\n    value: '513xxxx80',\n    probability: 0.9,\n    bbox: [ [Array], [Array], [Array], [Array] ],\n    type: 'NIF'\n  },\n  {\n    pageNumber: 0,\n    reconstructed: false,\n    value: 'Pxxxxxx004',\n    probability: 0.99,\n    bbox: [ [Array], [Array], [Array], [Array] ],\n    type: 'VAT NUMBER'\n  }\n]",
      "language": "json"
    }
  ]
}
[/block]
 

 

### Locale and currency
 

locale: Language ISO code

Contains two extra attributes:
> **language**: (String), first 2 letters of language ISO code
> **currency**: (String), ISO currency code
 

[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n {\n   input : \"invoice.pdf\",\n   inputType : 'path',\n }\n)\n  .then((res) => {\n    console.log(res.invoice.locale);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  probability: 0,\n  bbox: [],\n  language: 'pt',\n  currency: 'EUR'\n}",
      "language": "json"
    }
  ]
}
[/block]
 

 

### InvoiceNumber
 

[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n {\n   input : \"invoice.pdf\",\n   inputType : 'path',\n }\n)\n  .then((res) => {\n    console.log(res.invoice.invoiceNumber);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  value: 'Fxxxxxx1/4',\n  probability: 0.98,\n  bbox: [\n    [ 0.805, 0.09 ],\n    [ 0.954, 0.09 ],\n    [ 0.954, 0.112 ],\n    [ 0.805, 0.112 ]\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]

### checklist

Three boolean attributes that check the extracted data with tests. Note: a false value does not mean inaccurate extraction, but true is another confirmation of accurate data extraction.

[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.invoice.parse(\n {\n   input : \"invoice.pdf\",\n   inputType : 'path',\n }\n)\n  .then((res) => {\n    console.log(res.invoice.invoiceNumber);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "NodeJS"
    }
  ]
}
[/block]
> **taxesMatchTotalIncl**: (Boolean): returns true if (tax rate)*totalExcl +totalExcl = TotalIncl
> **taxesMatchTotalExcl**: (Boolean):  returns true if sum(tax value)/(tax rate))  = totalExcl
> **taxesPlusTotalExclMatchTotalIncl**: Boolean: returns true if (all taxes) + totalexcl = TotalIncl
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"taxesMatchTotalIncl\": true,\n    \"taxesMatchTotalExcl\": true,\n    \"taxesPlusTotalExclMatchTotalIncl\": true\n  }",
      "language": "json"
    }
  ]
}
[/block]