# Field types

## Overview

SmartHive Projects supports several custom field types, such as text, numeric, URL, date, and time. The following sections describe the field types available in the Create and Update APIs.

**Note**

- Send all inputs as an input stream `(application/json)`.
- Use API names for custom fields.

## Single-line field

Captures text on a single line. Maximum length: 200 characters.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"title": "Project Ara"}`

## Multi-line field

Captures text on multiple lines. Use `\n` to separate lines. Maximum length: 1,000 characters.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"description": "The respective team\n is a prototype."}`

## Pick list field

Captures a single option selected from a predefined list. Maximum options: 50.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"Material": "Vinyl"}`

## Multi-select field

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

## User pick list field

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

## Multi-user field

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
## Date field

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
## Time field

Captures the time in `HH:MM` format.

**JSON schema:** `{ "key": "string"}`
**Example:** 
```
{
"start_time": "23:30",
"end_time": "13:30"
}
```
## Time stamp field

Captures a date and time in ISO 8601 format. Use `yyyy-MM-dd'T'HH:mm:ss'Z'` for UTC, or `yyyy-MM-dd'T'HH:mm:ss[+|-]HH:mm` for other time zones. For details, see the ISO 8601 time stamp format.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"start_time": "2022-12-16T18:56:00.000Z"}`

## Check box field

Captures Boolean values (`true` or `false`) for a condition.

**JSON schema:** `{ "key": "boolean"}`
**Example:** `{"patent_applied": true}`

## Currency field

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
## Percentage field

Captures percentage values as numbers. Maximum length: 20 characters.

**JSON schema:** `{ "key": "number"}`
**Example:** `{"completion_percentage": 10}`

## Number field

Captures whole numbers. Maximum length: 19 digits.

**JSON schema:** `{ "key": "number"}`
**Example:** `{"tests_passed": 35 }`

## Decimal field

Captures decimal values. Maximum length: 17 digits.

**JSON schema:** `{ "key": "number"}`
**Example:** `{"accuracy": 21.05}`

## Email field

Captures email addresses. Maximum length: 200 characters.

**JSON Schema:** `{ "key": "string"}`
**Example:** `{"email":"chris@victa.com"}`

## Phone number field

Captures phone numbers. Maximum length: 15 characters, including `+` and `()`.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"mobile":"1234567890"}`

## URL field

Captures web links. If you don’t specify a protocol, the API uses `https://` by default. Maximum length: 200 characters.

**JSON schema:** `{ "key": "string"}`
**Example:** `{"link":"https://projects.smartHive.com"}`
