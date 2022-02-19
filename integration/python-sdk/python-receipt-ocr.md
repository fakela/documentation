---
title: Receipt API
excerpt: ''
---

## Data structure

```python
from mindee import Client

mindee_client = Client().config_receipt("receipt-api-key")
receipt_data = mindee_client.doc_from_path("/path/to/file").parse("receipt")
```

### Document level prediction
The receipt_data object returned by the **parse_receipt** method contains the following elements:

```python
receipt_data.receipt # returns a unique object from class Receipt
```

The receipt attribute is the Receipt object constructed by gathering all the pages into a single document. The method used for creating a single receipt object with multiple pages relies on field confidence scores. Basically, we iterate over each page, and for each field, we keep the one that has the highest probability.

### Page Level Prediction

```python
receipt_data.receipts # [Receipt, Receipt ...]
```

For multi-pages pdf, the receipts attribute contains one receipt object per input. For a single-page pdf or an image, the list will only contain 1 item, and for a multi-page pdf, it will contain one item per page.

### Raw HTTP Response

```python
receipt_data.http_response # full HTTP request object
```

Contains the full Mindee API HTTP response object in JSON format

## Extracted Fields
Each receipt object contains a set of different fields. Whatever the field type, each of them contains the four following attributes:

> **value**: (Str or Float depending on the field type), corresponds to the field value. Set to None if the >field was not extracted.
> **probability**: (Float), confidence score of the field prediction.
> **bbox**: (Array[Float]), contains the relative vertices coordinates of the bounding box containing the > field in the image. If the field is not written, the bbox is an empty array.
> **reconstructed**: (Bool), True if the field was reconstructed using other fields.

Depending on the Field type, there can be extra attributes.

- [Category](#category)
- [Dates](#dates)
- [Locale and Currency](#locale-and-currency)
- [Supplier informations](#supplier-informations)
- [Taxes](#taxes)
- [Time](#time)
- [Total amounts](#total-amounts)

### Category
**category**: Receipt category among the list:  toll, food, parking, transport, accommodation, gasoline, miscellaneous

```python
# To get the category
category = receipt_data.receipt.category.value
```

### Dates
Each date field comes with an extra attribute:

> **date_object**: (Datetime), datetime object from python datetime.date library

 **receipt.date**: Payment date related to the receipt

```python
# To get the receipt date of issuance (string)
receipt_date = receipt_data.receipt.value
```

### Locale and Currency
**locale**: Language ISO code

Contains an extra attribute:

**currency**: (String), ISO currency code

```python
# To get the total language code
language = receipt_data.receipt.locale.value

# To get the receipt currency code
currency = receipt_data.receipt.locale.currency
```

### Supplier informations
**receipt.supplier**: Supplier name as written in the receipt (logo)

```python
# To get the supplier name
supplier_name = receipt_data.receipt.supplier.value
```

### Taxes
**receipt.taxes**: Array of Tax fields

Each of the tax field has two extra attributes:

> **code**: (String), Optional tax code. (HST, GST... for canadian; City Tax, State tax for US etc..)
> **rate**: (Float), Optional tax rate.

```python
# To get the list of taxes
taxes = receipt_data.receipt.taxes

# Loop on each Tax field
for tax in taxes:
   # To get the tax amount
   tax_amount = tax.value

   # To get the tax code for from a tax object
   tax_code = tax.code

   # To get the tax rate
   tax_rate = tax.rate
```

### Time
**time**: Time of purchase with 24 hours formatting (hh:mm)

```python
# To get the category
category = receipt_data.receipt.time.value
```

### Total amounts
**receipt.total_incl:** Total amount including taxes

```python
# To get the total amount including taxes value (float), ex: 14.24
total_incl = receipt_data.receipt.total_incl.value
```

**receipt.total_excl**: Total amount excluding taxes

```python
# To get the total amount excluding taxes value (float), ex: 10.21
total_excl = receipt_data.receipt.total_excl.value
```

**receipt.total_tax**: Total tax value reconstructed from tax lines

```python
# To get the total tax amount value (float), ex: 8.42
total_tax = receipt_data.receipt.total_tax.value
```
