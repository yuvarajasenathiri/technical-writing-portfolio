# OAuth token limits

SmartHive limits how many OAuth tokens (access tokens and refresh tokens) a client can store and how many token requests a client can send at one time.

These limits have the following purposes:

- They make it easier for clients to store and maintain OAuth tokens.
- They prevent a malicious client from using resources that genuine clients need.
- They keep unnecessary requests from overloading our servers.

The limits differ for access tokens, refresh tokens, authorization codes, and device tokens.

## Limits for access tokens

Two types of limits apply to access tokens.

### 1. Maximum tokens per refresh token**

A client can store a maximum of 10 active access tokens per refresh token at one time. When a client requests another token after reaching 10, SmartHive provides a new token and invalidates the oldest one, 
so only 10 tokens remain at a time. If a client uses an invalidated access token, SmartHive throws the `INVALID_OAUTHTOKEN` exception.

### 2. Time-specific throttle limit**

A throttle limit also applies to how many times an app can request an access token in a specific period. A client can make a total of 10 access token requests within 10 minutes.

If your app reaches the throttle limit, SmartHive shows the following error message:

**JSON response**
```
{
"error_description": "You have made too many requests continuously. Please try again after some time.",
"error": "Access Denied"
}
```
**Roadblock error page**

`Access Denied: Maximum request limit reached for your account. Please try again after some time or contact the app’s developer.`

To avoid this error, reuse each access token until it expires, instead of using a different token for each request.

## Limit for refresh tokens

A client can store a maximum of 20 active refresh tokens for each user at one time. When a client requests another token after reaching 20 for a user, SmartHive provides a new token and invalidates the 
oldest one, so only 20 tokens remain at a time.

## Limit for authorization codes

Within 10 minutes, a client can generate a maximum of 10 authorization codes for each user. If a client reaches the limit, SmartHive throws the `access_denied` exception for the rest of that period. Each 
authorization code is valid for 2 minutes.

## Limit for device tokens

SmartHive applies a throttle limit based on the IP address that the requests come from. A client can request and generate a maximum of 30 device tokens from a specific IP address within 10 minutes. If a 
client reaches the limit, SmartHive throws the `access_denied` exception for the rest of that period. Each device token is valid for 5 minutes.