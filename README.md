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

### 11. Password Reset/Email Change - 2FA Disable
- **Summary**: Exploiting password reset or email change functions to bypass or disable 2FA.

### 12. Re-sending Code and Reset Limit
- **Summary**: Resetting the brute-force limit by resending the same code repeatedly.

### 13. Leaked Token
- **Summary**: Identifying tokens that are inadvertently leaked in the response or logs.

### 14. Infinite OTP Regeneration
- **Summary**: Generating OTPs indefinitely until one matches the required code.

### 15. Subdomain Vulnerabilities
- **Summary**: Using outdated or vulnerable subdomains to bypass modern 2FA systems.

---

## Advanced Bypass Techniques

### 16. Session Permission Attack
- **Summary**: Exploiting session vulnerabilities to pass 2FA checks on a victim's account using attacker session data.

### 17. Guessable Cookie Exploitation
- **Summary**: Exploiting weak cookie structures used in "remember me" features to bypass 2FA.

### 18. IP Address Manipulation
- **Summary**: Impersonating a user's IP address using headers like `X-Forwarded-For`.

---

## Comprehensive Checklist

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

#### **17. Sharing Unused Tokens**
- **Summary**: Using unused tokens from one account in another account to bypass 2FA.

#### **18. Leaked Token**
- **Summary**: Identifying tokens that are inadvertently leaked in the response or logs.

#### **19. Session Permission Attack**
- **Summary**: Exploiting session vulnerabilities to pass 2FA checks on a victim's account using attacker session data.

#### **20. Password Reset Function Exploitation**
- **Summary**: Abusing the password reset process to bypass 2FA and gain unauthorized access.

#### **21. Lack of Rate Limit**
- **Summary**: Checking if there are any limitations on the number of 2FA attempts.
- **Example**: Testing silent rate limits by trying multiple incorrect codes followed by a correct one.

#### **22. Flow Rate Limit but No Brute-Force Limit**
- **Summary**: Bypassing rate limits through slow brute-forcing techniques.

#### **23. Re-send Code and Reset Limit**
- **Summary**: Resetting the brute-force limit by resending the same code repeatedly.

#### **24. Client-Side Rate Limit Bypass**
- **Summary**: Using client-side bypass techniques to overcome rate limitations.

#### **25. Lack of Rate Limit Re-sending Code via SMS**
- **Summary**: Draining resources by continuously resending the 2FA code via SMS.

#### **26. Infinite OTP Regeneration**
- **Summary**: Generating OTPs indefinitely until one matches the required code.

#### **27. Guessable Cookie**
- **Summary**: Exploiting weak cookie structures used in "remember me" features.

#### **28. IP Address Manipulation**
- **Summary**: Impersonating a user's IP address using headers like `X-Forwarded-For`.

#### **29. Subdomain Vulnerabilities**
- **Summary**: Using outdated or vulnerable subdomains to bypass modern 2FA systems.

#### **30. API Endpoint Testing**
- **Summary**: Finding insecure versions of API endpoints to bypass 2FA checks.

#### **31. Previous Sessions Persistence**
- **Summary**: Ensuring that previous sessions are not terminated when 2FA is activated.

#### **32. Improper Access Control to Backup Codes**
- **Summary**: Stealing backup codes due to improper security controls.

#### **33. Information Disclosure on 2FA Page**
- **Summary**: Identifying sensitive information disclosed on the 2FA page.

#### **34. Bypass 2FA with Null or 000000 Code**
- **Summary**: Using null values or specific placeholder codes to bypass 2FA.

#### **35. Previously Created Sessions Continue After MFA Activation**
- **Summary**: Persistence of old sessions after multi-factor authentication (MFA) is enabled.

#### **36. Enable 2FA Without Email Verification**
- **Summary**: Allowing 2FA setup without verifying the registered email address.

#### **37. Password Not Checked When Disabling 2FA**
- **Summary**: Disabling 2FA without validating the password of the account.

#### **38. Bypass Using Email MFA Mode**
- **Summary**: Manipulating email-based MFA settings to bypass checks.

#### **39. 2FA Bypass by Sending Blank Code**
- **Summary**: Submitting a blank 2FA code to trick the server into bypassing the check.

---

## Legal and Ethical Disclaimer

This repository is intended solely for educational and research purposes to help improve system security. Unauthorized use of these techniques for illegal purposes is strictly prohibited. Always obtain permission before testing on any system. The misuse of the information contained in this repository may lead to criminal charges, and the creators are not responsible for any illegal activities that result from using this content.
