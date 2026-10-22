# Filter guide

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

## Filter payload structure

The filter payload has two key components, `criteria` and `pattern`. Together, they define the conditions in a request and how those conditions are combined.

### Payload Properties
| Property     | Data Type | Description |	
| `criteria`     | Array       | *required.*<br> The array of conditions. Each property of a condition represents a specific part of it and determines how the API interprets fields, operators, and values during filtering. |
| `field_name`   | String        | *required.*<br> The API name of the field to filter, for example, `status`, `due_date`, or `name`. To get valid field names for a module, use the Get Field Info API.     |
| `criteria_condition`  | String      | *required.*<br> The filter operation. The available conditions depend on the field type. See Conditions reference.   |
| `value`   | Array<String>    | *optional.*<br> Required for most conditions. Always an array. Omit it for presets (`today`, `is_empty`). `between` requires exactly 2 values. |
| `pattern`   | String        | *required.*<br> The logic that combines the criteria by using `AND` and `OR`. Reference each criterion by its 1-based index in the array order, for example, `1` for the first criterion and `2` for the second. Example: `"(1 AND 2) OR 3"`      |

### Pattern syntax

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
### Value format rules

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

## Conditions reference

### Text conditions

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

### Comparison Conditions

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

### User conditions

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
### Empty condition

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
## Frequently used filters

This section provides ready-made filter payloads for common requests. Copy a payload, URL-encode it, and pass it as the `filter` query parameter.

## Common filters

These filters work across modules such as tasks, issues, and custom modules.

### Filter by open status

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
### Filter by closed status

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
### Filter by status

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
### Filter by Owner

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
### Filter by name

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
### Filter by created time

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
### Filter by last modified time

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
## Task filters

These filters are available only in the Tasks module.

### Filter by subtask

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
### Filter by parent task

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
### Filter by task list

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


