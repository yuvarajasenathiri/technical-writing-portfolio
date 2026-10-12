# Self Client

If you want your app to fetch data from your own SmartHive account, or to set up app-to-app communication in the back end without user interaction, use the Self Client option. In this scenario, you’re the 
resource owner, and no end-user authorization is required. The client requests access permission on its own behalf, not on behalf of an end user.

## Set up a self client

### Create a self client in the API Console

1. Go to the SmartHive API Console.
2. Select **GET STARTED**.
3. Point to Self Client, and then select **CREATE NOW**.
4. Select **CREATE**, and then select **OK**. The console creates a client ID and client secret and displays them on the Client Secret tab. Copy them.

### Get an access token

You can get an access token for your self client by using one of these grant flows:

- Authorization code grant flow
- Client credentials grant flow

**Authorization code grant flow**

Generate an authorization code in the API Console, and then exchange it for an access token and a refresh token. When the access token expires, use the refresh token to get a new access token. For details, 
see Authorization code flow for self clients.

**Client credentials grant flow**

Provide your client credentials to get an access token. SmartHive doesn’t provide a refresh token, so when the access token expires, send the same request again to get a new one. For details, 
see Client credentials flow for self clients.