# Unprotected Admin Functionality with Unpredictable URL

**Difficulty:** Apprentice
**Category:** Access Control
**Lab:** [PortSwigger — Unprotected admin functionality with unpredictable URL](https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality-with-unpredictable-url)

## Objective
The admin panel URL is randomized/obfuscated rather than a guessable static path, but the panel itself still has no access control once found.

## Approach
1. Since the URL wasn't guessable, looked for it being disclosed elsewhere in the application rather than trying to brute force it.
2. Checked page source of the standard user pages and found the admin panel's full URL leaked in a JavaScript file loaded by the front end (a common way random paths still end up disclosed).
3. Navigated to the disclosed URL directly — again, no authentication was required to access or use admin functionality.

## Burp Suite Usage
- **Proxy history / HTTP history** to review all static resources (JS, CSS) loaded by the page, since the leak was in client-side code rather than the main HTML.
- Used **search** within Burp's proxy history to look for the word "admin" across all captured responses.

## Remediation
- An unpredictable URL is not a substitute for real access control — it only delays discovery, it doesn't prevent it.
- Ensure sensitive endpoints check the authenticated user's role/session server-side before returning any functionality or data.
