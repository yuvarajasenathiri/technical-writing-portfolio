# Add a user

Add a user to the SmartHive Projects portal. Use this API to invite a user to a portal and grant the user access.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/users`

**OAuth scope:** SmartHiveProjects.users.CREATE

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects. Get it from the Get All Portals with Details API (the `id` field in the response).|

**Request example**
```
curl -X POST \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/users' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa' \
 --form-string '
	userdetails=[{
		"email_id":"mark@victa.com",
		"email_template":"-",
		"role_id":"8000000000991",
		"profile_id":"2223806000000022149",
		"project_ids":["23806000074760021"],
		"bulk_projects":{
			"select_all":"false",
			"selected":{
				"group_ids":["2380600000612345"],
				"project_ids":["23806000074760021"]
				},
			"unselected":{
				"group_ids":["2380600000612345"],
				"project_ids":["23806000074760021"]
				},
			"rateupdatedprojects":"-",
			"costrateupdatedprojects":"-"
			},
		"rate":"55.00",
		"cost_rate_per_hour":"200",
		"revenue_budget":"14.00",
		"cost_budget":"20.00",
		"budget_threshold":"10.00",
		"include_projects":"8000000005863",
		"applyportalrate":"-",
		"reporting_manager":"-",
		"reporting_to":"8000000002411",
		"hourly_budget":"5.00",
		"hourly_budget_threshold":"3.00",
		"business_hours_id":"-"
		}]'
```
**Body parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

| Name	| Data type |	Required/Optional  | Description |
| :---        | :----  |  :----  |     :---- |	
| Name	| Data type | Required/Optional | 	Description |
| `userdetails`	| JSONArray| 	Required | The details of the users to add to the portal. |
| &emsp; userdetails[].`email_id` |	String |	| The email ID of the user. |
| &emsp; userdetails[].`email_template` |	Integer |	| The ID of the email template for the invitation email. |
| &emsp; userdetails[].`role_id`	| String | |	The ID of the role to assign to the user.|
| &emsp; userdetails[].`profile_id` |	String |	| The ID of the profile to assign to the user. |
| &emsp; userdetails[].`project_ids` |	JSONArray<br>*Maximum length: 600,000*<br>*Array size: 0 to 3,000* |	The IDs of the projects to assign to the user. |
| &emsp; userdetails[].`bulk_projects`	| JSONObject<br>*Maximum length: 200,000* |	The project assignment details for the user. |
| &emsp; &emsp; userdetails[].bulk_projects.`select_all` |	Boolean | 	| Whether to select all projects.<br> Accepted values: `true` or `false`. |
| &emsp; &emsp; userdetails[].bulk_projects.`selected` |	JSONObject<br>*Maximum length: 200,000* |	| The details of the projects to assign to the user. |
| &emsp; &emsp;&emsp; userdetails[].bulk_projects.selected.`group_ids` |	JSONArray<br> * Maximum length: 200,000*<br>*Array size: 0 to 10,000 |	|The IDs of the project groups to assign to the user.|
| &emsp; &emsp;&emsp; userdetails[].bulk_projects.selected.`project_ids` | 	JSONArray<br>*Maximum length: 200,000*<br>*Array size: 0 to 10,000* |	| The IDs of the projects to assign to the user. |
| &emsp;&emsp; userdetails[].bulk_projects.`unselected` | 	JSONObject<br>*Maximum length: 200,000* |	| The details of the projects to exclude from the user’s assignment. |
| &emsp;&emsp;&emsp;userdetails[].bulk_projects.unselected.`group_ids` | 	JSONArray<br>*Maximum length: 200,000*<br>*Array size: 0 to 10,000* |	| The IDs of the project groups to exclude from the user’s assignment. |
| &emsp;&emsp;&emsp; userdetails[].bulk_projects.unselected.`project_ids` |	JSONArray<br>*Maximum length: 200,000*<br>*Array size: 0 to 10,000* |	| The IDs of the projects to exclude from the user’s assignment. |
| &emsp;&emsp; userdetails[].bulk_projects.`rateupdatedprojects` |	JSONObject<br>*Maximum length: 200,000* |	| The projects and the user’s rate per hour in each project, in JSON format: `{"Project System ID":"Rate per hour"}`.<br> For example: `{"21446000000471005":"20","21446000000471111":"20"}`. |
| &emsp;&emsp; userdetails[].bulk_projects.`costrateupdatedprojects` |	JSONObject<br>*Maximum length: 200,000* |	| The projects and the user’s cost per hour in each project, in JSON format: `{"Project System ID":"Cost per hour"}`.<br> For example: `{"21446000000471005":"15","21446000000471111":"15"}`.|
| &emsp; userdetails[].`rate` |	String	| | The user’s rate per hour.<br> For example, $50 per hour. |
| &emsp; userdetails[].`cost_rate_per_hour` |	String	|   | The user’s cost per hour.<br> For example, $30 per hour.|
| &emsp; userdetails[].`revenue_budget`	| String |   | 	The revenue budget of the project.<br>For example, $10,000.|
| &emsp; userdetails[].`cost_budget`	| String |   | 	The project cost.<br> For example, $8,000.|
| &emsp; userdetails[].`budget_threshold`	 | String |   | 	The project budget threshold. <br> For example, $8,000.|
| &emsp; userdetails[].`include_projects`	 | String |   | 	The project details to include.|
| &emsp; userdetails[].`applyportalrate`	| String |   | 	The portal-level invoice rate of the user.|
| &emsp; userdetails[].`reporting_manager`	| Integer |   | 	The reporting manager.|
| &emsp; userdetails[].`reporting_to`	| Integer |   | 	The reporting manager.|
| &emsp; userdetails[].`hourly_budget`	| String	|   |  The hourly budget for the user.|
| &emsp; userdetails[].`hourly_budget_threshold`	| String |   | 	The hourly budget threshold for the user.|
| &emsp; userdetails[].`business_hours_id`	| String |   | 	The business hours ID of the user. |

**Sample input**
> *Content-Type: application/json
```
userdetails : [ {
  "email_id" : "mark@victa.com",
  "email_template" : "-",
  "role_id" : "8000000000991",
  "profile_id" : "2223806000000022149",
  "project_ids" : [ "23806000074760021" ],
  "bulk_projects" : {
    "select_all" : "false",
    "selected" : {
      "group_ids" : [ "2380600000612345" ],
      "project_ids" : [ "23806000074760021" ]
    },
    "unselected" : {
      "group_ids" : [ "2380600000612345" ],
      "project_ids" : [ "23806000074760021" ]
    },
    "rateupdatedprojects" : "-",
    "costrateupdatedprojects" : "-"
  },
  "rate" : "55.00",
  "cost_rate_per_hour" : "200",
  "revenue_budget" : "14.00",
  "cost_budget" : "20.00",
  "budget_threshold" : "10.00",
  "include_projects" : "8000000005863",
  "applyportalrate" : "-",
  "reporting_manager" : "-",
  "reporting_to" : "8000000002411",
  "hourly_budget" : "5.00",
  "hourly_budget_threshold" : "3.00",
  "business_hours_id" : "-"
} ]
```
**Sample response**
- 201 Created
```
{
  "is_upgrade" : "false",
  "emailvszpuid" : {
    "monica.hemsworth@victa.com" : "7000044352064"
  },
  "existing_users_list" : "[]",
  "active_user_count" : "10",
  "email_with_null_zuid" : [ "\"monica.hemsworth@victa.com\"" ],
  "deactivated_Users" : "[]",
  "trouble_shoot" : "https://smarthive.com/projects/help/add-project-users.html#troubleshoot-tips",
  "new_Users" : "[]",
  "success_emailId" : [ "\"monica.hemsworth@victa.com\"" ],
  "users" : [ {
    "is_viewer_follower" : false,
    "profile_type" : 6,
    "role" : "Manager",
    "is_user_closed" : false,
    "loginname" : "0",
    "active" : 1,
    "reporting_to" : "zp.general.none",
    "REPORTING_TO" : {
      "zpuid" : "7000000002623",
      "full_name" : "zp.general.none",
      "email" : "Any User",
      "zuid" : "-1"
    },
    "is_resend_invite" : false,
    "role_name" : "Manager",
    "profile_name" : "Manager",
    "zpuid" : "7000044352064",
    "last_updated_time" : 0,
    "role_id" : "7000000000991",
    "profile_id" : "7000000002347",
    "name" : "Monica Hemsworth",
    "is_user_confirmed" : false,
    "is_customized" : false,
    "is_group_user" : false,
    "id" : "0",
    "last_accessed_time" : "",
    "is_following" : false,
    "email" : "monica.hemsworth@victa.com"
  } ],
  "is_portal_owner" : "true",
  "remaining_user_count" : "990",
  "curr_projid" : "0",
  "is_invoice_integ" : "false",
  "is_admin" : "true",
  "is_crmplus_plus" : "false",
  "user_count" : {
    "Contractor" : "1",
    "Employee" : "6",
    "jointadmin" : "1",
    "admin" : "1",
    "portalusers" : "10",
    "Manager" : "1"
  },
  "existing_Users" : [ {
    "emailId" : "monica.hemsworth@victa.com"
  } ],
  "in_active_user_count" : "0",
  "success_zpuid" : [ "\"7000044352064\"" ]
}
```
**Possible errors**
- INPUT_PARAMETER_MISSING `HTTP 400`
```
{
  "error" : {
    "status_code" : "400",
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Input Parameter Missing",
      "field_name" : "email_id"
    } ],
    "title" : "INPUT_PARAMETER_MISSING"
  }
}
```
- INVALID_PARAMETER_VALUE `HTTP 401`
```
{
  "error" : {
    "status_code" : "400",
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Invalid Parameter Value",
      "field_name" : "email_id"
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
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Unauthorized Access"
    } ],
    "title" : "UNAUTHORIZED_ACCESS"
  }
}
```
- LITE_USER_LIMIT_REACHED ` HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Lite User limit Reached"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- READONLY_USER_LIMIT_REACHED `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Read-only User limit Reached"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- USER_ACCOUNT_NOT_CONFIRMED `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Please confirm your account before adding new users"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- USER_ADDED_IN_OTHER_DEPLOYMENT `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Email is already registered in another deployment/region. E.g., user registered in smarthive.eu cannot be added to smarthive.com region."
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- USER_ADD_GENERAL_ERROR `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Error Occured While Adding User"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- USER_ALREADY_ADDED_IN_ORG `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Existing user of this organization"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
- USER_INVALID_EMAIL `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Please enter a valid email address without any special characters."
    } ],
    "title" : "FORBIDDEN"
  }
}
- USER_INVITE_REJECTED `HTTP 403`
```
{
  "error" : {
    "status_code" : "403",
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Please enter a valid email address without any special characters."
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
    "instance" : "/api/v3/portal/45528313/users",
    "method" : "POST",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "User limit Reached"
    } ],
    "title" : "FORBIDDEN"
  }
}
```
