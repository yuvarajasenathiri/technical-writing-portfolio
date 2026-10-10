# Introduction to OAuth 2.0

## What is OAuth 2.0?

OAuth 2.0 is an industry standard protocol which allows you to grant a third-party website or an application (i.e., a client) delegated access to the protected resources of SmartHive via SmartHive APIs. 
It is a way to authenticate and authorize API requests made to SmartHive.

## Advantages of OAuth 2.0

- Clients are not required to support password authentication or store user credentials, because the authentication and authorization is done by exchanging OAuth tokens.
- Clients gain delegated access, i.e., access only to resources authorized by the user.
- Users can revoke third-party application's delegated access anytime.
- OAuth access tokens expire after a set time. If the client faces a security breach, user data will be compromised only until the access token is valid.

## OAuth 2.0 workflow

`Refer to the OAuth 2.0 glossary section to understand more about the terms used here.`

### Step 1: Register your app and get OAuth credentials

The first step in using OAuth authentication is registering your app with the SmartHive API console. Once you register your client, you will get a Client ID and Client secret for your application. 
This Client ID and Client secret are used to authorize your app's OAuth requests.

### Step 2: Obtain an access token

Access token is an OAuth token used to access SmartHive's protected resources. The way in which the access token can be generated depends on the type of app. For example, server-based apps can use the 
authorization code flow to generate an access token, while client-based apps can use the implicit flow to generate an access token. However, in any method, access token will be provided only after the 
user grants permission through consent. Also, access tokens are always granted for the specific scopes which are mentioned in the request, and the scopes will be displayed to the user while asking for 
permission.

To learn about the workflows for different types of clients, refer to the below pages:

- Server-based apps
- Client-based apps
- Self client

### Step 3: Access the resource using the access token

After your app has the access token, it can access SmartHive's protected resources. On giving the access token to the resource server, your app will be granted access as per the scopes defined in the request. 
SmartHive's OAuth implementation uses Bearer authentication scheme, hence while making API calls, the access token has to be passed in the `Authorization` header with the prefix `Bearer`.

Syntax: `Authorization: Bearer <space> {access-token-value}`
Example: `Authorization: Bearer 1000.2deaf8d0c2...`

### Step 4: Refresh the access token when it expires

Access tokens have limited validity. Their lifetime is only 1 hour, post which they expire and cannot be used to access the resources any longer. However, if the app wants to access the resource for more than
1 hour, then a refresh token can be retrieved and stored. This refresh token allows the app to generate a new access token whenever required.

### Step 5: Revoke unwanted tokens

If a refresh token is no longer required or appears to be compromised, it can be revoked and made invalid. It can be revoked by making an API request and after successful revocation, it can no longer be used 
to generate access tokens, and the existing access tokens generated using this refresh token will also become invalid.  

