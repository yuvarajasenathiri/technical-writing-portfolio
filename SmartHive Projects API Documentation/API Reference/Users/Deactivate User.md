# Deactivate a user

Deactivate a specific user in a portal. Use this API to revoke a user’s access to the portal without permanently removing the user’s account.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/users/[USER_ID]/deactivate`

**OAuth scope:** SmartHiveProjects.users.UPDATE

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects. Get it from the Get All Portals with Details API (the `id` field in the response).|
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user. Get it from the Get Users API. The `id` field in the response is the `user_id`. |

**Request example**
```
curl -X POST \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/users/[USER_ID]/deactivate' \
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
  "response" : "User Deactivated Successfully"
}
```
**Possible errors**
- UNAUTHORIZED_ACCESS `HTTP 401`
```
{
  "error" : {
    "status_code" : "401",
    "instance" : "/api/v3/portal/45528313/users/4000000012001/deactivate",
    "method" : "POST",
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
    "instance" : "/api/v3/portal/45528313/users/4000000012001/deactivate",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Users who have not accepted the portal invitation cannot be deleted or deactivated in your current plan."
    } ],
    "title" : "PAYMENT_REQUIRED"
  }
}
```
- DEACTIVATE_ERROR `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users/4000000012001/deactivate",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Error while deactivating user"
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
    "instance" : "/api/v3/portal/45528313/users/4000000099999/deactivate",
    "method" : "POST",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Resource Not Found"
    } ],
    "title" : "RESOURCE_NOT_FOUND"
  }
}
```