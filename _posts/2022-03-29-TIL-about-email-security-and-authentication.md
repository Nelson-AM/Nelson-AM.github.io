---
layout: post
title: "TIL (A Thing or Two) About Email Security and Authentication"
date: 2022-03-29 12:00:00
categories: blog
tags: email security
---

The main TIL here is that Email is surprisingly easy to spoof. For example, you can use [Emkei's mailer](https://emkei.cz/) to send emails as anyone to anyone. Using an online anonymous mailer like this is a good test of your email authentication and spam filter settings. The more surprising thing, to me at least, is that this is by design, kind of. Time to get into email standards!

<!-- more -->

## Email Protocols

The [Simple Mail Transfer Protocol (SMTP)](https://datatracker.ietf.org/doc/html/rfc5321) is an internet standard which is commonly used for sending and relaying email messages. SMTP client authentication can be done based on location or user credentials. However, to send email, all you need to do is to perform a valid SMTP transaction. An SMTP transaction consists of three sequences or commands. SMTP does not define what an acceptable sender mailbox specification is, this is up to the receiving party. To remedy this situation, there are three more standards/protocols to discuss.

The [Sender Policy Framework](https://datatracker.ietf.org/doc/html/rfc7208) (SPF) defines which servers can send email as coming from a specific domain. This can be done by adding a record to a server's DNS information. With an SPF record in place, receiving mail servers can check whether the originating server is authorised to have sent that email.

With [DomainKeys Identified Mail](https://datatracker.ietf.org/doc/html/rfc6376) (DKIM) a cryptographic signature is added to emails by the sending mailserver. The public key for DKIM is published as a DNS record against which the signatures can be checked. DKIM associates emails with a domain name so forged sender addresses can be detected. Since DKIM signs parts of the email message, it also ensures that these fields have not been (substantially) changed since the email was sent.

Finally, [Domain-based Message Authentication, Reporting & Conformance](https://datatracker.ietf.org/doc/html/rfc6376) (DMARC) ties it all together. DMARC is an advisory policy, informing receivers what should be done if an SPF or DKIM check fails. There are three policies:

- **None**: no special treatment is required. This should only be used for testing.
- **Quarantine**: treat with suspicion, for example flag messages as suspicious or deliver them to the spam folder.
- **Reject**: simply reject messages that fail a check (bounce).

Optionally, DMARC can produce aggregate and forensic reports which are sent to a specified email address.

## Checking your settings

MXToolBox (among others) has tools to check all three policies: [SPF](https://mxtoolbox.com/spf.aspx), [DKIM](https://mxtoolbox.com/dkim.aspx) and [DMARC](https://mxtoolbox.com/dmarc.aspx).
