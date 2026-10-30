# Get portal details

Get details of a specific SmartHive Projects portal.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]`

**OAuth scope:** *SmartHiveProjects.portals.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
|`portal_id` | String<br>*digits only[0-9]+* | Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the Get All Portals with Details API (the `id` field in the response). |

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
 ```
**Sample response**
- 200 Ok
```
{
  "portal_details" : {
    "owner" : {
      "zpuid" : "6000000002407",
      "full_name" : "Portal System",
      "name" : "Portal System",
      "last_name" : "",
      "id" : 23163805,
      "is_client_user" : false,
      "first_name" : "Portal System",
      "email" : "admin@victa.com"
    },
    "business_details" : {
      "start_time" : "00:00",
      "date_format" : "MM-dd-yyyy",
      "weekends" : [ ],
      "time_format" : "hh:mm aaa",
      "working_days" : [ "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" ],
      "week_start_day" : "SUNDAY",
      "end_time" : "24:00",
      "week_start_year" : "FIRST_DAY_OF_YEAR"
    },
    "logo_url" : "/images/svg/zps-logo-default.svg",
    "timezone" : "Europe/Dublin",
    "name" : "zylker",
    "id" : 26828068,
    "plan_details" : {
      "projects_service_plan" : "Free",
      "bugtracker_service_plan" : "Free"
    },
    "org_name" : "victaportalsmarthivedotcom",
    "is_customdomain_enabled" : false
  }
}
```