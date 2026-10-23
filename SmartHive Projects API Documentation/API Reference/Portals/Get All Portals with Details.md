# Get all portals with details

Get all portals that the current user can access, along with their details.

This is an enhanced version of the Get All Portals API. Each portal object includes metadata such as the company name, logo URL, time zone, and environment, and the plan information is grouped in the 
`plan_details object`.

**Method and endpoint:** `GET /api/v3/portals`

**OAuth scope:** *SmartHiveProjects.portals.READ*

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portals?status=active&environment=production' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Query parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
|`status` | String<br>*regex: active, inactive* | Optional | The status of the portals to return. <br> Accepted values: `active` or `inactive`.<br> If you omit this parameter, the API returns portals of every status. |
|`environment` | String<br>*regex: sandbox, production* | Optional| The environment of the portals to return.<br> Accepted values: `sandbox` or `production`.<br> If you omit this parameter, the API returns portals from every environment. |

**Sample input**
```
status : "active"
environment : "production"
``` 
**Sample response**
- 200 Ok
```
{
  "portals" : [ {
    "id" : "26828068",
    "name" : "victaportal",
    "environment" : "production",
    "url" : "https://projects.smarthive.com/portal/victaportal",
    "logo_url" : "https://static.smarthivecdn.com/projects/images/svg/productlogo/zps-logo-default_9f9ca_.svg",
    "timezone" : "Europe/Dublin",
    "is_default_portal" : false,
    "company_name" : "victaportalsmarthivedotcom",
    "profile" : {
      "name" : "Portal Owner",
      "id" : "9000000002844"
    },
    "owner" : {
      "zuid" : 23163805,
      "zpuid" : "6000000002407",
      "name" : "Portal System",
      "first_name" : "Portal System",
      "last_name" : "",
      "full_name" : "Portal System",
      "email" : "admin@victa.com"
    },
    "plan_details" : {
      "project_plan" : "Enterprise",
      "bug_plan" : "Enterprise"
    }
  } ]
}
```