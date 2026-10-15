# Error codes

SmartHive Projects uses HTTP status codes to indicate whether an API call succeeded or failed. Status codes in the 2xx range indicate success, codes in the 4xx range indicate an error in the information 
provided, and codes in the 5xx range indicate server-side errors. The following table lists some commonly used HTTP status codes:

## Status codes

| Status Code     | Description |
| :---        | :----  |      
| 200     | Ok      |
| 201   | Created |
| 202   | Accepted     |
| 204   | No content     |
| 206   | Partial Data      |
| 207   | Multi-status     |
| 400   | Bad request |
| 401   | Unauthorized     |
| 402   | Payment Required     |
| 403   | Forbidden (Unauthorised access)      |
| 405   | Method not allowed (Method called is not supported for the API invoked)      |
| 409   | Conflict |
| 429   | Too Many Requests     |
| 500   | Internal error     |
| 501   | Not Supported      |

## Other error responses

In addition to HTTP status codes and their error messages, error responses for SmartHive Projects APIs include a machine-parsable `errorCode` parameter to simplify error handling.

The following sections describe the error codes and their uses:

### URL_RULE_NOT_CONFIGURED 400

Check whether the URL you’re trying to access is correct.

**Resolution:** The request URL isn’t correct. Specify a valid request URL.

**URL_RULE_NOT_CONFIGURED**
```
{
  "error": {
    "status_code": "400",
    "instance": "/api/v3/portal/15403665/projects/6000000030017/forums",
    "title": "URL_RULE_NOT_CONFIGURED",
    "error_type": "FIELDS_VALIDATION_ERROR",
    "details": [
      {
        "message": "Given URL is wrong"
      }
    ]
  }
}
```
### INVALID_OAUTHTOKEN 400

The OAuth token isn’t valid or has expired.

**Resolution:** Generate a new OAuth token, and try again.

**INVALID_OAUTHTOKEN**
```
{
  "error": {
    "status_code": "400",
    "instance": "/api/v3/portal/15403665/projects/6000000030017/forums",
    "title": "INVALID_OAUTHTOKEN",
    "error_type": "FIELDS_VALIDATION_ERROR",
    "details": [
      {
        "message": "Invalid OAuth access token."
      }
    ]
  }
}
```
### INVALID_INPUTSTREAM 400

The HTTP request has an input parameter that isn’t valid.

**Resolution:** The input parameter in the request URL isn’t correct. Specify a valid input parameter.

**INVALID_INPUTSTREAM**
```
{
  "error": {
    "status_code": "400",
    "title": "INVALID_INPUTSTREAM",
    "error_type": "FIELDS_VALIDATION_ERROR",
    "details": [
      {}
    ]
  }
}
```
### INVALID_METHOD 400

The HTTP request method isn’t valid.

**Resolution:** You specified an HTTP method that isn’t valid for this API URL. Specify a valid request method.

**INVALID_METHOD**
```
{
  "error": {
    "status_code": "400",
    "instance": "/api/v3/portal/15403665/projects/6000000030017/forums",
    "title": "INVALID_METHOD",
    "error_type": "FIELDS_VALIDATION_ERROR",
    "details": [
      {
        "message": "Invalid request method",
        "field_name": "COPY"
      }
    ]
  }
}
```
### INVALID_PARAMETER_VALUE 400

The HTTP request has a parameter value that isn’t valid.

**Resolution:** The value of the input parameter in the request URL isn’t correct. Specify a valid parameter value.

**INVALID_PARAMETER_VALUE**
```
{
  "error": {
    "status_code": "400",
    "instance": "/api/v3/portal/15403665/projects/6000000030017/forums",
    "method": "GET",
    "error_type": "FIELDS_VALIDATION_ERROR",
    "details": [
      {
        "message": "You don't have sufficient permission to create an internal forum.",
        "field_name": "type"
      }
    ],
    "title": "INVALID_PARAMETER_VALUE"
  }
}
```
### INTERNAL_SERVER_ERROR 500

The server encountered an unexpected error.

**Resolution:** Contact support@smarthiveprojects.com

**INTERNAL_SERVER_ERROR**
```
{
  "error": {
    "status_code": "500",
    "instance": "/api/v3/portal/15403665/projects/6000000030017/forums",
    "method": "GET",
    "error_type": "OPERATIONAL_VALIDATION_ERROR",
    "details": [
      {
        "message": "Internal server error. Please contact support for further details.",
        "message_key": "zp.general.error"
      }
    ],
    "title": "INTERNAL_SERVER_ERROR"
  }
}
```