# Module layouts

## Get a layout list

Use this endpoint to:
- Retrieve the list of layouts in a module. 
- Identify layout IDs before you perform layout-level operations, such as updating layouts, adding fields, or managing sections.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/settings/layouts`

**OAuth scope:** *SmartHiveProjects.custom_fields.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details-API) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/settings/layouts?module=projects&index=1&range=100&page=1&per_page=10&filter=%7B%22is_association_info_needed%22%3A%22true%22%2C%22is_current_user_profile_associated%22%3A%22true%22%2C%22search_term%22%3A%22Zoho+Projects%22%2C%22search_by%22%3A%22project%22%7D' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `module` |	String |	Required | The API name or ID of the module.<br> Get it from the [Get Modules API](#get-modules)(the `id` field in the response).|
| `index` |	Integer | Optional |	The index of the layouts. |
| `range` |	Integer | Optional |	The range of the layouts. |
| `page`	| Integer<br>*Default: 1* |	Required | The page number. |
| `per_page` |	Integer<br>*Limit: 1 to 200*<br> *Default: 100* |	Required | The number of entries to display on each page. |
| `filter`	| JSONObject | Optional |	The filter criteria for refining the results.<br> You can combine multiple filter conditions. |
| &emsp; filter.`is_association_info_needed` | 	Boolean |	| Whether to include the association details.<br> Accepted values: `true` or `false`. |
| &emsp; filter.`is_current_user_profile_associated` |	Boolean	| | Whether the current user’s profile is associated.<br> Accepted values: `true` or `false`. |
| &emsp; filter.`search_term` |	String |	| The search term. |
| &emsp; filter.`search_by`	| String | | The field to search by.<br> Accepted values: `project`, `layout`, or `id`.

**Sample input**
```
module : "projects"
index : 1
range : 100
page : 1
per_page : 10
filter : {
  "is_association_info_needed" : "true",
  "is_current_user_profile_associated" : "true",
  "search_term" : "Smarthive Projects",
  "search_by" : "project"
}
```
** Sample Response**
- 200 Ok
```
[ {
  "associated_entities_count" : 2,
  "associated_entities" : [ {
    "name" : "Admin",
    "id" : "9000000002510"
  }, {
    "name" : "Manager",
    "id" : "9000000002513"
  } ],
  "name" : "New Layout 1",
  "id" : "9000000071079",
  "is_default" : false,
  "type" : "PUBLIC"
}, {
  "associated_entities_count" : 2,
  "associated_entities" : [ {
    "name" : "Admin",
    "id" : "9000000002510"
  }, {
    "name" : "Manager",
    "id" : "9000000002513"
  } ],
  "name" : "New Layout 2",
  "id" : "9000000054069",
  "is_default" : false,
  "type" : "PUBLIC"
} ]
```
**Possible errors**
- InVALID_PARAMETER_VALUE `HTTP 400`
```
{
  "error" : {
    "status_code" : 400,
    "instance" : "/api/v3/portal/25450296/settings/layouts",
    "method" : "GET",
    "error_type" : "FIELDS_VALIDATION_ERROR",
    "details" : [ {
      "message" : "Invalid module",
      "field_name" : "module"
    } ],
    "title" : "INVALID_PARAMETER_VALUE"
  }
}
```
