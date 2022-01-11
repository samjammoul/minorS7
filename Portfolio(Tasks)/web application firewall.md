---
layout: page
title: Web application firewall
parent: Tasks
permalink: /tasks14/
nav_order:
---
# Web application firewall 

## Table of contents

[ What is the web application firewall? ](#id1)

[ OWASP ModSecurity Core Rule Set ](#id1_2)

[ Set up web application firewall with Ubuntu server  ](#id1_3)

<a name="id1"></a>

## 1 What is the web application firewall?

A web application firewall (WAF) is a specific form of application firewall that filters, monitors, and blocks HTTP traffic to and from a web service. By inspecting HTTP traffic, it can prevent attacks exploiting a web application's known vulnerabilities, such as SQL injection, cross-site scripting (XSS), file inclusion, and improper system configuration. [[1]](#1)

<a name="id1_2"></a>

## 2 OWASP ModSecurity Core Rule Set

The OWASP ModSecurity Core Rule Set (CRS) is a set of generic attack detection rules for use with ModSecurity or compatible web application firewalls. The CRS aims to protect web applications from a wide range of attacks, including the OWASP Top Ten, with a minimum of false alerts. The CRS provides protection against many common attack categories, including SQL Injection, Cross Site Scripting, Local File Inclusion, etc. [[2]](#2)

<a name="id1_3"></a>

## 3 Set up web application firewall with Ubuntu server

In this section, I will set up a ModSecurity firewall in the Ubuntu server for my group project. In my group project, we should deploy two servers, the first one is for the backend and the second one for the front-end. I will use the OWASP ModSecurity Core Rule Set, which is standard rules to secure web applications and prevent the OWASP top 10 vulnerabilities. [[3]](#3)

### Step 1: Install ModSecurity with Apache on Debian/Ubuntu [[3]](#3)

The ModSecurity module for Apache is included in the default Debian/Ubuntu repository. To install it, run

```
sudo apt install libapache2-mod-security2

```

Then enable this module.

```
sudo a2enmod security2

```

Restart Apache for the change to take effect.

```
sudo systemctl restart apache2

```

### Step 2: Configure ModSecurity [[3]](#3)

In the `/etc/apache2/mods-enabled/security2.conf` configuration file, you can find the following line.

```
IncludeOptional /etc/modsecurity/*.conf
```

![Captcha verificatie vraag -
CheckMarket](../myMediaFolder/media/waf%201.PNG)

This means Apache will include all the `*.conf files in /etc/modsecurity/` directory. We need to rename the modsecurity.conf-recommended file to make it work.

```
sudo mv /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
```

Then edit this file with a command-line text editor like Nano.

```
sudo nano /etc/modsecurity/modsecurity.conf
```

Find the following line.

```
SecRuleEngine DetectionOnly

```

This config tells ModSecurity to log HTTP transactions, but takes no action when an attack is detected. Change it to the following, so ModSecurity will detect and block web attacks.

`SecRuleEngine On`
Then find the following line (line 186), which tells ModSecurity what information should be included in the audit log.

`SecAuditLogParts ABDEFHIJZ`


However, the default setting is wrong. You will know why later when I explain how to understand ModSecurity logs. The setting should be changed to the following.

`SecAuditLogParts ABCEFHJKZ`

Save and close the file. Then restart Apache for the change to take effect. (Reloding the web server isn’t enough.)

```
sudo systemctl restart apache2
```

### Step 3: Install the OWASP Core Rule Set (CRS) [[3]](#3)
To make ModSecurity protect your web applications, we need to define rules to detect malicious actors and block them. For beginners, it’s a good idea to install existing rule sets, so we can get started quickly and then learn the nitty-gritty down the road. There are several free rule sets for ModSecurity. The OWASP Core Rule Set (CRS) is the standard rule set used with ModSecurity.

Download the latest OWASP CRS from GitHub.
```
wget https://github.com/coreruleset/coreruleset/archive/v3.3.0.tar.gz
```

Extract the file.
```
tar xvf v3.3.0.tar.gz
```

Create a directory to store CRS files.
```
sudo mkdir /etc/apache2/modsecurity-crs/
```
Move the extracted directory to /etc/apache2/modsecurity-crs/.
```
sudo mv coreruleset-3.3.0/ /etc/apache2/modsecurity-crs/
```
Go to that directory.

```
cd /etc/apache2/modsecurity-crs/coreruleset-3.3.0/
```
Rename the crs-setup.conf.example file.

```
sudo mv crs-setup.conf.example crs-setup.conf
```

Edit the /etc/apache2/mods-enabled/security2.conf file.

```
sudo nano /etc/apache2/mods-enabled/security2.conf
```

Find the following line, which loads the default CRS files.

```
IncludeOptional /usr/share/modsecurity-crs/*.load
```
Change it to the following, so the latest OWASP CRS will be used.

```
IncludeOptional /etc/apache2/modsecurity-crs/coreruleset-3.3.0/crs-setup.conf
IncludeOptional /etc/apache2/modsecurity-crs/coreruleset-3.3.0/rules/*.conf
```
Save and close the file. Then test Apache configuration.

```
sudo apache2ctl -t
```

If the syntax is OK, then restart Apache.

```
sudo systemctl restart apache2
```

### Step 4: Testing [[3]](#3)
To check if ModSecurity is working, you can launch a simple SQL injection attack on your own website. (Please note that it’s illegal to do security testing on other people’s websites without authorization.) Enter the following URL in your web browser.

```
https://172.16.1.27/?id=3 or 'a'='a'
```

If ModSecurity is working properly, your Apache web server should return a 403 forbidden error message.

Figure 2 shows that the firewall has blocked the injected request.

![Captcha verificatie vraag -
CheckMarket](../myMediaFolder/media/waf%202.PNG)

*Figure 2*


# References

<a name="1"></a>
[1] Contributors to Wikimedia projects. (2014, February 18). Web application firewall - Wikipedia. Wikipedia, the free encyclopedia. [https://en.wikipedia.org/wiki/Web_application_firewall](https://en.wikipedia.org/wiki/Web_application_firewall)

<a name="2"></a>
[2] Unknown, U. (n.d.). OWASP ModSecurity Core Rule Set. OWASP Foundation | Open Source Foundation for Application Security. [https://owasp.org/www-project-modsecurity-core-rule-set/](https://owasp.org/www-project-modsecurity-core-rule-set/)

<a name="3"></a>
[3] Unknown, U. (n.d.). How to Use UFW Firewall on Debian, Ubuntu, Linux Mint. LinuxBabe. [https://www.linuxbabe.com/security/ufw-firewall-debian-ubuntu-linux-mint-server](https://www.linuxbabe.com/security/modsecurity-apache-debian-ubuntu)
