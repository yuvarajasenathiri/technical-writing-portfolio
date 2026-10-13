# Refresh access token

Use the refresh token to generate another access token for the same scopes.		

With a refresh token, your app can create up to 10 access tokens in 10 minutes. If your app reaches the limit, SmartHive blocks access token creation for the rest of the 10 minutes. For more information, 
see Token limits.

**Endpoint**: `POST {accounts-server-url}/oauth/v2/token`

> **Note:** The accounts-server-url depends on the datacenter where the user’s account is stored. This value is the `location` parameter in the response to the authorization request.

## Query parameters
| Parameter |	Description |
| :---        | :----  | 
| `client_id` |	*Required*.<br> The unique ID of your app. You can find it in the API console.|
| `client_secret` |	*Required*.<br> The unique secret for your app, known only to your app and SmartHive. You can find it in the API console.|
| `grant_type`	| *Required*.<br> Set this parameter to `refresh_token`.|
| `refresh_token` |	*Required*.<br> The refresh token you received in response to the access token request.|

**Request example**
```
https://accounts.smarthive.com/oauth/v2/token
?client_id=1000.GMB0YULZHJK411248S8I5GZ4CHUEX0
&client_secret=122c324d3496d5d777ceeebc129470715fbb856b7
&grant_type=refresh_token
&refresh_token=1000.86a03ca5dbfccb7445b1889b8215efb0.cad9e1ae4989a1196fe05aa729fcb4e1
```
## Response parameters
| Parameter	| Description |
| :---        | :----  | 
| `access_token` | The token your app uses to access the resources defined by the requested scopes. The token is valid for 1 hour. |
| `api_domain` | The domain your app sends API requests to when it accesses protected resources. |
| `token_type` | The type of access token that’s generated. SmartHive issues `Bearer` tokens. When your app makes API requests to access protected resources, send the access token in the `Authorization header`.<br> **Syntax:** `Authorization: Bearer {access token}` |
| `expires_in`| The time, in seconds, until the access token expires. An access token lasts 1 hour (3,600 seconds). |

**Response example**
```
{   
"access_token":"1000.2deaf8d0c268e3c85daa2a013a843b10.703adef2bb337b8ca36cfc5d7b83cf24",
"api_domain":"https://api.smarthive.com",
"token_type":"Bearer",
"expires_in":3600
}
```
## Error codes
| Error |	Reasons |
| :---        | :----  |
| `invalid_client` | The accounts-server URL isn’t valid. Check whether the URL matches the user’s datacenter location. See all accounts-server URLs.<br> The `client_id` parameter is missing, or its value isn’t valid.<br>The `grant_type` value isn’t valid. It must be `refresh_token`.|
| `invalid_client_secret` |	The `client_secret` parameter is missing, or its value isn’t valid. |
| `invalid_code` |	The `refresh_token` parameter is missing, or its value isn’t valid.<br>The `grant_type` value isn’t correct. It must be `refresh_token`.<br> The refresh token was already revoked. Learn more about revoking refresh tokens.|
| `400 Bad Request` |	The `HTTP` method isn’t correct. It must be `POST`.<br> The `grant_type` parameter is missing. |

## Send the request parameters

You can send the parameters in one of the following formats:

1. Query string: Send all parameters in the request URL as a query string.
**Example:**<br>
```
https://accounts.smarthive.com/oauth/v2/token?
client_id=1000.QVF8O5MXFUYATAQGJKEWUXJKZH7OOE
&grant_type=refresh_token
&client_secret=31a99ae27deff7fr34e419fe321b712a02cdedted7
&refresh_token=1000.3421ad0e1a6fe44663ea112b8b1c4fdf.cd38e645e3d7423651d17368855bc1c5
```
2. Request body: Send all parameters in the request body, using the form-data or x-www-form-urlencoded data type.
**Example:**<br>
```
client_id: 
"1000.QVF8O5MXFUYATAQGJKEWUXJKZH7OOE"
client_secret: 
"31a99ae27deff7fr34e419fe321b712a02cdedted7
"grant_type: 
"refresh_token"
refresh_token: 
"1000.3421ad0e1a6fe44663ea112b8b1c4fdf.cd38e645e3d7423651d17368855bc1c5"
```
3. Basic authentication header: Send only client_id and client_secret this way. Base64-encode the credentials before you send them.

**Encoding format:** `Base64encode(client_id:client_secret)`

**Header format:** `Authorization: Basic {Base64 encoded credentials}`

**Example:** 
```Authorization: Basic MTAwMC5RVkY4TzVNWEZVWUFUQVFHSktFV1VYSktaSDdPT0U6MzFhOTlhZTI3ZGVmZjdmcjM0ZTQxOWZlMzIxYjcxMmEwMmNkZWR0ZWQ3```