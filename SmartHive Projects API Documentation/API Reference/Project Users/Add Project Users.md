# Add a project user

Add a user to a specific project. Use this API to grant a portal user access to a project.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]/projectusers`

**OAuth scope:** *SmartHiveProjects.users.CREATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the Get All Portals with Details API (the `id` field in the response).|
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal.<br>Get it from the Get All Projects API (the `id` field in the response). |

**Request example**
```
curl -X POST \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/projects/23806000097545166/projectusers' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa' \
 --form-string '
	userdetails=[{
		"email_id":"mark@victa.com",
		"profile_id":"2223806000000022149",
		"role_id":"8000000000991",
		"rate":"55.00",
		"cost_rate_per_hour":"200",
		"revenue_budget":"14.00",
		"cost_budget":"20.00",
		"budget_threshold":"10.00",
		"hourly_budget":"5.00",
		"hourly_budget_threshold":"3.00"
	}]' \
 --form-string 'notify=true'
```

**Body parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

| Name	| Data type |	Required/Optional  | Description |
| :---        | :----  |  :----  |     :---- |	
| `userdetails` |	JSONArray | Required |	The details of the users to add to the project. |
| &emsp; userdetails[].`email_id`	| String |   |	The email ID of the user. |
| &emsp; userdetails[].`profile_id`	| String |   |	The ID of the profile to assign to the user. |
| &emsp; userdetails[].`role_id`	| String|   |	The ID of the role to assign to the user. |
| &emsp; userdetails[].`rate`	| String	|   |The invoice rate of the user.<br> For example, $30 per hour. |
| &emsp; userdetails[].`cost_rate_per_hour`	| String|   | The cost per hour of the user. <br> For example, $20 per hour. |
| &emsp; userdetails[].`revenue_budget`	| String|   |	The revenue budget of the project.<br>For example, $10,000.|
| &emsp; userdetails[].`cost_budget`	| String|   |	The project cost. <br> For example, $8,000. |
| &emsp; userdetails[].`budget_threshold`	| String|   |	The project budget threshold. <br> For example, $10,000. |
| &emsp;userdetails[].`hourly_budget`	| String|   |	The hourly budget for the user. |
| &emsp; userdetails[].`hourly_budget_threshold`	| String|   |	The hourly budget threshold for the user.| 
| `notify`	| Boolean	|   | Whether to notify the users.<br> Accepted values: `true` or `false`.|

**Sample input**
> *Content-Type: application/json
```
userdetails : [ {
  "email_id" : "mark@victa.com",
  "profile_id" : "2223806000000022149",
  "role_id" : "8000000000991",
  "rate" : "55.00",
  "cost_rate_per_hour" : "200",
  "revenue_budget" : "14.00",
  "cost_budget" : "20.00",
  "budget_threshold" : "10.00",
  "hourly_budget" : "5.00",
  "hourly_budget_threshold" : "3.00"
} ]
notify : "true"
```
**Sample response**
- 201 Created
```
{
  "is_upgrade" : "false",
  "emailvszpuid" : {
    "monica.hemsworth@victa.com" : "103368000002484141"
  },
  "trouble_shoot" : "https://smarthive.com/projects/help/add-project-users.html#troubleshoot-tips",
  "success_emailId" : [ "\"monica.hemsworth@victa.com\"" ],
  "users" : [ {
    "is_viewer_follower" : false,
    "profile_type" : 8,
    "role" : "Administrator",
    "is_user_closed" : false,
    "loginname" : "69014231",
    "active" : 1,
    "reporting_to" : "Monica Hemsworth",
    "REPORTING_TO" : {
      "zpuid" : "103368000000048003",
      "full_name" : "Monica Hemsworth",
      "email" : "monica.hemsworth@victa.com",
      "zuid" : "66295825"
    },
    "is_resend_invite" : false,
    "role_name" : "Administrator",
    "profile_name" : "Contractor",
    "zpuid" : "103368000002484141",
    "last_updated_time" : 0,
    "role_id" : "103368000000048005",
    "profile_id" : "103368000000048364",
    "name" : "Monica",
    "is_user_confirmed" : false,
    "is_customized" : false,
    "is_group_user" : false,
    "id" : "69014231",
    "last_accessed_time" : "",
    "is_following" : false,
    "email" : "monica.hemsworth@victa.com",
    "budget" : {
      "revenue_budget" : "0.000",
      "budget_threshold" : "0.000",
      "cost_rate_per_hour" : "0.000"
    }
  } ],
  "is_portal_owner" : "true",
  "curr_projid" : "103368000001263005",
  "is_admin" : "true",
  "is_invoice_integ" : "true",
  "is_crmplus_plus" : "false",
  "user_count" : {
    "Contractor" : "82",
    "jointadmin" : "4",
    "New Profile" : "1",
    "admin" : "44",
    "portalusers" : "211",
    "Employee" : "20",
    "Manager" : "59",
    "Profile1" : "1"
  },
  "existing_Users" : [ {
    "emailId" : "monica.hemsworth@victa.com"
  } ],
  "success_zpuid" : [ "\"103368000002484141\"" ]
}
```
**Possible errors**
- UNAUTHORIZED_ACCESS `HTTP 401`
```
{
  "error" : {
    "status_code" : "401",
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/projectusers",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Unauthorized Access"
    } ],
    "title" : "UNAUTHORIZED_ACCESS"
  }
}
```
- USER_ALREADY_ADDED_IN_PROJECT `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/projectusers",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Existing user(s) of this project"
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
    "instance" : "/api/v3/portal/45528313/projects/4000000009003/projectusers",
    "method" : "POST",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Resource Not Found"
    } ],
    "title" : "RESOURCE_NOT_FOUND"
  }
}
```