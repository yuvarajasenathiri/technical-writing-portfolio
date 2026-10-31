# REST API Documentation - SmartHive Projects

**Version:** 3.0  
**Last updated:** August 2026  
**Applies to:** SmartHive Projects API v3

------

## Table of contents

1.  [Introduction](#introduction)
2.  [Getting started](#getting-started)
	 - [What's new in v3](#what's-new-in-v3)
	 - [HTTP methods](#http-methods)
	 - [Error codes](#error-codes)
	 - [API limits](#api-limits)
	 - [Pagination](#pagination)
	 - [API names](#api-names)
	 - [Custom fields](#custom-fields)	
     - [Filter guide](#filter-guide)
3.  [OAuth Authentication](#OAuth-authentication)
	 - [Overview](#overview)
	 - [How it works](#how-it-works)
	 - [Scopes](#scopes)
	 - [Making API calls with access token](#making-API-calls-with-access-token)
	 - [API endpoints by data center](#API-endpoints-by-data-center)
	 - [Related resources on OAuth](#related-resources-on-Oauth)
----

## Introduction

SmartHive Projects provides REST APIs to manage your projects, connect third-party apps, and send data to or get data from SmartHive Projects.

**API Root Endpoint:** `https://projects.smartHive.com`

## Getting started

**Mandatory headers**

SmartHive Projects APIs require the `Authorization` header. The header contains the OAuth access token that authenticates the user who accesses the data.

**Example:**
```
curl -X GET https://projects.smarthive.com/api/v3/portal/{portal_id}/tasks  
-H "Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa"
```
### What's new in v3

Version 3 (v3) builds on the existing SmartHive Projects API. It introduces a more consistent structure across endpoints and extends support for common integration needs. Updates to date formats, filtering, 
custom fields, and pagination make it easier to work with data predictably. This section describes what’s new in v3, what has changed, and what to review when you move from v2.

**v3 API - Quick Example:**
```
GET /api/v3/portal/{portal_id}/projects
Authorization: Bearer {token}

Response:
{
  "page_info": {
    "page": 1,
    "per_page": 100,
    "page_count": 100,
    "has_next_page": true
  },
  "projects": [...]
}
```
#### Enhancements in the v3 API

v3 introduces a more consistent, structured way to work with the SmartHive Projects API. It simplifies how you format data, construct requests, and handle responses, which makes integrations easier to build 
and maintain. These updates also make it clearer how to work with filters, custom fields, and large datasets.

**v3 Improvements at a Glance:**
```
// 1. Dates → ISO 8601
"due_date": "2024-05-26T00:00:00.000Z"

// 2. Filtering → one request
"filter": {
  "criteria": [
    {
      "field_name": "status",
      "criteria_condition": "all_open"
    }
  ],
  "pattern": "1"
}

// 3. Custom fields → api_name
"cf_priority_level": "High"

// 4. Request = Response
"assignee": { "zpuid": "...", "name": "John Doe" }

// 5. Pagination → page-based
"page_info": {
  "page": 1,
  "per_page": 100,
  "page_count": 100,
  "has_next_page": true
}
```
#### Consistent date and time Format

All date and time values follow a single ISO 8601 format across endpoints. This makes parsing consistent, so you don’t need to handle multiple formats.

| Type     | v2 | v3 |
| :---        | :----  |      :---- |
| Date only     | `"05-26-2014"` (MM-DD-YYYY)      | `"2024-05-26"` (YYYY-MM-DD)  |
| Datetime   | `"05-13-2014 05:57 PM"` (12-hour)        | `"2024-05-26T11:25:58.000Z"` (ISO 8601)     |
| Human-readable   | `"May 26, 2014"`     | **removed**      |
| Epoch   | `1399620397255`     | **removed**       |
| Date input format   | `MM-DD-YYYY`       | `YYYY-MM-DD`      |

The `*_long` epoch fields are removed because ISO 8601 timestamps are widely supported.

#### Advanced filtering

You can define multiple conditions in a single request by using a structured filter object. The server does all the filtering, so the response contains only the relevant records.

- **Supported conditions:**
	- `is`
	- `is_not`
	- `contains`
	- `starts_with`
	- `before`
	- `after`
	- `is_empty`
	- `is_not_empty`
	- `between`
	
**Advanced Filter - Quick Example:**
```
{
  "filter": {
    "criteria": [
    {
      "field_name": "due_date",
      "criteria_condition": "today"
    },
    {
      "field_name": "assignee",
      "criteria_condition": "is",
      "value": ["user_zpuid"]
    }
  ],
  "pattern": "1 AND 2"
  }
}
```
- **Pattern logic:** Combine conditions by using `AND`, `OR`, and grouping, for example, `"(1 OR 2) AND 3"`.
- **Custom field support:** Use the `api_name` of any custom field as the criteria `field_name`.

For the complete syntax reference, see the Filter Guide.

#### Standardized custom fields

Custom fields now use clear, consistent `api_name` values. You can reference them across requests, filters, and responses without additional mapping.

|      | v2 | v3 |
| :---        | :----  |      :---- |
| In requests     | `UDF_CHAR1`, `UDF_LONG2`      | `expected_date`, `priority_level` |
| In responses   | Same **UDF_** keys, no context      | Same **api_name**, consistent everywhere     |

**v3 Custom Field in Response:**
```
{
  "expected_date": "2024-05-26"
}
```
**v3 Custom Field in Filter:**
```
{
  "criteria": [
    {
      "field_name": "expected_date",
      "criteria_condition": "is",
      "value": ["2024-05-26"]
    }
  ]
}
```
- **Stable references:** Field identifiers don’t change when you add or remove other fields.

- **Consistent names:** The same `api_name` works in requests, responses, and filter criteria.

For full details, see Custom Fields.

#### Request and response structure

Requests and responses use the same field structure. This makes the API more predictable and reduces the need for transformation logic when you handle API data.

|  Aspect    | Version 2 (/restapi) | Version 3 (/api/v3) |
| :---        | :----  |      :---- |
| Content Type     | *application/x-www-form-urlencoded*     | *application/json* |
| Body Style   | Flat, form-encoded parameters      | JSON body, nested objects     |
| Dates   | Mixed formats (MM-DD-YYYY, epoch, text)     | ISO 8601 everywhere     |
| Related Data   | Flat fields *(person_responsible, assignee_name)*     | Grouped objects *(assignee, status)*    |
| List Responses   | No pagination metadata      | *page_info* block with *has_next_page*     |

**v3 Request (JSON):**
```
POST /api/v3/portal/{portal_id}/projects/{project_id}/tasks
Content-Type: application/json

{
  "name": "Task Name",
  "assignee": { "zpuid": "user_id" },
  "due_date": "2024-05-26",
  "priority": "High"
}
```
**v3 Response:**
```
{
  "page_info": {
    "page": 1,
    "per_page": 100,
    "page_count": 100,
    "has_next_page": true
  },
  "tasks": [
    {
      "id": "12345",
      "name": "Task Name",
      "due_date": "2024-05-26T00:00:00.000Z",
      "assignee": {
        "zpuid": "...",
        "name": "John Doe",
        "email": "..."
      },
      "status": {
        "id": "...",
        "name": "Open",
        "color": "#...",
        "is_closed_type": false
      }
    }
  ]
}
```
#### Pagination

Pagination is now page-based, which makes it easier to work with large datasets.

 - Use `page` and `per_page` to control the results.
 - The `has_next_page` parameter indicates whether more records are available.
 - Pagination avoids duplicate or skipped records.
 - You don’t need to calculate offsets manually.
 
For full details and examples, see Pagination.
 
#### Base URL structure
 
All v3 endpoints follow a consistent URL pattern. The base URL is simplified and standardized, and trailing slashes aren’t required. This makes it easier to construct and predict endpoint URLs across the 
API.
|      | v2 | v3 |
| :---        | :----  |      :---- |
| Base URL    | */restapi/portal/{portal_id}/projects/*    | *api/v3/portal/{portal_id}/projects* |
| Trailing slashes   | Some endpoints require trailing `/`      | No trailing slashes     |

| Operation | v2 | v3 |
| :---        | :----  |      :---- |
| List tasks   | *GET /restapi/portal/{portal_id}/projects/{project_id}/tasks/*    | *GET api/v3/portal/{portal_id}/projects/{project_id}/tasks* |

**Note:** If you're migrating from v2, replace the `/restapi/` prefix with `/api/v3/` in all endpoint URLs.

#### Quick comparison

|  Area    | Version 2(/restapi) | Version 3(/api/v3) |
| :---        | :----  |      :---- |
| URL Pattern    | */restapi/portals/*    | */api/v3/portals* |
| Date Format   | `"05-26-2014"` or `"May 26, 2014"` or `1399620397255`     | `"2024-05-26"` (date only) or `"2024-05-26T11:25:58.000Z"` (ISO 8601)     |
| Pagination   | `index` + `range` (offset-based)   | `"page` + `per_page` with `has_next_page`     |
| HTTP Method for Updates  | POST   | PATCH     |
| Custom Fields  | `UDF_` prefix (for example, `UDF_CHAR1)` | `api_name` (for example, `"expected_date"`)    |
| Request and response schema  | Fields sent in requests often differed from response field names. | Request and response use the same field structure throughout. |
| API coverage | Limited modules and endpoints. | Additional modules and endpoints that expand the API.  |

**v3 Update Task Example**
```
PATCH /api/v3/portal/{portal_id}/projects/{project_id}/tasks/{task_id}
Content-Type: application/json

{
  "assignee": {
    "zpuid": "user_id"
  },
  "due_date": "2024-05-26",
  "cf_priority_level": "High"
}
```
### HTTP methods

SmartHive Projects supports the following methods.

| Method     | Purpose |
| :---        | :----  |      
| GET     | Retrieve data      |
| POST   | Add or create data and perform actions |
| PUT   | Update data     |
| PATCH   | Partial updates     |
| DELETE   | Delete data      |

### Error codes

SmartHive Projects uses HTTP status codes to indicate whether an API call succeeded or failed. Status codes in the 2xx range indicate success, codes in the 4xx range indicate an error in the information 
provided, and codes in the 5xx range indicate server-side errors. The following table lists some commonly used HTTP status codes:

#### Status codes

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

#### Other error responses

In addition to HTTP status codes and their error messages, error responses for SmartHive Projects APIs include a machine-parsable `errorCode` parameter to simplify error handling.

The following sections describe the error codes and their uses:

##### URL rule not configured 400

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
##### Invalid OAuth token 400

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
##### Invalid Inputstream 400

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
##### Invalid method 400

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
##### Invalid Parameter Value 400

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
##### Internal server error 500

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
### API limits

SmartHive Projects APIs have rate limits to ensure fair usage and optimal performance for all users.

**Request:** `GET /api/v3/portal/{portal_id}/projects`

**Notes**

- You can call each API up to **200 times in a 2-minute window**.
- The limit applies to **each API endpoint**.

#### Rate limit info

Each API response includes the following headers to help you monitor your usage: 

- `RateLimit`: The total number of requests allowed in the current window, for example, 200.
- `RateLimit-Remaining`: The number of requests remaining in the current window.
- `RateLimit-Window`: The duration of the rate limit window, for example, 120 seconds.
- `RateLimit-Window-Unit`: The time unit for the rate limit window, for example, seconds.
- `Retry-After`: The time, in seconds, to wait before you retry the request after you exceed the rate limit.

**Rate Limit Info**
```
RateLimit = 200
RateLimit-Remaining = 199
RateLimit-Window = 120
RateLimit-Window-Unit = seconds
Retry-After = 540 (seconds remaining)

**Note:** The API returns the Retry-After header only when you exceed the rate limit.
```
#### Rate limit exceeded

If you exceed the allowed number of requests:

- SmartHive Projects **blocks** that **API for 10 minutes**.
- During this period, all further requests to that API fail.
- The response includes a `Retry-After` header that shows the remaining time, in seconds, before the API is available again.

#### Important notes

- The restriction applies **only to the API that exceeds the limit**, not to all APIs.
- After the 10-minute cooldown, the API becomes available automatically.
- Repeated violations can affect app performance and reliability.

#### Best practices

To avoid reaching rate limits:

- Implement retry logic that uses the `Retry-After` header.
- Use **exponential backoff** instead of immediate retries. Use **exponential backoff** instead of immediate retries.
- Avoid sending unnecessary or duplicate requests.
- Use **batch APIs**, if available, to reduce the number of calls.
- Cache frequently used data when possible.

### Pagination

The v3 API uses page-based pagination on all list endpoints. To control which page of results the API returns, pass `page` and `per_page` as query parameters.

**Request:** `GET /api/v3/portal/{portal_id}/projects/{project_id}/tasks?page=2&per_page=50`

#### Query Parameters

| Parameter     | Type | Description |
| :---        | :----  |      :---- |
| `page`    | Integer      | The page number, starting from 1. The default is 1.  |
| `per_page`   | Integer   |  The number of records per page. The default is 100. Supported values: 1 to 200. |

**page_info Response:**
```
{
  "page_info": {
    "page": 2,
    "per_page": 50,
    "page_count": 10,
    "has_next_page": true
  }
}
```
#### Response

Every list response includes a `page_info` object. The `has_next_page` field tells your client when to stop fetching. You don’t need to calculate offsets, and you avoid duplicate or skipped records.

| Field     | Type | Description |
| :---        | :----  |      :---- |
| `page`    | Integer      | The current page number.  |
| `per_page`   | Integer        | The number of records per page.    |
| `page_count`   | Integer        | The total number of records in the result set.   |
| `has_next_page`   | Boolean      | The value is `true` if more pages exist and `false` if the current page is the last page.   |

### API names

Understand, locate, and use API names for modules, fields, and related APIs in SmartHive Projects.

SmartHive Projects assigns a unique identifier, called an API name, to every module and field.

Display names, the labels shown in the UI, can change and can include spaces or special characters. API names stay the same across API requests and responses, so they give you a consistent reference.

#### Display name vs. API name

| Aspect	| Display name |	API name |
| :---        | :----  |      :---- |
| Purpose	| A label shown in the UI |	An identifier used in APIs |
| Example	 | Start Date	| `start_date` |
| Stability |	Can change	| Stays constant |
| Used in	| Forms, views, and layouts |	Requests, responses, and filters|

#### Usage

You use API names in all programmatic interactions with SmartHive Projects.

##### Requests and responses

API names appear as keys in request payloads and response data. You reference fields such as priority, status, and department by their API names, not their display labels. This applies to operations such as 
creating, updating, retrieving, and filtering records.

#### Retrieve API names

You can find API names for modules and fields in SmartHive Projects in the product or by using the APIs.

##### Method 1: Use the product

The **Fields** section in SmartHive Projects shows the API names for custom fields next to other field details.

1. Select **Setup** > **Customization** > **Fields**.
2. Select the module you need.
3. Use **Search** Fields to find a specific field in the Fields list.
4. Copy the API name to use in API operations.

##### Method 2: Use the APIs

The Modules API returns metadata for all modules in a portal, including their API names. The Fields API returns metadata for all fields in a module, including API names, data types, and whether each field 
is custom. Together, they give you a complete reference of the available modules and fields.

- For the list of modules and their API names, see Get Modules.
- For field-level details, including API names, see Get Fields Info.

### Custom fields

Send custom field values when you create or update records through the SmartHive Projects APIs.

Custom fields are configured in module layouts to capture additional information based on business needs. To pass values in the request payload, use the API names of the corresponding fields.

For example, you can use a checkbox custom field to track a project condition and submit its value as true or false in the API request.

**Note:***

- Custom field API names are currently supported only in the Tasks and Projects APIs.
- Before you pass values, use the Custom Fields metadata API to get field details such as API names and field types.

#### Field types

##### Overview

SmartHive Projects supports several custom field types, such as text, numeric, URL, date, and time. The following sections describe the field types available in the Create and Update APIs.

**Note**

- Send all inputs as an input stream `(application/json)`.
- Use API names for custom fields.

##### Single-line field

Captures text on a single line. Maximum length: 200 characters.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"title": "Project Ara"}`

##### Multi-line field

Captures text on multiple lines. Use `\n` to separate lines. Maximum length: 1,000 characters.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"description": "The respective team\n is a prototype."}`

##### Pick list field

Captures a single option selected from a predefined list. Maximum options: 50.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"Material": "Vinyl"}`

##### Multi-select field

Captures multiple options selected from a predefined list. You can add or remove values, or replace the existing values. Maximum selectable options: 100.

**Note**

- The add and remove options optimize the update process for multi-select fields. You don’t need an extra GET call to retrieve the existing values before you update.
- You can add or remove values directly in an Update API request, or use the Create API format.

**Sample input of multi-select field in create APIs:** `{ "key": [ "C", "D" ] }`
**Example:** `{ "parts_required": [ "HDD", "CD" ] }`

**Sample input of multi-select field in create APIs:** 

```
{ 
"key": [ 
{ 
"add": [ "A", "B" ], 
"remove": [ "E", "F" ]
}]}
```

**Example:** 

```
{ 
"parts_required": [ 
{ 
"add": [ "processor", "GPU" ],
"remove": ["POWER-CORD", "RAM" ]  
}]}
```

##### User pick list field

Captures a single selected user.

**JSON schema:** 
```
{ 
"key": { 
"zpuid": "user id" 
}}
```
**Example:** 

```
{ "reporter": { 
"zpuid": "123454321" 
}}
```

##### Multi-user field

Captures multiple users selected from a predefined list. You can add or remove values, or replace the existing values. Maximum selectable users: 500.

**Note**

- The add and remove options optimize the update process for multi-user fields. You don’t need an extra GET call to retrieve the existing values before you update.
- You can add or remove values directly in an Update API request, or use the Create API format.

**Sample input of multi-user field in create APIs:** 
```
{ "key": [ 
{ "zpuid": "User Id 5" }, 
{ "zpuid": "User Id 6" } 
]}
```
**Example:** 
```
{ 
"user_group": [ 
{ "zpuid": "7845996622" },
{ "zpuid": "7876456433" } 
]}
```
**Sample input of multi-user field in create APIs:** 
```
{ "key": [ 
{ 
"add": [
{ "zpuid": "User Id 2" },
{ "zpuid": "User Id 3" }
],
"remove": [ 
{ "zpuid": "User Id 4" }, 
{ "zpuid": "User Id 5" } 
]}]}
```
**Example:** 
```
{"user_group": [ 
{ 
"add": [
{ "zpuid": "712554144112" },
{ "zpuid": "71255413512" }],
"remove": [ 
{ "zpuid": "778946456" }, 
{ "zpuid": "71346753132" } 
]}]}
```
##### Date field

Captures a date in the `yyyy-MM-dd` format (ISO 8601).

**JSON schema:** `{ "key": "string"}`
**Example:** 
```
{
"due_date": "2022-10-17",
"start_date":"2019-09-17",
"end_date": "2024-12-17"
}
```
##### Time field

Captures the time in `HH:MM` format.

**JSON schema:** `{ "key": "string"}`
**Example:** 
```
{
"start_time": "23:30",
"end_time": "13:30"
}
```
##### Time stamp field

Captures a date and time in ISO 8601 format. Use `yyyy-MM-dd'T'HH:mm:ss'Z'` for UTC, or `yyyy-MM-dd'T'HH:mm:ss[+|-]HH:mm` for other time zones. For details, see the ISO 8601 time stamp format.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"start_time": "2022-12-16T18:56:00.000Z"}`

##### Check box field

Captures Boolean values (`true` or `false`) for a condition.

**JSON schema:** `{ "key": "boolean"}`
**Example:** `{"patent_applied": true}`

##### Currency field

Captures currency values with the currency code, formatted amount, currency ID, and raw amount. Maximum length: 100 characters.

**JSON schema:** 
```
{ 
"currency": { 
"currency_code": "string", 
"formatted_amount": "string", 
"amount": "number (required)" 
}}
```
**Example:**
```
{ 
"cost_per_item": { 
"currency_code": "USD", 
"formatted_amount": "$ 5,353.54", 
"amount": 325.50 
}}
```
##### Percentage field

Captures percentage values as numbers. Maximum length: 20 characters.

**JSON schema:** `{ "key": "number"}`
**Example:** `{"completion_percentage": 10}`

##### Number field

Captures whole numbers. Maximum length: 19 digits.

**JSON schema:** `{ "key": "number"}`
**Example:** `{"tests_passed": 35 }`

##### Decimal field

Captures decimal values. Maximum length: 17 digits.

**JSON schema:** `{ "key": "number"}`
**Example:** `{"accuracy": 21.05}`

##### Email field

Captures email addresses. Maximum length: 200 characters.

**JSON Schema:** `{ "key": "string"}`
**Example:** `{"email":"chris@victa.com"}`

##### Phone number field

Captures phone numbers. Maximum length: 15 characters, including `+` and `()`.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"mobile":"1234567890"}`

##### URL field

Captures web links. If you don’t specify a protocol, the API uses `https://` by default. Maximum length: 200 characters.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"link":"https://projects.smartHive.com"}`

### Filter guide

Use the filter query parameter in SmartHive Projects v3 to retrieve only the records that match the conditions you define. This approach avoids fetching all records and filtering them on the client. This guide 
explains how to construct filter payloads, which conditions are available, and which value formats are supported.

**Filter example:**
```
{
  "criteria": [
    {
      "field_name": "name",
      "criteria_condition": "contains",
      "value": ["review"]
    }
  ],
  "pattern": "1"
}
```
**URL-encoded filter in GET request:**

`GET /api/v3/portal/{portal_id}/projects/{project_id}/tasks?filter=%7B%22criteria%22%3A%5B%7B%22field_name%22%3A%22name%22%2C%22criteria_condition%22%3A%22contains%22%2C%22value%22%3A%5B%22review%22%5D%7D%5D%2C%22pattern%22%3A%221%22%7D`

**Note**

- Pass the `filter` parameter as a URL-encoded JSON string.
- Combine one or more conditions by using a pattern expression.
- Status and date presets are currently supported only on specific modules. Support for other modules isn’t available yet.

#### Filter payload structure

The filter payload has two key components, `criteria` and `pattern`. Together, they define the conditions in a request and how those conditions are combined.

##### Payload Properties

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

| Property     | Data Type | Description |	
| :---        | :----  | :---- |
| `criteria`     | Array       | *required.*<br> The array of conditions. Each property of a condition represents a specific part of it and determines how the API interprets fields, operators, and values during filtering. |
| &emsp; criteria.`field_name`   | String        | *required.*<br> The API name of the field to filter, for example, `status`, `due_date`, or `name`. To get valid field names for a module, use the Get Field Info API.     |
| &emsp; criteria.`criteria_condition`  | String      | *required.*<br> The filter operation. The available conditions depend on the field type. See Conditions reference.   |
| &emsp; criteria.`value`   | Array<String>    | *optional.*<br> Required for most conditions. Always an array. Omit it for presets (`today`, `is_empty`). `between` requires exactly 2 values. |
| `pattern`   | String        | *required.*<br> The logic that combines the criteria by using `AND` and `OR`. Reference each criterion by its 1-based index in the array order, for example, `1` for the first criterion and `2` for the second. Example: `"(1 AND 2) OR 3"`      |

##### Pattern syntax

The `pattern` defines how the criteria are combined and evaluated together. Reference each condition by its position in the list, starting from 1, and use operators such as `AND` and `OR` to define the relationship between conditions. Use parentheses `()` to group conditions and control how they’re applied. The pattern is always required. When there’s only one condition, use `"1"`.

| Pattern     | Meaning |
| :---        | :----  |      
| `"1"`   | A single criterion.     |
| `"1 AND 2"`   | Both criteria must match. |
| `"1 OR 2"`   | Either criterion can match.     |
| `"1 AND 2 AND 3"`   | All three criteria must match.     |
| `"(1 AND 2) OR 3"`  | 	Criteria 1 and 2 both match, or criterion 3 matches.      |

**AND pattern**
```
{
  "criteria": [
    {
      "field_name": "assignee",
      "criteria_condition": "is",
      "value": ["4000000006061"]
    },
    {
      "field_name": "due_date",
      "criteria_condition": "is",
      "value": ["2026-12-31"]
    }
  ],
  "pattern": "1 AND 2"
}
```
**OR pattern**
```
{
  "criteria": [
    {
      "field_name": "priority",
      "criteria_condition": "is",
      "value": ["high"]
    },
    {
      "field_name": "milestone",
      "criteria_condition": "is_empty"
    }
  ],
  "pattern": "1 OR 2"
}
```
**Nested pattern**
```
{
  "criteria": [
    {
      "field_name": "priority",
      "criteria_condition": "is",
      "value": ["high"]
    },
    {
      "field_name": "due_date",
      "criteria_condition": "is",
      "value": ["2026-12-31"]
    },
    {
      "field_name": "assignee",
      "criteria_condition": "is",
      "value": ["4000000006061"]
    }
  ],
  "pattern": "(1 AND 2) OR 3"
}
```
##### Value format rules

The `value` field holds the input that the API uses to evaluate a condition. It’s always an array of strings. Most conditions require it, but presets don’t include a value. Range-based conditions such as 
`between` use exactly 2 values. The format varies by field type.

| Data Type     | Format | Example | Notes |
| :---        | :----  |      :---- | :---- |
| Text    | String     | `["review"]`  | A single value for most conditions. |
| Date (specific)   | `YYYY-MM-DD`       | `["2024-11-04"]`  | A single date value. |
| Date (range)  | `YYYY-MM-DD`       | `["2024-11-01", "2024-11-30"]`    | Exactly 2 values for `between` / `not_between` |
| User  | ZPUID      | `["4000000006061"]`   | A single value for most conditions. |
| Pick List  | Option name      | `["High"]`   | Use the display name, not the ID. |
| Multi Pick List  | Option ID      | `["4000000046001"]`   | Use the option ID, not the display name. |
| Check Box  | `"true"` or `"false"` or `"1"` or `"0"`      | `["true"]`   | Both formats are accepted. |
| Numeric  | Numeric string      | `["100"]`   | Pass numbers as strings. |

**Note**
- Only `is` and `is_not` support multiple values, for example, `["high", "medium"]`.
- `is` with multiple values uses **OR** logic and matches any value.
- `is_not` with multiple values uses **AND** logic and excludes all values.
- All other conditions accept a single value, or exactly 2 values for `between` and `not_between`.
- Preset conditions, such as `today` and `is_empty`, don’t require a value array.

#### Conditions reference

##### Text conditions

Use these conditions for text-based fields such as `name`, `email`, and custom fields, where matching is based on keywords or exact values. All comparisons are case-insensitive.

| Condition    | API Value | What it does | Value |
| :---        | :----  |      :---- | :---- |
| Contains    | `contains`     | Matches if the field contains the substring anywhere. | `["review"]` |
| Doesn't contain   | `not_contains`       | Excludes records that contain the substring.  | `["test"]` |
| Starts with  | `starts_with`       | Matches the beginning of the field value.   | `["API"]` |
| Ends with  | `ends_with`      | Matches the end of the field value.   | `[v2]` |
| Is  | `is`      | With multiple values, uses OR logic.  | `["High"]` or `["High", "Medium"]` |
| Is not  | `is_not`  | Excludes exact matches. With multiple values, uses AND logic.  | `["Low", "None"]` |

**Text: Contains**
```
{
  "criteria": [
    {
      "field_name": "name",
      "criteria_condition": "contains",
      "value": ["review"]
    }
  ],
  "pattern": "1"
}
```
**Multi-value IS**
```
{
  "criteria": [
    {
      "field_name": "waiting_for",
      "criteria_condition": "is",
      "value": ["frontend", "backend"]
    }
  ],
  "pattern": "1"
}
```
**Tip**
- `contains`, `not_contains`, `starts_with`, and `ends_with` accept only a single value. Only `is` and `is_not` support multiple values in the array.

##### Comparison Conditions

Use these conditions for numeric and date fields, where the API compares values by using operators such as greater than, less than, or within a range.

| Condition    | API Value | What it does | Value |
| :---        | :----  |      :---- | :---- |
| Is  | `is`      | Matches exactly. With multiple values, uses OR logic.  | `["100"]` or `["100", "200"]` |
| Is not  | `is_not`      | Excludes exact matches. With multiple values, uses AND logic.  | `["0"]` |
| Less than    | `less_than`     | The field value is less than the given value.  | `["50"]` |
| Less than or equal   | `less_than_or_equal`       | The field value is less than or equal to the given value.  | `["50"]` |
| Greater than  | `greater_than`       | The field value is greater than the given value.    | `["50"]` |
| Greater than or equal  | `greater_than_or_equal`      | The field value is greater than or equal to the given value.   | `["50"]` |
| Between    | `between`     | The field value is within the range (inclusive).  | `["10", "100"]` |
| Not between   | `not_between`       | The field value is outside the range.  | `["10", "100"]` |

**Date: Between**
```
{
  "criteria": [
    {
      "field_name": "start_date",
      "criteria_condition": "between",
      "value": ["2024-11-01", "2024-11-30"]
    }
  ],
  "pattern": "1"
}
```
**Numeric: Greater Than**
```
{
  "criteria": [
    {
      "field_name": "percentage_completion",
      "criteria_condition": "greater_than",
      "value": ["50"]
    }
  ],
  "pattern": "1"
}
```
**Tip**
- For date fields, use the `YYYY-MM-DD` format. Single value: `["2024-11-01"]`. Range: `["2024-11-01", "2024-11-30"]`.

##### User conditions

Use these conditions for fields related to users, including assignments, reporting structure, and user-specific states. These conditions require a ZPUID in the value array.

| Condition |	API value |	What it does |
| :---        | :----  |      :---- |
| Is |	`is` |	Matches records assigned to the given users. With multiple values, uses OR logic. |
| Is not |	`is_not` |	Excludes records assigned to the given users. |

**User: Is**
```
{
  "criteria": [
    {
      "field_name": "assignee",
      "criteria_condition": "is",
      "value": ["4000000006061"]
    }
  ],
  "pattern": "1"
}
```
**Overdue + Assigned to Me**
```
{
  "criteria": [
    {
      "field_name": "due_date",
      "criteria_condition": "is",
      "value": ["2026-12-31"]
    },
    {
      "field_name": "owner",
      "criteria_condition": "is",
      "value": ["4000000006061"]
    }
  ],
  "pattern": "1 AND 2"
}
```
##### Empty condition

Use this condition to find fields that don’t have a value.

| Condition |	Description |
| :---        | :----  |   
| `is_empty` |	The field has no value. |

**Tip:**
- Use this condition to find incomplete records, such as tasks with no due date or unassigned tasks.
- For date fields, use `unscheduled` instead of `is_empty` to filter records with no date set.

**Empty Field Check**
```
{
  "criteria": [
    {
      "field_name": "description",
      "criteria_condition": "is_empty"
    }
  ],
  "pattern": "1"
}
```
### Frequently used filters

This section provides ready-made filter payloads for common requests. Copy a payload, URL-encode it, and pass it as the `filter` query parameter.

#### Common filters

These filters work across modules such as tasks, issues, and custom modules.

##### Filter by open status

Returns all open tasks in a single request.

Use `status` with the `custom_condition` operator and the `${ALL_OPEN}` value.

**Filter by open status**
```
{
  "criteria": [
    {
      "field_name": "status",
      "criteria_condition": "custom_condition",
      "value": ["${ALL_OPEN}"]
    }
  ],
  "pattern": "1"
}
```
##### Filter by closed status

Returns all closed tasks in a single request.

Use `status` with the `custom_condition` operator and the `${ALL_CLOSED}` value.

**Filter by closed status**
```
{
  "criteria": [
    {
      "field_name": "status",
      "criteria_condition": "custom_condition",
      "value": ["${ALL_CLOSED}"]
    }
  ],
  "pattern": "1"
}
```
##### Filter by status

Returns tasks in a specific status.

Use `status` with the `is` condition and the status ID as the value.

**Filter by status**
```
{
  "criteria": [
    {
      "field_name": "status",
      "criteria_condition": "is",
      "value": ["268026000001877009"]
    }
  ],
  "pattern": "1"
}
```
##### Filter by Owner

Returns tasks owned by a specific user.

Use `owner` with the `is` condition and the user’s ZPUID as the value.

**Filter by owner**
```
{
  "criteria": [
    {
      "field_name": "owner",
      "criteria_condition": "is",
      "value": ["268026000002340076"]
    }
  ],
  "pattern": "1"
}
```
##### Filter by name

Returns tasks whose name contains the given text.

Use `name` with the `contains` condition and the search text as the value.

**Filter by name**
```
{
  "criteria": [
    {
      "field_name": "name",
      "criteria_condition": "contains",
      "value": ["test"]
    }
  ],
  "pattern": "1"
}
```
##### Filter by created time

Returns tasks created after a specific time.

Use `created_time` with the `greater_than` condition and a `YYYY-MM-DD` value.

**Filter by created time**
```
{
  "criteria": [
    {
      "field_name": "created_time",
      "criteria_condition": "greater_than",
      "value": ["2026-03-01"]
    }
  ],
  "pattern": "1"
}
```
##### Filter by last modified time

Returns tasks last updated after a specific date.

Use `last_updated_time` with the `greater_than` condition and a `YYYY-MM-DD` value.

**Filter by last modified time**
```
{
  "criteria": [
    {
      "field_name": "last_updated_time",
      "criteria_condition": "greater_than",
      "value": ["2026-03-01"]
    }
  ],
  "pattern": "1"
}
```
#### Task filters

These filters are available only in the Tasks module.

##### Filter by subtask

Returns only subtasks (tasks that have a parent task). 

Use `has_parents` with the value `true`. To return only top-level tasks, set the value to `false`. You can use `"true"` and `"false"`, or `"1"` and `"0"`.

**Filter by subtask**
```
{
  "criteria": [
    {
      "field_name": "has_parents",
      "criteria_condition": "is",
      "value": ["true"]
    }
  ],
  "pattern": "1"
}
```
##### Filter by parent task

Returns the subtasks of a specific parent task. 

Use `parent_task` with the `is` condition and the parent task ID as the value.

**Filter by parent task**
```
{
  "criteria": [
    {
      "field_name": "parent_task",
      "criteria_condition": "is",
      "value": ["268026000003251123"]
    }
  ],
  "pattern": "1"
}
```
##### Filter by task list

Returns tasks that belong to a task list whose name contains the given text. 

Set `module_name` to `tasklist` to filter on the related module’s `name` field.

**Filter by task list**
```
{
  "criteria": [
    {
      "module_name": "tasklist",
      "field_name": "name",
      "criteria_condition": "contains",
      "value": ["Codex"]
    }
  ],
  "pattern": "1"
}
```

## OAuth Authentication

### Overview

SmartHive Projects APIs use OAuth 2.0 for authentication. This page gives you an overview of the authentication process. 

For complete details on OAuth 2.0 flows, registration, token management, and more, refer to SmartHive OAuth 2.0 documentation.

### How it works

To access SmartHive Projects APIs, your application needs an **access token** obtained through one of the OAuth 2.0 flows. At a high level, the steps are:

1. Register your application in the SmartHive API console.
2. Get consent from user to access their data and obtain an access token.
3. Call SmartHive Projects APIs using the access token.

#### Token expiry

Access tokens expire periodically. The expiry duration is returned as `expires_in` (seconds) in the access token response.

To maintain uninterrupted access, you can request for an optional refresh token, store it, and use it to generate new access tokens as needed.

#### Token lifecycle

- Access tokens are required for every API request.
- Refresh tokens can be used to generate new access tokens without requiring user re-authorization.
- Users can revoke an application's access at any time, which invalidates the associated tokens.

For more details on token management, refer to SmartHive OAuth 2.0 documentation.

#### Different OAuth flows for different app types

SmartHive supports OAuth flows for different application types (server-based, client-based, and self client). You can choose the flow that matches your application.

For detailed information, refer to the OAuth documentation.

#### Multi DC support

SmartHive operates data centers in multiple regions. If your application serves users across regions, you must enable Multi DC support in the API console and use region-specific endpoints 
for both OAuth and SmartHive Projects API calls. See Multi-DC Support.

### Scopes

SmartHive Projects APIs require OAuth scopes to define the level of access your application needs. When requesting for access token, request only the scopes your application requires. 
These will be displayed to the users when asking for consent.

| Scope    | Description |
| :---        | :----  |      
| SmartHiveProjects.projects.READ    | Access project data (read-only)      |
| SmartHiveProjects.projects.ALL   | Full access to projects |
| SmartHiveProjects.tasks.ALL   | Full access to tasks     |
| SmartHiveProjects.timesheets.ALL   | Full access to time logs     |

To request multiple scopes, separate them with commas:

`scope=SmartHiveProjects.projects.READ,SmartHiveProjects.tasks.ALL`

For more details about scope format, see OAuth Scopes.

### Making API calls with access token

To authenticate your API calls, include the access token in the `Authorization` header of every API request with the prefix `Bearer`.

**Syntax:** `Authorization: Bearer {access-token-value}`

**Example:** `curl -X GET "https://projects.SmartHive.com/api/v3/portals" -H "Authorization: Bearer 1000.abc123def456..."`

#### Self-Client option

Use this method to generate the organization-specific grant token if your application does not have a domain and a redirect URL.
You can also use this option when your application is a standalone server-side application performing a back-end job.

1. Go to the **SmartHive Developer Console**, and then sign in with your SmartHive Projects username and password.
2. From the list of client types, select **Self Client**, and then select **Create Now**.
3. In the pop-up window, select **OK** to enable a self client for your account. Your client ID and client secret appear on the **Client Secret** tab.
3. Select the **Generate Code** tab.
4. In the **Scope** field, enter the required scopes, separated by commas. For a list of valid scopes, see Scopes.
	**Note:** If you enter one or more incorrect scopes, the system displays the error *“Enter a valid scope.”*
5. From the **Time Duration** field, select how long the grant token is valid.
	**Important:** The grant token expires after this time.
6. In the **Scope Description**, enter a description, and then select **Create**. The organization-specific grant token for the specified scopes appears.
7. Copy the grant token.

### API endpoints by data center

When making API calls, you must use the base URL corresponding to your user's data center. The access token response identifies the user's data center through the `location` and `api_domain` 
values - use it to pick the matching SmartHive Projects base URL from the table below.

| Data center   | API base URL |
| :---        | :----  |      
| United States (US)    | https://projects.smarthive.com      |
| European Union (EU)   | https://projects.smarthive.eu |
| India (IN)   | https://projects.smarthive.in     |
| Australia (AU)   | https://projects.smarthive.com.au     |
| Japan (JP)   | https://projects.smarthive.jp   |
| United Kingdom (UK)  | https://projects.smarthive.uk     |

**Important:** Never hardcode a single region's URL. Resolve the user's data center from the `location` / `api_domain` value in the access token response, then use the corresponding SmartHive Projects 
base URL from the table above. See Multi-DC Support.

### Related resources on OAuth

- Registering your app in API console
- OAuth glossary
- Token limits
- Incremental authorization

---

