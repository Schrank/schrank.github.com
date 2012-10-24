---
published: false
layout: article
title: Magentos Flex File Uploader
abstract: magento's file uploader and the workflow behind
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

Magento has a multiple file uploader in the admin backend written in flash and action script. It communicates with the website via JavaScript.

# File Uploader
Does anybody had a look on these uploader? I had it yesterday, because I ported it to the frontend customer area. I implemented a check, wether the customer is logged in or not, before handling the file upload, but it fails all the time.

# HTTP Header
A look into the HTTP traffic showed me a lot. The upload is made via HTTP post from the flash object. It sends (in the backend) a form-key, the file and the name with the request.

# Security?
The interessting thing is, there is no cookie send with it. This means, the admin-user is not identified. And the form key (normally saved in the session) can not be checked?

