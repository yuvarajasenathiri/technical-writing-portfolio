# Get associated projects

Use this API to retrieve all projects associated with a specific user in a portal.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/users/[USER_ID]/projects`

**OAuth scope:** SmartHIveProjects.users.READ

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects. Get it from the Get All Portals with Details API (the `id` field in the response).|
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user. Get it from the Get Users API. The `id` field in the response is the `user_id`. |

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/users/[USER_ID]/projects?status=active&search_term=smarthive+Projects&page=1&per_page=10' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Query parameters**

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `status` |	String |	Optional | The status of the projects to retrieve.<br> Accepted values: `active` or `archived`. |
| `search_term` |	String | Optional |	A search term to filter the projects. |
| `page` |	Integer<br>Default: 1  | Optional |	The page number. |
| `per_page` |	Integer<br>Limit: 1 to 200. Default: 100 | Optional |	The number of entries to display on each page.|

**Sample input **
```
status : "active"
search_term : "SmartHive Projects"
page : "1"
per_page : "10"
```
**Sample response**
- 200 Ok
```
{
  "projects" : [ {
    "number" : 253,
    "is_owner" : false,
    "name" : "deal 2",
    "is_strict_project" : false,
    "id" : "103368000001263005",
    "status" : "active",
    "group" : {
      "prefix" : "",
      "name" : "zp.projset.ungroupproj",
      "id" : "103368000000025001",
      "is_default" : true,
      "type" : "public"
    }
  } ],
  "page_info" : {
    "per_page" : "100",
    "has_next_page" : "false",
    "page" : "1"
  }
}
```
**Possible Errors**
- RESOURCE_NOT_FOUND `HTTP 404`
```
{
  "error" : {
    "status_code" : "404",
    "instance" : "/api/v3/portal/45528313/users/4000000099999/projects",
    "method" : "GET",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Resource Not Found"
    } ],
    "title" : "RESOURCE_NOT_FOUND"
  }
}
```