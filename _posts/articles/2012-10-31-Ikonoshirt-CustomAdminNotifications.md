---
published: true
layout: article
title: Ikonoshirt_CustomAdminNotifications
abstract: Looking for an easy way to add your Magento_AdminNotifications? Here it is.
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

The readme is already in markdown and I think readable. So have a look. I pushed the extension to [github](https://github.com/ikonoshirt/CustomAdminNotifications).

#Ikonoshirt_CustomAdminNotifications

As I wrote [in my blog](http://blog.fabian-blechschmidt.de/articles/Adminnotification-or-Magento-is-phoning-home.html), it is important to keep the people who use our extensions up-to-date. Magento implemented a great feature to do this, the Mage_AdminNotification.

As I wrote, there should be an easy way to add RSS feeds to the existing one, here it is.

## How to use
Install this module, install your own module and add a few lines to your `Package/Extensionname/etc/config.xml`. Just add a node to `ikonoshirt/custom_rss_feeds/feeds` with your RSS feed url.

    <default>
        <ikonoshirt>
            <custom_rss_feeds>
                <feeds>
                    <fbfeed>http://blog.fabian-blechschmidt.de/feed.xml</fbfeed>
                </feeds>
            </custom_rss_feeds>
        </ikonoshirt>
    </default>

It is important, that the feed have to be an RSS feed. The following nodes are MUST per item:

* date_added
* title
* description
* url

The following SHOULD:


* severity (int between 4 (NOTICE) and 1 (CRITICAL)) as showed in  `Mage_AdminNotification_Model_Inbox`. If no severity is present it is 4.


    const SEVERITY_CRITICAL = 1;
    const SEVERITY_MAJOR    = 2;
    const SEVERITY_MINOR    = 3;
    const SEVERITY_NOTICE   = 4;

## How to not use

Please don't spam your customer with offers, giftcodes, etc. If he likes your software and extensions, he'll come back and check for other interesting stuff. The notifications are NO advertising channel - as I already mentioned in my blog post.