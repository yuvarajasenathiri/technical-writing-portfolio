# Activate a user

Activate a specific user in a portal. Use this API to restore a deactivated user’s access to the portal.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/users/[USER_ID]/activate`

**OAuth scope:** SmartHiveProjects.users.UPDATE

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects. Get it from the Get All Portals with Details API (the `id` field in the response).|
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user. Get it from the Get Users API. The `id` field in the response is the `user_id`. |

**Request example**
```
curl -X POST \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/users/[USER_ID]/activate' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa' \
 --form-string 'notify=true'
```
**Query parameters**

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
|`notify` |	String |	Required | Whether to notify the user about the activation.<br> Accepted values: `true` or `false`. |

**Sample input **
```
notify : "true"
```
**Sample response**
- 200 Ok
```
{
  "response" : "User Activated Successfully"
}
```
**Possible errors**
- ACTIVATE_ERROR `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users/4000000012001/activate",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Error while activating user"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- USER_LIMIT_REACHED `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users/4000000012001/activate",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "User limit Reached"
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
    "instance" : "/api/v3/portal/45528313/users/4000000099999/activate",
    "method" : "POST",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Resource Not Found"
    } ],
    "title" : "RESOURCE_NOT_FOUND"
  }
}
```