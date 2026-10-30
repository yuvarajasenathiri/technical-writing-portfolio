# Delete a user

Remove a specific user from a portal. Use this API to permanently revoke a user’s access to a portal.

**Method and endpoint:** `DELETE /api/v3/portal/[PORTAL_ID]/users/[USER_ID]`

**OAuth scope:** SmartHiveProjects.users.DELETE

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the Get All Portals with Details API (the `id` field in the response).|
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user.<br>Get it from the Get Users API.<br>The `id` field in the response is the `user_id`. |

**Request example**
```
curl -X DELETE \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/users/[USER_ID]?notify=true&reporting_manager=8000000002411&reporting_to=8000000002411' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Query parameters**
| Name | 	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `notify`	| String |	Required | Whether to notify the user.<br> Accepted values: `true` or `false`. |
| `reporting_manager` |	Integer | Optional | 	The reporting manager of the user. |
| `reporting_to` |	Integer |	Optional | The reporting manager of the user.<br>  Get it from the Get All Portals with Details API (the `id` field in the response). |

**Sample input **
```
notify : "true"
reporting_manager : "8000000002411"
reporting_to : "8000000002411"
```
**Sample response**
- 204 No content

**Possible errors**
- UNAUTHORIZED_ACCESS `HTTP 401`
```
{
  "error" : {
    "status_code" : "401",
    "instance" : "/api/v3/portal/45528313/users/4000000012001",
    "method" : "DELETE",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Unauthorized Access"
    } ],
    "title" : "UNAUTHORIZED_ACCESS"
  }
}
```
- CANNOT_UPDATE_UNCONFIRMED_USER `HTTP 402`
```
{
  "error" : {
    "status_code" : "402",
    "instance" : "/api/v3/portal/45528313/users/4000000012001",
    "method" : "DELETE",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Users who have not accepted the portal invitation cannot be deleted or deactivated in your current plan."
    } ],
    "title" : "PAYMENT_REQUIRED"
  }
}
```
- ERROR_WHILE_DELETE `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users/4000000012001",
    "method" : "DELETE",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Delete operation failed"
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
    "instance" : "/api/v3/portal/45528313/users/4000000012001",
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
    "instance" : "/api/v3/portal/45528313/users/4000000099999",
    "method" : "DELETE",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Resource Not Found"
    } ],
    "title" : "RESOURCE_NOT_FOUND"
  }
}
```
