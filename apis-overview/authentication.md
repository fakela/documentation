---
title: Authentication
excerpt: ''
next:
  pages:
    - endpoints
    - error-management
  description: ''
---
## Authenticate your API calls
In order to authenticate your requests, you must include a valid API key using a custom HTTP Authorization header when calling Mindee's REST API:
[block:code]
{
  "codes": [
    {
      "code": "Authorization: Token <my-apikey-here>",
      "language": "text",
      "name": "HTTP Headers"
    }
  ]
}
[/block]

```bash
Authorization: Token <my-apikey-here>
```

For each API, you can create as many api keys as you want in the credentials page. See [Platform tour](doc:platform-tour#api----api-keys) for more information.

## API key revocation

You can revoke an api key at any time using the platform's credentials section. Note that once a key is revoked, using it to authenticate your request will lead to a 401 error.