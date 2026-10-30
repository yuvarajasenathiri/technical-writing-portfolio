# Restore a project

Retore a project from the trash in the SmartHive Projects portal.

**Method and endpoint:** `POST /api/v3/portal/[PORTAL_ID]/projects/[PROJECT_ID]/restore`

**OAuth scope:** *SmartHiveProjects.projects.UPDATE*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the Get All Portals with Details API (the `id` field in the response).| 
| `project_id` | String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the project in the sepcified portal.<br>Get it from the Get All Projects API (the `id` field in the response). |

**Request example**
```
curl -X POST \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/projects/23806000097545166/restore' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Sample response**
- 204 No content