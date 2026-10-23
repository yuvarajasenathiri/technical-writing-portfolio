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
		"remove":[{"id":"4000000062001"}],
			"id":"4000000062001"}],
	"business_hours_id":"7000000197013"
 }'