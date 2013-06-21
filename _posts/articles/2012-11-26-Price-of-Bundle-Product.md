---
published: true
layout: article
title: Price of Bundle Product
abstract: How to get the price of a bundle product
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

We have a template and `echo`ing prices of products. The products are of differenct kind. Simple product, bundle product, etc.

To get the price of a simple product you just call

	$_product->getPrice();
    
When you call this method on a bundle product, it returns 0.00. So how to get the price of a bundle product? Simply call

	$_product->getData('price');

To be honest I'm not sure, what price this is. We misuse bundle products as grouped products, that means we group products. No option to change the quantity or the "content" of the product. Because of this, our bundle product has only one price, not many ones, depending on the combination of the options.

One small note on this: There is a attribute on the bundle product object. It was something like `price_calculated` or `calculated_price`. I can't remember the name and didn't find it fast.