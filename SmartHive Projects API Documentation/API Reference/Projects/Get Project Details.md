# Get project details

Get a project details in the SmartHive Projects portal.

**Method and endpoint:** `GET /api/v3/portal/[PORTALID]/projects/[PROJECTID]`

**OAuth scope:** SmartHiveProjects.projects.READ

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
|`portal_id` | String<br>*digits only[0-9]+* | Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the Get All Portals with Details API (the `id` field in the response). |
|`project_id` | String<br>*digits only[0-9]+* | Required | The unique, immutable identifier of the project in the sepcified portal.<br>Get it from the Get All Projects API (the `id` field in the response). |

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