# Self Client - Client credentials flow

## Step 1: Use the client credentials to get an access token

**Endpoint:** `POST {accounts-server-url}/oauth/v2/token`

> **Note:** The accounts-server-url value depends on the data center where you registered the client. For a list of server-specific URLs, see SmartHive Accounts server information.

### Query parameters

| Parameter |	Description |
| :---        | :----  |    
| `client_id` |	*Required*. The unique ID that appears on the **Client Secret** tab of your self client. |
| `client_secret` |	*Required*. The unique, confidential secret that appears on the **Client Secret** tab of your self client. |
|`grant_type` |	*Required*. Pass the value `client_credentials`. |
| `scope` |	*Required*. The scope for the resource that you want to access by using the access token. Example: `SmartHiveProductMaster.settings.READ` |
| `soid` | *Required for some SmartHive apps*. Use this parameter only for apps that let you create multiple products or assets. To find out whether the parameter is required, see the API documentation 
for the module.<br> **Tip:** If a request without this parameter returns the `missing_org_info` error, include the parameter.<br> **Syntax:** `{servicename}.{ssoid}`<br> • `servicename`: The name of the service that 
the client makes API calls to. Every SmartHive pmodule has a unique service name, such as `SmartHiveAssetMaster` or `SmartHiveProductMaster`.<br> • `ssoid`: The unique ID of the app’s instance, also called the
product ID or asset ID. To find this ID, see the API documentation for the module.<br> **Example:** `SmartHiveProductMaster.600*****434` |

**Request example**
```
https://accounts.smarthive.com/oauth/v2/token
?client_id=1000.O1xxxxxxxxxx5Q91NTGH
&client_secret=74xxxxxxxxxxxx180
&grant_type=client_credentials
&scope=SmartHiveProductMaster.settings.READ
&soid=SmartHiveProductMaster.600*****434
```

### Response parameters

| Parameter |	Description |
| :---        | :----  |    
| `access_token` |	The key that your app uses to access the resource specified in the scope. Valid for 1 hour. |
| `api_domain` | The domain that your app sends service API requests to. |
|`token_type` |	The type of access token that SmartHive generates. SmartHive OAuth uses the `Bearer` token type. |
| `expires_in` | The number of seconds until the access token expires. |

**Response example**
```
{
    "access_token": "1000.875cf8ea310ae70c6fb26e25a5a48df0.be3bc88ab282cd58c6fd32f110c53c61",
    "api_domain": "https://www.zohoapis.in",
    "token_type": "Bearer",
    "expires_in": 3600
}
```

## Step 2: Use the access token to make API calls

Send API requests to the service that you want to access by using the `api_domain` value from the access token response. An access token is valid for 1 hour. After that, it expires. To get a new access token, 
repeat Step 1.