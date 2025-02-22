---
title: "How does Mail works with DNS MX records"
date: 2023-11-01
tags: ["Network"]
tags: ["#Other"]
---

## Breakdown of the email address

In general a email address is in formatted as `username @ domain.com`, we can break it down into:
- Address after the `@` sign, here `domain.com`, this is the domain of the target mail server, your server will check MX records of this domain from the DNS server, and sends the email to the corresponding IP of the domain.
- Address before the `@` sign, here `username`, is where the mail receiving server will put your emails at. In a classical mail (receiver) server, each user will have a unique folder, once a user ges a email from somebody on the internet, his/her email will get stored into this folder, here imagine there's a `\username` folder where all the `.eml` files will be located at.


## Sending email with help of DNS system

Email server is distinctive from the DNS system, in order for the email to work, the DNS system must be working. As the DNS system is the one that translates the domain name to the IP address, and the IP address is the one that is used by the email server to send and receive emails.



**Basic use-case of MX records**
- Once a email sender server request for the receiver server's address (using a domain name such as `gmail.com`, `outlook.com`, usually anything that comes after the `@` sign), they DNS server will check its **DNS MX records** and return the IP address. (note that alike the usual `A` and `CNAME` DNS record, the records will get cached onto your local network infrastructure until it reaches its its end of `TTL`) The mail sender server will then send the email through using the IP address.

**Multiple MX records**
- DNS system also have a unique features that will email server more stable, like how you might setup multiple web server redundancy in case of network failure, you can have multiple mail servers ready for receiving in case of a server failure on one server. This is achieved via having multiple MX records on the DNS server (for instance `MX1=111.111.111`, `MX2=222.222.222`, `MX3=333.333.333` ), if the mail sender fails to send the email to the the MX1 server (it might be busy, or down), the email will get send to the MX2 server (which will only **temporally store** the email and send it to the main MX1 server whenever it become available again; There can only be one server that saves the mails, MX2 only store the email before MX1 comes back)



----------
Reference:
- http://www.qqgzs.com/archives/email-dns.html
- https://cloud.tencent.com/developer/article/1115106