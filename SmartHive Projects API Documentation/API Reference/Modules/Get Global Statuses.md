# Get global statuses

Use this endpoint:
- To retrieve the list of global statuses configured for a module, along with their metadata, such as status ID, name, color, type, and sequence order. 
- To identify status IDs before you perform status-based operations.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/settings/global-statuses`

**OAuth scope:** *SmartHiveProjects.custom_fields.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details-API) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/settings/global-statuses?module=-&filter=%7B%22status_ids%22%3A%22-%22%2C%22status_names%22%3A%22-%22%2C%22search_term%22%3A%22Zoho+Projects%22%7D&page=-&per_page=-' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| module |	String |	Required | The API name or ID of the module.<br> Get it from the [Get Modules API](#get-modules) (the `id` field in the response). |
| filter	| JSONObject	|Optional  |The filter criteria for refining the results.<br> Use only one filter property per request. |
| &emsp; filter.`status_ids` |	JSONArray| 	| The IDs of the statuses to get.|
| &emsp; filter.`status_names` |	JSONArray|	| The names of the statuses to get. |
| &emsp; filter.`search_term` |	String<br>*Maximum length: 100*| 	| The search term for filtering statuses by name. |
| `page` |	Integer | Optional |	The page number. |
| `per_page` |	Integer | Optional |	The number of entries to display on each page.|

**Sample input**
```
module :  - 
filter : {
  "status_ids" : "-",
  "status_names" : "-",
  "search_term" : "Zoho Projects"
}
page :  - 
per_page :  -
```
**Sample response**
- 200 Ok
```
[ {
  "id" : "5000000000500",
  "name" : "Open",
  "color" : "transparent",
  "color_hexcode" : "transparent"
}, {
  "id" : "5000000000521",
  "name" : "Cancelled",
  "color" : "transparent",
  "color_hexcode" : "transparent"
} ]
```
**Possible errors**
- INVALID_PARAMETER_VALUE `HTTP 400`
```
{
  "error" : {
    "status_code" : "400",
    "instance" : "/api/v3/portal/25450296/settings/global-statuses",
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