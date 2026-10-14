# Get scope enhancement token

Get a scope enhancement token from the authorization server. Send the refresh token that you want to add the additional scopes to.

**Endpoint:** `POST {accounts-server-url}/oauth/v2/token/scopeenhance`

> **Note:** The accounts-server-url depends on the datacenter where your app is registered.

## Query parameters
| Parameter	| Description |
| :---        | :----  | 
|`client_id` |	*Required*. The unique ID of your app. You can find it in the API console.|
| `client_secret` |	*Required*. The unique secret for your app, known only to your app and SmartHive. You can find it in the API console. |
| `grant_type`	| *Required*. Set this parameter to `update_scopes_token`.|
| `refresh_token` |	*Required*. The refresh token that you want to add the additional scopes to.|

**Request example**
```
https://accounts.smarthive.in/oauth/v2/token/scopeenhance
?grant_type=update_scopes_token
&client_id=1000.HRLOVZ0U6LSAZ14OQHYZYTZBTL3SGR
&client_secret=fa10d952be6bd6654cbb6b5fe271042de9546541e781
&refresh_token=1000.0d50a4d6a383005cc1f899968b9f9d97.2183743f8798bea2f71e193e34e37ef0d
```
##  Response parameters
| Parameter |	Description |
| :---        | :----  | 
| `access_token` |	The scope enhancement token. Use it to add additional scopes to a refresh token. |
| `token_type` |	The type of token that’s generated. |
| `expires_in` |	The time, in seconds, until the scope enhancement token expires. |

**Response example**
```
{
"access_token": "1000.f95a0db717f52b825e3f94654f651.ced2cf4e786cf04c0e91daee545jh51cd",
"token_type": "update_scope",
"expires_in": 600
}
```
## Error codes
| Error	| Reasons |
| :---        | :----  | 
| `invalid_client`	 | The accounts-server URL isn’t valid. Check whether the URL matches the user’s datacenter location. See all accounts-server URLs.<br> The `client_id` parameter is missing, or its value isn’t valid.<br> The `grant_type` value isn’t valid. It must be `update_scopes_token`.<br>The `grant_type` parameter is missing.|
| `invalid_client_secret` |	The `client_secret` parameter is missing, or its value isn’t valid. |
| `invalid_code` |	The `refresh_token` parameter is missing, or its value isn’t valid or was already used.<br> The `grant_type` value isn’t correct. It must be `update_scopes_token`.|
| `400 Bad Request` |	The `HTTP` method isn’t correct. It must be `POST`.|