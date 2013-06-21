---
published: true
layout: article
title: Remove Values From Attribute
abstract: How to remove values from a magento (product) attribute
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

Today I had to change the values of a magento product attribute.

# Attribute before
I had an attribute `color` with the values: 

* aqua
* black
* blue
* fuchsia
* ... (all other CSS2.1 color names)

And I had to change it to german values.

So I had a look into `$installer->addAttribute()` the method checks wether the attribute exists or not and calles `$this->updateAttribute()`.

## Great, let's just update the Attribute
I updated the attribute, the result was:

* aqua
* black
* braun (german: brown)
* blau (german: blue)
* blue
* ...

That is wrong.

## Just remove the wrong values

I didn't find a way to remove the values from an attribute. If you have one, tell me!

# Solution

The easiest and nicest way I found was:

	$installer->removeAttribute(Mage_Catalog_Model_Product::ENTITY, 'color');
    // [...]
    $installer->addAttribute(Mage_Catalog_Model_Product::ENTITY, 'color', $data);
    
Remove the attribute and create it with the new values.