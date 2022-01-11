---
layout: page
title: Red Team - Blue Team test event
parent: Tasks
permalink: /tasks10/
nav_order: 10
---
# Red Team - Blue Team test event
{: .no_toc }


In this section, I will show how we as a group prepared for the red/blue and what we did during the event, and finally I will show the results from the event.


<nav>
  <h4>Table of Contents</h4>
  * this unordered seed list will be replaced by toc as unordered list
  {:toc}
</nav>

## 1. The project
The CTF portal is an application for my group project. This application was started by my group as an application to be tested with a general pen test at the network and application.

## 2. Preparing for event
Together with my group project, we decided to set up a second environment that is similar to the original environment that we already set up. We decided to use my own personal Netlab account for this event. We did that because we want to have a backup of the original environment.

### 2.1 Setup Ubuntu servers and web application firewall
I am responsible to set up 2 Ubuntu servers with two WAF(web application firewall).
Setting up the Ubuntu server is just using the Ubuntu server templates that already exist on Netlab.

**1.1.1 Install Apache server in Ubuntu**


To install Apache, install the latest meta-package apache2 by running: [[1]](#1)


`sudo apt update`

`sudo apt install apache2`

After letting the command run, all required packages are installed and we can test it out by typing in our IP address for the web server. [[1]](#1)


![No alt text provided for this
image](https://ubuntucommunity.s3.dualstack.us-east-2.amazonaws.com/original/2X/7/771159b35c97e429247aac754ad44bf06cc1efa8.png)
**Figure 1**

<b></b>

**1.1.2 Set up and install ModSecurity**
I already explain the steps, and I showed how I did it for my group project in my portfolio. [This is a link](https://samjammoul.github.io/S7/tasks14/) to my portfolio, and I explain and show the steps that I did to set up ModSecurity and how to config the firewall rules and test it.

## 3. During the event
Throughout the event, we were available for support and questions from the red team. 

## 4. Results of the event
The red teamers were able to find two issues.
If a flag was entered incorrectly, the hash of this flag was also returned. Even though it is hashed with BCrypt and salt, this hash can potentially be cracked with a brute force attack that can make the flag obsolete.
By intercepting the response of the API with BurpSuite after filling in the flag, the response body can be adjusted. With this, the flagStatus can be changed from 'Invalid' to 'Valid', so that the frontend thinks that this flag has been filled in successfully. This allows the next flag to be filled in and the story is already partially revealed. 
However, this only applies to the executing client and a refresh will undo this, because the state of the flags in the backend is not changed via this method.
By combining the above two issues, the hashes of all flags can be retrieved in the first few minutes of the event. 
This makes it possible to brute force all flag hashes immediately and may be able to crack one before the end of the event.

## 5. Measures
The hash of the banner may by no means be delivered and is in this manner eliminated from the Programming interface reaction.

Also, the request for the banners and subsequently the storyline will be checked by impeding the early filling of banners at Programming interface level.

The issue of blocking the Programming interface reaction and changing the flagStatus to 'Substantial' won't be tended to. Nothing can be accomplished with this other than seeing the movements of a further phase of the story. The portrayal that goes with this might be delivered by the Programming interface once the past banner has been effectively filled in.

## 6. Reflection
I like the concept of this event, and it is helpful to find out some vulnerabilities in the system. On the other hand, the event was not well organized. Many students did not know that there is a kick-off presentation, many things weren't clear at the beginning. The red teams found two issues, and we have already fixed them.

## 7. References

<a name="1"></a>
[1] Install and Configure Apache | Ubuntu. (n.d.). Ubuntu. [https://ubuntu.com/tutorials/install-and-configure-apache#2-installing-apache](https://ubuntu.com/tutorials/install-and-configure-apache#2-installing-apache)



