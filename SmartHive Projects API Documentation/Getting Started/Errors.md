# Error Codes

SmartHive Projects uses HTTP status codes to indicate success or failure of API calls. Status codes 2xx indicate success, 4xx indicate error in the information provided, and 5xx indicate server side errors. 
The following table lists some commonly used HTTP status codes.

## Status Codes

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

## Other Error Responses

Besides HTTP status codes and their corresponding error messages, error responses for SmartHive Projects APIs also include a machine-parsable errorCode param to simplify error handling.

The different errorCodes and their uses are described below.

### URL_RULE_NOT_CONFIGURED 400

Please check if the URL you are trying to access is correct.

**Resolution:** The request URL specified is incorrect. Specify a valid request URL.

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

This errorCode appears if the OAuthToken is invalid or has expired.

**Resolution:** Regenerate OAuthToken and try again.

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

The HTTP request specified has an invalid input parameter.

**Resolution:** The request URL input parameter specified is incorrect. Specify a valid request input parameter URL.

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

The http request method type is not a valid one

**Resolution:** You have specified an invalid HTTP method to access the API URL. Specify a valid request method.

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

The HTTP request specified has an invalid parameter value.

**Resolution:** The request URL input parameter value specified is incorrect. Specify a valid request input parameter value.

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

Server encountered an unexpected error. Contact

**Resolution:** support@smarthiveprojects.com

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