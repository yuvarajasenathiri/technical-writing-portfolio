# Project groups

This module covers operations related to project groups in SmartHive Projects.

## Get a user’s project groups

Use this endpoint to retrieve the project groups associated with a user.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/my-project-groups`

**OAuth scope:** *SmartHiveProjects.projectgroups.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details-API) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/my-project-groups?page=1&per_page=10' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `page` |	Integer<br>*Default: 1*| Optional |	The page number. |
| `per_page` |	Integer<br>*Limit: 1 to 200*<br>*Default: 100* | Optional |	The number of entries to display on each page.| 

**Sample input**
```
page : "1"
per_page : "10"
```
**Sample response**
- 200 Ok
```
{
  "project-groups" : [ {
    "name" : "Ungrouped Projects",
    "id" : "4000000005417"
  } ]
}
```