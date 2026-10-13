# Get access token

Request an access token from the authorization server. Specify the scopes you need permission for. The user sees the permissions you’re requesting. If the user grants permission, the authorization server 
sends an access token to the redirect URL. The access token is valid for 1 hour.

**Endpoint:** `GET {accounts-server-url}/oauth/v2/auth`

> **Note:** The accounts-server-url depends on the datacenter where your app is registered.

## Query parameters
| Parameter |	Description |
| :---        | :----  | 
| `client_id` |	*Required*.<br> The unique ID of your app. You can find it in the API console.|
| `response_type` |	*Required*.<br> Set this parameter to `token`.|
| `redirect_uri` |	*Required*.<br> The URI that the authorization server redirects the browser to with the access token. It must match the URI that you provided when you registered the app in the API console, and it must start with http:// or https://.<br> For example: `https://www.victa.com/oauthredirect`
| `scope` |	*Required*.<br> The scope of the resource you want to access from the user’s account. The user sees the scopes when your app asks for consent.<br>For example: `SmartHiveProductMaster.settings.READ` |

**Request example**
```
https://accounts.smarthive.com/oauth/v2/auth
?response_type=token
&client_id=1000.GMB0YULZHJK411284S8I5GZ4CHUEX0
&scope=SmartHiveProductMaster.settings.READ
&redirect_uri=https://www.victa.com/oauthredirect
```
## Response parameters

After the authorization server authenticates the user, it shows the user the permissions your app is requesting. When the user grants permission, the server sends the access token to the `redirect_uri`.

| Parameter |	Description |
| :---        | :----  | 
| `access_token` |	The token your app uses to access the resources defined by the requested scopes. The token is valid for 1 hour. |
| `api_domain` |	The domain your app sends API requests to when it accesses protected resources.|
| `location`| 	The datacenter (DC) where the user’s account is stored. |
| `expires_in` |	The time, in seconds, until the access token expires. An access token lasts 1 hour (3,600 seconds). |
| `granted_for_session` |	Whether the user granted permission for your app to refresh the access token. The value is `true` if the user granted permission.<br>If the user doesn’t grant permission, the response doesn’t include this parameter. In that case, your app must prompt the user to authenticate again to get a new access token. |

**Response example**
```
https://www.victa.com/oauthredirect 
#access_token=1000.2350e7afbb173426e5fe3e5977db2f69.0cddd2403ee2e6309d44e7007bf21c05 
&expires_in=3600 
&location=in 
&api_domain=https://www.smarthiveapis.in
&granted_for_session=true
```

## Error codes
|Error	| Reasons |
| :---        | :----  | 
| `access_denied` |	The user rejected the request for access. |
| `Invalid Client` |	The `client_id` value isn’t valid.<br>The `response_type` value isn’t correct. It must be `token`.|
| `Invalid response type` |	The `client_id` parameter is missing.<br>The `response_type` parameter is missing. |
| `Invalid OAuth scope` |	The `scope` parameter is missing, or the scope doesn’t exist.|
| `Invalid Redirect URI` |	The `redirect_uri` parameter is missing, or the URI doesn’t match the one configured in the API console. |
| `An error occurred/400 Bad Request` |	The `response_type value` isn’t valid. It must be `token`.|
| `400 Bad Request` |	The `HTTP` method isn’t correct. It must be `GET`.|