---
layout: page
title: Standard security principles
parent: Tasks
permalink: /tasks6/
nav_order: 6
---
# Standard security principles

These principles are taken from the OWASP Development Guide and comply
with the security principles outlined in Michael Howard and David
LeBlanc's book Writing Secure Code.

They include:

**Minimise attack surface area**

Adding a new feature to an application, increasing the risk of a
security vulnerability. The relationship between the restricting of
features and potential vulnerabilities is an inverse relationship that
means, if the application is restricted features has, the potential
vulnerabilities will be reduced. [[2]](#2)

Example[:]{dir="rtl"}

For example, if we have application X and that application has a search
feature. That search feature is potentially vulnerable to SQL injection
attacks, etc. To reduce the potential vulnerabilities, the developer
must limit the access of that feature for only registered users.

**Establish secure defaults**

The application must be secure by defaults. If a user wants to obtain
higher privileges, he should do steps to allowed him to obtain those
privileges. The application must have strong security rules, for example
how complex passwords should be, how often passwords must be
updated. [[2]](#2)

**The principle of Least privilege**

Conceding authorizations to a client past the extent of the fundamental
privileges of an activity can permit that client to acquire or change
data in undesirable ways. Subsequently, cautious appointment of access
rights can restrict aggressors from harming a framework. [[2]](#2)

**The principle of Defence in depth**

Multiple security controls that approach risks in different ways are the
best option for securing an application. So, instead of having one
security control for user access, you would have multiple layers of
validation, additional security auditing tools, and logging tools.

For example, instead of letting a user login with just a username and
password, you would use an IP check, a Captcha system, logging of their
login attempts, brute force detection, and so on. [[2]](#2)

**Fail securely**

This principle states that applications should fail in a secure way.
Failure should not give the user additional privileges, and it should
not show the user sensitive information like database queries or logs.
[[2]](#2)

**Don't trust services**

In many cases developers use external services to access additional
functions or data.

The application should not trust those services and should always check
the validation of data.

For example, it could be that the external service is hacked, and it
will send to application a malicious code instead of validated
data.[[2]](#2)

**Separation of duties**

The idea behind Separation of Duties is that no single role should have
too much authority.

While that focuses on making sure that people only have the privileges,
they need to do their job, this is about making sure their job isn't too
big.[[1]](#1)

**Avoid security by obscurity**

Imagine software which has a hard-coded secret username and password
combination. When authenticated, this account has full access to every
account in the system.
The [security](https://www.cprime.com/resource/white-papers/devsecops-playbook/) of
this system relies on the credentials of this account remaining a
secret. Over time, a growing number of users will gain access to this
account. Some will leave the company, but they won't forget the
password. At that point, the security of your application relies on the
good will of those employees. [[1]](#1)

**Keep security simple**

Developers should avoid the use of very sophisticated architecture when
developing security controls for their applications. Having mechanisms
that are very complex can increase the risk of errors.[[2]](#2)

**Fix security issues correctly**

If a security issue has been identified in an application, developers
should determine the root cause of the problem.

They should then repair it and test the repairs thoroughly. If the
application uses design patterns, it is likely that the error may be
present in multiple systems. Programmers should be careful to identify
all affected systems. [[2]](#2)

# References

<a name="1"></a>
[1] A. (2020, 11 december). Security by Design: 7 Application Security Principles You Need to Know. Cprime.  [https://www.cprime.com/resources/blog/security-by-design-7-principles-you-need-to-know/](https://www.cprime.com/resources/blog/security-by-design-7-principles-you-need-to-know/)

<a name="2"></a>
[2] Sveikauskas, D. (2021, 16 juni). Security By Design Principles According To OWASP. Patchstack. [ https://patchstack.com/security-design-principles-owasp/](https://patchstack.com/security-design-principles-owasp/)

