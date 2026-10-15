# API limits

SmartHive Projects APIs have rate limits to ensure fair usage and optimal performance for all users.

**Request:** `GET /api/v3/portal/{portal_id}/projects`

**Notes**

- You can call each API up to **200 times in a 2-minute window**.
- The limit applies to **each API endpoint**.

## Rate limit info

Each API response includes the following headers to help you monitor your usage: 

- `RateLimit`: The total number of requests allowed in the current window, for example, 200.
- `RateLimit-Remaining`: The number of requests remaining in the current window.
- `RateLimit-Window`: The duration of the rate limit window, for example, 120 seconds.
- `RateLimit-Window-Unit`: The time unit for the rate limit window, for example, seconds.
- `Retry-After`: The time, in seconds, to wait before you retry the request after you exceed the rate limit.

**Rate Limit Info**
```
RateLimit = 200
RateLimit-Remaining = 199
RateLimit-Window = 120
RateLimit-Window-Unit = seconds
Retry-After = 540 (seconds remaining)

**Note:** The API returns the Retry-After header only when you exceed the rate limit.
```
## Rate limit exceeded

If you exceed the allowed number of requests:

- SmartHive Projects **blocks** that **API for 10 minutes**.
- During this period, all further requests to that API fail.
- The response includes a `Retry-After` header that shows the remaining time, in seconds, before the API is available again.

## Important notes

- The restriction applies **only to the API that exceeds the limit**, not to all APIs.
- After the 10-minute cooldown, the API becomes available automatically.
- Repeated violations can affect app performance and reliability.

## Best Practices

To avoid reaching rate limits:

- Implement retry logic that uses the `Retry-After` header.
- Use **exponential backoff** instead of immediate retries. Use **exponential backoff** instead of immediate retries.
- Avoid sending unnecessary or duplicate requests.
- Use **batch APIs**, if available, to reduce the number of calls.
- Cache frequently used data when possible.

