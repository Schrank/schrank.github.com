---
published: true
layout: article
title: IE users are logged out by multiple uploader
abstract: After an upload with an IE, the admin session ended - what to do against this?
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

# Scenario
We upload images via Multiple-File-Uploader in the magento backend. The upload went on the first look well, the image is shown in the table under the other images. [As I hopefully wrote here](/articles/Magentos-Flex-Uploader.html) the images are loaded from the server in full size, but especally FROM THE server. This means the files were saved on the server.

# Logout after submitting the form
After submitting the form, I saw the admin login. I didn't check what exactly happens here. Thanks to google I found the answer [in the magento forum](http://www.magentocommerce.com/boards/index.php/viewthread/280566/#t411014):

	suhosin.session.cryptua = off 
    
This setting is in the standard `.htaccess` with this comment:

	# disable user agent verification to not break multiple image upload
    
I have really NO idea, why everything works, when I turn on this option, but afterwards I wasn't longer logged out after uploading an image.