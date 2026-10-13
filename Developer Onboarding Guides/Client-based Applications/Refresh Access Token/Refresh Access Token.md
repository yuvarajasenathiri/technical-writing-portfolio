# Refresh access token

When the access token expires, your app can get a new one without user intervention if the session is active and the user granted permission for the app to refresh the token.

If the user grants permission, the response to the access token request includes the `granted_for_session` parameter with the value `true`. Otherwise, the response doesn’t include this parameter.

**Endpoint:** `GET {accounts-server-url}/oauth/v2/auth/refresh`

> **Note:** The accounts-server-url depends on the datacenter where your app is registered.

**Token refresh behavior:**

- If the user granted permission and the session is active, send a request to the `oauth/v2/auth/refresh` endpoint to get a new access token.
- If the user didn’t grant permission, or the session expired or ended, prompt the user to authenticate again to get a new access token.

## Query parameters
| Parameter	| Description |
| :---        | :----  |
| `client_id` |	*Required*.<br> The unique ID of your app. You can find it in the API console. |
| `response_type` |	*Required*.<br> Set this parameter to `token`. |
| `redirect_uri` |	*Required*.<br> The URI that the authorization server redirects the browser to with the access token. It must match the URI that you provided when you registered the app in the API console, and it must start with http:// or https://.<br> For example:`https://www.zylker.com/oauthredirect` |
| `scope` |	*Required*.<br> The scopes to include in the new access token. You can include only scopes that the user granted in the `oauth/v2/auth` request. You can’t add new scopes. |

**Request example**
```
https://accounts.smarthive.com/oauth/v2/auth/refresh
?response_type=token
&client_id=1000.GMB0YULZHJK411284S8I5GZ4CHUEX0
&redirect_uri=https://www.victa.com/oauthredirect
&scope=SmartHiveProductMaster.settings.READ
```
## Response parameters

After the authorization server verifies your app, it sends the access token to the redirect_uri.

| Parameter |	Description |
| :---        | :----  |
| `access_token` |	The token your app uses to access the resources defined by the requested scopes. The token is valid for 1 hour. |
| `api_domain` |	The domain your app sends API requests to when it accesses protected resources. |
| `location` |	The datacenter (DC) where the user’s account is stored. |
| `expires_in`	The time, in seconds, until the access token expires. An access token lasts 1 hour (3,600 seconds). |

**Response example**
```
https://www.victa.com/oauthredirect
#access_token=1000.2350e7afbb173426e5fe3e5977db2f69.0cddd2403ee2e6309d44e7007bf21c05
&expires_in=3600
&location=in
&api_domain=https://www.smarthiveapis.in
```
## Error codes
| Error |	Reasons |
| :---        | :----  |
| `client_not_granted` |	The user didn’t grant permission for the entire session, so the access token can’t be refreshed.<br> The session ended.|
| `prompt_required` |	At least one scope in this request wasn’t granted in the initial `oauth/v2/auth` request. In a refresh request, you can include only scopes that the user already approved. |
| `OAuthErrorCode.invalid_scope` |	The `scope` parameter is missing. |
| `general_error` |	At least one of the included scopes doesn’t exist. |
| `An error occurred/40 Bad Request` |	The `client_id` parameter is misspelled.<br> The `response_type` value isn’t valid.<br>The `redirect_uri` parameter is misspelled.<br>The `HTTP` method isn’t correct. It must be `GET`.|
| `OAuthErrorCode.invalid_client` |	The `client_id` parameter is missing, or its value isn’t valid.<br> The `response_type parameter` is missing, or its value isn’t correct. It must be `token`. |
| `OAuthErrorCode.invlid_redirect_uri` |	The `redirect_uri` parameter is missing, or the URI doesn’t match the one configured in the API console. |