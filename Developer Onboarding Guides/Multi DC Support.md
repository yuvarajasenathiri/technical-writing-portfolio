# Multi DC support

Data protection and privacy laws in many countries require that user data be stored only in datacenters located in that country. To comply, SmartHive has set up datacenters in multiple countries. Each datacenter holds only the data of users who registered at that domain. 
See the available datacenters.

## When multi DC support is required

Clients need user data to run their business logic. Clients such as extensions and plugins have users in all datacenters (DCs) and need to reach all SmartHive users. These clients must turn on multi DC support in the SmartHive API console to access SmartHive’s global user base.

If your app is in the US datacenter and users in the EU datacenter use it, turn on EU DC support for your app. The response to the initial request includes the user’s location. Use the location to send further API calls to the server URL for that user’s datacenter.

The following table lists the datacenters and their server URLs:

| Datacenter	| Server URL |
| :---        | :----  |
| United States (US)	 | https://accounts.smarthive.com |
| Europe (EU) |	https://accounts.smarthive.eu |
| India (IN)	| https://accounts.smarthive.in |
| Australia (AU) |	https://accounts.smarthive.com.au |
| Japan (JP) 	| https://accounts.smarthive.jp |
| Canada (CA)	| https://accounts.smarthive.ca |
| Saudi Arabia (SA) |	https://accounts.smarthive.sa |
| United Kingdom (UK) |	https://accounts.smarthive.uk |

> Get the server URLs for all datacenters in JSON format.

The `client ID` is the same for all DCs. The `client secret` can be the same for all DCs or unique for each DC, depending on your preference.

See how the multi DC flow works in server-based apps and client-based apps.

## Turn on multi DC support

When you turn on multi DC support, you can use a separate client secret for each DC or the same client secret for all enabled DCs.

1. In the SmartHive API Console, select your client from the list of applications.
2. Go to the **Settings** tab.
3. Turn on the toggle next to each DC you need.
4. By default, each enabled DC has a unique client secret. To view and copy the client secret for a DC, select **SHOW CODE**.
5. To use the same client secret for all DCs instead:<br> a) Select **Use the same OAuth credentials for all data centers**.<br> b) Select **OK**. You can use the default client secret to make requests in all DCs.
	
## Server-based applications

The multi DC flow for server-based apps has these steps:

1. Identify the user’s location in the authorization request

Send the authorization request to the domain https://accounts.smarthive.com. The response includes the user’s DC in the `location` parameter. To view the server URL for this location, go to https://accounts.smarthive.com/oauth/serverinfo.

**Sample authorization response:**
```
https://oauth.pstmn.io/v1/browser-callback
?code=1000.abbb4c9e0902704b90cc556f32ec0336.5ff4478926a43657280d5cbe1af1917a
&location=in
&accounts-server=https://accounts.smarthive.in
```
In this example, the `location=in`.

2. Make the access token request to the server URL for the user’s location

After you identify the user’s datacenter, send the access token request to the server URL for that location. For example, if `location=eu`, send the request to https://accounts.smarthive.eu.

**Example request:**
```
https://accounts.smarthive.eu/oauth/v2/token
?client_id=1000.GMB0YULZHJK411248S8I5GZ4CHUEX0
&grant_type=authorization_code
&client_secret=122c324d3496d5d777ceeebc129470715fbb856b7
&redirect_uri=https://www.victa.com/oauthredirect
&code=1000.86a03ca5dbfccb7445b1889b8215efb0.cad9e1ae4989a1196fe05aa729fcb4e1
```
**Example response:**
```
{
"access_token":"1000.2deaf8d0c268e3c85daa2a013a843b10.703adef2bb337b 8ca36cfc5d7b83cf24",
"refresh_token":"1000.18e983526f0ca8575ea9c53b0cd5bb58.1bd83a6f2e22c3a7e1309d96ae439cc1",
"api_domain":"https://api.smarthive.eu",
"token_type":"Bearer",
"expires_in":3600
}
```
The response includes `api_domain`, the domain where you make service API requests.

3. Send service API requests to the api_domain for the user’s location

Send requests to the service you want to access through the `api_domain` value from the access token response.

## Client-based applications

The multi DC flow for client-based apps has these steps:

1. Identify the user’s location in the access token request

Send the access token request to the domain https://accounts.smarthive.com. The response includes the user’s DC in the `location` parameter. To view the server URL for this location, go to https://accounts.smarthive.com/oauth/serverinfo. The response also includes `api_domain`, the domain where you make service API requests.

**Sample access token response:**
```
https://www.victa.com/oauthredirect#
&access_token=1000.835d578e9a2103d2e87994ae8752074d.4496b74ddde6413f83fe615e8388e488
&expires_in=3600
&location=in
&api_domain=https://www.smarthiveapis.in
```
2. Send service API requests to the api_domain for the user’s location

Send requests to the service you want to access through the `api_domain` value from the access token response.