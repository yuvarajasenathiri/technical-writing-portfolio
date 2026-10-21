# Get all projects

Get the list of all projects in the SmartHive Projects portal.

**Method and endpoint:** `GET /api/v3/portal/[PORTALID]/projects`

**OAuth scope:** SmartHiveProjects.projects.READ

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/739121528/projects?page=1&per_page=10&%22filter%22=%7B%22criteria%22%3A%5B%7B%22cfid%22%3A%224000000000242%22%2C%22field_name%22%3A%22project%22%2C%22criteria_condition%22%3A%22contains%22%2C%22value%22%3A%5B%221752587000000097269%22%5D%2C%22relative_columns%22%3A%5B%7B%22cfid%22%3A%224000000000242%22%2C%22field_name%22%3A%22project%22%2C%22offset%22%3A%221%22%2C%22unit%22%3A%22days%22%2C%22prior%22%3A%22before%22%7D%5D%7D%5D%2C%22pattern%22%3A%221+AND+2%22%7D&sort_by=ASC%28last_modified_time%29&view_id=23806000074760021' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
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
**Query parameters**

| Name |	Data type |	Description |
| :---        | :----  |      :---- |
| `page` |	int |	The page number. |
| `per_page` |	int |	The number of entries to display on each page. |
| `filter` |	JSONObject |	The filter criteria for retrieving specific projects.<br>The filter is a JSON object that contains a list of conditions (`criteria`) and a logical `pattern` that defines how the conditions are combined.|
> | `criteria` |	JSONArray <br>*Maximum length: 10,000.* <br> *Array size: 0 or greater.* | A list of filter conditions.<br> Each condition specifies a field, a condition type, and a value to match. You can combine multiple conditions by using the pattern property, which references each condition by its position, starting from 1. |
> | `pattern` |	String <br> *Maximum length: 300.* | The logical expression that defines how the criteria are combined. <br> Use condition numbers (starting from 1) with the `AND` and `OR` operators and parentheses for grouping. For example, use `1` for a single condition, `1` AND `2` for both conditions, `1` OR `2` for either condition, and `(1 OR 2) AND 3` for grouped logic.|
| `sort_by`	| String	| The sort order for the results.<br>Wrap the field API name in `ASC()` for ascending order or `DESC()` for descending order. For example, `ASC(start_date)` sorts by start date in ascending order, and `DESC(created_time)` sorts by creation time in descending order. |
| `view_id` |	long |	The ID of a saved custom view to apply.<br>When you include it, the API applies the saved view’s filter criteria, columns, and sort order. <br>If you also include a `filter`, the API combines the filter conditions (AND) with the custom view’s criteria.  |

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
    "email" : "john@zylker.com"
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
    "email" : "john@zylker.com"
  },
  "created_time" : "2024-09-30T10:30:00.000Z",
  "updated_by" : {
    "id" : "6000000002069",
    "zpuid" : "7000000002083",
    "name" : "John Doe",
    "email" : "john@zylker.com"
  },
  "modified_time" : "2025-01-15T14:20:00.000Z"
} ]
```
