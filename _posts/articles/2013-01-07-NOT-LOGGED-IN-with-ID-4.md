---
published: true
layout: article
title: NOT LOGGED IN with ID 4
abstract: Standard customer group with "wrong" id and the consequences
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

Yesterday I debugged an interessting behaviour:

All categories were shown in the shop, no products. If you request the product directly `/catalog/product/view/id/12345` you found the product and everything was shown.

The standard errors were tested:

* reindex
* clean cache
* activate logging
* use the default template

Nothing helped. It took me about an hour to find the following bug. And to be honest, it was real luck. If you ask me, with this error you can search for days!

# How to find the problem?

I checked the database for the indexes, everything looked great, magento said, all indexes are ready and useable.

I had a look into the backend and everything was fine. Products were actived, had a qty > 0 and were in stock. I tried to add a product to the website but it didn't help.

Then I dig into the Product_List of the Category view. I `die($_productCollection->getSelect())` the query and played with it. after removing the price_index I got results!

# Yea! Results!

The price_index filtered for `customer_group = 0`. I know this is the id for the `NOT LOGGED IN`, so I had a look into the `customer_group` table. Don't ask me why but *THIS IS WRONG*:

    customer_group_id  |  customer_group_code  |  tax_class_id
    -------------------|-----------------------|--------------
                    4  |        NOT LOGGED IN  |             3

I had a look into the `price_index` and found prices for the customer groups with the IDs 1,2,3 and 4. No prices for 0.

Ok, I built a long query to change this, I tried it in a big transaction but it didn't work - don't ask me why, it threw after the first query a

    Cannot add or update a child row: a foreign key constraint fails
    
if you can tell my why, please send me an email!

So I skipped the foreign key check:

	START TRANSACTION;
	UPDATE `salesrule_customer_group` SET `customer_group_id` = '0' WHERE `salesrule_customer_group`.`customer_group_id` =4;
	UPDATE `salesrule_product_attribute` SET `customer_group_id` = '0' WHERE `salesrule_product_attribute`.`customer_group_id` =4;
	UPDATE `customer_group` SET `customer_group_id` = '0' WHERE `customer_group`.`customer_group_id` =4;
	UPDATE `catalog_product_bundle_price_index` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `catalog_product_entity_group_price` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `catalog_product_entity_tier_price` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `catalog_product_index_group_price` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `catalog_product_index_price` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `catalog_product_index_tier_price` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `catalogindex_minimal_price` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `catalogrule_customer_group` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `catalogrule_group_website` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `catalogrule_product` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `catalogrule_product_price` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	UPDATE `weee_discount` SET `customer_group_id` = '0' WHERE `customer_group_id` =4;
	COMMIT;

# But why is the wrong ID a problem?

Magento expects that the NOT_LOGGED_IN customer group have the id 0:

    Mage_Customer_Model_Group::NOT_LOGGED_IN_ID  = 0

And this const is used in:

    // app/code/core/Mage/Catalog/Model/Resource/Product/Collection.php:1340
    // Mage_Catalog_Model_Resource_Product_Collection::addPriceData()
    
    $customerGroupId = Mage::getSingleton('customer/session')->getCustomerGroupId();
  
    // app/code/core/Mage/Customer/Model/Session.php:174
    // Mage_Customer_Model_Session::getCustomerGroupId()
 
    public function getCustomerGroupId()
    {
        if ($this->getData('customer_group_id')) {
            return $this->getData('customer_group_id');
        }
        if ($this->isLoggedIn() && $this->getCustomer()) {
            return $this->getCustomer()->getGroupId();
        }
        return Mage_Customer_Model_Group::NOT_LOGGED_IN_ID;
    }
    

# How does this happen?

I have no idea. `Mage_Customer` has three install scripts, all of them create the customer group `NOT LOGGED IN` explicit with the ID 0.

# Conclusion
The index is created with a big SQL statement (I think, didn't check this) and therefore uses the `customer_group_id` from the database and magento's product list uses the constat from `Mage_Customer_Model_Group` if they don't match, you have a problem.