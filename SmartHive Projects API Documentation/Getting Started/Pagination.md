# Pagination

v3 uses page-based pagination on all list endpoints. Pass `page` and `per_page` as query parameters to control which page of results is returned.

**Request:** `GET /api/v3/portal/{portal_id}/projects/{project_id}/tasks?page=2&per_page=50`

## Query Parameters

| Parameter     | Type | Description |
| :---        | :----  |      :---- |
| `page`    | Integer      | Page number (starting from 1). Defaults to 1 if omitted.  |
| `per_page`   | Integer        | Number of records per page. Defaults to 100 if omitted. Supported values: `1-200`.    |

**page_info Response**
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
## Response

Every list response includes a `page_info` block. The `has_next_page` flag tells your client precisely when to stop fetching — no offset calculations, no risk of duplicate or skipped records.

| Field     | Type | Description |
| :---        | :----  |      :---- |
| `page`    | Integer      | Current page number  |
| `per_page`   | Integer        | Records per page    |
| `page_count`   | Integer        | Total number of records in the result set    |
| `has_next_page`   | Boolean      | `true` if more pages exist, `false` if this is the last page   |