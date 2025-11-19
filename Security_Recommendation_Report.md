# Security Recommendation Report
## Title
Reflected Cross-Site Scripting (XSS) Vulnerability in Search Function

## Risk Rating
Medium

## Vulnerability Description
The search parameter of the web application reflects user input directly into the web page without sanitization. As a result, an attacker can inject malicious JavaScript into the victim's browser.

## Steps to Reproduce
1. Navigate to the page:
http://<target-ip>/search.php?q=test

2. Replace the search value with:

<script>alert('XSS')</script>
3. Observe that the browser executes the script, showing a JavaScript alert box.

## Impact
If exploited, an attacker could:
- Steal session cookies
- Hijack user accounts
- Perform actions on behalf of a logged-in user
- Redirect users to malicious sites
- Deface the application

## Remediation
To mitigate this vulnerability:
- Apply **output encoding** on all reflected user input.
- Reject input that contains special characters (`<`, `>`, `'`, `"`, `/`, `(`, `)`).
- Implement security libraries (e.g., `DOMPurify` for JavaScript).
- Enforce security headers such as `Content-Security-Policy (CSP)`.

### Example Fix (PHP)
Example Fix (JavaScript)
element.textContent = userInput;
```php
echo htmlspecialchars($_GET['q'], ENT_QUOTES, 'UTF-8');
