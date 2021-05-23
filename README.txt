mwhois
Copyright (c) 2015 Antonios A. Chariton <daknob.mac@gmail.com>

Description: 
mwhois is server software compatible with the whois(1) command
on most Linux and Unix systems.  It is  fully compliant with the
RFC 3912. It can serve domain name and  IPv4  whois records when
queried and uses a Linux / Unix filesystem structure for storing
all the records. 

Requirements:
- Linux / Unix based operating system
- Python 2.7

License:
The project is under the MIT License on its whole,  except from
the "netaddr" python library that has a separate license, which
is included in the respective folder.  The library  is included
in order to ensure compatibility and is updated when deemed
necessary.

Usage:
In order to use the server, simply run the whois(1) command  in
any operating system with the -h flag followed by your server's
IP Address and then the  query.  An  example  asking  localhost
about 10.0.0.0 is: whois -h 127.0.0.1 10.0.0.1.

Configuration:
In the file mwhoisd there are four (4)  configuration variables
in the beggining, lines 8-11, conveniently named as  following: 
LISTEN_ADDRESS,   LISTEN_PORT,   MAX_QUERY_SIZE   and   LOGFILE
Each one is self-explanatory, but here is the explanation  just
in case:
- LISTEN_ADDRESS : The IPv4 Address  the  server   listens   to
- LISTEN_PORT : The Port Number where  the  server  listens  at
- MAX_QUERY_SIZE : The maximum size, in bytes, of a valid query
                   for either an IPv4 Address or a Domain  Name
- LOGFILE : The file path where the logs of the server will  be
            saved to. If it is empty the server keeps  no  logs

Files:
There are several files in this repository that required and  a
few others that are optional but increase the ease of  use  for
this software:
- mwhoisd : The primary server than runs and serves all clients
            If  it  runs on the default port 43, or writes logs 
            in the default directory it  has  to  be running as 
            the user 'root'. 
- LICENSE : The license of the software
- DOC : This file, containing useful documentation
- add-ip : A helpful script to add IP Ranges  in  the  database
- add-ip-auto : A wizard for adding IP Blocks to  the  database
- add-ip-wind : A wizard to add IP Blocks w/ "ID" instead of AS
- add-domain : A script to add domain  names  in  the  database
- hwhois : A bash script to use in order to  contact  a  custom
           whois server such  as  whois.daknob.net  (127.0.0.1)
- netaddr : An external python library required for the  server
- db : A folder in which lies the internal database for lookups

Storage Structure:
The database that is served by mwhois is using the Linux / Unix
filesystem in order to store content. There is a  folder  named
"db" with two primary sub-folders, "ipv4" and "domains". In the
first folder, all whois content for IPv4 Addresses is  located,
and in the second folder, there is all the  whois  content  for 
the domain names. All IPv4 records are stored  in  files  named
after the IP Address  CIDR  Block.  For  example,  the  network
10.0.0.0/8 is stored in a file named 10.0.0.0-8  that  contains
all the information that will be served. All the new  lines  in
this file must be represented by <CR><LF> in order to  maintain
full compatibility with RFC 3912. As far as  domain  names  are 
concerned, the storage is similar, where the name of  the  file 
is the actual domain name.
