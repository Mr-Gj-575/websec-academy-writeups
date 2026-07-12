# Remote Code Execution via Polyglot Web Shell Upload

**Difficulty:** Practitioner
**Category:** File Upload
**Lab:** [PortSwigger — Remote code execution via polyglot web shell upload](https://portswigger.net/web-security/file-upload/lab-file-upload-remote-code-execution-via-polyglot-web-shell-upload)

## Objective
The application validates that uploaded files are genuine images by inspecting their content (not just the extension), but still allows files with an image-valid structure to also carry executable PHP code.

## Approach
1. Confirmed that a plain `.php` file was rejected, and that the server appeared to actually parse the file content to confirm it was a real image (not just checking the extension or Content-Type).
2. Built a polyglot file: a valid JPEG image with PHP code embedded inside a metadata section (e.g. the EXIF comment field), so the file passes image-content validation while still containing executable PHP.
3. Uploaded the polyglot file through Burp Proxy, confirming it passed validation and was stored as a `.jpg`.
4. Since the upload directory still executed `.php` files based on extension in some configurations, renamed/accessed the file in a way that caused the server to interpret it as PHP (or, where the lab required, combined this with a secondary flaw such as a rename endpoint) to trigger execution of the embedded code.

## Burp Suite Usage
- **Repeater** to iterate on file content and headers while testing which validation checks were content-based versus extension-based.
- **Hex view** in Burp's Repeater/Inspector to insert and verify the embedded PHP snippet within the binary image data without corrupting the image structure.

## Remediation
- Content-based validation alone is not sufficient if the file format allows arbitrary embedded data (metadata, comments) to coexist with valid structure.
- Re-encode/re-process uploaded images server-side (stripping metadata, re-compressing) rather than storing the uploaded bytes verbatim.
- Serve all user-uploaded content from a separate domain/subdomain with no script execution permissions, regardless of extension.
