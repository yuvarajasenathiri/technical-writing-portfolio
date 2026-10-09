# API Authentication - Overview

SmartHive Projects APIs use OAuth 2.0 for authentication. This page gives you an overview of the authentication process. 

For complete details on OAuth 2.0 flows, registration, token management, and more, refer to SmartHive OAuth 2.0 documentation.

## How it works

To access SmartHive Projects APIs, your application needs an **access token** obtained through one of the OAuth 2.0 flows. At a high level, the steps are:

1. Register your application in the SmartHive API console.
2. Get consent from user to access their data and obtain an access token.
3. Call SmartHive Projects APIs using the access token.

## Token expiry

Access tokens expire periodically. The expiry duration is returned as `expires_in` (seconds) in the access token response.

To maintain uninterrupted access, you can request for an optional refresh token, store it, and use it to generate new access tokens as needed.

### Token lifecycle

- Access tokens are required for every API request.
- Refresh tokens can be used to generate new access tokens without requiring user re-authorization.
- Users can revoke an application's access at any time, which invalidates the associated tokens.

For more details on token management, refer to SmartHive OAuth 2.0 documentation.

### Different OAuth flows for different app types

SmartHive supports OAuth flows for different application types (server-based, client-based, and self client). You can choose the flow that matches your application.

For detailed information, refer to the OAuth documentation.

### Multi DC support

SmartHive operates data centers in multiple regions. If your application serves users across regions, you must enable Multi DC support in the API console and use region-specific endpoints for both OAuth and SmartHive Projects API calls.

## Scopes

SmartHive Projects APIs require OAuth scopes to define the level of access your application needs. When requesting for access token, request only the scopes your application requires. 
These will be displayed to the users when asking for consent.

| Scope    | Description |
| :---        | :----  |      
| SmartHiveProjects.projects.READ    | Access project data (read-only)      |
| SmartHiveProjects.projects.ALL   | Full access to projects |
| SmartHiveProjects.tasks.ALL   | Full access to tasks     |
| SmartHiveProjects.timesheets.ALL   | Full access to time logs     |

To request multiple scopes, separate them with commas:

`scope=SmartHiveProjects.projects.READ,SmartHiveProjects.tasks.ALL`

For more details about scope format, see OAuth Scopes.

## Making API calls with access token

To authenticate your API calls, include the access token in the `Authorization` header of every API request with the prefix `Bearer`.

**Syntax:** `Authorization: Bearer {access-token-value}`

**Example:** `curl -X GET "https://projects.SmartHive.com/api/v3/portals" -H "Authorization: Bearer 1000.abc123def456..."`

### Self-Client option

Use this method to generate the organization-specific grant token if your application does not have a domain and a redirect URL.
You can also use this option when your application is a standalone server-side application performing a back-end job.

1. Go to the **SmartHive Developer Console**, and then sign in with your SmartHive Projects username and password.
2. From the list of client types, select **Self Client**, and then select **Create Now**.
3. In the pop-up window, select **OK** to enable a self client for your account. Your client ID and client secret appear on the **Client Secret** tab.
3. Select the **Generate Code** tab.
4. In the **Scope** field, enter the required scopes, separated by commas. For a list of valid scopes, see Scopes.
	**Note:** If you enter one or more incorrect scopes, the system displays the error *“Enter a valid scope.”*
5. From the **Time Duration** field, select how long the grant token is valid.
	**Important:** The grant token expires after this time.
6. In the **Scope Description**, enter a description, and then select **Create**. The organization-specific grant token for the specified scopes appears.
7. Copy the grant token.