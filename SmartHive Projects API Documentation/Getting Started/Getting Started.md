# Getting Started

### Mandatory Headers

SmartHive Projects APIs require a mandatory header.

1. `Authorization`: The OAuth access token to authenticate the user accessing data.

**Example**
```
curl -X GET https://projects.smarthive.com/api/v3/portal/{portal_id}/tasks  
-H "Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa"
```