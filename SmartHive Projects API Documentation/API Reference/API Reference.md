# REST API references - SmartHive Projects

**Version:** 3.0  
**Last updated:** August 2026  
**Applies to:** SmartHive Projects API v3 
 
------

## Table of contents

1. [Portals](#portals)
   - [Get all portals with details](#get-all-portals-with-details)
   - [Get portal details](#get-portal-details)
2. [Users](#users)
   - [Add a user](#add-a-user)
   - [Activate a user](#activate-a-user)
   - [Deactivate a user](#deactivate-a-user)
   - [Delete a user](#delete-a-user)
   - [Get associated projects](#get-associated-projects)
   - [Get all portal users and contacts](#get-all-portal-users-and-contacts)
3. [Project users](#project-users)
   - [Get all users](#Get-all-users)
   - [Add a project user](#add-a-project-user)
   - [Update a project user details](#update-a-project-user-details)
   - [Delete a project user](#delete-a-project-user)
4. [Projects](#projects)
   - [Get all projects](#get-all-projects)
   - [Get a project details](#get-a-project-details)
   - [Create a project](#create-a-project)
   - [Update a project](#update-a-project)
   - [Trash a project](#trash-a-project)
   - [Restore a project](#restore-a-project)
   - [Delete a project](#delete-a-project)
5. [Profiles](#profiles)
   - [Get all portal profiles](#get-all-portal-profiles)
6. [Modules](#modules)
   - [Get Modules](#get-modules)
   - [Get Global Statuses](#get-global-statuses)
7. [Module layouts](#module-layouts)
   - [Get a layout list](#get-a-module-list)
8. [Project groups](#project-groups)
   - [Get a user’s project groups](#get-a-user’s-project-groups)
9. [Tags](#tags)
   - [Get all tags](#get-all-tags)
9. [Business hours](#business-hours)
   - [Get business hours](#get-business-hours)

--------

## Portals

This module handles portal-related operations in SmartHive Projects. Use the Portals API to create a portal, export portal data, manage portal settings, and get details such as portal license data 
and allowed features.

### Get all portals with details

Use this endpoint to retrieve all portals that the current user can access, along with their details. Each portal object includes metadata such as the company name, logo URL, time zone, and environment, 
and the plan information is grouped in the `plan_details object`.

**Method and endpoint:** `GET /api/v3/portals`

**OAuth scope:** *SmartHiveProjects.portals.READ*

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portals?status=active&environment=production' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Query parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
|`status` | String | Optional | The status of the portals to return. <br> Accepted values: `active` or `inactive`.<br> If you omit this parameter, the API returns portals of every status. |
|`environment` | String | Optional| The environment of the portals to return.<br> Accepted values: `sandbox` or `production`.<br> If you omit this parameter, the API returns portals from every environment. |

**Sample input**
```
status : "active"
environment : "production"
``` 
**Sample response**
- 200 Ok
```
{
  "portals" : [ {
    "id" : "26828068",
    "name" : "victaportal",
    "environment" : "production",
    "url" : "https://projects.smarthive.com/portal/victaportal",
    "logo_url" : "https://static.smarthivecdn.com/projects/images/svg/productlogo/zps-logo-default_9f9ca_.svg",
    "timezone" : "Europe/Dublin",
    "is_default_portal" : false,
    "company_name" : "victaportalsmarthivedotcom",
    "profile" : {
      "name" : "Portal Owner",
      "id" : "9000000002844"
    },
    "owner" : {
      "zuid" : 23163805,
      "zpuid" : "6000000002407",
      "name" : "Portal System",
      "first_name" : "Portal System",
      "last_name" : "",
      "full_name" : "Portal System",
      "email" : "admin@victa.com"
    },
    "plan_details" : {
      "project_plan" : "Enterprise",
      "bug_plan" : "Enterprise"
    }
  } ]
}
```
### Get portal details

Use this endpoint to retrieve details of a specific SmartHive Projects portal.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]`

**OAuth scope:** *SmartHiveProjects.portals.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
|`portal_id` | String<br>*digits only[0-9]+* | Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get all portals with details API](#get-all-portals-with-details) (the `id` field in the response). |

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Sample response**
- 200 Ok
```
{
  "portal_details" : {
    "owner" : {
      "zpuid" : "6000000002407",
      "full_name" : "Portal System",
      "name" : "Portal System",
      "last_name" : "",
      "id" : 23163805,
      "is_client_user" : false,
      "first_name" : "Portal System",
      "email" : "admin@victa.com"
    },
    "business_details" : {
      "start_time" : "00:00",
      "date_format" : "MM-dd-yyyy",
      "weekends" : [ ],
      "time_format" : "hh:mm aaa",
      "working_days" : [ "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" ],
      "week_start_day" : "SUNDAY",
      "end_time" : "24:00",
      "week_start_year" : "FIRST_DAY_OF_YEAR"
    },
    "logo_url" : "/images/svg/zps-logo-default.svg",
    "timezone" : "Europe/Dublin",
    "name" : "victa",
    "id" : 26828068,
    "plan_details" : {
      "projects_service_plan" : "Free",
      "bugtracker_service_plan" : "Free"
    },
    "org_name" : "victaportalsmarthivedotcom",
    "is_customdomain_enabled" : false
  }
}
```

----

## Users

This module covers user-related operations in SmartHive Projects. Use the Users API to manage portal users and resources. You can get user details, add or deactivate users, update user profiles, 
and view the projects a user is associated with.

### Add a user

Use this endpoint to add a user to the SmartHive Projects portal and to invite a user to a portal and grant the user access.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/users`

**OAuth scope:** *SmartHiveProjects.users.CREATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get all portals with details API](#get-all-portals-with-details) (the `id` field in the response).|

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
| `userdetails`	| JSONArray| 	Required | The details of the users to add to the portal. |
| &emsp; userdetails[].`email_id` |	String |	| The email ID of the user. |
| &emsp; userdetails[].`email_template` |	Integer |	| The ID of the email template for the invitation email. |
| &emsp; userdetails[].`role_id`	| String | |	The ID of the role to assign to the user.|
| &emsp; userdetails[].`profile_id` |	String |	| The ID of the profile to assign to the user. |
| &emsp; userdetails[].`project_ids` |	JSONArray<br>*Maximum length: 600,000*<br>*Array size: 0 to 3,000* |	| The IDs of the projects to assign to the user. |
| &emsp; userdetails[].`bulk_projects`	| JSONObject<br>*Maximum length: 200,000* |	| The project assignment details for the user. |
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
```
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

### Activate a user

Use this endpoint to activate a specific user in a portal and to restore a deactivated user’s access to the portal.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/users/[USER_ID]/activate`

**OAuth scope:** *SmartHiveProjects.users.UPDATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects. Get it from the [Get all portals with details API](#get-all-portals-with-details) (the `id` field in the response).|
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user. Get it from the [Get all portal users and contacts API](#get-all-portal-users-and-contacts). The `id` field in the response is the `user_id`. |

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

### Deactivate a user

Use this endpoint to deactivate a specific user in a portal and to revoke a user’s access to the portal without permanently removing the user’s account.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/users/[USER_ID]/deactivate`

**OAuth scope:** *SmartHiveProjects.users.UPDATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects. Get it from the [Get all portals with details API](#get-all-portals-with-details) (the `id` field in the response).|
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user. Get it from the [Get all portal users and contacts API](#get-all-portal-users-and-contacts). The `id` field in the response is the `user_id`. |

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

### Delete a user

Use this endpoint to remove a specific user from a portal and to permanently revoke a user’s access to a portal.

**Method and endpoint:** `DELETE /api/v3/portal/[PORTAL_ID]/users/[USER_ID]`

**OAuth scope:** *SmartHiveProjects.users.DELETE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get all portals with details API](#get-all-portals-with-details) (the `id` field in the response).|
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user.<br>Get it from the [Get all portal users and contacts API](#get-all-portal-users-and-contacts).<br>The `id` field in the response is the `user_id`. |

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
| `reporting_to` |	Integer |	Optional | The reporting manager of the user.<br>  Get it from the [Get all portal users and contacts API](#get-all-portal-users-and-contacts) (the `id` field in the response). |

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

### Get associated projects

Use this endpoint to retrieve all projects associated with a specific user in a portal.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/users/[USER_ID]/projects`

**OAuth scope:** *SmartHIveProjects.users.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br> Get it from the [Get all portals with details API](#get-all-portals-with-details) (the `id` field in the response).|
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user.<br> Get it from the [Get all portal users and contacts API](#get-all-portal-users-and-contacts).<br>The `id` field in the response is the `user_id`. |

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
**Possible errors**
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

### Get all portal users and contacts

Use this endpoint to retrieve all users and contacts in the SmartHive Projects portal.

**Method and endpoint:** `GET /api/v3.1/portal/[PORTAL_ID]/users`

**OAuth scope:** *SmartHiveProjects.users.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get all portals with details API](#get-all-portals-with-details) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3.1/portal/[PORTAL_ID]/users?type=portal_user&view_type=active&page=1&per_page=10&filter=%7B%22criteria%22%3A%5B%7B%22module%22%3A%22-%22%2C%22field_name%22%3A%22name%22%2C%22module_name%22%3A%22task%22%2C%22criteria_condition%22%3A%22contains%22%2C%22value%22%3A%5B%22Monica%22%5D%7D%5D%2C%22pattern%22%3A%221%22%7D&sort_by=ASC%28first_name%29' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `type`	| String | Optional |	The user type.<br> Accepted values: `portal_user`, `client_user`, or `client_contact`. |
| `view_type` |	String | Optional |	The view type.<br> Accepted values: `active`, `inactive`, `active_read_only`, `inactive_read_only`, `subordinates_active`, `direct_reporters_active`, `activate_user_request`, `sandboxdevelopers`, `inactive_lite_user`, or `active_lite_user`. |
| `page` |	Integer<br>Default: 1 |	Optional |The page number.|
| `per_page` |	Integer<br>Default: 100 | Optional	| The number of entries to display on each page. |
| filter |	JSONObject | Optional	| The filter criteria.|
| &emsp; filter.`criteria` | JSONArray<br>Maximum length: 10,000<br> Array size: 0 or greater |   | The criteria information.|
| &emsp; filter.`pattern` | String<br>Maximum length: 300 |   | The filter pattern.|
| `sort_by`	| String | Optional	| The sort criteria.<br> Accepted values: `ASC(field_name)` or `DESC(field_name)`.<br> Available fields: `first_name`, `last_name`, `portal_profile`, `role`, `rate_per_hour`, `cost_rate_per_hour`, `business_hours`, `added_time`, `updated_time`, `last_accessed_on`, and the `api_name` of a custom field. |

**Sample input**
```
type : "portal_user"
view_type : "active"
page : "1"
per_page : "10"
filter : {
  "criteria" : [ {
    "module" : "-",
    "field_name" : "name",
    "module_name" : "task",
    "criteria_condition" : "contains",
    "value" : [ "Monica" ]
  } ],
  "pattern" : "1"
}
sort_by : "ASC(first_name)"
```
**Sample response**
- 200 Ok
```
{
  "page_info" : {
    "per_page" : 50,
    "has_next_page" : false,
    "count" : 1,
    "page" : 1
  },
  "users" : [ {
    "business_hours" : {
      "name" : "Standard Business Hours",
      "id" : "4000000006095"
    },
    "updated_time" : "2025-11-27T12:14:38.609Z",
    "role" : {
      "name" : "Administrator",
      "id" : "4000000002963",
      "type" : 1
    },
    "added_time" : "2025-11-27T12:14:38.609Z",
    "is_confirmed" : true,
    "last_name" : "Cavendish",
    "reporting_to" : {
      "full_name" : "Monica Hemsworth",
      "last_name" : "Hemsworth",
      "id" : "4000000548001",
      "first_name" : "Monica",
      "zuid" : "66295825"
    },
    "zuid" : "45524228",
    "last_accessed_on" : "2026-06-12T11:43:18.605Z",
    "is_resend_invite" : false,
    "full_name" : "Katya Cavendish",
    "user_type" : "portal_user",
    "portal_profile" : {
      "name" : "Portal Owner",
      "id" : "4000000003455",
      "type" : "1",
      "is_default" : true
    },
    "id" : "4000000002961",
    "first_name" : "Katya",
    "email" : "katya.cavendish@victa.com",
    "status" : "active",
    "budget" : {
      "rate_per_hour" : {
        "amount" : 0,
        "formatted_amount" : "$ 0.00",
        "currency_code" : "USD",
        "currency_id" : "4000000082030"
      },
      "cost_rate_per_hour" : {
        "amount" : 0,
        "formatted_amount" : "$ 0.00",
        "currency_code" : "USD",
        "currency_id" : "4000000082030"
      }
    }
  } ]
}
```
**Possible errors**
- INTERNAL_SERVER_ERROR `HTTP 500`
```
{
  "error" : {
    "status_code" : "500",
    "instance" : "/api/v3.1/portal/45528313/users",
    "method" : "GET",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Internal server error. Please contact support@smarthiveprojects.com for further details.",
      "message_key" : "zp.general.error"
    } ],
    "title" : "INTERNAL_SERVER_ERROR"
  }
}
```
-----

## Project users

This module covers operations related to project users in SmartHive Projects. Use the Project Users API to get, add, and delete users associated with a project. You can also view specific user details in 
the context of a project.

### Get all users

Use this endpoint to retrieve all users in a project.

**Method and endpoint:** `GET /api/v3.1/portal/[PORTAL_ID]/projects/[PROJECT_ID]/users`

**OAuth scope:** *SmartHiveProjects.users.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br> Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response).| 
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal.<br> Get it from the [Get all projects API](#get-all-projects) (the `id` field in the response). |

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3.1/portal/[PORTAL_ID]/projects/23806000097545166/users?type=portal_user&view_type=active&page=1&per_page=10&filter=%7B%22criteria%22%3A%5B%7B%22module%22%3A%22-%22%2C%22field_name%22%3A%22name%22%2C%22module_name%22%3A%22task%22%2C%22criteria_condition%22%3A%22contains%22%2C%22value%22%3A%5B%22Monica%22%5D%7D%5D%2C%22pattern%22%3A%221%22%7D&sort_by=ASC%28first_name%29' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `type`	| String	| Optional | The user type.<br> Accepted values: `portal_user`, `client_user`, or `client_contact`. |
| `view_type`	| String| Optional |	The view type.<br> Accepted values: `active`, `inactive`, `active_read_only`, `inactive_read_only`, `subordinates_active`, `direct_reporters_active`, `activate_user_request`, `sandboxdevelopers`, `inactive_lite_user`, `active_lite_user`, or `project_viewers_active`. |
| `page` |	Integer<br>*Default: 1* |	Optional | The page number. |
| `per_page` |	Integer<br>*Default: 100* | Optional |	The number of entries to display on each page. |
| `filter` |	JSONObject | Optional |	The filter criteria. |
| &emsp; filter.`criteria` | 	JSONArray<br>*Maximum length: 10,000*<br>*Array size: 0 or greater* |	| The criteria information.
| &emsp;&emsp; filter.criteria.`module` | String | | The field module. |
| &emsp;&emsp; filter.criteria.`field_name` | String | | The field name. |
| &emsp;&emsp; filter.criteria.`module_name` | String | | The module name. |
| &emsp;&emsp; filter.criteria.`criteria_condition` | String<br>*Maximum length: 25* |  | The criteria condition.|
| &emsp;&emsp; filter.criteria.`value`| JSONArray<br>* Maximum length: 10,000*<br>*Array size: 0 or greater*	| | The criteria value. |
| &emsp; filter.`pattern` |	String<br>* Maximum length: 300* |	| The filter pattern.|
|`sort_by`	|String | Optional	| The sort criteria.<br> Accepted values: `ASC(field_name)` or `DESC(field_name)`.<br> Available fields: `first_name`, `last_name`, `portal_profile`, `role`, `project_rate`, `project_cost_rate`, `business_hours`, `added_to_project_time`, `updated_in_project_time`, and `last_accessed_on`. |

**Sample input**
```
type : "portal_user"
view_type : "active"
page : "1"
per_page : "10"
filter : {
  "criteria" : [ {
    "module" : "-",
    "field_name" : "name",
    "module_name" : "task",
    "criteria_condition" : "contains",
    "value" : [ "Monica" ]
  } ],
  "pattern" : "1"
}
sort_by : "ASC(first_name)"
```
**Sample response**
- 200 Ok
```
{
  "page_info" : {
    "per_page" : 50,
    "has_next_page" : false,
    "count" : 1,
    "page" : 1
  },
  "users" : [ {
    "business_hours" : {
      "name" : "Standard Business Hours",
      "id" : "4000000006095"
    },
    "project_profile" : {
      "name" : "Portal Owner",
      "is_customized" : false,
      "id" : "4000000003455",
      "type" : "1"
    },
    "updated_in_project_time" : "2026-06-16T05:59:04.588Z",
    "role" : {
      "name" : "Administrator",
      "id" : "4000000002963",
      "type" : 1
    },
    "added_to_project_time" : "2026-06-16T05:59:04.588Z",
    "is_confirmed" : true,
    "last_name" : "Cavendish",
    "reporting_to" : {
      "full_name" : "Monica Hemsworth",
      "last_name" : "Hemsworth",
      "id" : "4000000548001",
      "first_name" : "Monica",
      "zuid" : "66295825"
    },
    "zuid" : "45524228",
    "last_accessed_on" : "2026-06-16T14:39:49.390Z",
    "is_resend_invite" : false,
    "full_name" : "Katya Cavendish",
    "user_type" : "portal_user",
    "portal_profile" : {
      "name" : "Portal Owner",
      "id" : "4000000003455",
      "type" : "1",
      "is_default" : true
    },
    "id" : "4000000002961",
    "first_name" : "Katya",
    "email" : "katya.cavendish@victa.com",
    "status" : "active",
    "budget" : {
      "project_rate" : {
        "amount" : 0,
        "formatted_amount" : "$ 0.00",
        "currency_code" : "USD",
        "currency_id" : "4000000082030"
      },
      "hourly_budget" : "0:00"
    }
  } ]
}
```

### Add a project user

Use this endpoint to add a user to a specific project and to grant a portal user access to a project.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]/projectusers`

**OAuth scope:** *SmartHiveProjects.users.CREATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get all portals with details API](#get-all-portals-with-details) (the `id` field in the response).|
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal.<br>Get it from the [Get all projects API](#get-all-projects) (the `id` field in the response). |

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
| `notify`	| Boolean	| Required  | Whether to notify the users.<br> Accepted values: `true` or `false`.|

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

### Update a project user details

Use this endpoint to modify the details of a specific user within a project using their ZPUID, ZUID, or email address.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]/users/[USER_ID]`

**OAuth scope:** *SmartHiveProjects.users.UPDATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get all portals with details API](#get-all-portals-with-details) (the `id` field in the response).|
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal. <br> Get it from the [Get all projects API](#get-all-projects) (the `id` field in the response). |
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user.<br> Get it from the [Get all portal users and contacts API](#get-all-portal-users-and-contacts).<br>The `id` field in the response is the `user_id`. |

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
| `profile_id` |	Integer |	Optional | The profile ID of the user.<br> Get it from the [Get all portal profiles API](#get-all-portal-profiles) (the `id` field in the response). |

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

### Delete a project user

Use this endpoint to remove a specific user from a project and to revoke a user’s access to a project in a portal.

**Method and endpoint:** `DELETE /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]/users/[USER_ID]`

**OAuth scope:** *SmartHiveProjects.users.DELETE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get all portals with details API](#get-all-portals-with-details) (the `id` field in the response).|
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal. <br> Get it from the [Get all projects API](#get-all-projects) (the `id` field in the response). |
| `user_id`| String<br>digits only ([0-9]+ | Required | The ID of the user.<br> Get it from the [Get all portal users and contacts API](#get-all-portal-users-and-contacts).<br>The `id` field in the response is the `user_id`. |

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
------

## Projects

This module covers project-related operations in SmartHive Projects. Use the Projects API to get project activity, view or update project edits, get recent projects, and manage issues and tasks.

### Get all projects

Use this end point to retrieve the list of all projects in the SmartHive Projects portal.

**Method and endpoint:** `GET /api/v3/portal/[PORTALID]/projects`

**OAuth scope:** *SmartHiveProjects.projects.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
|`portal_id` | String<br>*digits only[0-9]+* | Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response). |

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/739121528/projects?page=1&per_page=10&%22filter%22=%7B%22criteria%22%3A%5B%7B%22cfid%22%3A%224000000000242%22%2C%22field_name%22%3A%22project%22%2C%22criteria_condition%22%3A%22contains%22%2C%22value%22%3A%5B%221752587000000097269%22%5D%2C%22relative_columns%22%3A%5B%7B%22cfid%22%3A%224000000000242%22%2C%22field_name%22%3A%22project%22%2C%22offset%22%3A%221%22%2C%22unit%22%3A%22days%22%2C%22prior%22%3A%22before%22%7D%5D%7D%5D%2C%22pattern%22%3A%221+AND+2%22%7D&sort_by=ASC%28last_modified_time%29&view_id=23806000074760021' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

| Name |	Data type | Required/Optional|	Description |
| :---        | :----  |  :----  |     :---- |
| `page` |	Integer<br>*default 1* | Optional |	The page number. |
| `per_page` |	Integer<br> *limit 1-200* <br> *default 100* | Optional |	The number of entries to display on each page. |
| `filter` |	JSONObject | Optional |	The filter criteria for retrieving specific projects.<br>The filter is a JSON object that contains a list of conditions (`criteria`) and a logical `pattern` that defines how the conditions are combined.|
| `criteria` |	JSONArray <br>*Maximum length: 10,000.* <br> *Array size: 0 or greater.* | Optional | A list of filter conditions.<br> Each condition specifies a field, a condition type, and a value to match. You can combine multiple conditions by using the pattern property, which references each condition by its position, starting from 1. |
| `pattern` |	String <br> *Maximum length: 300.* | Optional | The logical expression that defines how the criteria are combined. <br> Use condition numbers (starting from 1) with the `AND` and `OR` operators and parentheses for grouping. For example, use `1` for a single condition, `1` AND `2` for both conditions, `1` OR `2` for either condition, and `(1 OR 2) AND 3` for grouped logic.|
| `sort_by`	| String	| Optional | The sort order for the results.<br>Wrap the field API name in `ASC()` for ascending order or `DESC()` for descending order. For example, `ASC(start_date)` sorts by start date in ascending order, and `DESC(created_time)` sorts by creation time in descending order. |
| `view_id` |	String | Optional | The ID of a saved custom view to apply.<br>When you include it, the API applies the saved view’s filter criteria, columns, and sort order. <br>If you also include a `filter`, the API combines the filter conditions (AND) with the custom view’s criteria.  |

**Sample input**
```
page : "1"
per_page : "10"
"filter" : {
  "criteria" : [ {
    "cfid" : "4000000000242",
    "field_name" : "project",
    "criteria_condition" : "contains",
    "value" : [ "1752587000000097269" ],
    "relative_columns" : [ {
      "cfid" : "4000000000242",
      "field_name" : "project",
      "offset" : "1",
      "unit" : "days",
      "prior" : "before"
    } ]
  } ],
  "pattern" : "1 AND 2"
}
sort_by : "ASC(last_modified_time)"
view_id : "23806000074760021"
```

**Sample response**
 - 200 Ok
```
[ {
  "id" : "7000000082003",
  "name" : "Website Redesign",
  "key" : "54",
  "description" : "Redesign the company website with new branding",
  "project_type" : "active",
  "start_date" : "2024-09-30",
  "end_date" : "2025-06-30",
  "is_public_project" : "false",
  "is_strict_project" : "false",
  "is_rollup_project" : "false",
  "is_completed" : "false",
  "is_linked_project" : "false",
  "percent_complete" : 45,
  "color" : "#4573d2",
  "comments_count" : 12,
  "owner" : {
    "id" : "6000000002069",
    "zpuid" : "7000000002083",
    "name" : "John Doe",
    "email" : "john@victa.com"
  },
  "status" : {
    "id" : "7000000000361",
    "name" : "In Progress",
    "color" : "green",
    "color_hexcode" : "#3cb371",
    "is_closed_type" : "false",
    "is_default" : "false"
  },
  "layout" : {
    "id" : "7000000000305",
    "name" : "Standard Layout",
    "is_default" : "true",
    "type" : "public"
  },
  "tasks" : {
    "open_count" : 15,
    "closed_count" : 10
  },
  "issues" : {
    "open_count" : 5,
    "closed_count" : 3
  },
  "milestones" : {
    "open_count" : 2,
    "closed_count" : 1
  },
  "created_by" : {
    "id" : "6000000002069",
    "zpuid" : "7000000002083",
    "name" : "John Doe",
    "email" : "john@victa.com"
  },
  "created_time" : "2024-09-30T10:30:00.000Z",
  "updated_by" : {
    "id" : "6000000002069",
    "zpuid" : "7000000002083",
    "name" : "John Doe",
    "email" : "john@victa.com"
  },
  "modified_time" : "2025-01-15T14:20:00.000Z"
} ]
```
**Possible errors**
- Internal_Server_Error `HTTP 500`
```
{
  "error" : {
    "status_code" : "500",
    "instance" : "/api/v3/portal/45528313/projects",
    "method" : "GET",
    "error_type" : "OPERATIONAL_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Internal server error. Please contact support@smarthiveprojects.com for further details.",
      "message_key" : "zp.general.error"
    } ],
    "title" : "INTERNAL_SERVER_ERROR"
  }
}
```

### Get a project details

Use this endpoint to retrieve a project details in the SmartHive Projects portal.

**Method and endpoint:** `GET /api/v3/portal/[PORTALID]/projects/[PROJECTID]`

**OAuth scope:** *SmartHiveProjects.projects.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
|`portal_id` | String<br>*digits only[0-9]+* | Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response). |
|`project_id` | String<br>*digits only[0-9]+* | Required | The unique, immutable identifier of the project in the sepcified portal.<br>Get it from the [Get all projects API](#get-all-projects) (the `id` field in the response). |

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/739121528/projects/1752587000000097024' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Sample response**
- 200 Ok
 ```
 {
  "end_date" : "2029-01-01",
  "picklist_11sep" : "abc",
  "is_public_project" : "false",
  "description" : "source project  for testing clone project",
  "is_strict_project" : "false",
  "multiline_11sep" : "multiline \nMULTILINE",
  "budget_info" : {
    "hourly_budget" : "1200:00",
    "billing_method" : "project_hours",
    "forecasted_cost" : {
      "amount" : 0.0,
      "formatted_amount" : "$ 0.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "planned_hours" : "00:00",
    "bcy_forecasted_cost" : {
      "amount" : 0.0,
      "formatted_amount" : "$ 0.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "forecasted_hours" : "00:00",
    "remaining_hours" : "00:00",
    "actual_cost" : {
      "amount" : 0.0,
      "formatted_amount" : "$ 0.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "actual_hours" : "00:00",
    "bcy_planned_cost" : {
      "amount" : 0.0,
      "formatted_amount" : "$ 0.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "planned_cost" : {
      "amount" : 0.0,
      "formatted_amount" : "$ 0.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "budget_type" : "based_on_project",
    "bcy_actual_cost" : {
      "amount" : 0.0,
      "formatted_amount" : "$ 0.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "cost_budget" : {
      "amount" : "10000000",
      "formatted_amount" : "$ 1,00,00,000.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    }
  },
  "issues" : {
    "closed_count" : 0,
    "open_count" : 0
  },
  "is_completed" : "false",
  "id" : "7000000010005",
  "key" : "5",
  "tasks" : {
    "closed_count" : 0,
    "open_count" : 5
  },
  "number_11sep" : "1212",
  "start_date" : "2024-09-30",
  "phone_11sep" : "9879879877",
  "project_type" : "active",
  "created_time" : "2024-09-02T08:04:09.657Z",
  "check_box_sample_11sep" : "true",
  "is_rollup_project" : "true",
  "one" : "123456_single",
  "created_by" : {
    "zpuid" : "7000000002411",
    "name" : "Daniel",
    "last_name" : "Cooper",
    "first_name" : "Daniel",
    "zuid" : "25450833"
  },
  "percent_complete" : "0",
  "tags" : [ {
    "id" : "7000000015084",
    "color_hexcode" : "#7dcf7b"
  } ],
  "layout" : {
    "name" : "Standard Layout",
    "id" : "7000000000506",
    "is_default" : "true",
    "type" : "public"
  },
  "completed_time" : "1767099600000",
  "single_line_test_1446" : "singleline",
  "name" : "SourceP",
  "updated_by" : {
    "zpuid" : "7000000002411",
    "name" : "Daniel",
    "last_name" : "Cooper",
    "first_name" : "Daniel",
    "zuid" : "25450833"
  },
  "project_group" : {
    "name" : "zp.projset.ungroupproj",
    "id" : "7000000005369",
    "type" : "public"
  },
  "milestones" : {
    "closed_count" : 0,
    "open_count" : 0
  },
  "status" : {
    "is_closed_type" : "false",
    "name" : "Active",
    "id" : "7000000000665"
  }
}
```

### Create a project

Use this endpoint to create a project in the SmartHive Projects portal.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/projects`

**OAuth scope:** *SmartHiveProjects.projects.CREATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br> Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response).| 

**Request example**
```
curl -X POST \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/projects' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa' \
 -H 'Content-Type: application/json' \
 -d '
 {
	"name":"Website Redesign",
	"description":"Redesign the company website with new branding",
	"project_type":"active",
	"owner":{
		"zpuid":"4000000002055"
		},
	"is_public_project":false,
	"start_date":"2023-12-20",
	"end_date":"2024-12-20",
	"status":{
		"id":"4000000062001"
		},
	"layout":{
		"id":"4000000062001"
		},
	"added_via":"api",
	"is_rollup_project":false,
	"budget_info":{
		"billing_method":"project_hours",
		"budget_type":"based_on_project",
		"tracking_method":"project_hours",
		"currency":"USD",
		"cost_budget":{
			"amount":50000.0
			},
		"hourly_budget":"30:00",
		"rate_per_hour":{
			"amount":945.25
			},
		"cost_budget_threshold":{
			"amount":50000.0
			},
		"hourly_budget_threshold":"20:00",
		"fixed_cost":{
			"amount":50000.0
			},
		"cost_per_hour":{
			"amount":510.75
			},
		"revenue_budget":{
			"amount":50000.0
			}
		},
	"project_group":{
		"id":"4000000062001"
		},
	"tags":[{
		"add":[{
			"id":"4000000062001"
			}],
		"remove":[{
			"id":"4000000062001"
			}],
		"id":"4000000062001"
		}],
	"business_hours_id":"7000000197013"
 }'
 ```
**Body parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

| Name	| Data type |	Required/Optional  | Description |
| :---        | :----  |  :----  |     :---- |
| `name` |	String<br> *Maximum length: 200*|	Required | The project name. |
| `description` |	String<br>*Maximum length: 80,000* | Optional |	The project description. | 
| `project_type` |	String | Optional |	The project type.<br> Accepted values: `active` or `template`.| 
| `owner`| 	JSONObject| Required 	| The project owner.|
|&emsp;owner.`zpuid`|	String|	| The user ID of the project owner.<br> Get it from the [Get all portal users and contacts API](#get-all-portal-users-and-contacts)(the `id` field in the response).
| `is_public_project` | 	Boolean	| Optional | Whether the project is public.<br> Accepted values: `true` or `false`. |
| `start_date`	| String<br> *format:YYYY-MM-DD* | Optional |	The start date of the project.|
| `end_date` |	String<br>*format:YYYY-MM-DD* |Optional |	The end date of the project. |
| `status` | 	JSONObject<br>  *Maximum length: 1,000*| Optional	| The status of the project.| 
|&emsp;status.`id` | 	String<br>*Maximum length: 30* |  |	The identifier of the status.<br> Get it from the [Get Global Statuses API](#get-global-statuses).|
| `layout`	| JSONObject<br>*Maximum length: 1,000*	| Optional |The project layout details.|
|&emsp;layout.`id` |	String<br>*Maximum length: 30*|  |	The identifier of the layout.<br> Get it from the [Get a layout list API](#get-a-module-list) (the `id` field in the response). |
| `added_via` |	String | Optional |	The source of the project.<br> Accepted values: `web` or `api`. |
| `is_rollu1p_project` | 	Boolean	| Optional | Whether the project is a roll-up project.<br> Accepted values: `true` or `false`.  |
| `budget_info` | 	JSONObject<br> *Maximum length: 80,000* | Optional	| The project budget details.|
|&emsp; budget_info.`billing_method` |	String | 	| The billing method.<br> Accepted values: `project_hours`, `staff_hours`, `fixed_cost`, `issue_hours`, or `task_or_issue_hours`.|
|&emsp; budget_info.`budget_type`	| String | 	|The budget type.<br> Accepted values: `none`, `based_on_project`, `based_on_milestone`, `based_on_task`, or `based_on_user`.|
|&emsp; budget_info.`tracking_method`	| String | |	The tracking method.<br> Accepted values: `project_hours`, `staff_hours`, `issue_hours`, or `task_or_issue_hours`. |
|&emsp; budget_info.`currency` |	String |  |	The currency type. |
|&emsp; budget_info.`cost_budget`|	JSONObject|	| The budget details for the project. |
|&emsp;&emsp; budget_info.cost_budget.`amount` |	double |  |	The cost budget amount.|
|&emsp; budget_info.`hourly_budget`	|String|  |	The hourly budget details.|
|&emsp; budget_info.`rate_per_hour` |	JSONObject | |	The rate per hour. |
|&emsp;&emsp; budget_info.`rate_per_hour.amount` |	double| |	The amount of the rate per hour. |
|&emsp;budget_info.`cost_budget_threshold`|	JSONObject|  |	The budget threshold details. |
|&emsp;&emsp; budget_info.cost_budget_threshold.`amount`| double |  |	The cost budget threshold amount. |
|&emsp; budget_info.`hourly_budget_threshold`|	String |  |	The hourly budget threshold details. |
|&emsp; budget_info.`fixed_cost`|	JSONObject| |	The fixed cost.|
|&emsp;&emsp; budget_info.fixed_cost.`amount`|	double ||	The fixed cost amount.|
|&emsp; budget_info.`cost_per_hour` |	JSONObject| |	The cost per hour for the project.|
|&emsp;&emsp; budget_info.cost_per_hour.`amount`|	double|  |	The amount of the cost per hour.|
|&emsp; budget_info.`revenue_budget` |	JSONObject |	|The revenue budget.|
|&emsp;&emsp; budget_info.revenue_budget.`amount`	|double|  |	The revenue budget amount.|
|&emsp; budget_info.`budget_threshold`	|JSONObject|   |	The budget threshold details.|
|&emsp;&emsp; budget_info.budget_threshold.`amount`|	double |  |	The budget threshold amount. |
|`project_group`|	JSONObject<br>*Maximum length: 1,000*|	Optional |The project group details.|
|&emsp; project_group.`id` |	String<br>*Maximum length: 30*|  |	The identifier of the project group.<br> Get it from the [Get a user’s project groups API](#get-a-user’s-project-groups) (the `id` field in the response).|
|`sub_module_settings` |	JSONObject |	| The sub-module settings, which declare sub-module configurations. |
|&emsp; sub_module_settings.`sub_module_layouts_configuration` |	JSONObject |  |	The sub-module layouts. |
|`tags` |	JSONArray<br*Maximum length: 10,000* | Optional 	|The tags for the project.|
|&emsp; tags.`add`	|JSONArray<br>*Array size: 0 to 5,000*| 	| The tags to add to the project.|
|&emsp;&emsp; tags.add[].`id` |	String<br>*Maximum length: 30* |  |The identifier of the tag to add.<br> Get it from the [Get all tags API](#get-all-tags) (the `id` field in the response). |
|&emsp; tags.`remove` |	JSONArray<br>*Array size: 0 to 5,000* |	| The tags to remove from the project.|
|&emsp;&emsp; tags.remove[].`id` |	String<br>*Maximum length: 30* | |	The identifier of the tag to remove.<br> Get it from the [Get all tags API](#get-all-tags) (the `id` field in the response). |
|&emsp; tags[].`id`	| String<br>*Maximum length: 30* |	 | The identifier of the tag.<br> Get it from the [Get all tags API](#get-all-tags) (the `id` field in the response). |
| `copy_from` | 	Integer | 	Optional | The ID of the template or existing project to copy the new project from.<br> Get it from the [Get all projects API](#get-all-projects) (the `id` field in the response). |
| `business_hours_id` |	String	| Optional | The business hours ID.<br>  Get it from the [Get business hours API](#get-business-hours) (the `id` field in the response). |
| `<field_name>` |	String	| Optional |  The value of a project custom field.<br> Replace `<field_name>` with the custom field’s API name in snake_case, as listed in the Custom Fields Guide.<br> **Note:** The type shows as `String` by default because most basic custom fields accept string values. The value format and input structure depend on the custom field type. For details, see the Custom Fields Guide.|

**Sample input**
> *Content-Type: application/json
```
{
  "name" : "Website Redesign",
  "description" : "Redesign the company website with new branding",
  "project_type" : "active",
  "owner" : {
    "zpuid" : "4000000002055"
  },
  "is_public_project" : false,
  "start_date" : "2023-12-20",
  "end_date" : "2024-12-20",
  "status" : {
    "id" : "4000000062001"
  },
  "layout" : {
    "id" : "4000000062001"
  },
  "added_via" : "api",
  "is_rollup_project" : false,
  "budget_info" : {
    "billing_method" : "project_hours",
    "budget_type" : "based_on_project",
    "tracking_method" : "project_hours",
    "currency" : "USD",
    "cost_budget" : {
      "amount" : 50000.0
    },
    "hourly_budget" : "30:00",
    "rate_per_hour" : {
      "amount" : 945.25
    },
    "cost_budget_threshold" : {
      "amount" : 50000.0
    },
    "hourly_budget_threshold" : "20:00",
    "fixed_cost" : {
      "amount" : 50000.0
    },
    "cost_per_hour" : {
      "amount" : 510.75
    },
    "revenue_budget" : {
      "amount" : 50000.0
    }
  },
  "project_group" : {
    "id" : "4000000062001"
  },
  "tags" : [ {
    "add" : [ {
      "id" : "4000000062001"
    } ],
    "remove" : [ {
      "id" : "4000000062001"
    } ],
    "id" : "4000000062001"
  } ],
  "business_hours_id" : "7000000197013"
}
```
**Sample response**
- 200 Ok
```
{
  "end_date" : "2029-01-01",
  "picklist_11sep" : "abc",
  "is_public_project" : "false",
  "description" : "source project  for testing clone project",
  "is_strict_project" : "false",
  "multiline_11sep" : "multiline \nMULTILINE",
  "budget_info" : {
    "hourly_budget" : "1200:00",
    "billing_method" : "project_hours",
    "forecasted_cost" : {
      "amount" : 50000.0,
      "formatted_amount" : "$ 50000.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "planned_hours" : "20:00",
    "bcy_forecasted_cost" : {
      "amount" : 50000.0,
      "formatted_amount" : "$ 50000.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "forecasted_hours" : "20:00",
    "remaining_hours" : "10:00",
    "actual_cost" : {
      "amount" : 50000.0,
      "formatted_amount" : "$ 50000.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "actual_hours" : "50:00",
    "bcy_planned_cost" : {
      "amount" : 50000.0,
      "formatted_amount" : "$ 50000.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "planned_cost" : {
      "amount" : 50000.0,
      "formatted_amount" : "$ 50000.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "budget_type" : "based_on_project",
    "bcy_actual_cost" : {
      "amount" : 50000.0,
      "formatted_amount" : "$ 50000.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    },
    "cost_budget" : {
      "amount" : "10000000",
      "formatted_amount" : "$ 1,00,00,000.00",
      "currency_code" : "USD",
      "currency_id" : "7000000015018"
    }
  },
  "issues" : {
    "closed_count" : 10,
    "open_count" : 10
  },
  "is_completed" : "false",
  "id" : "7000000074003",
  "key" : "50",
  "tasks" : {
    "closed_count" : 10,
    "open_count" : 10
  },
  "number_11sep" : "1212",
  "start_date" : "2024-09-30",
  "phone_11sep" : "9879879877",
  "project_type" : "active",
  "created_time" : "2024-11-22T01:31:18.811Z",
  "check_box_sample_11sep" : "true",
  "is_rollup_project" : "false",
  "one" : "123456_single",
  "created_by" : {
    "zpuid" : "7000000002411",
    "name" : "Daniel",
    "last_name" : "Cooper",
    "first_name" : "Daniel",
    "zuid" : "25450833"
  },
  "percent_complete" : "10",
  "tags" : [ {
    "id" : "7000000015084",
    "color_hexcode" : "#7dcf7b"
  } ],
  "layout" : {
    "name" : "Standard Layout",
    "id" : "7000000000506",
    "is_default" : "true",
    "type" : "public"
  },
  "single_line_test_1446" : "singleline",
  "name" : "via_api_created_002_22nov_1230PM",
  "updated_by" : {
    "zpuid" : "7000000002411",
    "name" : "Daniel",
    "last_name" : "Cooper",
    "first_name" : "Daniel",
    "zuid" : "25450833"
  },
  "project_group" : {
    "name" : "zp.projset.ungroupproj",
    "id" : "7000000005369",
    "type" : "public"
  },
  "milestones" : {
    "closed_count" : 10,
    "open_count" : 10
  },
  "status" : {
    "is_closed_type" : "false",
    "name" : "Active",
    "id" : "7000000000665"
  }
}
```

### Update a project

Use this endpoint to modify an existing project in the SmartHive Projects portal.

**Method and endpoint:** `PATCH /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]`

**OAuth scope:** *SmartHiveProjects.projects.UPDATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br> Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the`id` field in the response).| 
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal.<br> Get it from the [Get all projects API](#get-all-projects) (the `id` field in the response). |

**Request example**
```
curl -X PATCH \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/projects/23806000097545166' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa' \
 -H 'Content-Type: application/json' \
 -d '
 {
	"name":"Website Redesign",
	"description":"Redesign the company website with new branding",
	"project_type":"active",
	"owner":{
		"zpuid":"4000000002055"
		},
	"is_public_project":false,
	"start_date":"2023-12-20",
	"end_date":"2024-12-20",
	"completed_time":"2025-12-30T18:30:00.000Z",
	"status":{
		"id":"4000000062001"
		},
	"layout":{
		"id":"4000000062001"
		},
	"added_via":"api",
	"is_rollup_project":false,
	"budget_info":{
		"billing_method":"project_hours",
		"budget_type":"based_on_project",
		"tracking_method":"project_hours",
		"currency":"USD",
		"cost_budget":{
			"amount":50000.0
			},
		"hourly_budget":"30:00",
		"rate_per_hour":{
			"amount":945.25
			},
		"cost_budget_threshold":{
			"amount":50000.0
			},
		"hourly_budget_threshold":"20:00",
		"fixed_cost":{
			"amount":50000.0
			},
		"cost_per_hour":{
			"amount":510.75
			},
		"revenue_budget":{
			"amount":50000.0
			}
		},
	"project_group":{
		"id":"4000000062001"
		},
	"tags":[{
		"add":[{
			"id":"4000000062001"
			}],
		"remove":[{
			"id":"4000000062001"
			}],
		"id":"4000000062001"
		}],
	"color":"#4573d2",
	"business_hours_id":"7000000197013"
 }'
```
**Body parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

| Name	| Data type |	Required/Optional  | Description |
| :---        | :----  |  :----  |     :---- |
| `name` |	String<br> *Maximum length: 200*|	Required | The project name. |
| `description` |	String<br>*Maximum length: 80,000* | Optional |	The project description. | 
| `project_type` |	String | Optional |	The project type.<br> Accepted values: `active` or `template`.| 
| `owner`| 	JSONObject | Required	| The project owner.|
|&emsp; owner.`zpuid`|	String|	 | The user ID of the project owner.<br> Get it from the [Get all users API](#Get-all-users) (the `id` field in the response).
| `is_public_project` | 	Boolean	| Optional | Whether the project is public.<br> Accepted values: `true` or `false`. |
| `start_date`	| String<br> *format:YYYY-MM-DD* | Optional |	The start date of the project.|
| `end_date` |	String<br>*format:YYYY-MM-DD* |Optional |	The end date of the project. |
| `completed_time`| String<br> *format: YYYY-MM-DDThh:mm:ssz (ISO-8601) * | Optional | The completed time of the project. |
| `status` | 	JSONObject<br>  *Maximum length: 1,000*| Optional	| The status of the project.| 
|&emsp; status.`id` | 	String<br>*Maximum length: 30* |  |	The identifier of the status.<br> Get it from the [Get Global Statuses API](#get-global-statuses).|
| `layout`	| JSONObject<br>*Maximum length: 1,000*	| Optional |The project layout details.|
|&emsp; layout.`id` |	String<br>*Maximum length: 30*|  |	The identifier of the layout.<br> Get it from the [Get a layout list API](#get-a-module-list) (the `id` field in the response). |
| `added_via` |	String | Optional |	The source of the project.<br> Accepted values: `web` or `api`. |
| `is_rollu1p_project` | 	Boolean	| Optional | Whether the project is a roll-up project.<br> Accepted values: `true` or `false`.  |
|  `budget_info` | 	JSONObject<br> *Maximum length: 80,000* | Optional	| The project budget details.|
|&emsp; budget_info.`billing_method` |	String | 	| The billing method.<br> Accepted values: `project_hours`, `staff_hours`, `fixed_cost`, `issue_hours`, or `task_or_issue_hours`.|
|&emsp; budget_info.`budget_type`	| String | 	|The budget type.<br> Accepted values: `none`, `based_on_project`, `based_on_milestone`, `based_on_task`, or `based_on_user`.|
|&emsp; budget_info.`tracking_method`	| String |  |	The tracking method.<br> Accepted values: `project_hours`, `staff_hours`, `issue_hours`, or `task_or_issue_hours`. |
|&emsp; budget_info.`currency` |	String |  |	The currency type. |
|&emsp; budget_info.`cost_budget`|	JSONObject|	| The budget details for the project. |
|&emsp;&emsp; budget_info.cost_budget.`amount` |	double| |	The cost budget amount.|
|&emsp; budget_info.`hourly_budget`	|String|  |	The hourly budget details.|
|&emsp; budget_info.`rate_per_hour` |	JSONObject| |	The rate per hour. |
|&emsp;&emsp; budget_info.rate_per_hour.`amount` |	double|  |	The amount of the rate per hour. |
|&emsp; budget_info.`cost_budget_threshold`|	JSONObject|  |	The budget threshold details. |
|&emsp;&emsp; budget_info.cost_budget_threshold.`amount`| double |  |	The cost budget threshold amount. |
|&emsp; budget_info.`hourly_budget_threshold`|	String |  |	The hourly budget threshold details. |
|&emsp; budget_info.`fixed_cost`|	JSONObject| |	The fixed cost.|
|&emsp;&emsp; budget_info.fixed_cost.`amount`|	double | |	The fixed cost amount.|
|&emsp; budget_info.`cost_per_hour` |	JSONObject| |	The cost per hour for the project.|
|&emsp;&emsp; budget_info.cost_per_hour.`amount`|	double|  |	The amount of the cost per hour.|
|&emsp; budget_info.`revenue_budget` |	JSONObject |	|The revenue budget.|
|&emsp;&emsp; budget_info.revenue_budget.`amount`	|double|  |	The revenue budget amount.|
|`project_group`|	JSONObject<br>*Maximum length: 1,000*|	Optional |The project group details.|
|&emsp; project_group.`id` |	String<br>*Maximum length: 30*|  |	The identifier of the project group.<br> Get it from the Get a user’s project groups API](#get-a-user’s-project-groups) (the `id` field in the response).|
|`tags` |	JSONArray<br*Maximum length: 10,000* |	Optional |The tags for the project.|
|&emsp; tags.`add`	|JSONArray<br>*Array size: 0 to 5,000*| 	| The tags to add to the project.|
|&emsp;&emsp; tags.add[].`id` |	String<br>*Maximum length: 30* |  |The identifier of the tag to add.<br> Get it from the [Get all tags API](#get-all-tags) (the `id` field in the response). |
|&emsp;  tags.`remove` |	JSONArray<br>*Array size: 0 to 5,000* |	| The tags to remove from the project.|
|&emsp;&emsp; tags.remove[].`id` |	String<br>*Maximum length: 30* | |	The identifier of the tag to remove.<br> Get it from the [Get all tags API](#get-all-tags) (the `id` field in the response). |
|&emsp; tags[].`id`	| String<br>*Maximum length: 30* |	 | The identifier of the tag.<br> Get it from the [Get all tags API](#get-all-tags) (the `id` field in the response). |
| `color` | 	String | 	Optional | The project color. |
| `business_hours_id` |	String	| Optional | The business hours ID.<br> Get it from the [Get business hours API](#get-business-hours) (the `id` field in the response). |
| `<field_name>` |	String	| Optional |  The value of a project custom field.<br> Replace `<field_name>` with the custom field’s API name in snake_case, as listed in the Custom Fields Guide.<br> **Note:** The type shows as `String` by default because most basic custom fields accept string values. The value format and input structure depend on the custom field type. For details, see the Custom Fields Guide.|

**Sample input**
> *Content-Type: application/json
```
{
  "name" : "Website Redesign",
  "description" : "Redesign the company website with new branding",
  "project_type" : "active",
  "owner" : {
    "zpuid" : "4000000002055"
  },
  "is_public_project" : false,
  "start_date" : "2023-12-20",
  "end_date" : "2024-12-20",
  "completed_time" : "2025-12-30T18:30:00.000Z",
  "status" : {
    "id" : "4000000062001"
  },
  "layout" : {
    "id" : "4000000062001"
  },
  "added_via" : "api",
  "is_rollup_project" : false,
  "budget_info" : {
    "billing_method" : "project_hours",
    "budget_type" : "based_on_project",
    "tracking_method" : "project_hours",
    "currency" : "USD",
    "cost_budget" : {
      "amount" : 50000.0
    },
    "hourly_budget" : "30:00",
    "rate_per_hour" : {
      "amount" : 945.25
    },
    "cost_budget_threshold" : {
      "amount" : 50000.0
    },
    "hourly_budget_threshold" : "20:00",
    "fixed_cost" : {
      "amount" : 50000.0
    },
    "cost_per_hour" : {
      "amount" : 510.75
    },
    "revenue_budget" : {
      "amount" : 50000.0
    }
  },
  "project_group" : {
    "id" : "4000000062001"
  },
  "tags" : [ {
    "add" : [ {
      "id" : "4000000062001"
    } ],
    "remove" : [ {
      "id" : "4000000062001"
    } ],
    "id" : "4000000062001"
  } ],
  "color" : "#4573d2",
  "business_hours_id" : "7000000197013"
}
```
**Sample response**
- 200 Ok
```
{
  "id" : "7000000278041",
  "key" : "174",
  "name" : "test",
  "project_type" : "active",
  "description" : "<div><br></div>",
  "owner" : {
    "zuid" : 25450833,
    "zpuid" : "7000000002411",
    "name" : "Marcus Ashford",
    "email" : "marcus.ashford@victa.com",
    "first_name" : "Marcus",
    "last_name" : "Ashford",
    "full_name" : "Marcus Ashford"
  },
  "is_public_project" : false,
  "start_date" : "2025-11-09",
  "end_date" : "2025-11-30",
  "completed_time" : "2025-12-30T18:30:00.000Z",
  "is_strict_project" : false,
  "created_time" : "2025-09-29T08:06:34.118Z",
  "created_by" : {
    "zuid" : 25450833,
    "zpuid" : "7000000002411",
    "name" : "Marcus Ashford",
    "email" : "marcus.ashford@victa.com",
    "first_name" : "Marcus",
    "last_name" : "Ashford",
    "full_name" : "Marcus Ashford"
  },
  "modified_time" : "2026-02-09T08:31:55.342Z",
  "updated_by" : {
    "zuid" : 25450833,
    "zpuid" : "7000000002411",
    "name" : "Marcus Ashford",
    "email" : "marcus.ashford@victa.com",
    "first_name" : "Marcus",
    "last_name" : "Ashford",
    "full_name" : "Marcus Ashford"
  },
  "status" : {
    "id" : "7000000000665",
    "name" : "Active",
    "color" : "transparent",
    "color_hexcode" : "transparent",
    "is_closed_type" : false
  },
  "layout" : {
    "id" : "7000000000506",
    "name" : "Standard Layout",
    "is_default" : true,
    "type" : "public"
  },
  "business_hours_id" : "7000000197013",
  "is_rollup_project" : false,
  "budget_info" : {
    "billing_method" : "staff_hours",
    "budget_type" : "none",
    "currency" : "USD",
    "cost_budget" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "hourly_budget" : "30:00",
    "rate_per_hour" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "cost_budget_threshold" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "hourly_budget_threshold" : "20:00",
    "fixed_cost" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "tracking_method" : "project_hours",
    "cost_per_hour" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "revenue_budget" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "planned_cost" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "actual_cost" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "forecasted_cost" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "planned_hours" : "50:00",
    "actual_hours" : "40:00",
    "remaining_hours" : "10:00",
    "forecasted_hours" : "20:00",
    "planned_value" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "earned_value" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "schedule_variance" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "cost_variance" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "bcy_planned_cost" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "bcy_actual_cost" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "bcy_forecasted_cost" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "bcy_planned_value" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "bcy_earned_value" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "planned_revenue" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "actual_revenue" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    },
    "forecasted_revenue" : {
      "currency_code" : "USD",
      "formatted_amount" : "$ 50000.00",
      "amount" : 50000.0
    }
  },
  "project_group" : {
    "id" : "7000000005369",
    "name" : "zp.projset.ungroupproj",
    "type" : "public"
  },
  "percent_complete" : 0,
  "tasks" : {
    "open_count" : 10,
    "closed_count" : 20
  },
  "issues" : {
    "open_count" : 10,
    "closed_count" : 20
  },
  "milestones" : {
    "open_count" : 10,
    "closed_count" : 20
  },
  "is_completed" : false,
  "date_std_lay_proj" : "2025-11-15",
  "single_line_test_1446" : "www.smarthive.com",
  "check_box_sample_11sep" : false,
  "is_equal_no_of_unit_and_cost_formula" : false,
  "check_box_19sep_cview_lay" : false
}
```
### Trash a project

Use this endpoint to move an existing project in the SmartHive Projects portal to the trash.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]/trash`

**OAuth scope:** *SmartHiveProjects.projects.UPDATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response).| 
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal.<br>Get it from the [Get all projects API](#get-all-projects) (the `id` field in the response). |

**Request example**
```
curl -X POST \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/projects/23806000097545166/trash' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Sample response**
- 204 No content

### Restore a project

Use this endpoint to Restore a project from the trash in the SmartHive Projects portal.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]/restore`

**OAuth scope:** *SmartHiveProjects.projects.UPDATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response).| 
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal.<br>Get it from the [Get all projects API](#get-all-projects) (the `id` field in the response). |

**Request example**
```
curl -X POST \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/projects/23806000097545166/restore' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Sample response**
- 204 No content

### Delete a project

Use this endpoint to remove a project from the trash permanently.

**Method and endpoint:** `DELETE /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]`

**OAuth scope:** *SmartHiveProjects.projects.UPDATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response).| 
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal.<br>Get it from the [Get all projects API](#get-all-projects) (the `id` field in the response). |

**Request example**
```
curl -X DELETE \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/projects/23806000097545166' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Sample response**
- 204 No content

-------

## Profiles

This module covers profile-related operations in Smarthive Projects. Use the Profiles API to manage portal profiles, update profile permissions, and set default profiles for your users.

### Get all portal profiles

Use this endpoint to retrieve all profiles in a specific portal and their configurations.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/profiles`

**OAuth scope:** *SmartHiveProjects.portals.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/profiles?sort_by=ASC%28last_updated_time%29&page=1&per_page=10&filter=%7B%22criteria%22%3A%5B%7B%22module%22%3A%22-%22%2C%22field_name%22%3A%22project%22%2C%22module_name%22%3A%22task%22%2C%22criteria_condition%22%3A%22contains%22%2C%22value%22%3A%5B1752587000000097269%5D%7D%5D%2C%22pattern%22%3A%221%22%7D&ids=4000000029001' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `sort_by`	| String | Optional |	The sort order.<br> Accepted values: `ASC(field_name)` or `DESC(field_name)`.<br> Available fields: `name`, `type`, `created_by`, `created_time`, `last_updated_by`, `last_updated_time`, `default_profile`, and system_defined`. |
| `page`	| Integer<br>*Default: 1* | Optional |	The page number.|
| `per_page` |	Integer<br>*Default: 25* | Optional |	| The number of entries to display on each page.|
| `filter`	| JSONObject |	Optional | The filter criteria for narrowing the profile results.|
| &emsp; filter.`criteria`|	JSONArray<br> *Maximum length: 10,000*<br>*Array size: 0 or greater* | |	The list of filter conditions.<br> The API combines the conditions by using the pattern property.|
| &emsp;&emsp; filter.criteria[].`module`|	String| 	|The module of the field.|
| &emsp;&emsp; filter.criteria[].`field_name`|	String | 	| The field name.|
| &emsp;&emsp; filter.criteria[].`module_name`|	String |	| The module name. |
| &emsp;&emsp; filter.criteria[].`criteria_condition` |	String<br>*Maximum length: 25* |	| The condition for the criteria.<br> For example, `is`, `contains`, or `greater_than`. | 
| &emsp;&emsp; filter.criteria[].`value` |	JSONArray<br>*Maximum length: 10,000*<br>*Array size: 0 or greater* |	| The values for the criteria condition. You can provide multiple values. |
| &emsp; filter.`pattern`|	String<br> Maximum length: 300.|	| The logical pattern that combines the filter conditions. For example, `1` AND `2`.| 
| `ids` |	String | 	| The profile IDs. |

**Sample input**
```
sort_by : "ASC(last_updated_time)"
page : 1
per_page : 10
filter : {
  "criteria" : [ {
    "module" : "-",
    "field_name" : "project",
    "module_name" : "task",
    "criteria_condition" : "contains",
    "value" : [ 1752587000000097269 ]
  } ],
  "pattern" : "1"
}
ids : 4000000029001
```
**Sample response**
- 200 Ok
```
{
  "page_info" : {
    "page" : 1,
    "per_page" : 25,
    "count" : 12,
    "page_count" : 1,
    "has_next_page" : false
  },
  "profiles" : [ {
    "is_primary" : true,
    "name" : "Manager",
    "id" : "7000000002347",
    "type" : "6",
    "is_default" : true
  } ]
}
```
-----

## Modules

This module covers operations for managing modules in Smarthive Projects. Use the Modules API to get lists of modules and their configuration details.

### Get modules

Use this endpoint:

- To retrieve a list of modules in the portal, along with their configuration details. 
- To identify module API names, IDs, and types before you perform module-level operations.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/settings/modules`

**OAuth scope:** *SmartHiveProjects.custom_fields.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/settings/modules?filter=%7B%22is_customized%22%3Atrue%2C%22is_default%22%3Atrue%2C%22is_web_tab%22%3Atrue%7D&page=1&per_page=10' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `filter`	| JSONObject | Optional |	The filter criteria for refining the results.<br> You can combine multiple filter conditions. |
| &emsp; filter.is_`customized` |	Boolean |	| Whether to include only customized modules. |
| &emsp; filter.is_`default`	| Boolean	| | Whether to include only default modules.|
| &emsp; filter.`is_web_tab` | 	Boolean | |Whether to include only web tab modules.| 
| `page` |	Integer<br>*Default: 1* | Optional	|The page number.|
| `per_page` |	Integer<br> *Limit: 1 to 200*<br>*Default: 1,000*| Optional 	| The number of entries to display on each page.|

**Sample input**
```
filter : {
  "is_customized" : true,
  "is_default" : true,
  "is_web_tab" : true
}
page : "1"
per_page : "10"
```
**Sample response**
- 200 Ok
```
[ {
  "id" : "4000000000152",
  "api_name" : "tasks",
  "singular_name" : "Task",
  "icon_class" : "smarthive-task",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Task",
  "module_name" : "Task",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "5",
    "is_indexed_module" : true,
    "default_layout_type" : "private"
  }
}, {
  "id" : "4000000000155",
  "api_name" : "issues",
  "singular_name" : "zp.general.issue",
  "plural_name" : "zp.general.issues",
  "icon_class" : "smarthive-bugs2",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Issue",
  "module_name" : "Issue",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "6",
    "is_indexed_module" : true,
    "default_layout_type" : "private"
  }
}, {
  "id" : "4000000000158",
  "api_name" : "timelogs",
  "singular_name" : "zp.tab.timelog",
  "plural_name" : "zp.tab.timelogs",
  "icon_class" : "smarthive-timesheet",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Timesheet",
  "module_name" : "Timesheet",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "private"
  }
}, {
  "id" : "4000000000521",
  "api_name" : "projects",
  "singular_name" : "Projects",
  "icon_class" : "smarthive-projects",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Projects",
  "module_name" : "Projects",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "2",
    "is_indexed_module" : true,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000000776",
  "api_name" : "phases",
  "singular_name" : "zp.module.rename.phase",
  "plural_name" : "zp.module.rename.phases",
  "icon_class" : "smarthive-milestone",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Milestone",
  "module_name" : "Milestone",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "3",
    "is_indexed_module" : true,
    "default_layout_type" : "private"
  }
}, {
  "id" : "4000000002061",
  "api_name" : "tasklists",
  "singular_name" : "zp.module.tasklist",
  "plural_name" : "zp.module.tasklists",
  "icon_class" : "smarthive-tasklist",
  "type" : "default",
  "status" : "active",
  "is_global_module" : false,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Tasklist",
  "module_name" : "Tasklist",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "4",
    "is_indexed_module" : true,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002064",
  "api_name" : "forums",
  "singular_name" : "zp.forum.tab",
  "plural_name" : "zp.profileform.forum",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Forum",
  "module_name" : "Forum",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "7",
    "is_indexed_module" : true,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002067",
  "api_name" : "statuses",
  "singular_name" : "zp.reports.status",
  "plural_name" : "zp.customfields.statuses",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Status",
  "module_name" : "Status",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "8",
    "is_indexed_module" : true,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002070",
  "api_name" : "events",
  "singular_name" : "zp.notification.event",
  "plural_name" : "zp.todo.events",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Events",
  "module_name" : "Events",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "9",
    "is_indexed_module" : true,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002073",
  "api_name" : "pages",
  "singular_name" : "zp.planacc.wikis",
  "plural_name" : "zp.planacc.wikis",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Pages",
  "module_name" : "Pages",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002076",
  "api_name" : "documents",
  "singular_name" : "zp.doc.tab",
  "plural_name" : "zp.doc.tab",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Documents",
  "module_name" : "Documents",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002079",
  "api_name" : "users",
  "singular_name" : "zp.general.user",
  "plural_name" : "zp.general.users",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Users",
  "module_name" : "Users",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002082",
  "api_name" : "clients",
  "singular_name" : "zp.client.clientcompuser",
  "plural_name" : "zp.planaccount.clients",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Clients",
  "module_name" : "Clients",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002085",
  "api_name" : "resources",
  "singular_name" : "zp.resources.resource",
  "plural_name" : "zp.tasklistexport.resource",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Resources",
  "module_name" : "Resources",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002088",
  "api_name" : "timeloggroup",
  "singular_name" : "zp.tsheet.tab",
  "plural_name" : "zp.invoice.timesheets",
  "icon_class" : "smarthive-timesheet-new",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "TimelogGroup",
  "module_name" : "TimelogGroup",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002091",
  "api_name" : "recyclebin",
  "singular_name" : "zp.module.recyclebin",
  "plural_name" : "zp.module.recyclebin",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Recyclebin",
  "module_name" : "Recyclebin",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002094",
  "api_name" : "customers",
  "singular_name" : "zp.client.clientcompname",
  "plural_name" : "zp.client.companies",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : false,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Customers",
  "module_name" : "Customers",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000060007",
  "api_name" : "tags",
  "singular_name" : "zp.links.tag",
  "plural_name" : "zp.tag.tags1",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Tag",
  "module_name" : "Tag",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000060016",
  "api_name" : "profiles",
  "singular_name" : "zp.userfilter.profile",
  "plural_name" : "zp.settings.profiles",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Profile",
  "module_name" : "Profile",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000060025",
  "api_name" : "roles",
  "singular_name" : "zp.userfilter.role",
  "plural_name" : "zp.settings.roles",
  "icon_class" : "smarthive-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Role",
  "module_name" : "Role",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
} ]
```
### Get global statuses

Use this endpoint:
- To retrieve the list of global statuses configured for a module, along with their metadata, such as status ID, name, color, type, and sequence order. 
- To identify status IDs before you perform status-based operations.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/settings/global-statuses`

**OAuth scope:** *SmartHiveProjects.custom_fields.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/settings/global-statuses?module=-&filter=%7B%22status_ids%22%3A%22-%22%2C%22status_names%22%3A%22-%22%2C%22search_term%22%3A%22smarthive+Projects%22%7D&page=-&per_page=-' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| module |	String |	Required | The API name or ID of the module.<br> Get it from the [Get Modules API](#get-modules) (the `id` field in the response). |
| filter	| JSONObject	|Optional  |The filter criteria for refining the results.<br> Use only one filter property per request. |
| &emsp; filter.`status_ids` |	JSONArray| 	| The IDs of the statuses to get.|
| &emsp; filter.`status_names` |	JSONArray|	| The names of the statuses to get. |
| &emsp; filter.`search_term` |	String<br>*Maximum length: 100*| 	| The search term for filtering statuses by name. |
| `page` |	Integer | Optional |	The page number. |
| `per_page` |	Integer | Optional |	The number of entries to display on each page.|

**Sample input**
```
module :  - 
filter : {
  "status_ids" : "-",
  "status_names" : "-",
  "search_term" : "Smarthive Projects"
}
page :  - 
per_page :  -
```
**Sample response**
- 200 Ok
```
[ {
  "id" : "5000000000500",
  "name" : "Open",
  "color" : "transparent",
  "color_hexcode" : "transparent"
}, {
  "id" : "5000000000521",
  "name" : "Cancelled",
  "color" : "transparent",
  "color_hexcode" : "transparent"
} ]
```
**Possible errors**
- INVALID_PARAMETER_VALUE `HTTP 400`
```
{
  "error" : {
    "status_code" : "400",
    "instance" : "/api/v3/portal/25450296/settings/global-statuses",
    "method" : "GET",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Invalid module",
      "field_name" : "module"
    } ],
    "title" : "INVALID_PARAMETER_VALUE"
  }
}
```
-----

## Module layouts

### Get a layout list

Use this endpoint to:
- Retrieve the list of layouts in a module. 
- Identify layout IDs before you perform layout-level operations, such as updating layouts, adding fields, or managing sections.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/settings/layouts`

**OAuth scope:** *SmartHiveProjects.custom_fields.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/settings/layouts?module=projects&index=1&range=100&page=1&per_page=10&filter=%7B%22is_association_info_needed%22%3A%22true%22%2C%22is_current_user_profile_associated%22%3A%22true%22%2C%22search_term%22%3A%22smarthive+Projects%22%2C%22search_by%22%3A%22project%22%7D' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `module` |	String |	Required | The API name or ID of the module.<br> Get it from the [Get Modules API](#get-modules)(the `id` field in the response).|
| `index` |	Integer | Optional |	The index of the layouts. |
| `range` |	Integer | Optional |	The range of the layouts. |
| `page`	| Integer<br>*Default: 1* |	Required | The page number. |
| `per_page` |	Integer<br>*Limit: 1 to 200*<br> *Default: 100* |	Required | The number of entries to display on each page. |
| `filter`	| JSONObject | Optional |	The filter criteria for refining the results.<br> You can combine multiple filter conditions. |
| &emsp; filter.`is_association_info_needed` | 	Boolean |	| Whether to include the association details.<br> Accepted values: `true` or `false`. |
| &emsp; filter.`is_current_user_profile_associated` |	Boolean	| | Whether the current user’s profile is associated.<br> Accepted values: `true` or `false`. |
| &emsp; filter.`search_term` |	String |	| The search term. |
| &emsp; filter.`search_by`	| String | | The field to search by.<br> Accepted values: `project`, `layout`, or `id`.

**Sample input**
```
module : "projects"
index : 1
range : 100
page : 1
per_page : 10
filter : {
  "is_association_info_needed" : "true",
  "is_current_user_profile_associated" : "true",
  "search_term" : "Smarthive Projects",
  "search_by" : "project"
}
```
** Sample Response**
- 200 Ok
```
[ {
  "associated_entities_count" : 2,
  "associated_entities" : [ {
    "name" : "Admin",
    "id" : "9000000002510"
  }, {
    "name" : "Manager",
    "id" : "9000000002513"
  } ],
  "name" : "New Layout 1",
  "id" : "9000000071079",
  "is_default" : false,
  "type" : "PUBLIC"
}, {
  "associated_entities_count" : 2,
  "associated_entities" : [ {
    "name" : "Admin",
    "id" : "9000000002510"
  }, {
    "name" : "Manager",
    "id" : "9000000002513"
  } ],
  "name" : "New Layout 2",
  "id" : "9000000054069",
  "is_default" : false,
  "type" : "PUBLIC"
} ]
```
**Possible errors**
- InVALID_PARAMETER_VALUE `HTTP 400`
```
{
  "error" : {
    "status_code" : 400,
    "instance" : "/api/v3/portal/25450296/settings/layouts",
    "method" : "GET",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Invalid module",
      "field_name" : "module"
    } ],
    "title" : "INVALID_PARAMETER_VALUE"
  }
}
```
----

## Project groups

This module covers operations related to project groups in SmartHive Projects.

### Get a user’s project groups

Use this endpoint to retrieve the project groups associated with a user.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/my-project-groups`

**OAuth scope:** *SmartHiveProjects.projectgroups.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details-API) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/my-project-groups?page=1&per_page=10' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `page` |	Integer<br>*Default: 1*| Optional |	The page number. |
| `per_page` |	Integer<br>*Limit: 1 to 200*<br>*Default: 100* | Optional |	The number of entries to display on each page.| 

**Sample input**
```
page : "1"
per_page : "10"
```
**Sample response**
- 200 Ok
```
{
  "project-groups" : [ {
    "name" : "Ungrouped Projects",
    "id" : "4000000005417"
  } ]
}
```
----

## Tags

This module covers operations related to tags in SmartHive Projects. Use the Tags API to create and update tags, associate tags with modules and projects, and delete tags.

### Get all tags

Use this endpoint to retrieve all tags in the SmartHive Projects portal.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/tags`

**OAuth scope:** *SmartHiveProjects.tags.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details-API) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/tags?page=1&per_page=10&filter=%7B%22criteria%22%3A%5B%7B%22field_name%22%3A%22project%22%2C%22criteria_condition%22%3A%22contains%22%2C%22value%22%3A%5B%221752587000000097269%22%5D%7D%5D%2C%22pattern%22%3A%221%22%7D' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- | 
| `page`	| Integer<br>*Default: 1* |	Optional | The page number. |
| `per_page` |	Integer<br>*Limit: 1 to 200*<br>*Default: 100*| Optional |	The number of entries to display on each page.|
| `filter` |	JSONObject| Optional |	The filter criteria.|
| &emsp; filter.`criteria`	| JSONArray<br>*Maximum length: 10,000<br>*Array size: 0 or greater* | 	| The criteria information.|
| &emsp;&emsp; filter.criteria.`field_name` | String | | The field name. |
| &emsp;&emsp; filter.criteria.`criteria_condition` | String<br>*Maximum length: 25*|  | The criteria condition. |
| &emsp;&emsp; filter.criteria.`value` | String<br>*Maximum length: 10,000*<br>*Array size: 0 or greater* |  | The  criteria value. |
| &emsp; filter.`pattern`	| String<br>*Maximum length: 300* |	| The filter pattern |

**Sample input**
```
page : "1"
per_page : "10"
filter : {
  "criteria" : [ {
    "field_name" : "project",
    "criteria_condition" : "contains",
    "value" : [ "1752587000000097269" ]
  } ],
  "pattern" : "1"
}
```
**Sample response**
- 200 Ok
```
{
  "page_info" : {
    "per_page" : 100,
    "has_next_page" : false,
    "count" : 1,
    "page" : 1
  },
  "tags" : [ {
    "usage_count" : 0,
    "name" : "tag129",
    "id" : "170876000008279193",
    "created_by" : {
      "zpuid" : "4000000002239",
      "full_name" : "Hector",
      "name" : "Hector",
      "last_name" : "",
      "id" : "21761641",
      "first_name" : "Hector",
      "email" : "hector@victa.com"
    },
    "color_hexcode" : "#7dcf7b"
  } ]
}
```
----

## Business hours

This module covers operations related to business hours in SmartHive Projects. Use the Business Hours API to create, update, and delete business hours.

### Get business hours

Use this endpoint to retrieve the list of business hours in the SmartHive Projects portal.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/business-hours`

**OAuth scope:** *SmartHiveProjects.portals.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details-API) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/business-hours?filter=%7B%22criteria%22%3A%5B%7B%22cfid%22%3A%224000000000242%22%2C%22field_name%22%3A%22project%22%2C%22criteria_condition%22%3A%22contains%22%2C%22value%22%3A%5B%221752587000000097269%22%5D%7D%5D%2C%22pattern%22%3A%221%22%7D&sort_by=ASC%28last_modified_time%29&page=1&per_page=10' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| filter| 	JSONObject| Optional |	The filter criteria. |
| &emsp; filter.`criteria`	| JSONArray<br>*Maximum length: 10,000*<br>*Array size: 0 or greater* |  | The criteria information.|
| &emsp;&emsp; filter.criteria[].`cfid` | 	Integer |	| The custom field ID. |
| &emsp;&emsp; filter.criteria[].`field_name`|	String| 	| The field name. |
| &emsp;&emsp; filter.criteria[].`criteria_condition`	| String<br>*Maximum length: 25*| |	The criteria condition.| 
| &emsp;&emsp; filter.criteria[].`value`	| JSONArray<br>* Maximum length: 10,000*<br>*Array size: 0 or greater*	| | The criteria values.| 
| &emsp; filter.`pattern`	| String<br>*Maximum length: 300*| 	| The filter pattern.| 
| `sort_by`	| String	| Optional | The sort order.<br> Accepted values: `ASC(field_name)` or `DESC(field_name)`.
| `page`	| Integer<br>*Default: 1* | Optional |	The page number. | 
| `per_page` |	Integer<br>*Limit: 1 to 200*<br>*Default: 100* |	Optional | The number of entries to display on each page. |

**Sample input**
```
filter : {
  "criteria" : [ {
    "cfid" : "4000000000242",
    "field_name" : "project",
    "criteria_condition" : "contains",
    "value" : [ "1752587000000097269" ]
  } ],
  "pattern" : "1"
}
sort_by : "ASC(last_modified_time)"
page : "1"
per_page : "10"
```
**Sample response**
- 200 Ok
```
{
  "business_hours" : [ {
    "created_time" : "2024-10-04T06:52:16.246Z",
    "updated_time" : "2024-10-04T06:52:16.246Z",
    "working_hours_type" : "same_hours",
    "working_hours" : [ {
      "start_time" : "09:00",
      "end_time" : "18:00",
      "break_hours" : [ ],
      "id" : "4000000066055",
      "day" : "1"
    } ],
    "name" : "US Shift",
    "updated_by" : {
      "zpuid" : "4000000002379",
      "full_name" : "Matthew Hayes",
      "email" : "matthew.hayes@victa.com",
      "zuid" : 22823316
    },
    "id" : "4000000066053",
    "is_default" : false,
    "created_by" : {
      "zpuid" : "4000000002379",
      "full_name" : "Matthew Hayes",
      "email" : "matthew.hayes@victa.com",
      "zuid" : 22823316
    },
    "version" : "1",
    "effective_from" : "2022-10-01"
  } ],
  "page_info" : {
    "per_page" : 50,
    "has_next_page" : false,
    "page" : 1,
    "sort_by" : [ {
      "field_names" : [ "name" ],
      "order_by" : "ASCENDING"
    } ]
  }
}
```
----




