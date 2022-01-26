---
title: Authentication
excerpt: ''
next:
  pages:
    - endpoints
    - error-management
  description: ''
---

Authentication is the process of identifying and verifying the identity of a user making the API call. Mindee API uses **API Keys** for authentication. The API key is a long string that you usually include either in the request URL or request header. To get your API key, see [Create your API key](https://developers.mindee.com/docs/make-your-first-request#create-an-api-key). Keep in mind that your API keys has alot of uses, so be careful to keep them safe! Keep your private API keys out of the public eye by avoiding putting them on GitHub, client-side code, or any other publicly accessible location.

## Authenticate Your API Calls
In order to authenticate your requests, you must include a valid API key using a custom HTTP Authorization header when calling Mindee's REST API, you do not need to provide a password. API requests without authentication will also fail.

```
Authorization: Token <my-apikey-here>
```

For each API, you can create as many API keys as you want in the API Key section. See [Platform tour](https://developers.mindee.com/docs/platform-tour#api----api-keys) for more information.

## API Key Revocation

You can revoke an API key at any time using the API Key section. 

**Note**: Once an API key is revoked, using it to authenticate your request will lead to a [401 error](https://developers.mindee.com/docs/error-management#possible-errors)
