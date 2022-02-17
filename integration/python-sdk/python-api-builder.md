
## Usage with the API Builder
If your document isn't covered by one of Mindee's Off-the-Shelf document endpoints,
you can create your own with the
[API Builder](https://developers.mindee.com/docs/build-your-first-document-parsing-api).

### Configuring the Client
Specification for a custom endpoint configuration:

#### Arguments

##### `document_type`
The "document type" field in the "Settings" page of the API Builder.

##### `singular_name`
The name of the attribute used to retrieve a _single_ document from the API response.

##### `plural_name`
The name of the attribute used to retrieve _multiple_ documents from the API response.

##### `account_name`
Your organization's username in the API Builder.

##### `api_key`
Your API key for the endpoint. Optional, since this can be set with an environment variable.

##### `version`
If set, locks the version of the model to use. If not set, use the latest version of the model.

If this is set, it will mean having to update your code every time a new model is trained.
This is probably not what you want for development, but can be very useful for production use.

##### Code Sample
```python
from mindee import Client

mindee_client = Client().config_custom_doc(
    document_type="pokemon-card",
    singular_name="card",
    plural_name="cards",
    account_name="pikachu",
    api_key="pokemon-card-api-key",  # optional, can be set in environment
    # version="1.2",  # optional, see arguments section above
)
```

#### Environment Variables
You can also set the API keys as environment variables.

The format is `MINDEE_<username>_<document_type>_API_KEY` where `<username>` and `<document_type>` are uppercase, any `-` replaced with `_`.

The example above would look for:
* `MINDEE_PIKACHU_POKEMON_CARD_API_KEY`


### Parsing Documents
The call to the `parse` method is the same as with Off-the-Shelf documents.

```python
loaded_doc = mindee_client.doc_from_path("/my/cards/pikachu.jpg")
parsed_data = loaded_doc.parse("pokemon-card")
```

**NOTE:** If your custom document has the same name as an Off-The-Shelf document,
you must specify your username when calling the `parse` method.

```python
from mindee import Client

mindee_client = Client().config_custom_doc(
    document_type="receipt",
    singular_name="receipt",
    plural_name="receipts",
    account_name="JohnDoe",
    api_key="johndoe-receipt-api-key",
)

loaded_doc = mindee_client.doc_from_path("/path/to/receipt.jpg")
parsed_data = loaded_doc.parse("receipt", "JohnDoe")
```
