---
published: true
layout: article
title: SSL Everywhere or HSTS
abstract: We have to secure all the data of our users, not only registration, checkout and login. We need to secure the session data too.
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

# SSL Everywhere or HTTP Strict Transport Security

(I hope) Everyone knows, that it is important to secure (read as encrypt) our customer’s data. Because of all the evil hackers in the world and the bad ISPs which intercept all our data. 

## TL;DR
Use HTTP Strict Transport Security!

## The first problem: unencrypted personal data

But the real problems are the all-day security problems:
* I’m sitting at Starbucks, surfing over their unencrypted wifi, enjoy my coffee and work. Hopefully, all connections are encrypted: email, jabber, VPN to the office, what’s app... But often this is not the case. What happens, if a connection is not encrypted? Everyone in the wifi can listen.

You can encrypt the wifi, but for example [WEP](http://en.wikipedia.org/wiki/Wired_Equivalent_Privacy) doesn't solve the problem, because it doesn't have user isolation. But [WPA](http://en.wikipedia.org/wiki/Wi-Fi_Protected_Access) helps.

If the connection is not encrypted, one can read your emails, your whats app messages or your email login.

## First solution: [TLS (formerly known as SSL)](http://en.wikipedia.org/wiki/Transport_Layer_Security)

Because of the painted scenario all our login and registration pages are SSL secured. We encrypt every transmission, where important data are sent. You can use TLS for nearly everything:

- SMTP -> SMTPS
- IMAP -> IMAPS
- POP3 -> POP3S
- HTTP -> HTTPS
- and so on

## Second problem: unencrypted session data

Do you only encrypt the login and registration page? Oh, the checkout too. Great! But what is with all the other pages, like »Home«, »Privacy Policy«, »About Us« and so on? 
Do you think there are no important data transmitted? You are wrong. With every request there is the session ID sent in a cookie. This means, you convey (a maybe authorized session id) unencrypted personal data in your HTTP header.

The attack vector might be (in Magento):
* getting personal data: address, order history, wishlist, payment data
* order with the cusomer’s account to a different address, billing the account owner
* spending the bonus points or the customer’s credit
* download already paid virtual content which is found in the account

## Second solution: [SSL Everywhere](https://www.eff.org/https-everywhere)

Use SSL everywhere. On every request. If the user comes to your page redirect him directly on HTTPS. [Use an official signed certificate, so the user knows, he can trust you](http://www.troyhunt.com/2011/01/ssl-is-not-about-encryption.html).

## Third problem: SSL Stripping and ARP Spoofing

There is still at least one problem left. It is called "HTTPS stripping attacks". [Moxie Marlinspike implemented a tool called sslstrip and recorded a nice video to demonstrate it](http://www.thoughtcrime.org/software/sslstrip/).

A hacker can pipe all your traffic (under the correct circumstances) through his own machine and transform all the secured (`https`) links to insecure links (`http`).

### ARP Spoofing
[ARP](http://en.wikipedia.org/wiki/Address_Resolution_Protocol) is a protocol to find the shortest path to another address inside the network, for example between your computer and the router in the network.
![Alt text](http://upload.wikimedia.org/wikipedia/commons/thumb/3/33/ARP_Spoofing.svg/500px-ARP_Spoofing.svg.png "Optional title")
visualization  made by [0x55534C](http://en.wikipedia.org/wiki/File:ARP_Spoofing.svg), thanks for that.

[ARP Spoofing](http://en.wikipedia.org/wiki/ARP_spoofing) means, you flood the network with ARP packets and define the way through your computer as the fastest way to the router. This way, all the traffic is piped through your machine.

Now you have the full control over all the traffic. You can read it, you can change it or you can drop some or all packets.

#### Encryption helps
If your packets are encrypted, you don't have this problem. Because the man-in-the-middle (MITM) can't do anything without your recognition. SSL checks itself for integrity.

### The precise problem: Redirection at the beginning
But you remember? The very first connection to your shop is to `HTTP://www.my-shop.example`. This means, the connection is unencrypted and an attacker can do his job.

The attacker (let's call him Mallory) ARP spoofs the victims (Alice) laptop, reroutes Alice's traffic through his machine and removes the HTTP `Location` header. Then Mallory loads the `https` version of the site Alice wants, changes every `https://` to `http://` and pipes it to Alice's computer. Now Mallory can do her evil work.

It is important to understand, that most users don't realize or check, wether they are on a `https://` site. Or wether their address bar is green or blue. Don't rely on the user.

## Third/Final solution: Use HTTP Strict Transport Security (HSTS)
`HSTS` is a server side HTTP Header, specified in [RFC 6796](http://tools.ietf.org/html/rfc6797).

It does two things:
1. It ensures, that the connection is secure. If it is not possible to connect to the server on a secure connection, then an error is shown. This is applied in Chrome, Firefox and Opera so, that a connection via `http` is no longer possible.
2. It transforms every link on the page from `http` to `https`.

### How HSTS works
HSTS is a HTTP Header:

    Strict-Transport-Security "max-age=31536000"
    Strict-Transport-Security "max-age=31536000; includeSubDomains"

This means: Don't allow insecure connections for the next 365 days to my domain, with or without subdomains.

There is still one problem: The very first request may still be `http`. This consideration is correct. But the idea is: Hopefully the user are at home or in any secure network, when the user makes this request. If not, he is doomed. ;-)

However, if this first request is made, he is secure for the next 365 (or whatever the timespan is) days (on this device!).

As you can see: This final solution I showed to you doesn't guarantee complete security but they minimize the risk for a security breach.

## Advertisement: Magento Module for HSTS
I implemented a module, which does all this for magento: [Ikonoshirt_StrictTransportSecurity](https://github.com/ikonoshirt/StrictTransportSecurity)

## More Information
- [Top 10 2010-A9-Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Top_10_2010-A9)
- [Top 10 2010-A3-Broken Authentication and Session Management](https://www.owasp.org/index.php/Top_10_2010-A3)
- [Firesheep](http://en.wikipedia.org/wiki/Firesheep)