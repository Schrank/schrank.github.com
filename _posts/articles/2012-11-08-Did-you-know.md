---
published: true
layout: article
title: Parameters of Varien_Data_Form?
abstract: You can change a lot with these parameters
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

Why do I write this? Because I had the problem a few hours ago that no form was rendered in my backend formular. And as a few of you may know, the [FireGento GermanSetup Team](https://github.com/firegento/firegento-germansetup) met today. Noone of us knew instantly why. So here are a few tipps.

# HTML Attributes

You can set the html attributes `id`, `name`, `method`, `action`, `enctype`, `class` and `onsubmit`. Especially `method` and `enctype` is needed for file uploads. With `onsubmit` you can implement more checks in javascript. And with `action` the target of the form is defined, as you should know.

# Container yes or no?

As you can see [in the code](https://github.com/LokeyCoding/magento-mirror/blob/magento-1.7/lib/Varien/Data/Form.php#L234) there is another parameter: `use_container`. With `use_container` you decied wether to wrap a &lt;form&gt; around your form elements and add a form_key.
