# OAuth 2.0 glossary

| Term    | Description |
| :---        | :----  |      
| Protected resource    | Data in a SmartHive service that the client wants to access. For example, if a client wants to use an API to access the Inventory module in SmartHive, the Inventory module is the protected resource. A client can access this data only after OAuth authorization, which is why it’s called a protected resource.    |

| Resource owner   | The user who can give the client permission to access the protected resources in their SmartHive account. |

| Resource sever   | The server that stores the protected resources and receives the client’s API calls. For SmartHive, the SmartHive app that has the resource the client wants to access is the resource server.     |

| Authorization server | The server that grants access tokens and refresh tokens to the client on behalf of the resource owner (the user), so the client can access protected resources. For SmartHive, SmartHive Accounts is the authorization server.|

| Client  | The app that needs access to the protected resource. A client can be a server-based app, a single-page JavaScript app, or a self-client. After the authorization server authorizes the client on behalf of the user, the client can make API requests to the resource server.|

| Client type   | The type of app that you develop. There are three client types: <br> • **Server-based application:** A web app that’s built to run on a dedicated HTTP server. It uses the OAuth authorization code flow. <br> • **Client-based application:** A single-page JavaScript app that’s built to run exclusively in browsers, independent of web servers. It uses the OAuth implicit flow. <br> • **Self-client:** An app that doesn’t have a redirect URI and is used only to fetch information automatically from your own account. |

| Client ID   | A unique identifier for your app. You receive it when you register your app in the SmartHive API Console. |

| Client secret   | A unique secret key for your app. You receive it when you register your app in the SmartHive API Console. Only your app and SmartHive know the client secret, so keep it confidential. Client-based apps don’t need a client secret, and SmartHive doesn’t provide one.  |

| Access token   | A token that the authorization server (SmartHive Accounts) grants and that the client uses to access protected resources. It contains information about the user and the scopes. It tells the resource server that the user authorized the bearer of the token to access the protected resource within the defined scopes. An access token is valid for 1 hour. |

| Refresh token  | A token that the client uses to generate a new access token after the old one expires. The authorization server (SmartHive Accounts) grants refresh tokens, and the client can store them to generate access tokens when needed.|

| Authorization code   | A code that the client exchanges for an access token. Server-based can’t generate access tokens directly. Instead, the client first gets an authorization code from the authorization server (SmartHive Accounts), and then exchanges it for an access token. An authorization code is valid for only 2 minutes and can be used only once. |


