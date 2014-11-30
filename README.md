NeNews2JSON
=========

news2json - News (RFC5536 / RFC1036) to JNTP (JSON) GateWay for INN

Copyright (c) 2014, Gérald Niel

SYNOPSIS
========

INN gives us

 	@token@ <message-id> feeds
 	
for each article that needs to be sended.  We invoke sm on the
localhost to get the actual article, convert it to json string and
send it to JNTP server over HTTP.

In the INN's newsfeeds file, you need to have a channel feed:

 	news2json!:!*:Ac,Tc,Wnm*:<pathbin>/news2json

and a site for each of the various jntp site you're feeding,
such as

 	nemo.gegeweb.org/from-jntp:!*,local.*:Ap,Tm:news2json!

According to JNTP RFC (see http://www.nemoweb.net/?page_id=75),
if your hostname doesn't match with your public ip/hostname
configured for your server by the JNTP server you're feeding you
need to fix your 'fromname' in the optional &lt;pathetc&gt;/news2json.cf.

This file map jntp fqdn feed with hostname in one line per feed needed
to be fixed.

For exemple if your hostname (fromhost in innfeed.conf) is
name.domain.local but you need to be jntp.public.tld :

	# Feed (fqdn in newsfeeds)		Fromname
	name.domain.local				jntp.public.tld

Signing Jid with ssl/RSA 1024 key:
----------------------------------
this program attempt to find ssl/RSA keys pair in <pathetc>/ssl.

Create the folder if not exists:

	$ sudo -u news mkdir <pathetc>/ssl
	$ sudo chmod 700 <pathetc>/ssl

Generate keys pair

	$ sudo -u news openssl genrsa -out <pathetc>/ssl/jntp.key 1024
	$ sudo -u news openssl rsa -in <pathetc>/ssl/jntp.key -pubout <pathetc>/ssl/jntp.cert

DESCRIPTION
===========

News (NNTP) to JSON (JNTP) channel backend.

AUTHOR
======

Gérald Niel, gerald.niel@gmail.com

All rights reserved.

This program is free software; you can redistribute it and/or modify it
under the same terms as Perl 5.10.0. For more details, see the full
text of the licenses in the directory LICENSES.
