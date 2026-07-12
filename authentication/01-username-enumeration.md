# Username Enumeration via Different Responses

**Difficulty:** Apprentice
**Category:** Authentication
**Lab:** [PortSwigger — Username enumeration via different responses](https://portswigger.net/web-security/authentication/username-enumeration/lab-username-enumeration-via-different-responses)

## Objective
The login form returns subtly different responses depending on whether a submitted username exists, allowing an attacker to build a list of valid usernames before attempting password guessing.

## Approach
1. Submitted a login attempt with an obviously invalid username/password pair and noted the exact error message and response length.
2. Submitted a login attempt with a known-valid username but wrong password, and compared the response — the error message text differed slightly ("invalid password" vs "invalid username").
3. Sent the login request to Burp **Intruder**, using the username field as the payload position, and loaded a wordlist of candidate usernames.
4. Filtered results by response length/content to identify which usernames triggered the "wrong password" response versus the generic "invalid username" response, revealing valid accounts.

## Burp Suite Usage
- **Intruder** (Sniper attack) to automate submission of many candidate usernames against the login endpoint.
- **Grep-match** / column sorting on response length within Intruder results to quickly separate valid from invalid usernames.

## Remediation
- Return an identical, generic error message and identical response timing/length regardless of whether the username or password was incorrect.
- Consider rate-limiting and account lockout/backoff mechanisms to slow down automated enumeration attempts regardless of response uniformity.
