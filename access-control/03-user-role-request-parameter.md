# User Role Controlled by Request Parameter

**Difficulty:** Apprentice
**Category:** Access Control
**Lab:** [PortSwigger — User role controlled by request parameter](https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter)

## Objective
The application determines whether a user is an admin based on a value sent from the client (e.g. a cookie or hidden parameter), rather than checking it server-side against the actual account.

## Approach
1. Logged in as a low-privilege user and intercepted the request/response in Burp Proxy.
2. Noticed a parameter such as `Admin=false` being sent as a cookie value alongside the session.
3. Sent the intercepted request to **Repeater**, flipped the value to `Admin=true`, and re-sent it.
4. The server trusted the client-supplied value and granted admin access to protected pages.

## Burp Suite Usage
- **Proxy** to intercept the login flow and spot the suspicious client-controlled role parameter.
- **Repeater** to modify and re-send the request with the tampered value, then navigate the admin panel using the modified cookie.

## Remediation
- Never trust role or permission data supplied by the client — always determine privilege level from server-side session state tied to the authenticated user.
- Treat any client-controllable field influencing authorization as an immediate red flag in code review.
