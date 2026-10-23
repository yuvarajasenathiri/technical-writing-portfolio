# Create project

Create a project in the SmartHive Projects portal.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/projects`

**OAuth scope:** SmartHiveProjects.projects.CREATE

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects. Get it from the Get All Portals with Details API (the `id` field in the response).| 

**Request example**
```
curl -X POST \
 'https://projects.zoho.com/api/v3/portal/[PORTAL_ID]/projects' \
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
			"id":"4000000062001"}],
		"remove":[{
			"id":"4000000062001"}],
		"id":"4000000062001"}],
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
| `owner.zpuid`|	String|	Required | The user ID of the project owner.<br> Get it from the Get Portal Users API (the `id` field in the response).
| `is_public_project` | 	boolean	| Optional | Whether the project is public.<br> Accepted values: `true` or `false`. |
| `start_date`	| String<br> *format:YYYY-MM-DD* | Optional |	The start date of the project.|
| `end_date` |	String<br>*format:YYYY-MM-DD* |Optional |	The end date of the project. |
| `status` | 	JSONObject<br>  *Maximum length: 1,000*| 	| The status of the project.| 
| `status.id` | 	String<br>*Maximum length: 30* | Optional |	The identifier of the status.<br> Get it from the Get Global Statuses API.|
| `layout`	| JSONObject<br>*Maximum length: 1,000*	| |The project layout details.|
| `layout.id` |	String<br>*Maximum length: 30*| Optional |	The identifier of the layout.<br> Get it from the Get Layouts API (the `id` field in the response). |
| `added_via` |	String | Optional |	The source of the project.<br> Accepted values: `web` or `api`. |
| `is_rollup_project` | 	boolean	| Optional | Whether the project is a roll-up project.<br> Accepted values: `true` or `false`.  |
| `budget_info` | 	JSONObject<br> *Maximum length: 80,000* | 	| The project budget details.|
| > `budget_info.billing_method` |	String | 	| The billing method.<br> Accepted values: `project_hours`, `staff_hours`, `fixed_cost`, `issue_hours`, or `task_or_issue_hours`.
budget_info.budget_type	String	The budget type. Accepted values: none, based_on_project, based_on_milestone, based_on_task, or based_on_user.
budget_info.tracking_method	String	The tracking method. Accepted values: project_hours, staff_hours, issue_hours, or task_or_issue_hours.
budget_info.currency	String	The currency.
budget_info.cost_budget	JSONObject	The budget details for the project.
budget_info.cost_budget.amount	double	The cost budget amount.
budget_info.hourly_budget	String	The hourly budget details.
budget_info.rate_per_hour	JSONObject	The rate per hour.
budget_info.rate_per_hour.amount	double	The amount of the rate per hour.
budget_info.cost_budget_threshold	JSONObject	The budget threshold details.
budget_info.cost_budget_threshold.amount	double	The cost budget threshold amount.
budget_info.hourly_budget_threshold	String	The hourly budget threshold details.
budget_info.fixed_cost	JSONObject	The fixed cost.
budget_info.fixed_cost.amount	double	The fixed cost amount.
budget_info.cost_per_hour	JSONObject	The cost per hour for the project.
budget_info.cost_per_hour.amount	double	The amount of the cost per hour.
budget_info.revenue_budget	JSONObject	The revenue budget.
budget_info.revenue_budget.amount	double	The revenue budget amount.
budget_info.budget_threshold	JSONObject	The budget threshold details.
budget_info.budget_threshold.amount	double	The budget threshold amount.
project_group	JSONObject	The project group details. Maximum length: 1,000.
project_group.id	String	The identifier of the project group. Maximum length: 30. Get it from the Get Project Groups API (the id field in the response).
sub_module_settings	JSONObject	The sub-module settings, which declare sub-module configurations.
sub_module_settings.sub_module_layouts_configuration	JSONObject	The sub-module layouts.
tags	JSONArray	The tags for the project. Maximum length: 10,000.
tags.add	JSONArray	The tags to add to the project. Array size: 0 to 5,000.
tags.add[].id	String	The identifier of the tag to add. Maximum length: 30. Get it from the Get Tags API (the id field in the response).
tags.remove	JSONArray	The tags to remove from the project. Array size: 0 to 5,000.
tags.remove[].id	String	The identifier of the tag to remove. Maximum length: 30. Get it from the Get Tags API (the id field in the response).
tags[].id	String	The identifier of the tag. Maximum length: 30. Get it from the Get Tags API (the id field in the response).
copy_from	int	The ID of the template or existing project to copy the new project from. Get it from the Get All Projects API (the id field in the response).
business_hours_id	String	The business hours ID. Get it from the Get Business Hours API (the id field in the response).
<field_name>	String	The value of a project custom field. Replace <field_name> with the custom field’s API name in snake_case, as listed in the Custom Fields Guide.
Note: The type shows as String by default because most basic custom fields accept string values. The value format and input structure depend on the custom field type. For details, see the Custom Fields Guide.