# Web Shell Upload via Content-Type Restriction Bypass

**Difficulty:** Apprentice
**Category:** File Upload
**Lab:** [PortSwigger — Web shell upload via Content-Type restriction bypass](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-content-type-restriction-bypass)

## Objective
The server checks the `Content-Type` header of the uploaded file (expecting something like `image/jpeg`) but does not verify the actual file content matches that type.

## Approach
1. Attempted to upload a PHP web shell directly — the server rejected it, returning an error about disallowed file type.
2. Intercepted the upload request in Burp Proxy and inspected the multipart body, noticing a `Content-Type: application/x-php` field tied to the file part.
3. Sent the request to Repeater and manually changed that `Content-Type` value to `image/jpeg`, while leaving the actual PHP file content and `.php` filename untouched.
4. The server's check passed since it only trusted the client-supplied header, and the file was stored and executable exactly as before.

## Burp Suite Usage
- **Repeater** to edit the raw multipart body, specifically the `Content-Type` field within the file part, independent of the filename or actual bytes.

## Remediation
- Never trust a client-supplied `Content-Type` header for validation — it is trivially spoofable.
- Validate file type server-side using actual content inspection (magic byte / MIME sniffing libraries), not header metadata.
