# Delete project user

Remove a specific user from a project. Use this API to revoke a user’s access to a project in a portal.

**Method and endpoint:** `DELETE /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]/users/[USER_ID]`

**OAuth scope:** SmartHiveProjects.users.DELETE

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the Get All Portals with Details API (the `id` field in the response).|
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal. <br> Get it from the Get All Projects API (the `id` field in the response). |
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user.<br> Get it from the Get Users API.<br>The `id` field in the response is the `user_id`. |

**Request example**
```
curl -X DELETE \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/projects/23806000097545166/users/[USER_ID]?notify=true' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Query parameters**
| Name | 	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `notify`	| String |	Required | Whether to notify the user.<br> Accepted values: `true` or `false`. |

**Sample input **
```
notify : "true"
```
**Sample response**
- 204 No content

**Possible errors**
- CANNOT_REMOVE_ADMIN_FROM_PROJECT `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/users/4000000012001",
    "method" : "DELETE",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Cannot remove admin/jointadmin from project"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- CANNOT_REMOVE_CRM_ASSPCIATED_USER `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/users/4000000012001",
    "method" : "DELETE",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Cannot remove CRM associated user from project"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- CANNOT_REMOVE_PROJECTOWNER_FROM_PROJECT `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/users/4000000012001",
    "method" : "DELETE",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Cannot remove project owner from project"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- ERROR_WHILE_DELETE_ADDED_VIA_TEAM `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/users/4000000012001",
    "method" : "DELETE",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Delete operation failed - User added via team"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- RESOURCE_NOT_FOUND `HTTP 404`
```
{
  "error" : {
    "status_code" : "404",
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/users/4000000099999",
    "method" : "DELETE",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Resource Not Found"
    } ],
    "title" : "RESOURCE_NOT_FOUND"
  }
}
```