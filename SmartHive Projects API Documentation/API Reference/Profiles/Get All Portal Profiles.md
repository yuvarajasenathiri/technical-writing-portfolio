# Get all portal profiles

Use this endpoint to retrieve all profiles in a specific portal and their configurations.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/profiles`

**OAuth scope:** *SmartHiveProjects.portals.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details-API) (the `id` field in the response).|

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
| &emsp;&emsp; filter.criteria[].`module_name`|	String |	The module name. |
| &emsp;&emsp; filter.criteria[].`criteria_condition` |	String<br>*Maximum length: 25* |	| The condition for the criteria.<br> For example, `is`, `contains`, or `greater_than`. | 
| &emsp;&emsp; filter.criteria[].`value` |	JSONArray<br>*Maximum length: 10,000*<br>*Array size: 0 or greater* |	The values for the criteria condition. You can provide multiple values. |
| &emsp; filter.`pattern`|	String<br> Maximum length: 300.|	| The logical pattern that combines the filter conditions. For example, `1` AND `2`.| 
| `ids` |	String| 	| The profile IDs. |

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