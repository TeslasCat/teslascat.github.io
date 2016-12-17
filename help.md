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

	/secure set macak_pw <password>

And now we need to tell weechat to use the login data.

	/set irc.server.Macak.sasl_username <username>
	/set irc.server.Macak.sasl_password "${sec.data.macak_pw}"


# Services 

## NickServ

NickServ allows users to 'register' a nickname, and stop others from using that nick. NickServ allows the owner of a nickname to disconnect a user from the network that is using their nickname.
If a registered nick is not used by the owner for 30 days, NickServ will drop the nickname, allowing it to be reregistered.
 
For more information on a command, type:

	/msg NickServ help <command>

For a verbose listing of all commands, type:
	
	/msg NickServ help commands
 
The following commands are available:

| Command 		  | Description 								   |
|:---------------|:-----------------------------------------------|
|FDROP           | Forces dropping an account registration.|
|FREEZE          | Freezes an account.|
|FUNGROUP        | Forces removal of a nickname from an account.|
|GHOST           | Reclaims use of a nickname.|
|GROUP           | Adds a nickname to your account.|
|IDENTIFY        | Identifies to services for a nickname.|
|INFO            | Displays information on registrations.|
|LISTCHANS       | Lists channels that you have access to.|
|MARK            | Adds a note to a user.|
|REGISTER        | Registers a nickname.|
|SENDPASS        | Email registration passwords.|
|SET             | Sets various control flags.|
|UNGROUP         | Removes a nickname from your account.|
|VHOST           | Manages user virtualhosts.|
 
### Other commands

ACC, BADMAIL, DROP, FVERIFY, HELP, HOLD, 
LIST, LISTMAIL, LISTVHOST, LOGOUT, REGNOLIMIT, 
RESETPASS, RETURN, SETPASS, STATUS, TAXONOMY, 
VACATION, VERIFY

## ChanServ 

ChanServ gives normal users the ability to maintain control of a channel, without the need of a bot. Channel takeovers are virtually impossible when a channel is registered with ChanServ.
Registration is a quick and painless process. Once registered, the founder can maintain complete and total control over the channel. 
Please note that channels will expire after 30 days of inactivity, or if there are no eligible channel successors.
Activity is defined as a user with one of ```+FORforsv``` being on the channel.
Successors are primarily those who have the ```+R``` flag set on their account in the channel, although other people may be chosen depending on their access level and activity.
 
Commands can also be given on channel by prefixing one of '!' and omitting the channel name. These are called "fantasy" commands and can also be disabled on a per-channel basis.

For more information on a command, type:

	/msg ChanServ help <command>

For a verbose listing of all commands, type:
	
	/msg ChanServ help commands

The following commands are available:

| Command 		  | Description 								   |
|:----------------|:-----------------------------------------------|
| CLOSE           | Closes a channel. |
| FDROP           | Forces dropping of a channel registration. |
| FLAGS           | Manipulates specific permissions on a channel. |
| FTRANSFER       | Forces foundership transfer of a channel. |
| INVITE          | Invites you to a channel. |
| OP              | Gives channel ops to a user. |
| RECOVER         | Regain control of your channel. |
| REGISTER        | Registers a channel. |
| SET             | Sets various control flags. |
| UNBAN           | Removes a ban on a channel. |

### Other commands

ACCESS, AKICK, BAN, CLEAR, COUNT, DEOP, 
DEVOICE, DROP, GETKEY, HELP, HOLD, INFO, 
KICK, KICKBAN, LIST, MARK, ROLE, STATUS, 
TAXONOMY, TEMPLATE, TOPIC, TOPICAPPEND, 
TOPICPREPEND, VOICE, WHY
