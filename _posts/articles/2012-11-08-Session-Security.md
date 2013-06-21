---
published: false
layout: article
title: Session Security
abstract: Sessions. Secure them. Secure the Session ID.
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

# Session and Session ID

The user is identified with his session id. The session id is usually saved in a cookie in the user's browser. In magento there is no alternative to the cookies. If you don't have cookies enabled and they are needed (for example to add something to the cart), you are redirected to this site: [/enable-cookies](http://demo.magentocommerce.com/enable-cookies). By the way, often this site is not styled, because it is forgotten.

# Why is it important to secure the session?

Downloadable products? Customer Credit & Reward Points? (@VinaiKopp)
Change shipping address to receive packages :) (@pavelnovitsky)