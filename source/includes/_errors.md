# Errors

The Veho API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request
401 | Unauthorized -- The header did not include a valid apiKey.
403 | Forbidden -- The requested resource cannot be accessed with this app ID.
404 | Not Found -- The requested resource could not be found.
405 | Method Not Allowed -- You tried to access an endpoint with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
410 | Gone -- The resource requested has been removed from our servers.
429 | Too Many Requests
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
