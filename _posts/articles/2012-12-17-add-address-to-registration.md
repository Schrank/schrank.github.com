---
published: true
layout: article
title: Add Address To Registration
abstract: Ask for the customer's address during the registration
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

# TL;DR
Thanks to [Steven Henk Don](http://www.shdon.com/blog/2011/06/24/magento-show-address-fields-in-account-creation-form)

	<customer_account_create>
    	<reference name="customer_form_register">
        	<action method="setShowAddressFields">
            	<param>true</param>
            </action>
        </reference>
    </customer_account_create>

# Longer story

I talked a few days ago with [Sascha from melovely.de](http://www.melovely.de) about old, not more functional or "wrong" answers to "standard" magento questions. I had to add address fields to the customer registration and thought about a observer to do it, but there is an easier way. This is my contribution to replace the google finds with better answers to always the same questions.

## Dig in to the controller

I took a look into the `Mage_Customer_AccountController` and found:

	[...]
	if ($this->getRequest()->getPost('create_address')) {
    [... create address ...]
    
## Deeper into the template    
    
So obviously magento has the option to ask for the address in the registration. A look into the form template brought the finding:

	<?php if($this->getShowAddressFields()): ?>
    // echo address fields

## How to return true?

Ok, how use this method and how to return true?    

### The "wrong" answers

* [Hack the core layout XML file or the core template](http://blog.chapagain.com.np/magento-show-billing-shipping-address-in-customer-signup-registration-page/)
* [Change the core template in another way](http://blog.chapagain.com.np/magento-show-billing-shipping-address-in-customer-signup-registration-page/)
* [Write an extension, rewrite the whole block, add a admin option to switch it on and off](http://learntipsandtricks.com/blog/magento/149/How-to-enable-Address-Information-on-Magento-Customer-Registration-Page), this option is the best of the three.

There is the suggestion to [add the XML to your local.xml](http://tutorials.easyshoppingstore.com/2012/09/12/magento-display-address-fields-create-account/) I prefer not to use the local.xml but this is ok too - if you ask me.

### The right answer

Writing an extension is a lot of overkill but does the job. Adding the Setter to the layout or local XML is the way I prefer.

But hacking the core, changing core templates or layout XML files brings a lot of problems while updating!