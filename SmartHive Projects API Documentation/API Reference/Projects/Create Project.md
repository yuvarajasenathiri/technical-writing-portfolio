# Create project

Create a project in the SmartHive Projects portal.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/projects`

**OAuth scope:** SmartHiveProjects.projects.CREATE

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br> Get it from the Get All Portals with Details API (the `id` field in the response).| 

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
| `owner`| 	JSONObject| 	| The project owner.|
|&emsp;owner.`zpuid`|	String|	Required | The user ID of the project owner.<br> Get it from the Get Portal Users API (the `id` field in the response).
| `is_public_project` | 	Boolean	| Optional | Whether the project is public.<br> Accepted values: `true` or `false`. |
| `start_date`	| String<br> *format:YYYY-MM-DD* | Optional |	The start date of the project.|
| `end_date` |	String<br>*format:YYYY-MM-DD* |Optional |	The end date of the project. |
| `status` | 	JSONObject<br>  *Maximum length: 1,000*| 	| The status of the project.| 
|&emsp;status.`id` | 	String<br>*Maximum length: 30* | Optional |	The identifier of the status.<br> Get it from the Get Global Statuses API.|
| `layout`	| JSONObject<br>*Maximum length: 1,000*	| |The project layout details.|
|&emsp;layout.`id` |	String<br>*Maximum length: 30*| Optional |	The identifier of the layout.<br> Get it from the Get Layouts API (the `id` field in the response). |
| `added_via` |	String | Optional |	The source of the project.<br> Accepted values: `web` or `api`. |
| `is_rollu1p_project` | 	Boolean	| Optional | Whether the project is a roll-up project.<br> Accepted values: `true` or `false`.  |
| `budget_info` | 	JSONObject<br> *Maximum length: 80,000* | 	| The project budget details.|
|&emsp; budget_info.`billing_method` |	String | Optional	| The billing method.<br> Accepted values: `project_hours`, `staff_hours`, `fixed_cost`, `issue_hours`, or `task_or_issue_hours`.|
|&emsp; budget_info.`budget_type`	| String | Optional	|The budget type.<br> Accepted values: `none`, `based_on_project`, `based_on_milestone`, `based_on_task`, or `based_on_user`.|
|&emsp; budget_info.`tracking_method`	| String | Optional |	The tracking method.<br> Accepted values: `project_hours`, `staff_hours`, `issue_hours`, or `task_or_issue_hours`. |
|&emsp; budget_info.`currency` |	String | Optional |	The currency type. |
|&emsp; budget_info.`cost_budget`|	JSONObject|	| The budget details for the project. |
|&emsp;&emsp; budget_info.cost_budget.`amount` |	double|Optional |	The cost budget amount.|
|&emsp; budget_info.`hourly_budget`	|String| Optional |	The hourly budget details.|
|&emsp; budget_info.`rate_per_hour` |	JSONObject| |	The rate per hour. |
|&emsp;&emsp; budget_info.`rate_per_hour.amount` |	double| Optional |	The amount of the rate per hour. |
|&emsp;budget_info.`cost_budget_threshold`|	JSONObject|  |	The budget threshold details. |
|&emsp;&emsp; budget_info.cost_budget_threshold.`amount`| double | Optional |	The cost budget threshold amount. |
|&emsp; budget_info.`hourly_budget_threshold`|	String | Optional |	The hourly budget threshold details. |
|&emsp; budget_info.`fixed_cost`|	JSONObject| |	The fixed cost.|
|&emsp;&emsp; budget_info.fixed_cost.`amount`|	double |Optional|	The fixed cost amount.|
|&emsp; budget_info.`cost_per_hour` |	JSONObject| |	The cost per hour for the project.|
|&emsp;&emsp; budget_info.cost_per_hour.`amount`|	double| Optional |	The amount of the cost per hour.|
|&emsp; budget_info.`revenue_budget` |	JSONObject |	|The revenue budget.|
|&emsp;&emsp; budget_info.revenue_budget.`amount`	|double| Optional |	The revenue budget amount.|
|&emsp; budget_info.`budget_threshold`	|JSONObject|   |	The budget threshold details.|
|&emsp;&emsp; budget_info.budget_threshold.`amount`|	double | Optional |	The budget threshold amount. |
|`project_group`|	JSONObject<br>*Maximum length: 1,000*|	|The project group details.|
|&emsp; project_group.`id` |	String<br>*Maximum length: 30*| Optional |	The identifier of the project group.<br> Get it from the Get Project Groups API (the `id` field in the response).|
|`sub_module_settings` |	JSONObject |	| The sub-module settings, which declare sub-module configurations. |
|&emsp; sub_module_settings.`sub_module_layouts_configuration` |	JSONObject | Optional |	The sub-module layouts. |
|`tags` |	JSONArray<br*Maximum length: 10,000* |	|The tags for the project.|
|&emsp; tags.`add`	|JSONArray<br>*Array size: 0 to 5,000*| 	| The tags to add to the project.|
|&emsp;&emsp; tags.add[].`id` |	String<br>*Maximum length: 30* | Optional |The identifier of the tag to add.<br> Get it from the Get Tags API (the `id` field in the response). |
|&emsp; tags.`remove` |	JSONArray<br>*Array size: 0 to 5,000* |	| The tags to remove from the project.|
|&emsp;&emsp; tags.remove[].`id` |	String<br>*Maximum length: 30* |Optional |	The identifier of the tag to remove.<br> Get it from the Get Tags API (the `id` field in the response). |
|&emsp; tags[].`id`	| String<br>*Maximum length: 30* |	Optional | The identifier of the tag.<br> Get it from the Get Tags API (the `id` field in the response). |
| `copy_from` | 	Integer | 	Optional | The ID of the template or existing project to copy the new project from.<br> Get it from the Get All Projects API (the `id` field in the response). |
| `business_hours_id` |	String	| Optional | The business hours ID.<br>  Get it from the Get Business Hours API (the `id` field in the response). |
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