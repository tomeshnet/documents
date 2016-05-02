# tomesh.net Emails

Our email service is hosted by our friends from [Seattle Meshnet](https://seattlemesh.net).

## DNS Configurations

| Hostname | Record Type | Value |
| --- | --- | --- |
| tomesh.net | MX | mail.seattlemesh.net |
| tomesh.net | TXT | v=spf1 redirect=seattlemesh.net |
| q._domainkey.tomesh.net | TXT | v=DKIM1; k=rsa; t=y; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDOza/1J8LNAL1TPGtz2RpI0Cai9LokJmO7pxX/zk2tyyPD8yY5BRl3PabSvofR1o77dLnSCBoBAY/q4RgqnmFWRxxLxEwQjttTwCMv9EDSFonzu9D6v1+UsZwHJa22Vwi/dzfad9oQ2XIOwfsAkVFevWjMUFAgFdrtJpkznpMcJQIDAQAB |
| _dmarc.tomesh.net | TXT | v=DMARC1; p=none; rua=mailto:dmarc@seattlemesh.net; ruf=mailto:dmarcf@seattlemesh.net; fo=1 |
| autoconfig.tomesh.net | CNAME | autoconfig.meshwith.me |
| webmail.tomesh.net | CNAME | webmail.meshwith.me |

Here is [a tool to verify that everything is set up correctly](https://test.mail.meshwith.me/tomesh.net).

## Accounts

Mailbox accounts are set up through [this link](https://q.meshwith.me/postfixadmin/). The admin account is currently managed by @benhylau, please message him if you need mailboxes or forwarders set up. To access your tomesh.net email, it is recommended that you use your favourite IMAP/SMTP/POP3 client, but [a web client](https://webmail.tomesh.net) is also available.

**Note:** After creating a new mailbox, you need to send it an email before you can access it through webmail.
