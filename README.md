# 2FA Bypass Techniques Repository

This repository contains various methods and techniques for bypassing Two-Factor Authentication (2FA) across different systems. It is intended for educational purposes and security research only, aiming to highlight potential vulnerabilities in 2FA implementations and raise awareness about the importance of security in authentication systems.

---

## Table of Contents

1. [Bypass Techniques](#bypass-techniques)
   - Using Caching Mechanism for Cookie Policy
   - Changing Request Method
   - Referer Header Bypass
   - Missing 2FA Code Integrity Validation
   - Bypassing via Custom Cookie Parameter in Mobile Apps
   - Reset Password Endpoint Manipulation
2. [Misconfiguration Exploits](#misconfiguration-exploits)
   - Response Manipulation
   - Status Code Manipulation
   - 2FA Code Leakage in Response
   - 2FA Code Reusability
   - Lack of Brute-Force Protection
   - Bypass with Null/000000 Code
3. [Advanced Bypass Techniques](#advanced-bypass-techniques)
   - Session Permission Attack
   - Backup Code Abuse
   - Subdomain Vulnerabilities
   - Guessable Cookie Exploitation
4. [Comprehensive Checklist](#comprehensive-checklist)

---

## Bypass Techniques

### 1. Flawed Two-Factor Verification Logic
- **Summary**: Flawed logic allows attackers to manipulate cookies or session variables after the first authentication step to access another user's account.
- **Example**: Manipulating the `account` cookie to impersonate a victim after the first login step.

### 2. Clickjacking on 2FA Disable Feature
- **Summary**: Using iframes and social engineering to trick the victim into disabling their own 2FA settings.
- **Key Steps**: 
   - Iframe the 2FA disable page.
   - Exploit user interaction through social engineering.

### 3. Response Manipulation
- **Summary**: Modifying server response values to trick the system into accepting an unsuccessful 2FA attempt.
- **Example**: Change `success: false` to `success: true` in the response payload.

### 4. Status Code Manipulation
- **Summary**: Changing the HTTP status code to bypass security checks.
- **Example**: Modify a `4xx` error code to `200 OK` to bypass 2FA.

### 5. 2FA Code Reusability
- **Summary**: Reusing old 2FA codes to bypass checks.
- **Key Steps**: Test code reusability over multiple sessions and across longer durations.

### 6. CSRF on 2FA Disable Feature
- **Summary**: Exploiting Cross-Site Request Forgery to disable 2FA without user interaction.
- **Example**: Use existing session information to disable 2FA through CSRF attacks.

### 7. Backup Code Abuse
- **Summary**: Using brute-force and response manipulation techniques to bypass backup code checks.

### 8. 2FA Refer Check Bypass
- **Summary**: Manipulating the referer header to fool the application into skipping 2FA checks.
- **Example**: Change the referer header to a URL that appears to come from a 2FA-confirmed page.

---

## Misconfiguration Exploits

### 9. Lack of Brute-Force Protection
- **Summary**: The absence of rate-limiting allows unlimited attempts to brute-force the 2FA code.
- **Example**: Repeatedly sending 2FA code requests or brute-forcing code input fields.

### 10. Missing 2FA Code Integrity Validation
- **Summary**: Using a valid 2FA code from another account to bypass the victim's 2FA.

### 11. MFA Challenge Context Binding
- Summary: Testing whether an MFA challenge or verification token is correctly bound to the intended user, session, authentication transaction, and security-sensitive action.
- Key Checks:
  - Test whether a challenge created in one session can be verified in another session.
  - Test whether a challenge can be used for another account.
  - Test whether a verified challenge can be replayed against a different sensitive action.
  - Verify that MFA completion cannot be detached from the intended authentication context.

### 12. Password Reset/Email Change - 2FA Disable
- **Summary**: Exploiting password reset or email change functions to bypass or disable 2FA.

### 13. Re-sending Code and Reset Limit
- **Summary**: Resetting the brute-force limit by resending the same code repeatedly.

### 14. Leaked Token
- **Summary**: Identifying tokens that are inadvertently leaked in the response or logs.

### 15. Infinite OTP Regeneration
- **Summary**: Generating OTPs indefinitely until one matches the required code.

### 16. Subdomain Vulnerabilities
- **Summary**: Using outdated or vulnerable subdomains to bypass modern 2FA systems.

---

## Advanced Bypass Techniques

### 17. Session Permission Attack
- **Summary**: Exploiting session vulnerabilities to pass 2FA checks on a victim's account using attacker session data.

### 18. Guessable Cookie Exploitation
- **Summary**: Exploiting weak cookie structures used in "remember me" features to bypass 2FA.

### 19. IP Address Manipulation
- **Summary**: Impersonating a user's IP address using headers like `X-Forwarded-For`.

### 20. Content-Type / Parser Differential Bypass
- Summary: Testing whether changing the Content-Type causes the same logical request to be parsed or routed differently, potentially bypassing 2FA enforcement.
- Key Checks:
  - Test `application/json` vs `application/x-www-form-urlencoded`.
  - Test `multipart/form-data` and other accepted content types.
  - Test the same parameter as scalar, array, null, empty string, boolean, or numeric value where applicable.
  - Verify that MFA validation is enforced consistently across all request representations.
  - Check for alternate middleware, parser, or route behavior triggered by Content-Type changes.

### 21. Duplicate Parameter / Parameter Pollution in MFA
- Summary: Testing whether duplicate MFA parameters are interpreted differently by frontend, middleware, proxy, or backend components.
- Key Checks:
  - Test duplicate OTP/code parameters.
  - Test duplicate user/account identifiers.
  - Compare first-value and last-value parsing behavior.
  - Test duplicate parameters across query string and request body.
  - Check for parser inconsistencies between security middleware and application logic.

### 22. Header-Based MFA Trust
- Summary: Testing whether the application or an upstream component incorrectly trusts client-controlled headers to determine MFA verification state.
- Key Checks:
  - Identify headers related to MFA, authentication level, internal routing, or verification state.
  - Determine whether such headers are accepted from untrusted clients.
  - Compare behavior with and without suspected MFA-related headers.
  - Check whether proxies, gateways, or backend services interpret these headers differently.

---

## Comprehensive Checklist

- Main Test Cases:
    - [ ]  Test email activation link for automatic 2FA bypass
    - [ ]  Check if password reset functionality bypasses 2FA
    - [ ]  Attempt response manipulation (e.g., changing parameter values)
    - [ ]  Try deleting or nullifying 2FA parameters in multi-step authentication
    - [ ]  Access features without completing 2FA after initial login
    - [ ]  Skip individual MFA workflow steps and access subsequent steps directly
    - [ ]  Replay a post-MFA request without completing the preceding verification step
    - [ ]  Test whether workflow state can be advanced by directly invoking later endpoints
    - [ ]  Test whether MFA completion state can be forged, omitted, reset, or downgraded between workflow steps
    - [ ]  Test API endpoints for user information retrieval without 2FA
    - [ ]  Attempt user information updates without completing 2FA
- Advanced Techniques:
    - [ ]  Exploit caching mechanisms related to cookie policies
    - [ ]  Change request methods to bypass 2FA (e.g., GET to POST)
    - [ ]  Test equivalent request representations across JSON, form, multipart, and other accepted encodings
    - [ ]  Move 2FA-related parameters between body, query string, path, and headers where applicable
    - [ ]  Test whether parameter location changes alter MFA enforcement
    - [ ]  Compare server-side authorization/MFA behavior for semantically equivalent requests
    - [ ]  Manipulate referrer headers to bypass 2FA checks
    - [ ]  Test for missing 2FA code integrity validation
    - [ ]  Attempt to use reset password endpoints to bypass 2FA
- OTP Brute Force Scenarios:
    - [ ]  Time-based limited environment: Distribute OTP attempts across multiple instances
    - [ ]  IP-based restrictions: Utilize IP rotation services (e.g., AWS)
    - [ ]  Rate-limited environment: Test case-sensitive variations in email addresses
    - [ ]  Complex scenarios (time-limited, IP-based, with CAPTCHA):
        - [ ]  Attempt CAPTCHA bypass techniques (OCR, nopecha.com)
        - [ ]  Search for staging or development instances sharing the same database
        - [ ]  Combine IP rotation with CAPTCHA bypass methods

- Additional Test Cases:
    - [ ]  Test for race conditions in login requests
    - [ ]  Check for session fixation vulnerabilities
    - [ ]  Analyze the OTP generation algorithm for predictability
    - [ ]  Verify 2FA enforcement across all API endpoints
          - [ ] API endpoints, methods, Content-Types, parameter locations, API versions, and alternate routes
    - [ ]  Verify 2FA enforcement across all HTTP methods
    - [ ]  Verify 2FA enforcement across all parameter locations
    - [ ]  Verify 2FA enforcement across alternate API versions and routes
    - [ ]  Verify 2FA enforcement across web, mobile, and third-party API clients
    - [ ]  Verify 2FA enforcement at the business-action execution layer
    - [ ]  Verify 2FA enforcement across all accepted Content-Types
    - [ ]  Verify MFA/2FA is bound to each sensitive business action, not only the authentication flow
    - [ ]  Test whether sensitive actions remain protected across alternate routes, methods, and request representations
    - [ ]  Test whether the same business operation can be reached through an endpoint that does not enforce MFA
    - [ ]  Verify server-side MFA state is required at the point of sensitive action execution
    - [ ]  Investigate 2FA bypass through account linking
    - [ ]  Test for subdomain takeover if 2FA is on a separate subdomain
    - [ ]  Attempt time-based attacks on TOTP implementations
    - [ ]  Verify 2FA persistence across different devices/browsers
    - [ ]  Test whether MFA verification on one device/session incorrectly authorizes sensitive actions in another session
    - [ ]  Test cross-session and cross-device MFA state propagation
    - [ ]  Verify that MFA state is bound to the intended authentication context
    - [ ]  Test 2FA in account recovery processes
    - [ ]  Test alternative account-recovery methods for MFA bypass
    - [ ]  Test recovery email, recovery phone, backup codes, trusted devices, and support-assisted recovery
    - [ ]  Check whether account recovery changes MFA enforcement or authentication assurance
    - [ ]  Verify that recovery tokens cannot be used to skip MFA on sensitive actions
    - [ ]  Check if 2FA can be disabled without proper authentication
    - [ ]  Investigate potential 2FA bypass in mobile app versions
    - [ ]  Test 2FA enforcement in third-party integrations
    - [ ]  Test MFA method downgrade and fallback paths
    - [ ]  Check whether stronger MFA methods can be replaced with weaker fallback methods
    - [ ]  Verify that fallback methods enforce the same authentication assurance level
    - [ ]  Test whether removing or modifying MFA method parameters changes the required verification flow
- Miscellaneous Checks:
    - [ ]  Test backup code feature for potential abuse
    - [ ]  Check for clickjacking vulnerabilities on 2FA disabling page
    - [ ]  Verify if enabling 2FA expires previously active sessions
    - [ ]  Attempt to bypass 2FA with null or 000000 as OTP
    - [ ]  Test browser extensions' impact on 2FA functionality


This summarized checklist includes all techniques for testing 2FA bypass vulnerabilities:

- [ ] **Test Race Conditions**
- [ ] **Check for Session Fixation**
- [ ] **Test Flawed Verification Logic**
- [ ] **Clickjacking on 2FA Disable**
- [ ] **Response Manipulation**
- [ ] **Status Code Manipulation**
- [ ] **Test for 2FA Code Reusability**
- [ ] **CSRF on 2FA Disable**
- [ ] **Test Backup Code Abuse**
- [ ] **Check Session Expiry on 2FA Enabling**
- [ ] **Refer Header Manipulation**
- [ ] **Analyze for 2FA Code Leakage**
- [ ] **Check JavaScript for Exploitable Info**
- [ ] **Test Brute-Force Protection**
- [ ] **Test Password Reset/Email Change Effects**
- [ ] **Test Direct Requests**
- [ ] **Check Reuse of Tokens**
- [ ] **Test Sharing Unused Tokens**
- [ ] **Check for Leaked Tokens**
- [ ] **Test Access Control on Backup Codes**
- [ ] **Test OAuth Login Bypass**
- [ ] **Investigate OpenID Misconfiguration**
- [ ] **Check Sensitive Info Disclosure on 2FA Page**
- [ ] **Validate Backup Code Generation Exploitability**
- [ ] **Test Victim Account Blocking Technique**
- [ ] **Try JSON OTP Bypass Methods**
- [ ] **Make two HTTP requests with different accounts to generate OTP (SMS/Email to send email) and then use OTP code Num1 for Account 2 and vice versa**

# all:
#### **1. Flawed Two-Factor Verification Logic**
- **Summary**: Flawed logic allows attackers to manipulate cookies or session variables after the first authentication step to access another user's account.
- **Example**: Manipulating the `account` cookie to impersonate a victim after the first login step.

#### **2. Clickjacking on 2FA Disable Feature**
- **Summary**: Using iframes and social engineering to trick the victim into disabling their own 2FA settings.
- **Key Steps**: 
   - Iframe the 2FA disable page.
   - Exploit user interaction through social engineering.

#### **3. Response Manipulation**
- **Summary**: Modifying server response values to trick the system into accepting an unsuccessful 2FA attempt.
- **Example**: Change `success: false` to `success: true` in the response payload.

#### **4. Status Code Manipulation**
- **Summary**: Changing the HTTP status code to bypass security checks.
- **Example**: Modify a `4xx` error code to `200 OK` to bypass 2FA.

#### **5. 2FA Code Reusability**
- **Summary**: Reusing old 2FA codes to bypass checks.
- **Key Steps**: Test code reusability over multiple sessions and across longer durations.

#### **6. CSRF on 2FA Disable Feature**
- **Summary**: Exploiting Cross-Site Request Forgery to disable 2FA without user interaction.
- **Example**: Use existing session information to disable 2FA through CSRF attacks.

#### **7. Backup Code Abuse**
- **Summary**: Using brute-force and response manipulation techniques to bypass backup code checks.

#### **8. Enabling 2FA Doesn't Expire Previous Sessions**
- **Summary**: Failure to invalidate existing sessions upon enabling 2FA.
- **Example**: Testing session persistence across multiple devices.

#### **9. 2FA Refer Check Bypass**
- **Summary**: Manipulating the referer header to fool the application into skipping 2FA checks.
- **Example**: Change the referer header to a URL that appears to come from a 2FA-confirmed page.

#### **10. 2FA Code Leakage in Response**
- **Summary**: Inspecting server responses to detect if the 2FA code is being leaked inadvertently.

#### **11. JS File Analysis**
- **Summary**: Analyzing JavaScript files for exploitable information that may compromise the 2FA process.

#### **12. Lack of Brute-Force Protection**
- **Summary**: Absence of rate-limiting allows unlimited attempts to brute-force the 2FA code.
- **Example**: Repeatedly sending 2FA code requests or brute-forcing code input fields.

#### **13. Password Reset/Email Change - 2FA Disable**
- **Summary**: Exploiting password reset or email change functions to bypass or disable 2FA.

#### **14. Missing 2FA Code Integrity Validation**
- **Summary**: Using a valid 2FA code from another account to bypass the victim's 2FA.

#### **15. Direct Request**
- **Summary**: Directly accessing authenticated pages or steps without completing 2FA.
- **Example**: Navigating directly to pages and altering the referer header to appear 2FA authenticated.

#### **16. Reusing Tokens**
- **Summary**: Attempting to reuse tokens or one-time codes beyond their intended session scope.

#### **17. MFA Token Scope Confusion**
- **Summary**: Testing whether MFA tokens are valid outside their intended scope.

#### **18. Sharing Unused Tokens**
- **Summary**: Using unused tokens from one account in another account to bypass 2FA.

#### **19. Leaked Token**
- **Summary**: Identifying tokens that are inadvertently leaked in the response or logs.

#### **20. Session Permission Attack**
- **Summary**: Exploiting session vulnerabilities to pass 2FA checks on a victim's account using attacker session data.

#### **21. Password Reset Function Exploitation**
- **Summary**: Abusing the password reset process to bypass 2FA and gain unauthorized access.

#### **22. Lack of Rate Limit**
- **Summary**: Checking if there are any limitations on the number of 2FA attempts.
- **Example**: Testing silent rate limits by trying multiple incorrect codes followed by a correct one.

#### **23. Flow Rate Limit but No Brute-Force Limit**
- **Summary**: Bypassing rate limits through slow brute-forcing techniques.

#### **24. Re-send Code and Reset Limit**
- **Summary**: Resetting the brute-force limit by resending the same code repeatedly.

#### **25. Client-Side Rate Limit Bypass**
- **Summary**: Using client-side bypass techniques to overcome rate limitations.

#### **26. Lack of Rate Limit Re-sending Code via SMS**
- **Summary**: Draining resources by continuously resending the 2FA code via SMS.

#### **27. Infinite OTP Regeneration**
- **Summary**: Generating OTPs indefinitely until one matches the required code.

#### **28. Guessable Cookie**
- **Summary**: Exploiting weak cookie structures used in "remember me" features.

#### **29. IP Address Manipulation**
- **Summary**: Impersonating a user's IP address using headers like `X-Forwarded-For`.

#### **30. Subdomain Vulnerabilities**
- **Summary**: Using outdated or vulnerable subdomains to bypass modern 2FA systems.

#### **31. API Endpoint Testing**
- **Summary**: Finding insecure versions of API endpoints to bypass 2FA checks.

#### **32. Previous Sessions Persistence**
- **Summary**: Ensuring that previous sessions are not terminated when 2FA is activated.

#### **33. Improper Access Control to Backup Codes**
- **Summary**: Stealing backup codes due to improper security controls.

#### **34. Information Disclosure on 2FA Page**
- **Summary**: Identifying sensitive information disclosed on the 2FA page.

#### **35. Bypass 2FA with Null or 000000 Code**
- **Summary**: Using null values or specific placeholder codes to bypass 2FA.

#### **36. Previously Created Sessions Continue After MFA Activation**
- **Summary**: Persistence of old sessions after multi-factor authentication (MFA) is enabled.

#### **37. Enable 2FA Without Email Verification**
- **Summary**: Allowing 2FA setup without verifying the registered email address.

#### **38. Password Not Checked When Disabling 2FA**
- **Summary**: Disabling 2FA without validating the account password.

#### **39. Bypass Using Email MFA Mode**
- **Summary**: Manipulating email-based MFA settings to bypass checks.

#### **40. 2FA Bypass by Sending Blank Code**
- **Summary**: Submitting a blank 2FA code to trick the server into bypassing the check.

---

## Some Other Methods And Refreness:
   1. HowToHunt By Kathan Patel: [OTP ByPass](https://kathan19.gitbook.io/howtohunt/authentication-bypass/otp_bypass) 

---

## Legal and Ethical Disclaimer

This repository is intended solely for educational and research purposes to help improve system security. Unauthorized use of these techniques for illegal purposes is strictly prohibited. Always obtain permission before testing on any system. Misusing the information in this repository may lead to criminal charges, and the creators are not responsible for any illegal activities resulting from using this content.
