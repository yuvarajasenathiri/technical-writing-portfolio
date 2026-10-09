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
} 
] 
}
```

**Example:** 

```
{ 
"parts_required": [ 
{ 
"add": [ "processor", "GPU" ],
"remove": ["POWER-CORD", "RAM" ]  
}
] 
}
```

## User Pick List Field

Allows selection of a single user.

**JSON Schema:** 

```
{ 
"key": { 
"zpuid": "user id" 
}
}
```
**Example:** 

```
{ "reporter": { 
"zpuid": "123454321" 
}
}
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
] 
}
```

**Example:** 
```
{ 
"user_group": [ 
{ "zpuid": "7845996622" },
{ "zpuid": "7876456433" } 
] 
}
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
}
] 
}
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
}
] 
}
```