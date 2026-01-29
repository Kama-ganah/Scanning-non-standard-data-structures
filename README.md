# Overview
During an assessment of the application’s session handling mechanisms, I identified a high-severity stored Cross-Site Scripting (XSS) vulnerability within a non-standard session cookie structure. The application used a custom cookie format that included user-controlled data, which was not properly sanitized before being processed and later rendered in an administrative context. By targeting this unconventional data structure with focused scanning, it was possible to trigger stored XSS, steal the administrator’s session cookie, and gain full administrative access.

# Steps Undertaken

Step 1: Logged into the application using standard user credentials to observe normal session behavior.

Step 2: Inspected HTTP traffic in Burp Suite and identified a non-standard session cookie format (username:token), where part of the value was user-controlled.

Step 3: Selected the user-controlled portion of the session cookie and performed a targeted “Scan selected insertion point” using Burp Scanner.

Step 4: Reviewed scan results indicating a stored XSS vulnerability in the cookie handling logic.

Step 5: Leveraged the identified XSS to exfiltrate the administrator’s session cookie when it was rendered in the admin’s browser.

Step 6: Reused the stolen session cookie to access the admin panel and perform privileged actions, including deleting a user.

# Conclusion

This assessment demonstrated that non-standard or legacy data structures, such as custom session cookie formats, can introduce critical vulnerabilities when user input is not strictly sanitized. By scanning beyond typical parameters and focusing on unconventional insertion points, a stored XSS flaw was uncovered that led to full session hijacking and administrative compromise. Robust input validation, secure session design, and regular testing of atypical data structures are essential to prevent similar issues.
