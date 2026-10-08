# Getting Started

### Mandatory Headers

SmartHive Projects APIs require a mandatory header.

1. `Authorization`: The OAuth access token to authenticate the user accessing data.

**Example:**
```
curl -X GET https://projects.smarthive.com/api/v3/portal/{portal_id}/tasks  
-H "Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa"
```
	
## What's New in V3

Version-3 (V3) builds on the existing smarthive Projects API by introducing a more consistent structure across endpoints and extending support for common integration needs. 
Updates to areas like date formats, filtering, custom fields, and pagination make it easier to work with data in a predictable way. In this section, you'll find 
what's new in v3, what has been updated, and what to review when moving from v2.

**V3 API - Quick Example:**
```
GET /api/v3/portal/{portal_id}/projects
Authorization: Bearer {token}
```
```
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


