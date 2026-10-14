# Incremental authorization overview

Incremental authorization is an OAuth implementation strategy. Your app requests a permission from the user only when it needs it, not up front. This improves your app’s user experience.

Incremental authorization has these advantages:

- Users don’t have to grant permission for scopes they don’t need, such as scopes for features they don’t use.
- Your app doesn’t have to repeatedly ask for permissions that the user already granted.

For example, suppose you’re developing an app that integrates with SmartHive Mail. When the user signs in, your app needs only the user’s basic profile information and permission to display the user’s inbox and 
email messages. Later, the user might choose to send email from your app, which your app supports. At that point, your app requests permission to send email. The user is asked only for that permission, not 
for the ones already granted, such as basic profile information and permission to view email.

## How it works

Your app initially gets the basic permissions it needs up front. When your app later needs more permissions from the user, follow these steps:

1. Make a POST request to the `oauth/v2/token/scopeenhance` endpoint to get a scope enhancement token from SmartHive. Include a `refresh token` as a parameter. For details, see the API reference.
2. Make a scope enhancement request to the `oauth/v2/token/addextrascope` endpoint, and include the scope enhancement token and the additional scopes you need. For details, see the API reference.

The user sees a consent screen that asks for the newly required permissions. If the user approves, SmartHive adds the additional scopes to the refresh token (sent in step 1) and its associated access tokens,
and returns a success response.