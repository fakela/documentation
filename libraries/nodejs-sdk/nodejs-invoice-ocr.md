---
title: Invoice API
excerpt: ''
hidden: false
---

The Node.js SDK supports the [invoice API](https://developers.mindee.com/docs/invoice-ocr) for extracting data from invoice.

```node
const { Client } = require("mindee");

const mindeeClient = new Client({
  invoiceToken: "yourInvoiceToken"
});

mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
  console.log(res.invoice);
})
.catch((err) => {
  console.error(err);
});
```

> 📘 **Info**
>
> You can also [use an environment variable for the token](https://developers.mindee.com/docs/getting-started-1#instantiate-your-client)

### Client Invoice Parse Parameters

| Parameter name    | Description | Default value |
| ----------- | ----------- | -------|
| input     | Document object    |
| inputType  | **path**: File path <br /> **stream**: From file object <br /> **base64**: From a base64 encoded file      | path |
| cutPdf |  (Boolean) If set to `true`, when sending a multi pages PDF of more than 5 pages, the library create a new PDF by concatenating the first 4 pages and the last page. | true
| includeWords | (Boolean) If set to `true`, the `raw_http` response will include all the words in the document associated to their positions. |false|
| filename | (String) Specify a filename of your input. | undefined |

Using this sample invoice below, we are going to illustrate how to extract the data that we want using the SDK.
![sample invoice](https://files.readme.io/a74eaa5-c8e283b-sample_invoice.jpeg)

## Invoice Data Structure
To access a receipt object, you need to create a `mindee.Client` and call the `Client.receipt.parse` method.

The receipt object JSON data structure consists of:

- [Document level prediction](#document-level-prediction)
- [Page level prediction](#page-level-prediction)
- [Raw HTTP response](#raw-http-response)

### Document level prediction
For document level prediction, we construct the document class by combining the different pages in a single document. This method used for creating a single receipt object from multiple pages relies on field confidence scores.

Basically, we iterate over each page, and for each field, we keep the one that has the highest probability.

For example, if you send a three-page receipt, document level will provide you one tax, one total, and so on.

```node
res.invoice
```

Code Example

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
  console.log(res.invoice);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
invoice {
  filepath: '/var/folders/cf/06c5ln2s71jdwhb2r1cb82yh0000gn/T/upload_bcacef3504bc9e51e6aa10f9bbe60ef6a74eaa5-c8e283b-sample_invoice.jpeg',
  filename: 'upload_bcacef3504bc9e51e6aa10f9bbe60ef6a74eaa5-c8e283b-sample_invoice.jpeg',
  fileExtension: 'image/jpeg',
  checklist: {
    taxesMatchTotalIncl: true,
    taxesMatchTotalExcl: false,
    taxesPlusTotalExclMatchTotalIncl: false
  },
  words: [],
  locale: {
    pageNumber: 0,
    reconstructed: false,
    probability: 0,
    bbox: [],
    language: 'en',
    currency: 'CAD'
  },
  totalIncl: {
    pageNumber: 0,
    reconstructed: false,
    value: 2608.2,
    probability: 1,
    bbox: [ [Array], [Array], [Array], [Array] ]
  },
  totalTax: {
    pageNumber: 0,
    reconstructed: true,
    value: 193.2,
    probability: 1,
    bbox: []
  },
  totalExcl: {
    pageNumber: 0,
    reconstructed: true,
    value: 2415,
    probability: 1,
    bbox: []
  },
  date: {
    pageNumber: 0,
    reconstructed: false,
    value: '2018-09-25',
    probability: 0.99,
    bbox: [ [Array], [Array], [Array], [Array] ],
    dateObject: '2018-09-25T00:00:00.000Z'
  },
  invoiceDate: {
    pageNumber: 0,
    reconstructed: false,
    value: '2018-09-25',
    probability: 0.99,
    bbox: [ [Array], [Array], [Array], [Array] ],
    dateObject: '2018-09-25T00:00:00.000Z'
  },
  taxes: [
    {
      pageNumber: 0,
      reconstructed: false,
      value: 193.2,
      probability: 1,
      bbox: [Array],
      rate: 8
    }
  ],
  orientation: {
    pageNumber: 0,
    reconstructed: false,
    value: 0,
    probability: 0.99,
    bbox: []
  },
  companyNumber: [],
  dueDate: {
    pageNumber: 0,
    reconstructed: false,
    value: '2018-09-25',
    probability: 0.86,
    bbox: [ [Array], [Array], [Array], [Array] ],
    dateObject: '2018-09-25T00:00:00.000Z'
  },
  invoiceNumber: {
    pageNumber: 0,
    reconstructed: false,
    value: '14',
    probability: 0.99,
    bbox: [ [Array], [Array], [Array], [Array] ]
  },
  supplier: {
    pageNumber: 0,
    reconstructed: false,
    value: 'TURNPIKE DESIGNS CO',
    probability: 0.74,
    bbox: [ [Array], [Array], [Array], [Array] ]
  },
  paymentDetails: []
}
```

### Page level prediction
We create the document class by iterating over each page one by one. Each page in the pdf is treated as a unique page.

For example, if you send a three-page receipt, page level prediction will provide you with three tax, three total and so on.

```node
res.invoices
```

Code Example

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
  console.log(res.invoices);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
[
  Invoice {
    filepath: '/Users/fharper/Documents/code/mindee/datasets/invoices/00da35ce-0827-4f2f-b094-6021c04e3457.pdf',
    filename: '00da35ce-0827-4f2f-b094-6021c04e3457.pdf',
    fileExtension: 'application/pdf',
    checklist: {
      taxesMatchTotalIncl: false,
      taxesMatchTotalExcl: false,
      taxesPlusTotalExclMatchTotalIncl: false
    },
    level: 'page',
    constructPrediction: [Function (anonymous)],
    words: [],
    locale: Locale {
      pageNumber: 0,
      reconstructed: false,
      value: undefined,
      probability: 0.83,
      bbox: [],
      language: 'fr',
      country: undefined,
      currency: 'EUR'
    },
    totalIncl: Amount {
      pageNumber: 0,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    totalTax: Amount {
      pageNumber: 0,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    totalExcl: Amount {
      pageNumber: 0,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    date: DateField {
      pageNumber: 0,
      reconstructed: false,
      value: '2020-06-30',
      probability: 0.99,
      bbox: [Array],
      dateObject: 2020-06-30T00:00:00.000Z
    },
    invoiceDate: DateField {
      pageNumber: 0,
      reconstructed: false,
      value: '2020-06-30',
      probability: 0.99,
      bbox: [Array],
      dateObject: 2020-06-30T00:00:00.000Z
    },
    taxes: [],
    companyNumber: [ [Field], [Field], [Field] ],
    dueDate: DateField {
      pageNumber: 0,
      reconstructed: false,
      value: '2020-07-30',
      probability: 0.99,
      bbox: [Array],
      dateObject: 2020-07-30T00:00:00.000Z
    },
    invoiceNumber: Field {
      pageNumber: 0,
      reconstructed: false,
      value: '0660',
      probability: 0.99,
      bbox: [Array]
    },
    supplier: Field {
      pageNumber: 0,
      reconstructed: false,
      value: 'SOMONIAN',
      probability: 0.89,
      bbox: [Array]
    },
    supplierAddress: Field {
      pageNumber: 0,
      reconstructed: false,
      value: '9, Rue Buffault 75009 Paris',
      probability: 0.73,
      bbox: [Array]
    },
    customerName: Field {
      pageNumber: 0,
      reconstructed: false,
      value: 'CELINNI',
      probability: 0.9,
      bbox: [Array]
    },
    customerAddress: Field {
      pageNumber: 0,
      reconstructed: false,
      value: '9, Rue Buffault 75009 Paris',
      probability: 0.73,
      bbox: [Array]
    },
    customerCompanyRegistration: [],
    paymentDetails: [],
    orientation: Orientation {
      pageNumber: 0,
      reconstructed: false,
      value: 0,
      probability: 0.99,
      bbox: []
    }
  },
  Invoice {
    filepath: '/Users/fharper/Documents/code/mindee/datasets/invoices/00da35ce-0827-4f2f-b094-6021c04e3457.pdf',
    filename: '00da35ce-0827-4f2f-b094-6021c04e3457.pdf',
    fileExtension: 'application/pdf',
    checklist: {
      taxesMatchTotalIncl: false,
      taxesMatchTotalExcl: false,
      taxesPlusTotalExclMatchTotalIncl: false
    },
    level: 'page',
    constructPrediction: [Function (anonymous)],
    words: [],
    locale: Locale {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0.83,
      bbox: [],
      language: 'fr',
      country: undefined,
      currency: 'EUR'
    },
    totalIncl: Amount {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    totalTax: Amount {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    totalExcl: Amount {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    date: DateField {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: [],
      dateObject: undefined
    },
    invoiceDate: DateField {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: [],
      dateObject: undefined
    },
    taxes: [],
    companyNumber: [],
    dueDate: DateField {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: [],
      dateObject: undefined
    },
    invoiceNumber: Field {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    supplier: Field {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    supplierAddress: Field {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    customerName: Field {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    customerAddress: Field {
      pageNumber: 1,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    customerCompanyRegistration: [],
    paymentDetails: [],
    orientation: Orientation {
      pageNumber: 1,
      reconstructed: false,
      value: 0,
      probability: 0.99,
      bbox: []
    }
  },
  Invoice {
    filepath: '/Users/fharper/Documents/code/mindee/datasets/invoices/00da35ce-0827-4f2f-b094-6021c04e3457.pdf',
    filename: '00da35ce-0827-4f2f-b094-6021c04e3457.pdf',
    fileExtension: 'application/pdf',
    checklist: {
      taxesMatchTotalIncl: true,
      taxesMatchTotalExcl: true,
      taxesPlusTotalExclMatchTotalIncl: true
    },
    level: 'page',
    constructPrediction: [Function (anonymous)],
    words: [],
    locale: Locale {
      pageNumber: 2,
      reconstructed: false,
      value: undefined,
      probability: 0.83,
      bbox: [],
      language: 'fr',
      country: undefined,
      currency: 'EUR'
    },
    totalIncl: Amount {
      pageNumber: 2,
      reconstructed: false,
      value: 13200,
      probability: 1,
      bbox: [Array]
    },
    totalTax: Amount {
      pageNumber: 0,
      reconstructed: true,
      value: 2200,
      probability: 1,
      bbox: []
    },
    totalExcl: Amount {
      pageNumber: 2,
      reconstructed: false,
      value: 11000,
      probability: 1,
      bbox: [Array]
    },
    date: DateField {
      pageNumber: 2,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: [],
      dateObject: undefined
    },
    invoiceDate: DateField {
      pageNumber: 2,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: [],
      dateObject: undefined
    },
    taxes: [ [Object] ],
    companyNumber: [],
    dueDate: DateField {
      pageNumber: 2,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: [],
      dateObject: undefined
    },
    invoiceNumber: Field {
      pageNumber: 2,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    supplier: Field {
      pageNumber: 2,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    supplierAddress: Field {
      pageNumber: 2,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    customerName: Field {
      pageNumber: 2,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    customerAddress: Field {
      pageNumber: 2,
      reconstructed: false,
      value: undefined,
      probability: 0,
      bbox: []
    },
    customerCompanyRegistration: [],
    paymentDetails: [],
    orientation: Orientation {
      pageNumber: 2,
      reconstructed: false,
      value: 0,
      probability: 0.99,
      bbox: []
    }
  }
]
```

### Raw HTTP response
Get the full API response as a Node.js HTTP Response object

```node
const { Client } = require("mindee");

const mindeeClient = new Client({
  invoiceToken: "yourInvoiceToken"
});

mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
  console.log(res.httpResponse);
})
.catch((err) => {
  console.error(err);
});
```

## Extracted Fields
Each receipt object contains a set of different fields. Each field contains the four following attributes:

- **value** (`String` or `Float` depending on the field type): corresponds to the field value. Set to None if the `field` was not extracted.
- **probability** (`Float`): the confidence score of the field prediction.
- **bbox** (`Array[Float]`): contains the relative vertices coordinates of the bounding box containing the `field` in the image. If the field is not written, the `bbox` is an empty array.
- **reconstructed** (`Boolean`): `True` if the field was reconstructed using other fields.

### Additional Attributes
Depending on the field type specified, additional attributes can be extracted in the receipt object. Using the above [invoice example](https://files.readme.io/a74eaa5-c8e283b-sample_invoice.jpeg), the following are the basic fields that can be extracted.

- [Dates](#dates)
- [Invoice Number](#invoice-number)
- [Locale](#locale)
- [Supplier Informations](#supplier-informations)
- [Taxes](#taxes)
- [Tests](#tests)
- [Total Amounts](#total-amounts)

### Dates

- **invoice.invoiceDate** (string): Issuance date of the invoice. Each date field comes with an extra attribute:

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.invoiceDate);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
DateField {
  pageNumber: 0,
  reconstructed: false,
  value: '2018-09-25',
  probability: 0.99,
  bbox: [
    [ 0.84, 0.305 ],
    [ 0.932, 0.305 ],
    [ 0.932, 0.318 ],
    [ 0.84, 0.318 ]
  ],
  dateObject: '2018-09-25T00:00:00.000Z'
}
```

- **invoice.dueDate** (string): Due date of payment of the invoice.

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.dueDate);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
DateField {
  pageNumber: 0,
  reconstructed: false,
  value: '2018-09-25',
  probability: 0.86,
  bbox: [
    [ 0.841, 0.323 ],
    [ 0.941, 0.323 ],
    [ 0.941, 0.338 ],
    [ 0.841, 0.338 ]
  ],
  dateObject: '2018-09-25T00:00:00.000Z'
}
```

### Invoice Number

- **invoice.invoiceNumber** (string): unique number that is assigned to the invoice.

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.invoiceNumber);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
Field {
  pageNumber: 0,
  reconstructed: false,
  value: '14',
  probability: 0.99,
  bbox: [
    [ 0.841, 0.264 ],
    [ 0.864, 0.264 ],
    [ 0.864, 0.279 ],
    [ 0.841, 0.279 ]
  ]
}
```

### Locale

- **invoice.locale** (string): Language and country ISO code.
    - **language** (String): Language code in [ISO 639-1](https://en.wikipedia.org/wiki/ISO_639-1) format as seen on the invoice. The following language codes are supported: `ca`, `de`, `en`, `es`, `fr`, `it`, `nl` and `pt`.
    - **country** (String): Country code in [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) format as seen on the invoice. The following country codes are supported: `CA`, `CH`, `DE`, `ES`, `FR,` `GB`, `IT`, `NL`, `PT` and `US`.
    - **currency** (String): Currency code in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format as seen on the invoice. The following country codes are supported: `CAD`, `CHF`, `GBP`, `EUR`, `USD`.

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.locale);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
Locale {
  pageNumber: 0,
  reconstructed: false,
  probability: 0,
  bbox: [],
  language: 'en',
  country: undefined,
  currency: 'CAD'
}
```

### Supplier Informations

- **invoice.company_number**:  List of detected supplier's company registration number. Each object in the list contains extra attribute:

Each company number object contains an extra attribute:

- **type** (String Generic): Type of company registration number among:  [VAT NUMBER](https://en.wikipedia.org/wiki/VAT_identification_number), [SIRET](https://en.wikipedia.org/wiki/SIRET_code), [SIREN](https://en.wikipedia.org/wiki/SIREN_code), [NIF](https://en.wikipedia.org/wiki/VAT_identification_number), [CF](https://en.wikipedia.org/wiki/Italian_fiscal_code), [UID](https://en.wikipedia.org/wiki/VAT_identification_number), [STNR](https://de.wikipedia.org/wiki/Steuernummer), [HRA/HRB](https://en.wikipedia.org/wiki/German_Commercial_Register), [TIN](https://en.wikipedia.org/wiki/Taxpayer_Identification_Number) (includes EIN, FEIN, SSN, ATIN, PTIN, ITIN), [RFC](https://wise.com/us/blog/clabe-rfc-curp-abm-meaning-mexico), [BTW](https://en.wikipedia.org/wiki/European_Union_value_added_tax), [ABN](https://abr.business.gov.au/Help/AbnFormat), [UEN](https://www.uen.gov.sg/ueninternet/faces/pages/admin/aboutUEN.jspx), [CVR](https://en.wikipedia.org/wiki/Central_Business_Register_(Denmark)), [ORGNR](https://en.wikipedia.org/wiki/VAT_identification_number), [INN](https://www.nalog.gov.ru/eng/exchinf/inn/), [DPH](https://en.wikipedia.org/wiki/Value-added_tax), [GSTIN](https://en.wikipedia.org/wiki/VAT_identification_number), [COMPANY REGISTRATION NUMBER](https://en.wikipedia.org/wiki/VAT_identification_number) (UK), [KVK](https://business.gov.nl/starting-your-business/registering-your-business/lei-rsin-vat-and-kvk-number-which-is-which/), [DIC](https://www.vatify.eu/czech-vat-number.html)
- **value** (String): Value of the company identifier

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.companyNumber);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
Supplier Company Number [
  Field {
    pageNumber: 3,
    reconstructed: false,
    value: '52747908301026',
    probability: 0.99,
    bbox: [ [Array], [Array], [Array], [Array] ],
    type: 'SIRET'
  },
  Field {
    pageNumber: 3,
    reconstructed: false,
    value: 'FR18527479083',
    probability: 0.99,
    bbox: [ [Array], [Array], [Array], [Array] ],
    type: 'VAT NUMBER'
  },
  Field {
    pageNumber: 3,
    reconstructed: false,
    value: '527479583',
    probability: 0.99,
    bbox: [ [Array], [Array], [Array], [Array] ],
    type: 'SIREN'
  }
]
```

- **invoice.paymentDetails**: List of Supplier's payment details written in the invoice. Each payment details object contains extra attributes:
    - iban (String)
    - swift (String)

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.paymentDetails);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
Supplier Payment Details
[
  PaymentDetails {
    pageNumber: 1,
    reconstructed: false,
    value: undefined,
    probability: 0.76,
    bbox: [ [Array], [Array], [Array], [Array] ],
    accountNumber: '0500013M026',
    iban: 'FR14 2004 1010 0505 0001 3M02 606',
    routingNumber: undefined,
    swift: 'CTBAAU2S'
  }
]
```

- **invoice.supplier** (string): Supplier name as written in the invoice.

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.supplier);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
Supplier Name {
  pageNumber: 0,
  reconstructed: false,
  value: 'TURNPIKE DESIGNS CO',
  probability: 0.74,
  bbox: [
    [ 0.159, 0.085 ],
    [ 0.391, 0.085 ],
    [ 0.391, 0.15 ],
    [ 0.159, 0.15 ]
  ]
}
```

### Taxes

- **receipt.taxes** (string): Contains tax fields as seen on the receipt.
    - value (number): The tax amount.
    - code (string): The tax code (HST, GST... for Canadian; City Tax, State tax for US, etc..).
    - rate (number): The tax rate.

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.taxes);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
[
  {
    pageNumber: 1,
    reconstructed: false,
    value: 193.2,
    probability: 1,
    bbox: [ [Array], [Array], [Array], [Array] ],
    rate: 8,
    code: 'GST'
  }
]
```

### Tests
A checklist of three `Boolean` attributes that check the extracted total amounts and taxes data is correct with some basic tests.

> 📘 **Info**
>
> A false value does not mean inaccurate extraction, but true is another confirmation of accurate data extraction.

- **taxesMatchTotalIncl** (Boolean): returns `true` if `taxes.rate * totalExcl + totalExcl = totalIncl`
- **taxesMatchTotalExcl** (Boolean): returns `true` if `(all taxes) * 100 / taxes.rate = totalExcl`
- **taxesPlusTotalExclMatchTotalIncl** (Boolean): returns `true` if `(all taxes) + totalexcl = totalIncl`

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.checklist);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
{
  taxesMatchTotalIncl: true,
  taxesMatchTotalExcl: false,
  taxesPlusTotalExclMatchTotalIncl: false
}
```

### Total Amounts

- **invoice.totalIncl** (number): Total amount including taxes.

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.totalIncl);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
Amount {
  pageNumber: 0,
  reconstructed: false,
  value: 2608.2,
  probability: 1,
  bbox: [
    [ 0.886, 0.839 ],
    [ 0.971, 0.839 ],
    [ 0.971, 0.858 ],
    [ 0.886, 0.858 ]
  ]
}
```

- **invoice.totalExcl** (number): Total amount excluding taxes.

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.totalExcl);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
Amount {
  pageNumber: 0,
  reconstructed: true,
  value: 2415,
  probability: 1,
  bbox: []
}
```

- **invoice.totalTax** (number): Total taxes reconstructed from tax lines.

```node
mindeeClient.invoice.parse({
    input : "invoice.pdf",
    inputType : 'path',
    filename : undefined,
    cutPdf : true,
    includeWords : false
})
.then((res) => {
    console.log(res.invoice.totalTax);
})
.catch((err) => {
  console.error(err);
});
```

Output

```json
Amount {
  pageNumber: 0,
  reconstructed: true,
  value: 193.2,
  probability: 1,
  bbox: []
}
```
