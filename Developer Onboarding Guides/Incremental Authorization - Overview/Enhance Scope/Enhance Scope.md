# Enhance scope

Use the scope enhancement request to add additional scopes to a refresh token.

**Endpoint:** `GET {accounts-server-url}/oauth/v2/token/addextrascope`

> **Note:** The accounts-server-url depends on the datacenter where your app is registered.

## Query parameters
| Parameter	| Description |
| :---        | :----  |
| `client_id`	| *Required*.<br> The unique ID of your app. You can find it in the API console. |
| `response_type` |	*Required*.<br> Set this parameter to `update_scopes`. |
| `redirect_uri`	| *Required*.<br> The URI that the authorization server redirects the browser to with a success or failure response. It must match the URI that you provided when you registered the app in the API console, and it must start with http:// or https://.<br> For example: `https://www.victa.com/oauthredirect` |
| `scope` | *Required*.<br> The list of additional scopes for the resource you want to access from the user’s account. The user sees the scopes when your app asks for consent.<br> For example: `SmartHiveProductMaster.settings.READ` |
| `enhance_token`	*Required*.<br> The scope enhancement token you received in response to the previous request (step 1). |
| `logout` |	*Required*.<br> If you want the user’s session to end after the user grants or rejects the permission, set this parameter to `true`. |

**Request example**
```
https://accounts.smarthive.in/oauth/v2/token/addextrascope
?response_type=update_scopes
&client_id=1000.HRLOVZ0544JSAZ14OQ1NHYHZBTL3SGR
&redirect_uri=https://victa.com/oauthredirect
&scope=SmartHiveProductMaster.settings.READ,SmartHiveAssetMaster.settings.READ,SmartHiveStationTracker.settings.READ.users.READ
&enhance_token=1000.e3b9859da1d36faf1e299889f6354da75.d83c513417fdfsdg514fb9ee38a6775fd50
&logout=true
```
## Response parameters

After the authorization server authenticates the user, it shows the user the permissions your app is requesting. When the user grants permission, the server adds the additional scopes to the refresh token 
and returns a success response. If the user rejects the permissions, the server returns a failure response.

**Response example**

Success Response: `https://www.victa.com/oauthredirect?status=success&scope_enhanced=true`

failure Response: `https://www.victa.com/oauthredirect?error=access_denied`