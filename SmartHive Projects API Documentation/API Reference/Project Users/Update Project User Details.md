# Update project user details

Update the details of a specific user within a project using their ZPUID, ZUID, or email address.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]/users/[USER_ID]`

**OAuth scope:** SmartHiveProjects.users.UPDATE

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the Get All Portals with Details API (the `id` field in the response).|
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal. <br> Get it from the Get All Projects API (the `id` field in the response). |
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user.<br> Get it from the Get Users API.<br>The `id` field in the response is the `user_id`. |

**Request example**
```
curl -X POST \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/projects/23806000097545166/users/[USER_ID]' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa' \
 --form-string 'invoice=30.00' \
 --form-string 'costrate=15.00' \
 --form-string 'profile_id=2223806000000022149'
 ```
 
**Body parameters**
| Name	| Data type |	Required/Optional  | Description |
| :---        | :----  |  :----  |     :---- |	
| `invoice` |	String | Optional	| The invoice rate.<br> For example, $30 per hour. |
| `costrate` |	String	| Optional | The cost per hour.<br> For example, $15 per hour. |
| `profile_id` |	Integer |	Optional | The profile ID of the user.<br> Get it from the Get Profiles API (the id field in the response). |

**Sample input**
> *Content-Type: application/json
```
invoice : "30.00"
costrate : "15.00"
profile_id : "2223806000000022149"
```
**Sample response**
- 200 Ok
```
{
  "CURR_PROJID" : "4000000008005",
  "PROJOWNER" : "4000000002961",
  "ISOFFICEUSER" : false,
  "CURR_USERZUID" : "45524228",
  "CURR_USERZPUID" : "4000000002961",
  "USERLIST" : [ {
    "ISRESENDINVITE" : true,
    "PROFILE_ID" : "4000000003464",
    "DISPLAYNAME" : "Katya Cavendish",
    "business_hours" : {
      "name" : "Standard Business Hours",
      "id" : 4000000006095
    },
    "ZPUID" : "4000000016001",
    "COST_EFFECTIVE_DATE" : "12-18-2025",
    "ISGROUPUSER" : false,
    "INVOICE" : "55.00",
    "EMAIL" : "user@example.com",
    "ISACTIVE" : true,
    "ZPRole" : "Employee",
    "COST_PER_HOUR" : "22.00",
    "PROFILE_NAME" : "Employee",
    "last_updated_time" : 1766039954490,
    "role_id" : "4000000002967",
    "USER_BUDGET" : "0.000",
    "ISUSERCLOSED" : false,
    "ISFOLLWING" : false,
    "PROFILETYPE" : 7,
    "LOGINNAME" : 16027110,
    "REVENUE_BUDGET" : 0
  } ],
  "ACTIVEUSERCOUNT" : 2,
  "ISINVINTEG" : false,
  "INACTIVEUSERCOUNT" : 0,
  "ISPORTALOWNER" : true,
  "PROJSTAT" : "active",
  "ISADMIN" : true,
  "USERCNT" : {
    "Employee" : 1,
    "projusers" : 2,
    "Client" : 0,
    "Portal Owner" : 1
  },
  "CURR_ROLE" : "admin",
  "ISUPGRADE" : false,
  "ISCRMPLUSPORTAL" : false,
  "ISDEMOUSER" : false
}
```
**Possible errors**
- INVALID_PARAMETER_VALUE `HTTP 400`
```
{
  "error" : {
    "status_code" : "400",
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/users/4000000012001",
    "method" : "POST",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Invalid Parameter Value",
      "field_name" : "cost_effective_from_date"
    } ],
    "title" : "INVALID_PARAMETER_VALUE"
  }
}
```
- UNAUTHORIZED_ACCESS `HTTP 401`
```
{
  "error" : {
    "status_code" : "401",
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/users/4000000012001",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Unauthorized Access"
    } ],
    "title" : "UNAUTHORIZED_ACCESS"
  }
}
```
- RESOURCE_NOT_FOUND `HTTP 404`
```
{
  "error" : {
    "status_code" : "404",
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/users/4000000099999",
    "method" : "POST",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Resource Not Found"
    } ],
    "title" : "RESOURCE_NOT_FOUND"
  }
}
```
