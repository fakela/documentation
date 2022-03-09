---
title: Receipt API
excerpt: ''
hidden: false
---
## Receipt data structure


To access a receipt object, you need to create a **mindee.Client **and call the **Client.receipt.parse** method:
[block:code]
{
  "codes": [
    {
      "code": "const { Client } = require(\"mindee\");\n\nconst mindeeClient = new Client({\n  receiptToken: \"yourReceiptToken\"\n});\n\nmindeeClient.receipt.parse(\n    {\n        input : \"receipt.jpg\",\n        inputType : 'path',\n        filename : undefined,\n        cutPdf : true,\n        includeWords : false\n    }\n)\n    .then((res) => {\n        console.log(res.receipt);\n    })\n    .catch((err) => {\n        console.error(err);\n    });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]

### Client.receipt.parse parameters
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

```res.receipt```

The document attribute is the receipt object constructed by gathering all the pages into a single document.


[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.receipt.parse(\n    {\n        input : \"receipt.jpg\",\n        inputType : 'path',\n        cutPdf : true,\n        includeWords : false\n    }\n)\n    .then((res) => {\n        console.log(res.receipt);\n    })\n    .catch((err) => {\n        console.error(err);\n    });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]
### Page level prediction

```res.receipts```

For multi-pages pdf, the 'pages' attribute is a list of document objects, each object is constructed using a unique page of the pdf.


[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.receipt.parse(\n    {\n        input : \"receipt.jpg\",\n        inputType : 'path',\n        cutPdf : true,\n        includeWords : false\n    }\n)\n  .then((res) => {\n    console.log(res.receipts);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
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
      "code": "mindeeClient.receipt.parse(\n  \t{\n        input : \"receipt.jpg\",\n        inputType : 'path',\n        cutPdf : true,\n        includeWords : false\n    }\n)\n  .then((res) => {\n    console.log(res.httpResponse);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "Node.js"
    }
  ]
}
[/block]

## Extracted receipt fields

Each receipt object contains a set of different fields.

Most fields contain the following attributes:

>**value**: (Str or Float depending on the field type), corresponds to the field value. Set to None if the field was not extracted. For reconstructed fields, the value attribute might not be present in the field (this will be changed in a later version of the node.js SDK)
>**probability**: (Float), the confidence score of the field prediction.
>**bbox**:(Array[Float]), contains the relative vertices coordinates of the bounding box containing the field in the image. If the field is not written, the bbox is an empty array. 
>**reconstructed**: (Bool), True if the field was reconstructed using other fields.
>**pageNumber**: (int), the page number of the extracted field
 

Depending on the Field type, there can be extra attributes.

### Total amounts

receipt.totalIncl: Total amount including taxes
receipt.totalExcl: Total amount excluding taxes
receipt.totalTax: Total tax value reconstructed from tax lines

[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.receipt.parse(\n  \t{\n        input : \"receipt.jpg\",\n        inputType : 'path',\n    }\n)\n  .then((res) => {\n    console.log(res.receipt.totalIncl);\n    console.log(res.receipt.totalExcl);\n    console.log(res.receipt.totalTax);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  value: 10.2,\n  probability: 1,\n  bbox: [\n    [ 0.549, 0.619 ],\n    [ 0.715, 0.619 ],\n    [ 0.715, 0.64 ],\n    [ 0.549, 0.64 ]\n  ]\n}\n{\n  pageNumber: 0,\n  reconstructed: true,\n  value: 8.5,\n  probability: 1,\n  bbox: []\n}\n{\n  pageNumber: 0,\n  reconstructed: true,\n  value: 1.7,\n  probability: 1,\n  bbox: []\n}",
      "language": "json"
    }
  ]
}
[/block]
 

### Taxes

receipt.taxes: Array of Tax fields

Each tax field has two extra attributes:

> **rate**: (Float), Optional tax rate.
> **code**: (String), Optional tax code. (HST, GST... for Canadian; City Tax, State tax for US, etc..)
[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.receipt.parse(\n  \t{\n        input : \"receipt.jpg\",\n        inputType : 'path',\n    }\n)\n  .then((res) => {\n    console.log(res.receipt.taxes);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
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
 
receipt.date: Payment date of the receipt

Each date field comes with an extra attribute:

> **dateObject**:: (Datetime), DateTime object 
 
[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.receipt.parse(\n  \t{\n        input : \"receipt.jpg\",\n        inputType : 'path',\n    }\n)\n  .then((res) => {\n    console.log(res.receipt.date);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
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
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  value: '2016-02-26',\n  probability: 0.99,\n  bbox: [\n    [ 0.479, 0.173 ],\n    [ 0.613, 0.173 ],\n    [ 0.613, 0.197 ],\n    [ 0.479, 0.197 ]\n  ],\n  dateObject: '2016-02-26T00:00:00.000Z'\n}",
      "language": "json"
    }
  ]
}
[/block]
 
### Merchant name
 
receipt.merchantName: Supplier name as written in the receipt (logo)
[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.receipt.parse(\n  \t{\n        input : \"receipt.jpg\",\n        inputType : 'path',\n    }\n)\n  .then((res) => {\n    console.log(res.receipt.merchantName);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
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
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  value: 'CLACHAN',\n  probability: 0.71,\n  bbox: [\n    [ 0.394, 0.068 ],\n    [ 0.477, 0.068 ],\n    [ 0.477, 0.087 ],\n    [ 0.394, 0.087 ]\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
 
### Locale and currency
 

receipt.locale: Language ISO code

Contains three extra attributes:
> **language**: (String), first 2 letters of language ISO code
> **country**: (String), 2 letter abbreviation of country 
> **currency**: (String), ISO currency code
 

[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.receipt.parse(\n  \t{\n        input : \"receipt.jpg\",\n        inputType : 'path',\n    }\n)\n  .then((res) => {\n    console.log(res.receipt.locale);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
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
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  value: 'en-GB',\n  probability: 0.82,\n  bbox: [],\n  language: 'en',\n  country: 'GB',\n  currency: 'GBP'\n}",
      "language": "json"
    }
  ]
}
[/block]
 

 

### Category

receipt.category: Receipt category among the list:  toll, food, parking, transport, accommodation, gasoline, miscellaneous


[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.receipt.parse(\n  \t{\n        input : \"receipt.jpg\",\n        inputType : 'path',\n    }\n)\n  .then((res) => {\n    console.log(res.receipt.category);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "NodeJS"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  value: 'food',\n  probability: 0.99,\n  bbox: []\n}",
      "language": "json"
    }
  ]
}
[/block]

### Time

receipt.time: Time of purchase with 24 hours formatting (hh:mm)
[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.receipt.parse(\n  \t{\n        input : \"receipt.jpg\",\n        inputType : 'path',\n    }\n)\n  .then((res) => {\n    console.log(res.receipt.time);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
      "language": "javascript",
      "name": "NodeJS"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "{\n  pageNumber: 0,\n  reconstructed: false,\n  value: '15:20',\n  probability: 0.99,\n  bbox: [\n    [ 0.62, 0.173 ],\n    [ 0.681, 0.173 ],\n    [ 0.681, 0.191 ],\n    [ 0.62, 0.191 ]\n  ]\n}",
      "language": "json",
      "name": ""
    }
  ]
}
[/block]

### Orientation

receipt.orientation: Rotation (in degrees) of receipt.


[block:code]
{
  "codes": [
    {
      "code": "mindeeClient.receipt.parse(\n  \t{\n        input : \"receipt.jpg\",\n        inputType : 'path',\n    }\n)\n  .then((res) => {\n    console.log(res.receipt.orientation);\n  })\n  .catch((err) => {\n    console.error(err);\n  });",
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
      "code": "{\n    \"pageNumber\": 0,\n    \"reconstructed\": false,\n    \"value\": 0,\n    \"probability\": 0.99,\n    \"bbox\": []\n  }",
      "language": "json"
    }
  ]
}
[/block]


### checklist

> **taxesMatchTotalIncl**: (Boolean) verifies (tax rate)*totalExcl + totalExcl = TotalIncl