---
published: true
layout: article
title: Removing the coupon box from the cart
abstract: How to remove the coupon box from the cart, layout XML snipplet included
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

# Remove the coupon field from the cart

**The solution of this is at the end**

I monitor "magento" on twitter. Sometimes I read the tweets. A few minutes ago I found a tweet to a blog article which describes how to remove the coupon field from the cart.

It starts with: 

> There is no button in the backend to deactivate the coupon field in magento. Because of this you have to change the source code.

Then there is a description how to change `app/code/core/Mage/Checkout/Block/Cart/Coupon.php`

## NO! NEVER touch files in app/code/core! NEVER! NEVER! NEVER!

IF you need to change them - and there are ALWAYS ways around this, copy them to `app/code/local/Mage` and change them there.

There are a lot of reasons why this is a really bad idea. The first one is, if you change it this way you have a lot of trouble while updating OR all your changes are lost, because you overwrite them all.

### Copies in app/code/local/Mage

If you copy the files to `app/code/local/Mage` the changes are not lost, but you have a lot of trouble too, because the files after an update in `app/code/core/` are not used.

### Core hacks

The question ["Why core hacks in magento are a really bad idea?"](https://www.google.com/search?q=magento+core+hack) can answer google for me.

## How to change the layout

If you want changes in the layout, there are two main ways to achieve this:

1. [have your own theme](http://www.webguys.de/magento/ein-magento-theme-erstellen/)
1. or change the layout.xml (it is described in the german article at the webguys too)

## Removing the coupon box from the cart
    <default>
        <reference name="checkout.cart">
            <remove name="checkout.cart.coupon" />
        </reference>
    </default>