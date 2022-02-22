---
title: Python SDK Getting started
excerpt: ''
next:
  pages:
    - python-receipt-ocr
    - python-passport-ocr
    - python-invoice-ocr
  description: ''
---
Get started with Mindee's python SDK.

## Installation

### Requirements
This library is officially supported on Python 3.7 to 3.10.

### Normal Installation
The preferred installation method is via `pip`:
```shell script
pip install mindee
```

### Development Installation
If you'll be modifying the source code, you'll need to install the development requirements as well.

First clone the repo:
```shell script
git clone git@github.com:mindee/mindee-api-python.git
```

Then navigate to the cloned directory and install all development requirements:
```shell script
cd mindee-api-python
pip install .[dev,test]
```

 
## The Client
The client centralizes document configurations in a single object.

Documents are added to the `Client` using a *config_xxx* method.

Since each *config_xxx* method returns the current `Client` object, you can simply chain all the calls together.

You only need to specify the API keys for the document endpoints you'll be using.

```python
from mindee import Client

mindee_client = (
    Client()
        .config_receipt("receipt-api-key")
        .config_invoice("invoice-api-key")
        .config_financial_doc("receipt-api-key", "invoice-api-key")
        .config_passport("passport-api-key")
        .config_custom_doc(
          document_type="pokemon-card",
          singular_name="card",
          plural_name="cards",
          account_name="pikachu",
          api_key="pokemon-card-api-key"
    )
)
```

### Environment Variables
We highly suggest to use environment variables for the API keys, especially for production.

For Off-The-Shelf APIs, here are the keys you can set:

* `MINDEE_RECEIPT_API_KEY`
* `MINDEE_INVOICE_API_KEY`
* `MINDEE_PASSPORT_API_KEY`

Custom documents can be set as well, in keeping with the example above:
* `MINDEE_PIKACHU_POKEMON_CARD_API_KEY`


## Handling Documents

### Loading Documents
You can load your document in several ways.

The various methods are called from the `Client` and return an object you can
then serialize to the API.

#### Path
An absolute path, as a string.
```python
loaded_doc = mindee_client.doc_from_path('/path/to/invoice.pdf')
```

#### File Object
A normal Python file object/handle. Must be in binary mode!
```python
with open('/path/to/receipt.jpg', 'rb') as fo:
     loaded_doc = mindee_client.doc_from_file(fo)
```

#### Base64
A base64 encoded string.

**Note:** the original filename of the encoded file is required when calling the method.
```python
b64_string = "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLD...."
loaded_doc = mindee_client.doc_from_b64string(b64_string, "receipt.jpg")
```

#### Bytes
Raw bytes.

**Note:** the original filename is required when calling the method.
```python
raw_bytes = b"%PDF-1.3\n%\xbf\xf7\xa2\xfe\n1 0 ob..."
loaded_doc = mindee_client.doc_from_bytes(raw_bytes, "invoice.pdf")
```

Loading from bytes is useful when using FastAPI `UploadFile` objects:
```python
@app.post("/invoice")
async def upload(upload: UploadFile):
    invoice_data = mindee_client.doc_from_bytes(
        upload.file.read(),
        filename=upload.filename
    ).parse(
        "invoice"
    )
```

### Document Parsing
Once a document is loaded, you can send it to the API endpoint(s).

The document parse type must be specified when calling the `parse` method.

The object containing the parsed data will be an attribute of the response object.

#### Receipts
```python
api_response = loaded_doc.parse("receipt")
print(api_response.receipt)
```

#### Invoices
```python
api_response = loaded_doc.parse("invoice")
print(api_response.invoice)
```

#### Passports
```python
api_response = loaded_doc.parse("passport")
print(api_response.passport)
```

#### Financial
Mixed data flow of invoices and receipts.

**Note:** You'll need an API key for _both_ invoice and receipts endpoints.
```python
api_response = loaded_doc.parse("financial_doc")
print(api_response.financial_doc)
```
