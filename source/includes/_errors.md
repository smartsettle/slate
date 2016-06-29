# Errors

The Smartsettle API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request
401 | Unauthorized -- Your API key is wrong
403 | Forbidden
404 | Not Found 
405 | Method Not Allowed 
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone
429 | Too Many Requests
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
