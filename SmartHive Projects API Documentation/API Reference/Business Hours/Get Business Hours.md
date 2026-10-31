# Business hours

This module covers operations related to business hours in SmartHive Projects. Use the Business Hours API to create, update, and delete business hours.

## Get business hours

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
| &emsp; filter.`criteria`	| JSONArray<br>*Maximum length: 10,000*<br>*Array size: 0 or greater* | Optional | The criteria information.|
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
      "email" : "matthew.hayes@zylker.com",
      "zuid" : 22823316
    },
    "id" : "4000000066053",
    "is_default" : false,
    "created_by" : {
      "zpuid" : "4000000002379",
      "full_name" : "Matthew Hayes",
      "email" : "matthew.hayes@zylker.com",
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
