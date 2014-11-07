GearTranslations API
====================

This is a JSON API offered by GearTranslations.

Making a request
----------------

The base URL for the API is `http://clients.geartranslations.com/v1/`.

Client-side Errors
------------------

API calls may have one of many of the following errors:

* Sending an invalid or incomplete JSON will yield a `400 Bad Request` response.

```
HTTP/1.1 400 Bad Request

{ "error": "Missing Parameters" }
```

* Asking for inexistent resources will yield a `404 Not Found` response.

```
HTTP/1.1 404 Not Found

{ "error": "Resource not found" }
```

Server-side Errors
------------------

Any error with a 5XX error is a server-side error. These mean that either the app is not available, under maintenance or a connection error. In any case, try again later.

Contact us
----------

If you have any ideas or suggestions to help make the GearTranslations API better, please do not hesitate to either contact us at <mailto:api@geartranslations.com> or leave us an issue on GitHub.
