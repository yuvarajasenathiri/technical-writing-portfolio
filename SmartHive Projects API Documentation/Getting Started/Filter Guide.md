# Filter Guide

The filter query parameter in SmartHive Projects v3 enables retrieving only records that match defined conditions. This approach avoids fetching all records and applying filtering on the client side. 
This guide explains how to construct filter payloads, available conditions, and supported value formats.

**Filter Example:**
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

**URL-Encoded Filter in GET Request:** 
`GET /api/v3/portal/{portal_id}/projects/{project_id}/tasks?filter=%7B%22criteria%22%3A%5B%7B%22field_name%22%3A%22name%22%2C%22criteria_condition%22%3A%22contains%22%2C%22value%22%3A%5B%22review%22%5D%7D%5D%2C%22pattern%22%3A%221%22%7D`

**Note**

- Pass the `filter` parameter as a URL-encoded JSON string
- Combine one or more conditions using a pattern expression
- Status and date presets are currently supported on specific modules only; support for the other modules will be provided soon.

## Filter Payload Structure

The filter payload is organized into key components that together represent how the conditions are defined and applied within a request : `criteria` and `pattern`.

### Payload Properties

| Property     | Data Type | Description |
| :---        | :----  |      :---- |
| criteria     | Array *required*      | Each property within the filter payload represents a specific part of a condition, contributing to how fields, operators, and values are interpreted during filtering.  |
| field_name   | String *required*        | API name of the field to filter (for example, `status`, `due_date`, `name`). Use the Get Field Info API to retrieve valid field names for a module.     |
| criteria_condition  | String *required*     | Filter operation. Available conditions depend on the field type.      |
| value   | Array<String> *optional*    | Required for most conditions. Always an array. Omit for presets (`today`, `is_empty`). `between` requires exactly 2 values.       |
| pattern   | String *required*       | Defines how criteria are combined using `AND` / `OR` logic. References criteria by their 1-based index in the array order (for example, first criterion = `1`, second = `2`). Example: `"(1 AND 2) OR 3"`.      |

### Pattern Syntax

The `pattern` shows how criteria are combined and evaluated together. Each condition is referenced by its position in the list (starting from 1), and operators like `AND`, `OR` are used to define the relationship between them. Parentheses `()` can be used to group conditions and control how they are applied. The pattern is always required, with `"1"` used when only a single condition is present.

| Pattern     | Meaning |
| :---        | :----  |      
| `"1"`   | Single criterion      |
| `"1 AND 2"`   | Both must match |
| `"1 OR 2"`   | Either can match     |
| `"1 AND 2 AND 3"`   | All three must match     |
| `"(1 AND 2) OR 3"`  | 	1 & 2 together, or 3 alone      |

**AND Pattern**

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

**OR Pattern**

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
**Nested Pattern**

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

### Value Format Rules

The `value` field represents the input used to evaluate a condition and is always structured as an array of strings. It is required for most conditions, while presets do not include a value. 
Range-based conditions such as `between` using exactly two values, and the format varies based on the field type.

| Data Type     | Format | Example | Notes |
| :---        | :----  |      :---- | :---- |
| Text    | String     | `["review"]`  | Single value for most conditions |
| Date (specific)   | `YYYY-MM-DD`       | `["2024-11-04"]`  | Single date value |
| Date (range)  | `YYYY-MM-DD`       | `["2024-11-01", "2024-11-30"]`    | Exactly 2 values for `between` / `not_between` |
| User  | ZPUID      | `["4000000006061"]`   | Single value for most conditions |
| Pick List  | Option name      | `["High"]`   | Use the display name, not the ID |
| Multi Pick List  | Option ID      | `["4000000046001"]`   | Use the option ID, not the display name |
| Check Box  | `"true"` / `"false"` or `"1"` / `"0"`      | `["true"]`   | Both formats accepted |
| Numeric  | Numeric string      | `["100"]`   | Numbers passed as strings |

**Note**

- Only `is` and `is_not` support multiple values (for example, `["high", "medium"]`).
- `is` with multiple values = **OR** logic (matches any).
- `is_not` with multiple values = **AND** logic (excludes all).
- All other conditions accept a single value (or exactly 2 for `between` / `not_between`).
- Preset conditions (`today`, `is_empty`, etc.) do not require a `value` array.