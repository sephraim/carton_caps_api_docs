# Errors

The Carton Caps API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
404 | Not Found -- The specified user could not be found.
405 | Method Not Allowed -- You tried to access a user or a referral with an invalid method.
422 | Unprocessable Entity -- Your JSON request is well-formed but contains invalid value(s), e.g. referral code.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
