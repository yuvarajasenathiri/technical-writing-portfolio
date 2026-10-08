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

