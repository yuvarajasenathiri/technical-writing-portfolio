# Getting Started

### Mandatory Headers

SmartHive Projects APIs require a mandatory header.

1. `Authorization`: The OAuth access token to authenticate the user accessing data.

**Example**
```
curl -X GET https://projects.smarthive.com/api/v3/portal/{portal_id}/tasks  
-H "Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa"
```
	
## What's New in V3

Version-3 (V3) builds on the existing smarthive Projects API by introducing a more consistent structure across endpoints and extending support for common integration needs. 
Updates to areas like date formats, filtering, custom fields, and pagination make it easier to work with data in a predictable way. In this section, you'll find 
what's new in v3, what has been updated, and what to review when moving from v2.

**V3 API - Quick Example**
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
### Enhancements in v3 API

V3 introduces a more consistent and structured way to work with the SmartHive Projects API. It simplifies how data is formatted, how requests are constructed, and how responses are handled, 
making integrations easier to build and maintain. These updates also bring more clarity when working with filters, custom fields, and large datasets.

**V3 Improvements at a Glance**
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
### Consistent Date and Time Format

All date and time values follow a single ISO 8601 format across endpoints. This ensures consistent parsing and removes the need to handle multiple formats.

| Type     | V2 | V3 |
| :---        | :----  |      :---- |
| Date only     | `"05-26-2014"` (MM-DD-YYYY)      | `"2024-05-26"` (YYYY-MM-DD)  |
| Datetime   | `"05-13-2014 05:57 PM"` (12-hour)        | `"2024-05-26T11:25:58.000Z"` (ISO 8601)     |
| Human-readable   | `"May 26, 2014"`     | **removed**      |
| Epoch   | `1399620397255`     | **removed**       |
| Date input format   | `MM-DD-YYYY`       | `YYYY-MM-DD`      |

The `*_long` epoch fields are removed. ISO 8601 timestamps are universally parseable.

### Advanced filtering

You can define multiple conditions within a single request using a structured filter object. Filtering is processed entirely on the server, so only relevant records are returned.

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
	
**Advanced Filter - Quick Example**
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

- **Pattern logic:** Combine conditions using `AND`, `OR`, and grouping - for example, `"(1 OR 2) AND 3"`
- **Custom field support:** Use the `api_name` of any custom field as the criteria `field_name`

For the complete syntax reference, see the Filter Guide.

### Standardized Custom fields

Custom fields now use clear and consistent api_name values. This makes it easier to reference them across requests, filters, and responses without additional mapping.

|      | V2 | V3 |
| :---        | :----  |      :---- |
| In requests     | `UDF_CHAR1`, `UDF_LONG2`      | `expected_date`, `priority_level` |
| In responses   | Same **UDF_** keys, no context      | Same **api_name**, consistent everywhere     |

**V3 Custom Field in Response**
```
{
  "expected_date": "2024-05-26"
}
```
**V3 Custom Field in Filter**
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


- **Stable references** - field identifiers don't shift when other fields are added or removed
- **Works everywhere** - same `api_name` in requests, responses, and filter criteria

For full details, see Custom Fields.

### Request and Response Structure

The same field structure is used in both requests and responses. This improves predictability and reduces the need for transformation logic when handling API data.

|  Aspect    | V2/restapi | V3/api/v3 |
| :---        | :----  |      :---- |
| Content Type     | *application/x-www-form-urlencoded*     | *application/json* |
| Body Style   | Flat, form-encoded parameters      | SJSON body, nested objects     |
| Dates   | Mixed formats (MM-DD-YYYY, epoch, text)     | ISO 8601 everywhere     |
| Related Data   | Flat fields *(person_responsible, assignee_name)*     | Grouped objects *(assignee, status)*    |
| List Responses   | No pagination metadata      | *page_info* block with *has_next_page*     |

**V3 Request (JSON)**
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
**V3 Response**
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

### Pagination

Pagination is now page-based, making it easier to work with large datasets.

 - Use page and per_page to control results
 - has_next_page indicates if more records are available
 - Avoids duplicate or skipped records
 - No need for manual offset calculations
 
 For full details and examples, see Pagination.
 
 ### Base URL Structure
 
 All endpoints in v3 follow a consistent URL pattern. The base URL is simplified and standardized, and trailing slashes are no longer required. This makes it easier to construct and predict endpoint URLs across the API.
 
|      | V2 | V3 |
| :---        | :----  |      :---- |
| Base URL    | */restapi/portal/{portal_id}/projects/*    | *api/v3/portal/{portal_id}/projects* |
| Trailing slashes   | Some endpoints require trailing `/`      | No trailing slashes     |

| Operation | V2 | V3 |
| :---        | :----  |      :---- |
| List tasks   | *GET /restapi/portal/{portal_id}/projects/{project_id}/tasks/*    | *GET api/v3/portal/{portal_id}/projects/{project_id}/tasks* |

**Note**

- If you're migrating from V2, update all endpoint URLs - the `/restapi/` prefix is replaced with `/api/v3/`.

### Quick Comparison

|  Area    | V2(/restapi) | V3(/api/v3) |
| :---        | :----  |      :---- |
| URL Pattern    | */restapi/portals/*    | */api/v3/portals* |
| Date Format   | `"05-26-2014"` or `"May 26, 2014"` or `1399620397255`     | `"2024-05-26"` (date only) or `"2024-05-26T11:25:58.000Z"` (ISO 8601)     |
| Pagination   | `index` + `range` (offset-based)   | `"page` + `per_page` with `has_next_page`     |
| HTTP Method for Updates  | POST   | PATCH     |
| Custom Fields  | `UDF_` prefix (for example, `UDF_CHAR1)` | `api_name` (for example, `"expected_date"`)    |
| Request / Response Schema  | Fields sent in requests often differed from response field names | Request and response use the same field structure throughout    |
| API Coverage | Limited modules and endpoints | Additional modules and endpoints, significantly expanding the overall API surface area   |

**V3 Update Task Example**
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