# Self Client - Authorization code flow

## Step 1: Generate an authorization code

1. Go to your self client in the API Console.
2. Select the **Generate Code** tab.
	a. In the **Scope** field, enter the scopes that your app needs. Separate multiple scopes with commas. For the required scopes, see the API documentation for the module.
	b. In the **Time Duration** field , select how long the authorization code is valid. The default is 3 minutes.
	c. In the **Scope Description** field, enter a description for the scopes.
3. Select **CREATE**.
4. If prompted, select the SmartHive app, and then select the portal that the app needs to access.
5. Select **CREATE**. The console generates and displays an authorization code.
6. Copy or download the authorization code.

## Step 2: Get an access token and a refresh token

Exchange the authorization code for an access token and a refresh token.

**Endpoint:** `POST {accounts-server-url}/oauth/v2/token`

> **Note:** The accounts-server-url value depends on the data center where you registered the client. For a list of server-specific URLs, see SmartHive Accounts server information.

### Query parameters

| Parameter |	Description |
| :---        | :----  |    
| `client_id` |	*Required.* The unique ID that appears on the **Client Secret** tab of your self client. |
| `client_secret` |	*Required.* The unique, confidential secret that appears on the **Client Secret** tab of your self client. |
|`grant_type` |	*Required.* Pass the value `authorization_code.` |
| `code` |	*Required.* The authorization code that you generated in Step 1. |

**Request example**
```
https://accounts.smarthive.in/oauth/v2/token
?client_id=1000.XMDEG1KBDO9SE2IFTMDFSRPYYJ5L0U
&client_secret=1632308b34e2cf614fed922c5d6c4193c7778a5f13
&grant_type=authorization_code
&code=1000.406a3b53bad3f6824d4fb43108604cd7.a74aef3010243f0fae78111e2a673847
```

### Response parameters

| Parameter |	Description |
| :---        | :----  | 
| `access_token` |	The key that your app uses to access the resource specified in the scope. Valid for 1 hour. |
| `refresh_token` |	A token that your app uses to get a new access token after the current one expires. This token doesn’t expire. |
| `api_domain` |	The domain that your app sends service API requests to. |
| `token_type` |	The type of access token that SmartHive generates. SmartHive OAuth uses the `Bearer` token type. |
| `expires_in` |	The number of seconds until the access token expires. |

**Response example**
```
{
    "access_token": "1000.875cf8ea310ae70c6fb26e25a5a48df0.be3bc88ab282cd58c6fd32f110c53c61",
    "refresh_token": "1000.ce79a5110c4097744b17aecbb95dcfeb.db3167fy73ca0082fa4f6182474fc80e",
    "api_domain": "https://www.smarthiveapis.in",
    "token_type": "Bearer",
    "expires_in": 3600
}
```

## Step 3: Use the access token to make API calls

Send API requests to the service that you want to access by using the api_domain value from the access token response. An access token is valid for 1 hour. After that, it expires. To get a new access token, 
use the refresh token, as described in Step 4.

## Step 4: Refresh the access token

When an access token expires, use the refresh token to get a new one.

**Endpoint:** `POST	{accounts-server-url}/oauth/v2/token`

> **Note:** The accounts-server-url value depends on the data center where you registered the client. For a list of server-specific URLs, see SmartHive Accounts server information.

### Query parameters

| Parameter |	Description |
| :---        | :----  |    
| `client_id` |	*Required.* The unique ID that appears on the **Client Secret** tab of your self client. |
| `client_secret` |	*Required.* The unique, confidential secret that appears on the **Client Secret** tab of your self client. |
|`grant_type` |	*Required.* Pass the value `refresh_token.` |
| `refresh_token` |	*Required.* The refresh token that you got in Step 2. |

**Request example**
```
https://accounts.smarthive.in/oauth/v2/token
?client_id=1000.GMB0YULZHJK411248S8I5GZ4CHUEX0
&grant_type=refresh_token
&client_secret=122c324d3496d5d777ceeebc129470715fbb856b7
&refresh_token=1000.18e983526f0ca8575ea9c53b0cd5bb58.1bd83a6f2e22c3a7e1309d96ae439cc1
```

### Response parameters

| Parameter |	Description |
| :---        | :----  | 
| `access_token` |	The key that your app uses to access the resource specified in the scope. Valid for 1 hour. |
| `api_domain` |	The domain that your app sends service API requests to. |
| `token_type` |	The type of access token that SmartHive generates. SmartHive OAuth uses the `Bearer` token type. |
| `expires_in` |	The number of seconds until the access token expires. |

**Response example**
```
{
    "access_token": "1000.875cf8ea310ae70c6fb26e25a5a48df0.be3bc88ab282cd58c6fd32f110c53c61",
    "api_domain": "https://www.zohoapis.in",
    "token_type": "Bearer",
    "expires_in": 3600
}
```
