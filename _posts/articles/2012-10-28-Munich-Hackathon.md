---
published: true
layout: article
title: Magento Hackathon in Munich
abstract: 26. - 28. October 2012, Meeting great hackers, developers and friends. With the same spirit, we discuss problems, find solutions and implements them.
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

# Overview
Thanks to all the sponsors, we had a great weekend in Munich. 

##Sponsors

###[Jarlssen](http://www.jarlssen.de/)
In [Jarlssen's](http://www.jarlssen.de/) office, we had a lot of space to develope and extend together extension.

###[Anolo](http://www.anolo.de/magento-hackathon.html)
The energy was sponsored by [Anolo](http://www.anolo.de/magento-hackathon.html). They brought a lot of snickers, mars, milka tender, chips and other sweet and salty things with them.

###Karl Spies
Beside a lot of water and limonade from Jarlssen, Karl Spies brought, as last time, Club Mate with him, as far as I know, we didn't empty all of it.

###[Shirtinator](http://www.shirtinator.de/)
Thanks to shirtinator, we had, like last time, wonderful shirts for everyone:
![First status meeting in hackathon shirts](https://pbs.twimg.com/media/A6OXq_hCQAEbkE7.jpg)

###[SysEleven](http://www.syseleven.de/) & [NARF STUDIOS](http://www.narf-studios.de/)
I'm not quite sure, what we did exactly with the support of [SysEleven](http://www.syseleven.de/) and [NARF STUDIOS](http://www.narf-studios.de/). I think we paid the lunch, dinner and the cake?


## Talks
We had two talks this weekend.
### Tim 
Tim talked saturday morning about upgrading magento. He had a lot of projects the last weeks, magento 1.3, 1.4, 1.5 etc. All upgraded to the latest version (1.7.0.2). He talked about creating fast quotes for customers and what the problems are and might be.

You can find [Tim's slides](http://www.openstream.ch/wp-content/uploads/2012/11/Estimating-Magento-Upgrades.pdf) on the [openstream.ch site](http://www.openstream.ch/)

If you have any tipps, share them with us, [make a pull request](https://github.com/magento-hackathon/upgrade-checklist)!

### Fabian Blechschmidt
I had the second talk. It was - like many of my talks the last time - about security. To be more specific: ["OWASP Top 10 - im Kontext von Magento" (OWASP Top 10 in context with magento)](http://www.ikonoshirt.de/stuff/12-10-27%20OWASP%20und%20Magento.pdf).
![Fabian Blechschmidt, talking about security](https://pbs.twimg.com/media/A6SM3dGCYAEL4UD.jpg)

## Projects
And now, before my laptop battery runs out, a short summary of all the projects this weekend

###[Magento-Socialcommerce](https://github.com/magento-hackathon/Magento-Socialcommerce)
This group implemented a small framework which allows to tweet or publish messages on facebbook. It is extendable with other social network and other link shortener (at the moment there is only bit.ly).

They support at the moment category creation, product creation and order creation. 

But there can be much more, like products are nearly out, products are back, etc.

###[products-drag-n-drop](https://github.com/magento-hackathon/products-drag-n-drop)
> A Magento extension that allows changing products sort order within category by dragging and dropping.

Great extension which allows in the frontend to rearrange the products inside the list view and in the backend inside the product grid inside the category-view.

###[magento-composer-installer](https://github.com/magento-hackathon/magento-composer-installer)

> Composer installer for Magento modules

Everybody knows [composer](http://getcomposer.org/)? It is a dependency management tools, which allows to define dependencies and install them automatically. It is widely used in the [Symfony community](http://packagist.org/).

We have a great tool for this: [modman implemented by Colin Mollenhour](https://github.com/colinmollenhour/modman), but it is written in bash, so not workable under windows.

What the magent-composer-installer does is to fetch the files from the repository check for a modman file, if one is in place it is executed (it was reimplemented in PHP, so it runs on windows too!). If there is no modman file, all files are copied? I'm not sure, have a look into the repo!

###[composer-repository](https://github.com/magento-hackathon/composer-repository)
What packagist is for symfony, might become [http://packages.firegento.com](http://packages.firegento.com) for Magento. [Read the tutorial](https://github.com/magento-hackathon/composer-repository/), to publish your module there too!


###[HoneySpam](https://github.com/magento-hackathon/HoneySpam)
We implemented a few ideas to prevent customer-registration spam and review-spam.

This module adds a honeypot input element and checks how fast the submit of the formular was.

There is a check for name rules too, but I didn't had a look in this yet.


###[LoginProviderFramework](https://github.com/magento-hackathon/LoginProviderFramework)
Do you want to have other was to authenticate admin users? We implemented a (at the moment broken) login provider framework, which means we have an interface which needs to be implemented and a registration in the config.xml and afterwards you can login with you personal LoginProvider.

###[Magento-FeltInLoveWithVagrant](https://github.com/magento-hackathon/Magento-FeltInLoveWithVagrant)
I have absolutely no idea what this is, I really need to have a look on vagrant!

###[mage-hackathon-site](https://github.com/magento-hackathon/mage-hackathon-site)

> informations and registration for mage-hackathons

Our page got an update on Symfony 2.1 and we changed from RuianBootstrapBundle to MopaBootstrapBundle. More to come!