# Web Security Academy — Lab Writeups

Personal writeups from working through [PortSwigger's Web Security Academy](https://portswigger.net/web-security), covering the vulnerability class, the approach taken to solve each lab, how Burp Suite was used, and the recommended remediation.

These are intentionally vulnerable training labs built by PortSwigger for learning purposes — writeups focus on methodology and defensive takeaways rather than raw exploit payloads.

## 🗂️ Path Traversal
| Lab | Difficulty |
|---|---|
| [File path traversal, simple case](path-traversal/01-simple-case.md) | Apprentice |
| [Traversal sequences blocked with absolute path bypass](path-traversal/02-absolute-path-bypass.md) | Practitioner |
| [Traversal sequences stripped non-recursively](path-traversal/03-stripped-non-recursively.md) | Practitioner |
| [Traversal sequences stripped with superfluous URL-decode](path-traversal/04-superfluous-url-decode.md) | Practitioner |
| [Validation of start of path](path-traversal/05-validation-start-of-path.md) | Practitioner |
| [Validation of file extension with null byte bypass](path-traversal/06-null-byte-bypass.md) | Practitioner |

## 🔑 Access Control
| Lab | Difficulty |
|---|---|
| [Unprotected admin functionality](access-control/01-unprotected-admin-functionality.md) | Apprentice |
| [Unprotected admin functionality with unpredictable URL](access-control/02-unpredictable-url.md) | Apprentice |
| [User role controlled by request parameter](access-control/03-user-role-request-parameter.md) | Apprentice |
| [User role can be modified in user profile](access-control/04-user-role-modifiable-in-profile.md) | Apprentice |
| [User ID controlled by request parameter](access-control/05-user-id-request-parameter.md) | Apprentice |
| [User ID controlled by request parameter, with unpredictable user IDs](access-control/06-unpredictable-user-ids.md) | Apprentice |
| [User ID controlled by request parameter with data leakage in redirect](access-control/07-data-leakage-in-redirect.md) | Apprentice |

## 🔓 Authentication
| Lab | Difficulty |
|---|---|
| [Username enumeration via different responses](authentication/01-username-enumeration.md) | Apprentice |
| [2FA simple bypass](authentication/02-2fa-simple-bypass.md) | Apprentice |
| [Password reset broken logic](authentication/03-password-reset-broken-logic.md) | Apprentice |

## 📤 File Upload
| Lab | Difficulty |
|---|---|
| [Remote code execution via web shell upload](file-upload/01-rce-via-web-shell-upload.md) | Apprentice |
| [Web shell upload via Content-Type restriction bypass](file-upload/02-content-type-restriction-bypass.md) | Apprentice |
| [Web shell upload via obfuscated file extension](file-upload/03-obfuscated-file-extension.md) | Practitioner |
| [Remote code execution via polyglot web shell upload](file-upload/04-polyglot-web-shell-upload.md) | Practitioner |

---

**Tools used:** Burp Suite (Proxy, Repeater, Intruder)
**Author:** GJ — MCA (AI/ML & Cybersecurity), Amrita Vishwa Vidyapeetham. Currently pursuing CEH v13 & CompTIA Security+ under the Front Runner Cybersecurity Diploma (FRCD).
