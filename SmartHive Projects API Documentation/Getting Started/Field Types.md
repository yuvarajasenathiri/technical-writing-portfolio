# Field Types

SmartHive Projects supports various custom field types, such as text, numeric, URL, date, and time. Below are the field types available in the Create and Update APIs.

**Note**
- Send all inputs as an input stream (application/json).
- Use API names for custom fields.

## Single-Line Field

Captures text in a single line. Maximum length: 200 characters

**JSON Schema:** `{ "key": "string"}`
**Example:** `{"title": "Project Ara"}`

## Multi-Line Field

Captures text in multiple lines. Use "\n" to separate lines. Maximum length: 1,000 characters

**JSON Schema:** `{ "key": "string"}`
**Example:** `{"description": "The respective team\n is a prototype."}`

## Pick List Field

Allows selection of a single option from a predefined list. Maximum options: 50

**JSON Schema:** `{ "key": "string"}`
**Example:** `{"Material": "Vinyl"}`

## Multi-Select Field

Allows selection of multiple options from a predefined list. You can add or remove values dynamically, or replace the existing values. Maximum selectable options: 100

**Note**
- The add and remove options optimize the update process for Multi-Select fields, eliminating the additional GET call to retrieve existing values before updating.
- You can directly add or remove values in an Update API request or use the Create API format.

**Sample Input of Multi-Select Field in Create APIs:** `{ "key": [ "C", "D" ] }`
**Example:** `{ "parts_required": [ "HDD", "CD" ] }`

**Sample Input of Multi-Select Field in Create APIs:** 

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

## User Pick List Field

Allows selection of a single user.

**JSON Schema:** 

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

## Multi-User Field

Allows selection of multiple users from a predefined list. You can add or remove values dynamically, or replace the existing values. Maximum selectable users: 500

**Note**
- The add and remove options optimize the update process for Multi-User fields, eliminating the additional GET call to retrieve existing values before updating.
- You can directly add or remove values in an Update API request or use the Create API format.

**Sample Input of Multi-User Field in Create APIs:** 

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

**Sample Input of Multi-User Field in Create APIs:** 

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
] 
}]}
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
] 
}]}
```

## Date Field

Captures date in the yyyy-MM-dd format (ISO 8601).

**JSON Schema:** `{ "key": "string"}`
**Example:** 
```
{
"due_date": "2022-10-17",
"start_date":"2019-09-17",
"end_date": "2024-12-17"
}
```

## Time Field

Captures the time in HH:MM format.

**JSON Schema:** `{ "key": "string"}`
**Example:** 
```
{
"start_time": "23:30",
"end_time": "13:30"
}
```

## Time Stamp Field

Captures date and time in ISO 8601 format. Use yyyy-MM-dd'T'HH:mm:ss'Z' for UTC or yyyy-MM-dd'T'HH:mm:ss[+|-]HH:mm for other time zones. (ISO 8601 Time Stamp format).

**JSON Schema:** `{ "key": "string"}`
**Example:** `{"start_time": "2022-12-16T18:56:00.000Z"}`

## Check Box Field

Captures boolean values (true or false) for a condition.

**JSON Schema:** `{ "key": "boolean"}`
**Example:** `{"patent_applied": true}`

## Currency Field

Captures currency values with currency code, formatted amount, currency ID, and raw amount. Maximum length: 100 characters

**JSON Schema:** 
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

## Percentage Field

Captures percentage values as numbers. Maximum length: 20 characters

**JSON Schema:** `{ "key": "number"}`
**Example:** `{"completion_percentage": 10}`

## Number Field

Captures whole numbers. Maximum length: 19 digits

**JSON Schema:** `{ "key": "number"}`
**Example:** `{"tests_passed": 35 }`

## Decimal Field

Captures decimal values. Maximum length: 17 digits

**JSON Schema:** `{ "key": "number"}`
**Example:** `{"accuracy": 21.05}`

## Email Field

Captures email addresses. Maximum length: 200 characters

**JSON Schema:** `{ "key": "string"}`
**Example:** `{"email":"chris@zylker.com"}`

## Phone Number Field

Captures phone numbers (Maximum length: 15 characters, including + and ()).

**JSON Schema:** `{ "key": "string"}`
**Example:** `{"mobile":"1234567890"}`

## URL Field

Captures web links. If no protocol is specified, https:// is used by default. Maximum length: 200 characters

**JSON Schema:** `{ "key": "string"}`
**Example:** `{"link":"https://projects.smartHive.com"}`



