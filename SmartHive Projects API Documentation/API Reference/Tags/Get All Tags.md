# Tags

This module covers operations related to tags in SmartHive Projects. Use the Tags API to create and update tags, associate tags with modules and projects, and delete tags.

## Get all tags

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
| &emsp; filter.`criteria`	| JSONArray<br>*Maximum length: 10,000<br>*Array size: 0 or greater* | Optional 	| The criteria information.|
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