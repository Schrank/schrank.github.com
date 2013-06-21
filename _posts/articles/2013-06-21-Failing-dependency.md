---
layout: article
published: 
  - false
  - "false"
title: Failing dependency
abstract: "Notice: Trying to get property of non-object in /var/www/app/code/core/Mage/Core/Model/Config.php on line 1239"
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories: articles
---

#Error
I hope you found this page, because you have this error and no idea what happend.

    Notice: Trying to get property of non-object in /var/www/app/code/core/Mage/Core/Model/Config.php on line 1239 

#Problem
One possible problem (I encountered) was: I had a dependency between two extensions, like this:

    <?xml version="1.0"?>
    <config>
        <modules>
            <MyCustomer_Customer>
                <active>true</active>
                <codePool>local</codePool>
                <depends>
                    <Mage_Customer />
                    <Ikonoshirt_ExtendedAccountNavigation /> <!-- DEPENDENCY! -->
                    <Mage_Catalog />
                </depends>
            </MyCustomer_Customer>
        </modules>
    </config>


The problem is, that if the dependency is not fulfilled, an error is thrown:

    //app/code/core/Mage/Core/Model/Config.php:847
    Mage::throwException(
        Mage::helper('core')->__('Module "%1$s" requires module "%2$s".', $moduleName, $depend)
    );
    
And because the config is not yet loaded, the try to get the helper class name failed:
    //app/code/core/Mage/Core/Model/Config.php:1227
    $config = $this->_xml->global->{$groupType.'s'}->{$group}
    // $config is null!

This happens only in `MAGE_IS_DEVELOPER_MODE`. I don't know why. If it is not developer mode, you get a report:

    a:4:{i:0;s:83:"Module "MyCustomer_Customer" requires module "Ikonoshirt_ExtendedAccountNavigation".";i:1;s:765:"#0 /var/www/app/code/core/Mage/Core/Model/Config.php(849): Mage::throwException('Module "MyCustomer...')
    #1 /var/www/app/code/core/Mage/Core/Model/Config.php(812): Mage_Core_Model_Config->_sortModuleDepends(Array)
    #2 /var/www/app/code/core/Mage/Core/Model/Config.php(315): Mage_Core_Model_Config->_loadDeclaredModules()
    #3 /var/www/app/code/core/Mage/Core/Model/App.php(414): Mage_Core_Model_Config->loadModules()
    #4 /var/www/app/code/core/Mage/Core/Model/App.php(343): Mage_Core_Model_App->_initModules()
    #5 /var/www/app/Mage.php(683): Mage_Core_Model_App->run(Array)
    #6 /var/www/index.php(71): Mage::run('', 'store')
    #7 {main}";s:3:"url";s:1:"/";s:11:"script_name";s:10:"/index.php";}

#Solution
Solution is easy, fulfill the depdency or remove it.
