# Pagination

The v3 API uses page-based pagination on all list endpoints. To control which page of results the API returns, pass `page` and `per_page` as query parameters.

**Request:** `GET /api/v3/portal/{portal_id}/projects/{project_id}/tasks?page=2&per_page=50`

## Query Parameters

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
## Response

Every list response includes a `page_info` object. The `has_next_page` field tells your client when to stop fetching. You don’t need to calculate offsets, and you avoid duplicate or skipped records.

| Field     | Type | Description |
| :---        | :----  |      :---- |
| `page`    | Integer      | The current page number.  |
| `per_page`   | Integer        | The number of records per page.    |
| `page_count`   | Integer        | The total number of records in the result set.   |
| `has_next_page`   | Boolean      | The value is `true` if more pages exist and `false` if the current page is the last page.   |