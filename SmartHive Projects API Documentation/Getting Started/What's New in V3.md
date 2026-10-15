# What's new in v3

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
## Enhancements in the v3 API

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
## Consistent date and time Format

All date and time values follow a single ISO 8601 format across endpoints. This makes parsing consistent, so you don’t need to handle multiple formats.

| Type     | v2 | v3 |
| :---        | :----  |      :---- |
| Date only     | `"05-26-2014"` (MM-DD-YYYY)      | `"2024-05-26"` (YYYY-MM-DD)  |
| Datetime   | `"05-13-2014 05:57 PM"` (12-hour)        | `"2024-05-26T11:25:58.000Z"` (ISO 8601)     |
| Human-readable   | `"May 26, 2014"`     | **removed**      |
| Epoch   | `1399620397255`     | **removed**       |
| Date input format   | `MM-DD-YYYY`       | `YYYY-MM-DD`      |

The `*_long` epoch fields are removed because ISO 8601 timestamps are widely supported.

## Advanced filtering

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

## Standardized custom fields

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

## Request and response structure

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
## Pagination

Pagination is now page-based, which makes it easier to work with large datasets.

 - Use `page` and `per_page` to control the results.
 - The `has_next_page` parameter indicates whether more records are available.
 - Pagination avoids duplicate or skipped records.
 - You don’t need to calculate offsets manually.
 
For full details and examples, see Pagination.
 
## Base URL Structure
 
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

## Quick Comparison

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