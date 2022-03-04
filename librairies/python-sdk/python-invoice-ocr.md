---
title: Invoice API
excerpt: ''
---
The Python SDK supports the [invoice API](https://developers.mindee.com/docs/invoice-ocr) for extracting data from invoices.

```python
from mindee import Client

mindee_client = Client().config_invoice("invoice-api-key")
invoice_data = mindee_client.doc_from_path("/path/to/file").parse("invoice")
```

## Invoice Data Structure
The invoice object JSON data structure consists of:

- [Document level prediction](#document-level-prediction)
- [Page level prediction](#page-level-prediction)
- [Raw HTTP response](#raw-http-response)

### Document Level Prediction
For document level prediction, we construct the document class by using the different pages put in a single document. The method used for creating a single invoice object with multiple pages relies on field confidence scores.

Basically, we iterate over each page, and for each field, we keep the one that has the highest probability.

```python
# returns a unique object from class Invoice
invoice_data.invoice
```

```shell
-----Invoice data-----
Filename: 995b49c5-acc4-4272-a01a-2e44e99ff704.pdf
Invoice number: 149118
Total amount including taxes: 4386.0
Total amount excluding taxes: 3655.0
Invoice date: 2020-09-29
Invoice due date:
Supplier name: SupplierName
Supplier address: 8 rue d'Uzès - 75002 Paris
Customer name: ClientName
Customer company registration:
Customer address: 137 rue d'Aboukir 75002 Paris FRANCE
Payment details: FR76***************92; SOGEFRPP;
Company numbers: FR9544****591; 44****59100032; ****7591
Taxes: 731.0 20.0%
Total taxes: 731.0
Locale: fr; fr; EUR;
----------------------
```

### Page Level Prediction
For page level prediction, in a multi-page pdf we construct the document class by using a unique page of the pdf.

```python
# [Invoice, Invoice ...]
invoice_data.invoices
```

### Raw HTTP Response
This contains the full Mindee API HTTP response object in JSON format

```python
# full HTTP request object
invoice_data.http_response
```

```json
{
  "api_request": {
    "error": {},
    "resources": [
      "document"
    ],
    "status": "success",
    "status_code": 201,
    "url": "http://api.mindee.net/v1/products/mindee/invoices/v3/predict"
  },
  "document": {
    "annotations": {
      "labels": {}
    },
    "id": "9833cdf7-41c5-49ed-a45f-8d374dfbb08f",
    "inference": {
      "extras": {},
      "finished_at": "2022-03-03T11:03:24+00:00",
      "pages": [
        {
          "extras": {},
          "id": 0,
          "prediction": {
            "company_registration": [
              {
                "confidence": 1,
                "polygon": [
                  [
                    0.297,
                    0.963
                  ],
                  [
                    0.424,
                    0.963
                  ],
                  [
                    0.424,
                    0.975
                  ],
                  [
                    0.297,
                    0.975
                  ]
                ],
                "type": "VAT NUMBER",
                "value": "FR95449587591"
              },
              {
                "confidence": 1,
                "polygon": [
                  [
                    0.087,
                    0.963
                  ],
                  [
                    0.216,
                    0.963
                  ],
                  [
                    0.216,
                    0.975
                  ],
                  [
                    0.087,
                    0.975
                  ]
                ],
                "type": "SIRET",
                "value": "44958759100032"
              },
              {
                "confidence": 1,
                "polygon": [
                  [
                    0.297,
                    0.963
                  ],
                  [
                    0.424,
                    0.963
                  ],
                  [
                    0.424,
                    0.975
                  ],
                  [
                    0.297,
                    0.975
                  ]
                ],
                "type": "SIREN",
                "value": "449587591"
              }
            ],
            "customer": {
              "confidence": 1,
              "polygon": [
                [
                  0.564,
                  0.159
                ],
                [
                  0.619,
                  0.159
                ],
                [
                  0.619,
                  0.173
                ],
                [
                  0.564,
                  0.173
                ]
              ],
              "value": "ClientName"
            },
            "customer_address": {
              "confidence": 1,
              "polygon": [
                [
                  0.564,
                  0.193
                ],
                [
                  0.706,
                  0.193
                ],
                [
                  0.706,
                  0.257
                ],
                [
                  0.564,
                  0.257
                ]
              ],
              "value": "137 rue d'Aboukir 75002 Paris FRANCE"
            },
            "customer_company_registration": [],
            "date": {
              "confidence": 1,
              "polygon": [
                [
                  0.751,
                  0.071
                ],
                [
                  0.852,
                  0.071
                ],
                [
                  0.852,
                  0.087
                ],
                [
                  0.751,
                  0.087
                ]
              ],
              "value": "2020-09-29"
            },
            "document_type": {
              "value": "INVOICE"
            },
            "due_date": {
              "confidence": 0,
              "polygon": [],
              "raw": null,
              "value": null
            },
            "invoice_number": {
              "confidence": 1,
              "polygon": [
                [
                  0.747,
                  0.041
                ],
                [
                  0.825,
                  0.041
                ],
                [
                  0.825,
                  0.059
                ],
                [
                  0.747,
                  0.059
                ]
              ],
              "value": "149118"
            },
            "locale": {
              "confidence": 0.94,
              "currency": "EUR",
              "language": "fr"
            },
            "orientation": {
              "confidence": 0.99,
              "degrees": 0
            },
            "payment_details": [
              {
                "account_number": null,
                "confidence": 1,
                "iban": "FR763**********0037292",
                "polygon": [
                  [
                    0.207,
                    0.865
                  ],
                  [
                    0.552,
                    0.865
                  ],
                  [
                    0.552,
                    0.876
                  ],
                  [
                    0.207,
                    0.876
                  ]
                ],
                "routing_number": null,
                "swift": "SOGEFRPP"
              }
            ],
            "supplier": {
              "confidence": 1,
              "polygon": [
                [
                  0.098,
                  0.865
                ],
                [
                  0.153,
                  0.865
                ],
                [
                  0.153,
                  0.876
                ],
                [
                  0.098,
                  0.876
                ]
              ],
              "value": "SupplierName"
            },
            "supplier_address": {
              "confidence": 1,
              "polygon": [
                [
                  0.039,
                  0.903
                ],
                [
                  0.216,
                  0.903
                ],
                [
                  0.216,
                  0.915
                ],
                [
                  0.039,
                  0.915
                ]
              ],
              "value": "8 rue d'Uzès - 75002 Paris"
            },
            "taxes": [
              {
                "confidence": 1,
                "polygon": [
                  [
                    0.723,
                    0.755
                  ],
                  [
                    0.926,
                    0.755
                  ],
                  [
                    0.926,
                    0.769
                  ],
                  [
                    0.723,
                    0.769
                  ]
                ],
                "rate": 20,
                "value": 731
              }
            ],
            "total_excl": {
              "confidence": 1,
              "polygon": [
                [
                  0.856,
                  0.731
                ],
                [
                  0.926,
                  0.731
                ],
                [
                  0.926,
                  0.746
                ],
                [
                  0.856,
                  0.746
                ]
              ],
              "value": 3655
            },
            "total_incl": {
              "confidence": 1,
              "polygon": [
                [
                  0.856,
                  0.782
                ],
                [
                  0.926,
                  0.782
                ],
                [
                  0.926,
                  0.796
                ],
                [
                  0.856,
                  0.796
                ]
              ],
              "value": 4386
            }
          }
        }
      ],
      "prediction": {
        "company_registration": [
          {
            "confidence": 1,
            "page_id": 0,
            "polygon": [
              [
                0.297,
                0.963
              ],
              [
                0.424,
                0.963
              ],
              [
                0.424,
                0.975
              ],
              [
                0.297,
                0.975
              ]
            ],
            "type": "VAT NUMBER",
            "value": "FR95449587591"
          },
          {
            "confidence": 1,
            "page_id": 0,
            "polygon": [
              [
                0.087,
                0.963
              ],
              [
                0.216,
                0.963
              ],
              [
                0.216,
                0.975
              ],
              [
                0.087,
                0.975
              ]
            ],
            "type": "SIRET",
            "value": "44958759100032"
          },
          {
            "confidence": 1,
            "page_id": 0,
            "polygon": [
              [
                0.297,
                0.963
              ],
              [
                0.424,
                0.963
              ],
              [
                0.424,
                0.975
              ],
              [
                0.297,
                0.975
              ]
            ],
            "type": "SIREN",
            "value": "449587591"
          }
        ],
        "customer": {
          "confidence": 1,
          "page_id": 0,
          "polygon": [
            [
              0.564,
              0.159
            ],
            [
              0.619,
              0.159
            ],
            [
              0.619,
              0.173
            ],
            [
              0.564,
              0.173
            ]
          ],
          "value": "ClientName"
        },
        "customer_address": {
          "confidence": 1,
          "page_id": 0,
          "polygon": [
            [
              0.564,
              0.193
            ],
            [
              0.706,
              0.193
            ],
            [
              0.706,
              0.257
            ],
            [
              0.564,
              0.257
            ]
          ],
          "value": "137 rue d'Aboukir 75002 Paris FRANCE"
        },
        "customer_company_registration": [],
        "date": {
          "confidence": 1,
          "page_id": 0,
          "polygon": [
            [
              0.751,
              0.071
            ],
            [
              0.852,
              0.071
            ],
            [
              0.852,
              0.087
            ],
            [
              0.751,
              0.087
            ]
          ],
          "value": "2020-09-29"
        },
        "document_type": {
          "value": "INVOICE"
        },
        "due_date": {
          "confidence": 0,
          "page_id": null,
          "polygon": [],
          "raw": null,
          "value": null
        },
        "invoice_number": {
          "confidence": 1,
          "page_id": 0,
          "polygon": [
            [
              0.747,
              0.041
            ],
            [
              0.825,
              0.041
            ],
            [
              0.825,
              0.059
            ],
            [
              0.747,
              0.059
            ]
          ],
          "value": "149118"
        },
        "locale": {
          "confidence": 0.94,
          "currency": "EUR",
          "language": "fr"
        },
        "payment_details": [
          {
            "account_number": null,
            "confidence": 1,
            "iban": "FR763**********0037292",
            "page_id": 0,
            "polygon": [
              [
                0.207,
                0.865
              ],
              [
                0.552,
                0.865
              ],
              [
                0.552,
                0.876
              ],
              [
                0.207,
                0.876
              ]
            ],
            "routing_number": null,
            "swift": "SOGEFRPP"
          }
        ],
        "supplier": {
          "confidence": 1,
          "page_id": 0,
          "polygon": [
            [
              0.098,
              0.865
            ],
            [
              0.153,
              0.865
            ],
            [
              0.153,
              0.876
            ],
            [
              0.098,
              0.876
            ]
          ],
          "value": "SupplierName"
        },
        "supplier_address": {
          "confidence": 1,
          "page_id": 0,
          "polygon": [
            [
              0.039,
              0.903
            ],
            [
              0.216,
              0.903
            ],
            [
              0.216,
              0.915
            ],
            [
              0.039,
              0.915
            ]
          ],
          "value": "8 rue d'Uzès - 75002 Paris"
        },
        "taxes": [
          {
            "confidence": 1,
            "page_id": 0,
            "polygon": [
              [
                0.723,
                0.755
              ],
              [
                0.926,
                0.755
              ],
              [
                0.926,
                0.769
              ],
              [
                0.723,
                0.769
              ]
            ],
            "rate": 20,
            "value": 731
          }
        ],
        "total_excl": {
          "confidence": 1,
          "page_id": 0,
          "polygon": [
            [
              0.856,
              0.731
            ],
            [
              0.926,
              0.731
            ],
            [
              0.926,
              0.746
            ],
            [
              0.856,
              0.746
            ]
          ],
          "value": 3655
        },
        "total_incl": {
          "confidence": 1,
          "page_id": 0,
          "polygon": [
            [
              0.856,
              0.782
            ],
            [
              0.926,
              0.782
            ],
            [
              0.926,
              0.796
            ],
            [
              0.856,
              0.796
            ]
          ],
          "value": 4386
        }
      },
      "processing_time": 1.825,
      "product": {
        "features": [
          "locale",
          "invoice_number",
          "date",
          "due_date",
          "total_excl",
          "total_incl",
          "taxes",
          "payment_details",
          "supplier",
          "company_registration",
          "supplier_address",
          "customer",
          "customer_company_registration",
          "customer_address",
          "document_type",
          "orientation"
        ],
        "name": "mindee/invoices",
        "type": "standard",
        "version": "3.0"
      },
      "started_at": "2022-03-03T11:03:22+00:00"
    },
    "n_pages": 1,
    "name": "995b49c5-acc4-4272-a01a-2e44e99ff704.pdf"
  },
  "document_type": "invoice",
  "input_type": "path",
  "filename": "995b49c5-acc4-4272-a01a-2e44e99ff704.pdf",
  "filepath": "/Users/fharper/Documents/code/mindee/datasets/invoices/995b49c5-acc4-4272-a01a-2e44e99ff704.pdf",
  "file_extension": "application/pdf"
}
```

## Extracted Fields
Each invoice object contains a set of different fields. Each field contains the four following attributes:

- **value** (Str or Float depending on the field type): corresponds to the field value. Set to None if the `>field` was not extracted.
- **probability** (Float): the confidence score of the field prediction.
- **bbox** (Array[Float]): contains the relative vertices coordinates of the bounding box containing the `>field` in the image. If the field is not written, the bbox is an empty array.
- **reconstructed** (Bool): True if the field was reconstructed using other fields.

### Additional Attributes
Depending on the field type, there might be additional attributes that will be extracted in the invoice object. Below is the list of basic fields that can be extracted:

- [Company Information](#company-information)
- [Customer Information](#customer-information)
- [Dates](#dates)
- [Locale and Currency](#locale-and-currency)
- [Payment Information](#payment-information)
- [Supplier Information](#supplier-information)
- [Taxes](#taxes)
- [Total Amounts](#total-amounts)


### Customer Information

- **Invoice.customer_name**: Customer name

```python
# To get the customer name (string)
customer_name = invoice_data.invoice.customer_name.value
```

- **Invoice.customer_address**: Customer address

```python
# To get the customer address (string)
customer_address = invoice_data.invoice.customer_address.value
```

- **Invoice.customer_company_registration**: Customer Company Registration

```python
# To get the customer company registation (string)
customer_registration_numbers = invoice_data.invoice.customer_company_registration.value
```

### Dates
**date_object**: Contains the date of issuance of the invoice. Each date field comes with extra attributes:

- **invoice.invoice_date**: Datetime object from python datetime date library.

```python
# To get the invoice date of issuance (string)
invoice_date = invoice_data.invoice.invoice_date.value
```

- **invoice.due_date**: Payment due date of the invoice.

```python
# To get the invoice due date (string)
due_date = invoice_data.invoice.due_date.value
```

### Locale and Currency

- **invoice_data.locale**: Language ISO code.

```python
# To get the total language code
language = invoice_data.invoice.locale.value
```

- **currency** (String): ISO currency code.

``` python
# To get the invoice currency code
currency = invoice_data.invoice.locale.currency
```

### Payment Information
**Invoice.payment_details**: List of invoice's supplier payment details. Each object in the list contains extra attributes:

- **iban**: (String)
- **swift**: (String)
- **routing_number**: (String)
- **account_number**: (String)

```python
# To get the list of payment details
payment_details = invoice_data.invoice.payment_details

# Loop on each object
for payment_detail in payment_details:
   # To get the IBAN
   iban = payment_detail.iban

   # To get the swift
   swift = payment_detail.swift

   # To get the routing number
   routing_number = payment_detail.routing_number

   # To get the account_number
   account_number = payment_detail.account_number
```

### Supplier Information

**Invoice.company_number**:  List of detected supplier's company registration number. Each object in the list contains extra attribute:

- **type** (String Generic): Type of company registration number among: 
    [VAT NUMBER](https://en.wikipedia.org/wiki/VAT_identification_number),
    [SIRET](https://en.wikipedia.org/wiki/SIRET_code),
    [SIREN](https://en.wikipedia.org/wiki/SIREN_code),
    [NIF](https://en.wikipedia.org/wiki/VAT_identification_number),
    [CF](https://en.wikipedia.org/wiki/Italian_fiscal_code),
    [UID](https://en.wikipedia.org/wiki/VAT_identification_number),
    [STNR](),
    [HRA/HRB](https://en.wikipedia.org/wiki/German_Commercial_Register),
    [TIN](https://en.wikipedia.org/wiki/Taxpayer_Identification_Number) (includes EIN, FEIN, SSN, ATIN, PTIN, ITIN),
    [RFC](https://wise.com/us/blog/clabe-rfc-curp-abm-meaning-mexico),
    [BTW](https://en.wikipedia.org/wiki/European_Union_value_added_tax),
    [ABN](https://abr.business.gov.au/Help/AbnFormat),
    [UEN](https://www.uen.gov.sg/ueninternet/faces/pages/admin/aboutUEN.jspx),
    [CVR](https://en.wikipedia.org/wiki/Central_Business_Register_(Denmark)),
    [ORGNR](https://en.wikipedia.org/wiki/VAT_identification_number),
    [INN](https://www.nalog.gov.ru/eng/exchinf/inn/),
    [DPH](https://en.wikipedia.org/wiki/Value-added_tax),
    [GSTIN](https://en.wikipedia.org/wiki/VAT_identification_number),
    [COMPANY REGISTRATION NUMBER](https://en.wikipedia.org/wiki/VAT_identification_number) (UK),
    [KVK](https://business.gov.nl/starting-your-business/registering-your-business/lei-rsin-vat-and-kvk-number-which-is-which/),
    [DIC](https://www.vatify.eu/czech-vat-number.html)
- **Value** (String): Value of the company identifier

```python
# To get the list of company numbers
company_registration_numbers = invoice_data.invoice.company_number

# Loop on each object
for company_number in company_registration_numbers:
   # To get the type of number
   company_number_type = company_number.type

   # To get the company number
   company_number_value = company_number.value
```

- **Invoice.supplier**: Supplier name as written in the invoice (logo or supplier Infos).

```python
# To get the supplier name
supplier_name = invoice_data.invoice.supplier.value
```

- **Invoice.supplier_address**: Supplier address as written in the invoice.

```python
# To get the supplier address
supplier_address = invoice_data.invoice.supplier_address.value
```

### Taxes
**invoice.taxes**: Contains array of tax fields. Each of the tax fields has two extra attributes:

- **code** (String): Optional tax code (HST, GST... for Canadian; City Tax, State tax for US, etc..).
- **rate** (Float): Optional tax rate.

```python
# To get the list of taxes
taxes = invoice_data.invoice.taxes

# Loop on each Tax field
for tax in taxes:
   # To get the tax amount
   tax_amount = tax.value

   # To get the tax code for from a tax object
   tax_code = tax.code

   # To get the tax rate
   tax_rate = tax.rate
```

### Total Amounts

- **Invoice.total_incl**: Total amount including taxes.

```python
# To get the total amount including taxes value (float), ex: 14.24
total_incl = invoice_data.invoice.total_incl.value
```

- **Invoice.total_excl**: Total amount excluding taxes.

```python
# To get the total amount excluding taxes value (float), ex: 10.21
total_excl = invoice_data.invoice.total_excl.value
```

- **Invoice.total_tax**: Total tax value from tax lines.

```python
# To get the total tax amount value (float), ex: 8.42
total_tax = invoice_data.invoice.total_tax.value
```