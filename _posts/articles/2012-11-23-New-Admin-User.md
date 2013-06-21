---
published: true
layout: article
title: Create a Magento Admin User
abstract: Magento Admin User with SQL
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

I copied the `local.xml` file from one magento to another and changed the database. Afterwards I accessed the magento installation `http://shop.dev`. Magento run all his update and install scripts.

Afterwards I had two problems:

1. I had no admin user. The solution, how to create one [I found here, thanks to Volodymyr Vygovskyi](http://www.atwix.com/magento/reset-admin-password-mysql/)
1. I had no base_url set:

	>  {{base_url}} is not recommended to use in a production environment to declare the Base Unsecure URL / Base Secure URL. It is highly recommended to change this value in your Magento configuration.

[Jerome Dennis wrote in his blog](http://haijerome.wordpress.com/2010/11/29/magento-base_url-is-not-recommended/) how to change this, but when we have a look into 

	// app/code/core/Mage/Core/Model/Config.php:982
	// Mage_Core_Model_Config::getDistroServerVars()
	    if (isset($_SERVER['SCRIPT_NAME']) && isset($_SERVER['HTTP_HOST'])) {
                $secure = (!empty($_SERVER['HTTPS']) && ($_SERVER['HTTPS']!='off')) || $_SERVER['SERVER_PORT']=='443';
                $scheme = ($secure ? 'https' : 'http') . '://' ;

                $hostArr = explode(':', $_SERVER['HTTP_HOST']);
                $host = $hostArr[0];
                $port = isset(
                    $hostArr[1]) && (!$secure && $hostArr[1]!=80 || $secure && $hostArr[1]!=443
                ) ? ':'.$hostArr[1] : '';
                $path = Mage::app()->getRequest()->getBasePath();

                $baseUrl = $scheme.$host.$port.rtrim($path, '/').'/';
            } else {
                $baseUrl = 'http://localhost/';
            }
    
we see, that this setting is great for development. We can just use magento without caring about the URL.
