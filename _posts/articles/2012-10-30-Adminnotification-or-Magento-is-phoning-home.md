---
published: true
layout: article
title: Adminnotification or Magento is phoning home
abstract: How this feature works and what we should do with it
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

# Mage_Adminnotification

There is this tiny module, which goes us on our nerves all the time we install a new magento. It is called Mage_Adminnotification. If you don't know, what I'm talking about, maybe this picture will help you:
![Adminnotification bar under the navigation](/img/adminnotification.png)

This little bar should be interessting for administrators, store owners, marketing and product people, but not for us developers. It is just annoying.

# The workflow behind

Whenever you request a page, the `Mage_AdminNotification_Model_Observer::preDispatch()` method is called, which listens on `controller_action_predispatch`.

It checks wether an admin is logged in and checks for updates

	// app/code/core/Mage/AdminNotification/Model/Observer.php:42
	if (Mage::getSingleton('admin/session')->isLoggedIn()) {
	    Mage::getModel('adminnotification/feed')->checkUpdate()
	}
    

In `checkUpdate()` it is checked, wether the last request for updates was more than an hour ago, if yes, the data are requested from the [Magento Notifications RSS Feed](http://notifications.magentocommerce.com/community/notifications.rss) and written to the database.

	if (($this->getFrequency() + $this->getLastUpdate()) > time()) {
        return $this;
    }

	$feedXml = $this->getFeedData();
    
# What we should do with it

If you ask me, this notifications are awesome. I saw a few modules which use this notifications to send informations to their module buyers. We should have an easy to use extension which only needs a configuration node with an url. This url is checked regularly for updates for all the people which USE the backend.

It is really important to inform the shop owners about security problems of modules, but although to achive, that the shop owner update our modules.

# Avoid spam

Please be careful with this feature. Don't send them offers, discounts or informations about new modules. This is an **information channel, not a marketing channel**!

# Phoning home

I think this URL `notifications.magentocommerce.com/community/notifications.rss` is only used inside of magento, this means, every request to [this RSS feed](http://notifications.magentocommerce.com/community/notifications.rss) is a magento shop.

If you don't want these informations or don't want, that magento knows, that you installed their awsome software, you can disable the observer with this snipplet in a config.xml of you module:

	<config>
    	<adminhtml>
        	<events>
            	<controller_action_predispatch>
                	<observers>
                    	<adminnotification>
                        	<type>disabled</type>
                    	</adminnotification>
                	</observers>
            	</controller_action_predispatch>
        	</events>
    	</adminhtml>
	</config>


Thanks to Fabrizio Branca for his [gist](https://gist.github.com/3975149).