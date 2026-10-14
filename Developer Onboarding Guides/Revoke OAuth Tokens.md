# Revoke OAuth tokens

You can revoke OAuth tokens in two ways:

- Users can revoke them, or 
- Your app can revoke them programmatically.

## Users: 

Users can remove the tokens for apps they’ve granted permission to. To revoke a token:

1. Sign in at accounts.smarthive.com.
2. In the left menu, select **Sessions**, and then go to **Connected Apps**.
3. Hover over the app whose token you want to revoke, and select **Revoke Access**.
4. Select **Yes**, **Proceed**.

## Programmatically: 

Make a POST request to the `oauth/v2/revoke/token` endpoint. You can revoke both access tokens and refresh tokens. When you revoke a refresh token, all the access tokens generated from it are also revoked.

**Endpoint:** `POST {accounts-server-url}/oauth/v2/revoke/token`

> **Note:** The accounts-server-url depends on the datacenter where your app is registered.

### Headers
| Header |	Description |
| :---        | :----  | 
| `Authorization` |	*Required*.<br> Your app’s Base64-encoded credentials (the client ID and client secret), sent with the `Basic` scheme.<br> Syntax: `Authorization: Basic {Base64Encoded(client_id:client_secret)}`<br>Example: `Authorization: Basic MTAwMC5IVUZBV0xBO.......`<br> If your app is a client-based app, you don’t need to include `client_secret`. Otherwise, `client_secret` is required. |

### Parameters
| Parameter	 | Description |
| :---        | :----  | 
| `token` |	*Required*.<br> The refresh token or access token to revoke. |
| `token_type` |	*Optional*.<br> The type of token to revoke. Accepted values: `refresh_token` and `access_token`.<br> If you don’t include this parameter, the default is `refresh_token`. To revoke an access token, you must set `token_type=access_token`. |

**Request example:**
```
curl --location --request POST 'https://accounts.smarthive.com/oauth/v2/revoke/token' \
--header 'Authorization: Basic MTAwMC5IVUZBV0xBODdXQVg2VzIyUDIwRzhXNE1aWEhNTUwNjE2ODExYTMxN2QwZGI0MTdl' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'token=1000.18e983526f0ca8575ea9c53b0cd5bb58.1bd83a6f2e22c3a7e1309d96ae439cc1' \
--data-urlencode 'token_type=refresh_token'
```
**Response**
| Status code |	Description |
| :---        | :----  | 
| `200` | 	The token was revoked. |
| `400 Bad Request` |	The token in the request isn’t valid, the `token_type` doesn’t match the token, or the token isn’t associated with the provided client credentials.|