# Getting started

## Mandatory headers

SmartHive Projects APIs require the `Authorization` header. The header contains the OAuth access token that authenticates the user who accesses the data.

**Example:**
```
curl -X GET https://projects.smarthive.com/api/v3/portal/{portal_id}/tasks  
-H "Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa"
```