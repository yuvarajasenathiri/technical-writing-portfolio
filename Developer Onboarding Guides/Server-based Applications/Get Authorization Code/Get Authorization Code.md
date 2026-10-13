# Get authorization code

Request an authorization code from the authorization server. Specify the scopes you need permission for. The user sees the permissions you’re requesting. If the user grants permission, the authorization 
server sends an authorization code to the redirect URL. The code is valid for 2 minutes.

**Endpoint:** `GET {accounts-server-url}/oauth/v2/auth`

> **Note:** The accounts-server-url depends on the datacenter where your app is registered.

## Query parameters
| Parameter |	Description |
| :---        | :----  | 
| `client_id` |	*Required*.<br> The unique ID of your app. You can find it in the API console.
| `response_type` |	*Required*.<br> Set this parameter to `code`.
| `redirect_uri` |	*Required*.<br> The URI that the authorization server redirects the browser to with the authorization code. It must match the URI that you provided when you registered the app in the API console, and it must start with http:// or https://.<br> For example: `https://www.victa.com/oauthredirect`
| `scope` |	*Required*.<br> The scope of the resource you want to access from the user’s account. The user sees the scopes when your app asks for consent.<br> For example: `SmartHiveProductMaster.settings.READ`
| `access_type` |	*Optional*.<br>  Specifies whether your app can refresh the access token on its own after it expires, without user intervention. If the value is `online`, the app gets only an access token and can’t refresh it after it expires. If the value is `offline`, the app also gets a refresh token the first time it requests an access token. The app can store the refresh token and use it to refresh the access token when needed.<br> Default value: `online`
| `prompt` |	*Optional*.<br> If you include this parameter, your app asks the user for consent every time it requests access to the resource. If you don’t include it, the app asks only the first time. The value must be `consent`.

**Request example**
```
https://accounts.smarthive.com/oauth/v2/auth
?response_type=code
&client_id=1000.GMB0YULZHJK411284S8I5GZ4CHUEX0
&scope=SmartHiveProductMaster.settings.READ
&redirect_uri=https://www.victa.com/oauthredirect
&access_type=offline
&prompt=consent
```
## Response parameters

After the authorization server authenticates the user, it shows the user the permissions your app is requesting. When the user grants permission, the server sends the authorization code to the `redirect_uri`.

| Parameter |	Description |
| :---        | :----  |
| `code` |	The authorization code that you can exchange for an access token. The code is valid for 2 minutes and can be used only once. |
| `location` |	The datacenter (DC) where the user’s account is stored. If the user’s DC is different from your app’s DC, turn on multi DC support and make the access token request to the user’s DC.|

**Response example**
```
https://oauth.pstmn.io/v1/browser-callback
?code=1000.a1110799eac53c491fee9efef8246535.df7da86ff64daa66413e2899e9b7fad7
&location=in
&accounts-server=https://accounts.smarthive.in
```
## Error codes
| Error	| Reasons |
| :---        | :----  |
| `access_denied` |	The user rejected the request for access. |
| `Invalid Client` | The `client_id` value isn’t valid.<br> The `response_type` value isn’t correct. It must be `code`. |
| `Invalid response type` |	The `client_id` parameter is missing.<br> The `response_type` parameter is missing.|
| `Invalid OAuth scope` |	The `scope` parameter is missing, or the scope doesn’t exist. |
| `Invalid Redirect Uri` |	The `redirect_uri` parameter is missing, or the URI doesn’t match the one configured in the API console. |
| `An error occurred/500 server error` |	The `response_type` value isn’t valid. It must be `code`.
| `400 not found` |	The `HTTP` method isn’t correct. It must be `GET`. |