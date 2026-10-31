# Module fields

This module covers operations related to managing fields in SmartHive Projects modules. Use the Module Fields API to get field details, create fields, update fields, delete fields, and associate fields 
with layouts.

## Get field info for a custom module

Use this endpoint:
- To retrieve the list of fields in a module, along with their metadata, such as API name, display name, and field type. 
- To understand the structure of a module before you create or update records.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/settings/fields`

**OAuth scope:** *SmartHiveProjects.custom_fields.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details-API) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/settings/fields?module=projects&filter=%7B%22is_mandatory%22%3A%22-%22%2C%22is_renamed%22%3A%22-%22%2C%22is_default%22%3A%22-%22%2C%22is_unassociated%22%3A%22-%22%2C%22is_association_info_needed%22%3A%22-%22%2C%22is_formula_based_list%22%3A%22-%22%2C%22layout_id%22%3A%22-%22%2C%22project_id%22%3A%2223806000097545166%22%2C%22field_ids%22%3A%22-%22%2C%22fields%22%3A%22-%22%2C%22search_term%22%3A%22-%22%7D&page=1&per_page=10' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `module` |	String	| Required | The API name or ID of the module. Get it from the [Get Modules API](#get-modules) (the `id` field in the response). |
| filter |	JSONObject| Optional |	The filter criteria for refining the results.<br> You can combine multiple filter conditions. |
| &emsp; filter.`is_mandatory`	| Boolean |	| Whether the field is mandatory.<br> Accepted values: `true` or `false`. |
| &emsp; filter.`is_renamed` |	Boolean	| | Whether the field was renamed.<br> Accepted values: `true` or `false`. |
| &emsp; filter.`is_default` |	Boolean | 	| Whether the field is a default field.<br> Accepted values: `true` or `false`. |
| &emsp; filter.`is_unassociated` | Boolean | 	| Whether the field is unassociated.<br> Accepted values: `true` or `false`. |
| &emsp; filter.`is_association_info_needed` |	Boolean |	| Whether to include association information.<br> Accepted values: `true` or `false`. |
| &emsp; filter.`is_formula_based_list` |	Boolean	| | Whether to return the list of fields that formula fields can use.<br> Accepted values: `true` or `false`. |
| &emsp; filter.`layout_id`	| String |	| The layout ID.|
| &emsp; filter.`project_id`	| String |	| The project ID.|
| &emsp; filter.`field_ids` |	JSONArray<br>*Maximum length: 10,000*<br>*Array size: 0 or 50*| 	| The field IDs. |
| &emsp; filter.`fields`	| JSONArray<br>*Maximum length: 10,000*<br>*Array size: 0 or 50*|	| The field API names. |
| &emsp; filter.`search_term` |	String |	| A keyword to search fields by name. |
| page |	Integer<br>*Default: 1* |	| The page number. |
| per_page |	Integer<br>*Limit: 1 to 200*<br>*Default: 1,000* |	| The number of entries to display on each page. |

**Sample input**
```
module : "projects"
filter : {
  "is_mandatory" : "-",
  "is_renamed" : "-",
  "is_default" : "-",
  "is_unassociated" : "-",
  "is_association_info_needed" : "-",
  "is_formula_based_list" : "-",
  "layout_id" : "-",
  "project_id" : "23806000097545166",
  "field_ids" : "-",
  "fields" : "-",
  "search_term" : "-"
}
page : 1
per_page : 10
```
**Sample response**
- 200 Ok
```
[ {
  "id" : "7000000309482",
  "field_name" : "name",
  "display_name" : "Name",
  "field_type" : "singleline",
  "is_default" : true,
  "field_property" : {
    "field_type_properties" : {
      "max_length" : 100
    },
    "is_pii" : false,
    "is_encrypted" : false,
    "metadata_property" : {
      "is_property_mutable" : false,
      "is_removable" : false,
      "is_mandate_enabled" : false,
      "has_field_level_permission" : false
    },
    "scope" : "global_scope"
  },
  "is_deactivated" : false
} ]
```
----
