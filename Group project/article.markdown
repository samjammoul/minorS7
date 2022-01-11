---
layout: page
title: Article
parent: Group project
permalink: /Group-project-8/
nav_order: 8
---
# Secure your system in 10 minutes without writing one line of code!

![img_1.png](img_1.png)

## Introduction
Present-day sophisticated and innovative attacks have resulted in exponentially increasing security problems. This article, therefore, presents a project case and an easy security solution that is used to minimize the risk of breaking the authentication and authorization of that project. Besides that, the article will show the Keycloak concept and what is keycloak, and how keycloak works with other software.


## Concept of the project
First, we will explain the project concept and the project case, and then we will discuss the chosen solution for this case. The project is about a cybersecurity training environment for ICT students and governmental trainees. To deliver a blue team experience, there will be a dashboard to monitor if there are abnormalities with the application and to take countermeasures against them. For the red team experience, there will be the option to perform attacks on the application. By performing the attacks, they get a better understanding of how the attacks work. Therefore, it will be easier to take countermeasures against them.

The target users of the Red VS Blue team training game workshop are relatively new to cybersecurity and have limited to no experience in performing cybersecurity attacks or working in a SOC (Security Operations Center). They need to be guided during the workshop and have a smooth and fun learning experience.


## The reason to choose Keycloak:
After developing the basic features, we need to have user management that could limit the user access to data and features of the project system. Keycloak was one of the options to have easy and secure user access management services. We need a solution which is doesn't take a long time to set up and provides security features and is easy to use and maintain. We have chosen Keycloak because it provides security features and is easy to set up and maintain. Furthermore, Keycloak provides a flexible single sign-on that the client could use in the future.


## What is Keycloak?
We already mentioned Keycloak many times, but what is keycloak, and how keycloak works with OIDC protocol? Keycloak is an open-source identity and access management solution which mainly aims at applications and services. Users can authenticate with Keycloak rather than individual applications. So, the applications don’t have to deal with login forms, authenticating users, and storing users. Once logged in to Keycloak, users don’t have to log in again to access different applications. The same thing is applicable to sign-out. Keycloak offers everything a sophisticated user management tool needs – without having to log on repeatedly with every login and into every system-as well as system security, social logins, support for mobile apps, and integration into other solutions. [[1]](#1)


## How keycloak works with OIDC protocol?


![img_12.png](img_12.png)

OIDC is an authentication protocol that is an extension of OAuth 2.0. OAuth 3.0 is only a framework for building authorization protocols, but OIDC is a full-fledged authentication and authorization protocol. OIDC authentication flow when integrated with keycloak: [[1]](#1)

Browser visits application. The application notices the user is not logged in, so it redirects the browser to keycloak to be authenticated. The application passes along a call-back URL(a redirect URL) as a query parameter in this browser redirect that keycloak will use when it finishes authentication.

Keycloak authenticates the user and creates a one-time, very short-lived, temporary code. Keycloak redirects back to the application using the call-back URL provided earlier, and additionally adds the temporary code as a query parameter in the call-back URL.

The application extracts the temporary code and makes a background out of band REST invocation to keycloak to exchange the code for identity, access, and refresh token. Once this temporary code has been used to obtain the tokens, it can never be used again. This prevents potential replay attacks.


## Conclusion
There are many available solutions for user access management like cloud solutions (for example Amazon cloud Identity and Access Management) or another service that offers IAM solutions like Okta. Analyzing the project requirements is the first step to choosing the right security framework for this project. If the requirements required some features that do not exist in an existed security framework solution, then developing a security service that suits the requirements will be a better option. Maybe some developers like to develop their own IAM framework by using some security libraries and features, but the question is how long will take to develop this framework, and is this framework well secured?


# References

<a name="1"></a>
[1] Securing Applications and Services Guide. (n.d.). Keycloak.  [https://www.keycloak.org/docs/latest/securing_apps/](https://www.keycloak.org/docs/latest/securing_apps/)
