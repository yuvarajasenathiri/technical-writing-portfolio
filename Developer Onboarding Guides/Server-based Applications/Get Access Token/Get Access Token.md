# Get access token

Exchange the authorization code for an access token from the authorization server.

**Endpoint:** `POST {accounts-server-url}/oauth/v2/token`

> **Note:** The accounts-server-url depends on the datacenter where the user’s account is stored. This value is the `location` parameter in the response to the authorization request.

## Query parameters
| Parameter |	Description |
| :---        | :----  | 
| `client_id` |	*Required*.<br> The unique ID of your app. You can find it in the API console. |
| `client_secret` |	*Required*.<br> The unique secret for your app, known only to your app and SmartHive. You can find it in the API console. |
| `grant_type`	| *Required*. <br> Set this parameter to `authorization_code`.|
| `code`	| *Required*.<br> The authorization code you received in response to the authorization code request. |
| `redirect_uri` |	*Required*.<br> The redirect URI. It must match the URI that you provided when you registered the app in the API console, and it must start with http:// or https://.<br> For example: https://www.victa.com/oauthredirect

**Request example**
```
https://accounts.smarthive.com/oauth/v2/token
?client_id=1000.GMB0YULZHJK411248S8I5GZ4CHUEX0
&client_secret=122c324d3496d5d777ceeebc129470715fbb856b7
&grant_type=authorization_code
&redirect_uri=https://www.victa.com/oauthredirect
&code=1000.86a03ca5dbfccb7445b1889b8215efb0.cad9e1ae4989a1196fe05aa729fcb4e1
```
## Response parameters
| Parameter	| Description |
| :---        | :----  | 
| `access_token` |	The token your app uses to access the resources defined by the requested scopes. The token is valid for 1 hour. |
| `refresh_token` |	A token your app can use to refresh the access token after it expires. The response includes the refresh token if you set the `access_type` parameter to `offline` in the authorization code request (the first time you make it). |
| `api_domain`	| The domain your app sends API requests to when it accesses protected resources. |
| `token_type` | The type of access token that’s generated. SmartHive issues `Bearer` tokens. When your app makes API requests to access protected resources, send the access token in the `Authorization header`. **Syntax:** `Authorization: Bearer {access token}`
| `expires_in` |	The time, in seconds, until the access token expires. An access token lasts 1 hour (3,600 seconds). |

**Response example**
```
{   
"access_token":"1000.2deaf8d0c268e3c85daa2a013a843b10.703adef2bb337b8ca36cfc5d7b83cf24",
"refresh_token":"1000.18e983526f0ca8575ea9c53b0cd5bb58.1bd83a6f2e22c3a7e1309d96ae439cc1",
"api_domain":"https://api.smarthive.com",
"token_type":"Bearer",
"expires_in":3600
}
```
## Error codes
| Error |	Reasons |
| :---        | :----  | 
| `invalid_client` |	The accounts-server URL isn’t valid. Check whether the URL matches the user’s datacenter location. See all accounts-server URLs.<br> The `client_id` parameter is missing, or its value isn’t valid.<br>The `grant_type` value isn’t valid. It must be `authorization_code`.
| `invalid_client_secret` |	The `client_secret` parameter is missing, or its value isn’t valid. |
| `invalid_redirect_uri` |	The `redirect_uri` parameter is missing, or the URI doesn’t match the one configured in the API console.|
| `invalid_code` |	The `code` parameter is missing, or its value isn’t valid or was already used.<br> The `grant_type` value isn’t correct. It must be `authorization_code`.
| `400 Bad Request` |	The `HTTP` method isn’t correct. It must be `POST`.<br> The `grant_type` parameter is missing. |