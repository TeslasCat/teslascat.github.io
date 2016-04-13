# How to access the Macak IRC net

At minimum all our servers run SSL on port 6697.  
Please make sure to verify the SSL fingerprint.

## Servers 

You can randomly be assigned a server via round robin by using: 

| Domain Name | Ports |
|:--|:--|
| irc.macak.co.uk | 6697 |

The table below details the features of out srevers.

| Domain Name | Ports | Server Name | Location | SSL Fingerprint |
|:--|:--|:--|:--|:--|
| irc.hackthis.co.uk | 6697 | Keef | London, UK | Missing |
| irc.port22.co.uk | 6697	  | HammerFall | London, UK | Missing |
| irc.matrix.ac | 6697 	  | Matrix | Frankfurt, Germany | Missing |

## Tor

Our Tor servers do not use SSL, not even self-signed. This is a weakness and you should take extra precautions (Such as GPG/mpOTR/OMEMO/Np1sec) depending on your threat model.

Read Tor's IRC guide for more information on how to protect yourself and best guidelines - <https://trac.torproject.org/projects/tor/wiki/doc/TorifyHOWTO/IrcSilc>

| Address | SSL Fingerprint | Notes |
|:--|:--|:--|
| tp7nwuggtryzbla7.onion/6697 | N/A | N/A |

# Services 

## NickServ 

- commands 

## ChanServ 

- commands 