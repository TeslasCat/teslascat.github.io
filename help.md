# How to access the Macak IRC net

All our servers run SSL on port 6697.  
Please make sure to verify the SSL fingerprint.

## Servers 

You can randomly be assigned a server via round robin by using: 

| Domain Name | Ports |
|:--|:--|
| irc.macak.co.uk | 6697 |

The table below details our services.

| Domain Name | Ports | Server Name | Location | SSL Fingerprint |
|:--|:--|:--|:--|:--|
| irc.hackthis.co.uk | 6697 | Keef | London, UK | F0:06:59:F2:84:9E:89:DA:F2:78:18:2A:25:32:0A:EB:C5:B2:97:16 |
| irc.port22.co.uk   | 6697 | HammerFall | London, UK | AB:8C:5B:3F:11:5A:0F:52:E4:14:47:E5:56:EB:19:5B:CE:59:53:7E |

### Verifying SSL Fingerprint

Vertify the server you're connecting to by running the below command and check the fingerprint out matches the above.

	echo | openssl s_client -connect <hostname:port> | openssl x509 -noout -fingerprint

- **echo** - This sends a newline command to the connection, forcing it to close so we don't have to wait for it to time out.
- **openssl s_client** - This tells openssl to act as a generic SSL/TLS client.
- **-connect \<hostname:port\>** - This is the server to connect too. e.g. *irc.port22.co.uk:6697*
- **x509 -noout -fingerprint** - This decodes the key and displays the fingerprint.

## Tor

Our Tor servers do not use SSL, not even self-signed. This is a weakness and you should take extra precautions (Such as GPG/mpOTR/OMEMO/Np1sec) depending on your threat model.

Read Tor's IRC guide for more information on how to protect yourself and best guidelines - <https://trac.torproject.org/projects/tor/wiki/doc/TorifyHOWTO/IrcSilc>

| Address | SSL Fingerprint | Notes |
|:--|:--|:--|
| tp7nwuggtryzbla7.onion/6697 | N/A | N/A |

# Services 

## NickServ {} 

- commands 

## ChanServ 

- commands 

# Clients

## WeeChat

WeeChat is a command line IRC client. [User Guide](https://weechat.org/files/doc/stable/weechat_user.en.html)

Screen allows you to detach and attach a running process.

	screen weechat

Add a server and connect.

	/server add macak irc.macak.co.uk/6697 -ssl
	/connect macak

You should now be connected to the IRC network, and able to register/identify your nickname via the [services](#NickServ)

If you want to detach the session press ```ctrl+a+d``` and to attach: 

	screen -r 

### SASL Authentication

Once you've registered your nickname you should identify yourself to the server via SASL.

First make sure that weechat stores your information encrypted. By using a passphrase.

	/secure passphrase <your passphrase>

To add secured data use ```/secure set```. In this case we want to store our nick password.

	/secure set macak <password>

And now we need to tell weechat to use the login data.

	/set irc.server.Macak.sasl_username <username>
	/set irc.server.Macak.sasl_password "${sec.data.freenode}"
