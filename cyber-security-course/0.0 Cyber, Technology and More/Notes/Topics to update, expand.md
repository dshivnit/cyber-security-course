SSL/TLS (Layer 4 - Transport Layer)
HTTPS
MQTTS (Message Queuing Telemetry Transport Secured
DoT (DNS over TLS)
SIPS
SMTPS 465 and 587
POP3S 995
IMAPS 993
SFTP (SSH FTP)  same as SSH 22
FTPS (FTP Secure) port 990


```We have set the browser to log the session’s TLS keys so we can take a closer look at the traffic using Wireshark. This logging was achieved by adding an extra option to the browser shortcut. Executing `chromium --ssl-key-log-file=~/ssl-key.log` dumps the TLS keys to the `ssl-key.log` file.```
(THM lab -- just putting this as a placeholder so I can do some testing later)


man -k 'keyword' to search for man pages that have a particular keyword in them
