# Get all users

Use this endpoint to retrieve all users in a project.

**Method and endpoint:** `GET /api/v3.1/portal/[PORTAL_ID]/projects/[PROJECT_ID]/users`

**OAuth scope:** *SmartHiveProjects.users.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br> Get it from the [Get All Portals with Details API](#get-all-portals-with-details-API) (the `id` field in the response).| 
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
| &emsp; filter.`criteria` | 	JSONArray<br>*Maximum length: 10,000*<br>*Array size: 0 or greater* |Optional	| The criteria information.
| &emsp;&emsp; filter.criteria.`module` | String | | The field module. |
| &emsp;&emsp; filter.criteria.`field_name` | String | | The field name. |
| &emsp;&emsp; filter.criteria.`module_name` | String | | The module name. |
| &emsp;&emsp; filter.criteria.`criteria_condition` | String<br>*Maximum length: 25* |  | The criteria condition.|
| &emsp;&emsp; filter.criteria.`value`| JSONArray<br>* Maximum length: 10,000*<br>*Array size: 0 or greater*	| | The criteria value. |
| &emsp; filter.`pattern` |	String<br>* Maximum length: 300* |	| The filter pattern.|
|`sort_by`	|String|	| The sort criteria.<br> Accepted values: `ASC(field_name)` or `DESC(field_name)`.<br> Available fields: `first_name`, `last_name`, `portal_profile`, `role`, `project_rate`, `project_cost_rate`, `business_hours`, `added_to_project_time`, `updated_in_project_time`, and `last_accessed_on`. |

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
    "email" : "katya.cavendish@zylker.com",
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
