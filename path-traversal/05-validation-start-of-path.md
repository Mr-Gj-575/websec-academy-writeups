# File Path Traversal — Validation of Start of Path

**Difficulty:** Practitioner
**Category:** Path Traversal
**Lab:** [PortSwigger — File path traversal, validation of start of path](https://portswigger.net/web-security/file-path-traversal/lab-validate-start-of-path)

## Objective
The application only checks that the user-supplied path *starts with* an expected base folder (e.g. `/var/www/images/`), without validating the rest of the path.

## Approach
1. Noted the app expected the filename parameter to begin with the images directory.
2. Reasoned that if only the prefix is checked, a traversal sequence could still be appended after a valid-looking prefix to escape the directory.
3. Crafted a payload starting with the expected base path followed by traversal sequences, e.g. `/var/www/images/../../../etc/passwd`.
4. Sent via Burp Repeater — the prefix check passed, and the traversal sequences still resolved outside the intended directory.

## Burp Suite Usage
- **Repeater** to iterate on the payload, adjusting the traversal depth needed to reach the target file from the given base path.

## Remediation
- Checking a prefix string is not equivalent to validating the resolved path.
- Always resolve the full canonical path and confirm it is contained within the intended directory before use.
