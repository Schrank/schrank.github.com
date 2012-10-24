---
published: true
layout: article
title: EAV attributes, default values and source models
abstract: To have a select box for an EAV attribute with default value you need a source model - I think.
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

# EAV Attribute

I tried to [add an EAV attribut](http://www.magentocommerce.com/knowledge-base/entry/magento-for-dev-part-7-advanced-orm-entity-attribute-value), set a default value and that without using a source model, set this options:
    
    $this->addAttribute('customer', 'customer_type', array(
		'type' => 'int'	    
    	'option' => array('values' => array('Customer', 'Artist'))
        'default' => 'Customer',
		[...]
    );

# Default value
Magento adds the values into the `eav_attribute_option_value` table and shows them in the backend. The problem is, if we save them as int, we can't set 'Customer' as default. And we can't set the `eav_attribute_option_value.value_id`, because we don't know it.

# Solution
I removed the options from the attribute and added a soure model.

    $this->addAttribute('customer', 'customer_type', array(
		'type' => 'int'	    
		'source' => 'company_extension/entity_attribute_source_modelName',
        'default' => 1,
   		[...]
    );
    
A source model needs to implement the `Mage_Eav_Model_Entity_Attribute_Source_Interface`. To make life easier there is an abstract class `Mage_Eav_Model_Entity_Attribute_Source_Abstract` we can extend.

So just implement the source model, then you know the int value of your options and you can set it.