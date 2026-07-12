# File Path Traversal — Simple Case

**Difficulty:** Apprentice
**Category:** Path Traversal
**Lab:** [PortSwigger — File path traversal, simple case](https://portswigger.net/web-security/file-path-traversal/lab-simple)

## Objective
The application loads product images from disk using a filename supplied in a request parameter. The goal is to read an arbitrary file (`/etc/passwd`) by manipulating that parameter.

## Approach
1. Identified the endpoint that fetches images (e.g. `filename=` parameter in the request).
2. Sent the request through Burp Suite and routed it to **Repeater** for manipulation.
3. Replaced the legitimate filename with a traversal sequence (`../../../etc/passwd`) to walk up out of the intended image directory.
4. Confirmed the server had no filtering on directory-traversal sequences — the file contents were returned directly in the response.

## Burp Suite Usage
- **Proxy** to intercept and capture the original image request.
- **Repeater** to iteratively adjust the number of `../` sequences and re-send without needing to go through the browser each time.

## Remediation
- Never build file paths directly from user input.
- Resolve the canonical path of the requested file and verify it still falls within the intended base directory before serving it.
- Prefer allow-listing valid filenames/IDs over trying to block traversal patterns.
