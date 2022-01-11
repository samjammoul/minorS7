---
layout: page
title: Database security
parent: Tasks
permalink: /tasks12/
nav_order: 12
---
# Database security 

## Table of contents
1. [ Principle of least privilege ](#principleOfLeastPrivilege)
2. [ Data encryption in the database ](#dataencryptioninthedatabase)
3. [ Backup and recovery ](#backupandrecovery)

<a name="principleOfLeastPrivilege"></a>
## 1 Principle of least privilege
The principle of the least privilege goes about the access control of the users. The user should have minimum access to the database base to do a specific job or use limited features.

I set up a MySQL server in order to add new users to the database.  Figure 1 shows the dashboard of PhpMyAdmin. I added a new user in the database, this user could only insert new data and update data and read data.
![No alt text provided for this
image](../myMediaFolder/media/Capture55.png)

**figure 1**

<b></b>
<b></b>

Figure 2 shows all the users of the database. User 1 has limited access to the database, and this user could access the database from any hot. The root of the database has no access limit, but the root could only access the database locally.
![No alt text provided for this
image](../myMediaFolder/media/Capture 66.png)
**figure 2**
<a name="dataencryptioninthedatabase"></a>
## 2 Data encryption in the database
**Data encryption best practices**

1. Keep encryption key secure
It can be easy to make mistakes that allow unauthorized parties to access your data. If the hackers could have the access keys, that means that they could also access the sensitive encrypted data. To solve that, the key should be stored in a local encrypted file. [[1]](#1)

2. Encrypt all types of sensitive data, no matter where they are stored or how unlikely you think someone is to find them. A Lot of big-name companies have been breached simply because they left important data unencrypted and someone gained access to it. Encrypting data, make it much harder for someone who is able to breach your systems to do something bad. [[1]](#1)

3. Effective data encryption entails not just making data unreadable to unauthorized parties but doing so in a way that uses resources efficiently. If it is taking too long or consuming too much CPU time and memory to encrypt data, consider switching to a different algorithm or experimenting with settings in data encryption tools. [[1]](#1)


I already implement AES algorithm by using Java language([Implement data encryption](ImplementDataEncryption.md). The simple application that I implemented will be used also in order to encrypt and decrypt the data before insert/read it from the database.



<a name="backupandrecovery"></a>
## 3 Backup and recovery

### 3.1 Backup

Figure 3 shows that the step to make a backup for the database. The user could choose which tables must be exported and which format. It's a manual option. This solution isn't useful for the companies, it's a better option if this process will be automated by using special tools to make a local backup or even in the cloud.
![No alt text provided for this
image](../myMediaFolder/media/backup db.png)
**figure 3**

### 3.2 Recovery

Figure 4 shows how we could recover and import a file that contains the tables and the databases we backed up if we lost the data.
![No alt text provided for this
image](../myMediaFolder/media/Recovery.png)
**figure 4**
# References

<a name="1"></a>
1. <https://www.precisely.com/blog/data-security/data-encryption-101-guide-best-practices>