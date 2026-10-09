# API Limits

SmartHive Projects APIs are governed by rate limits to ensure fair usage and optimal performance of all users.

**Request:** `GET /api/v3/portal/{portal_id}/projects`

**Notes**

- Each API can be invoked up to **200 times within a 2-minute window.**
- The limit is applied **per API endpoint.**

## Rate Limit Info

Each API response includes the following headers to help you monitor your usage:

- `RateLimit`: Total allowed requests in the current window (for example, 200).
- `RateLimit-Remaining`: Remaining requests available in the current window.
- `RateLimit-Window`: Duration of the rate limit window (for example, 120 seconds).
- `RateLimit-Window-Unit`: Time unit for the rate limit window (for example, seconds).
- `Retry-After`: Time (in seconds) to wait before retrying the request after the rate limit has been exceeded.

**Rate Limit Info**
```
RateLimit = 200
RateLimit-Remaining = 199
RateLimit-Window = 120
RateLimit-Window-Unit = seconds
Retry-After = 540 (seconds remaining)

**Note:** Retry-After key is returned only when the rate limit has been exceeded.
```

## Rate Limit Exceeded

If the number of requests exceeds the allowed limit:

- The specific API will be **temporarily blocked for 10 minutes.**
- During this period, all further requests to that API will fail.
- A `Retry-After` header will be included in the response, indicating the remaining time (in seconds) before the API becomes available again.

## Important Notes

- The restriction applies **only to the API that exceeds the limit**, not all APIs.
- After the 10-minute cooldown, the API will become available automatically.
- Continuous violations may impact application performance and reliability.

## Best Practices

To avoid hitting rate limits:

- Implement **retry mechanisms** using the `Retry-After` header.
- Use **exponential backoff** instead of immediate retries.
- Avoid sending unnecessary or duplicate requests.
- Use **batch APIs (if available)** to reduce the number of calls.
- Cache frequently used data whenever possible.

