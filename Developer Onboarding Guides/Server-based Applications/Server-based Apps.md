# Server-based apps overview

## About server-based apps

Server-based apps typically separate the front-end (client-side) and back-end (server-side) components. The server runs the application logic and sends the rendered content to the browser for display.

These apps can securely store credentials, such as client secrets, on the server. In OAuth terminology, they’re called “confidential clients.”

For these apps, use the Authorization Code Flow to get access tokens. In this flow, you exchange an authorization code (from the authorization server) for access tokens. You can also get refresh tokens, so 
your app can get new access tokens without user intervention.

## Authorization code flow

First, register your app in the API console as a “server-based app.” You get a client ID and client secret, which you need to make the API calls that return OAuth tokens. After you receive an access token, 
you can use it to access protected SmartHive resources.

> For added security, you can use the authorization code flow with the **Proof Key for Code Exchange (PKCE)** extension. PKCE is required for mobile apps and recommended for server-based apps. Learn more 
about PKCE.

**To get an access token:**

1. Step 1:<br> Make a GET request to the `oauth/v2/auth endpoint`, and specify the required scopes. The permissions you’re requesting appear to the user. If the user grants access, the authorization server 
returns an authorization code to the redirection URL. The code is valid for 2 minutes. For details, see the API reference.
2. Step 2:<br> Make a POST request to the `oauth/v2/token` endpoint, using the authorization code you received. The authorization server returns an access token and an optional refresh token. The access 
token is valid for 1 hour. For details, see the API reference.
3. Step 3:<br> Use the access token to call SmartHiveAPIs and access protected resources. When the access token expires, send a POST request to the `oauth/v2/token` endpoint with the refresh token to get a 
new access token. For details, see the API reference.

## Multi DC support

SmartHive stores users’ information in different data centers (DCs). This information isn’t shared between data centers. Learn more about data centers.

If your app is registered in one DC and needs to access data for users in other DCs, turn on multi DC support for your app. After you turn it on, change your endpoint URL to match the user’s DC when you 
make API calls.

- Turn on multi DC support
- Workflow for server-based apps

## Incremental authorization

With incremental authorization, your app requests permission from the user only when it needs it, not up front. For example, your app might need profile information for basic functionality and extra 
permission for certain features. Without incremental authorization, your app has to request all permissions up front when the user grants access. That’s a bad experience, because people have to grant 
permissions for features they aren’t using yet. Incremental authorization avoids this and gives users a better experience.

- Implement incremental authorization

## Revoking refresh tokens

You can revoke refresh tokens programmatically, and users can revoke them too.

Users can revoke refresh tokens in two ways:

- Users can go to Connected Apps in `accounts.smarthive.com` and revoke the access they’ve granted to an app.
- Users can choose to revoke access for connected apps when they change their password or turn on multifactor authentication.

To revoke a refresh token programmatically, make a POST request to the `oauth/v2/revoke/token endpoint`. For details, see the API reference.

> **Note:** You can also revoke access tokens programmatically. If you revoke an access token that was issued from a refresh token, the refresh token is also revoked.