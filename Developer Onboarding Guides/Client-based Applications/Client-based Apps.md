# Client-based apps overview

## About client-based apps

Client-based apps, such as single-page JavaScript apps, run the application logic directly in the browser through JavaScript.

These apps typically can’t securely store credentials, including client secrets, on the client side because the credentials might be exposed or compromised. In OAuth, client-based apps are often called “public clients” because they can’t keep credentials confidential.

For these apps, use the implicit flow to get access tokens. This flow returns the access token directly to the client-side environment as part of the redirection process. The implicit flow doesn’t provide refresh tokens, but the app might be able to get new access tokens without user intervention if the user granted permission for the session.

## Implicit flow

First, register your app in the API console as a “client-based app.” You get a client ID, which you need to make the API calls that return access tokens. After you receive an access token, you can use it to access protected SmartHive resources.

**To get an access token:**

1. Step 1:<br>
Make a GET request to the `oauth/v2/auth` endpoint, and specify the required scopes. The permissions you’re requesting appear to the user. If the user grants access, the authorization server returns an access token to the redirection URL. The access token is valid for 1 hour. For details, see the API reference.

2. Step 2:<br>
Use the access token to call SmartHive APIs and access protected resources. When the access token expires, you can get another one if the user granted access for the entire session in step 1. To get another access token, send a GET request to the `oauth/v2/auth/refresh` endpoint. For details, see the API reference.

## Multi DC support

SmartHive stores users’ information in different datacenters (DCs). This information isn’t shared between datacenters. Learn more about datacenters.

If your app is registered in one DC and needs to access data for users in other DCs, turn on multi DC support for your app. After you turn it on, change your endpoint URL to match the user’s DC when you make API calls.

- Turn on multi DC support
- Workflow for client-based apps

## Revoking access tokens

You can revoke access tokens programmatically, and users can revoke them too. Users can go to Connected Apps in accounts.smarthive.com and revoke the access they’ve granted to an app, which also revokes the access tokens.

To revoke an access token programmatically, make a POST request to the `oauth/v2/revoke/token` endpoint. For details, see the API reference.

