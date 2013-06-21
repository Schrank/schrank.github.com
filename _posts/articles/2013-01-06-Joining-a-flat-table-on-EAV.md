---
published: true
layout: article
title: Joining a flat table on EAV
abstract: How to use the `Mage_Eav_Model_Entity_Collection_Abstract::joinTable()` method to join a flat table on a magento EAV collection
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

Joining a "normal" (aka flat table) to a magento EAV table is easy - if you know how to do.

As always there are a lot resources with tipps I don't like about joining Tables, because they all use `getSelect()->join()` and fall back to `Zend_Db` to join the tables. This can (but don't have to) lead to a few problems. In my past I got for example problems with getSize(), because the changes are only made to the Select-Statement not the Count-Statement.

# joinTable() TL;DR

But magento collections have a method `joinTable()` it took me 45min to fizzle out how it is used. To avoid this for you, I share it.

	$productCollection->joinTable(
		array('bonus' => 'mycompany/bonus'), 'product_id=entity_id',
		array('bonus_id' => 'bonus_id')
	);
    
The parameters are:

	public function joinTable($table, $bind, $fields = null, $cond = null, $joinType = 'inner')

1. Table is easy, it is the magento `namespace/entity` format, which you use in your configuration, resource models and the collection. You can use an array of the format `array('alias' => 'namespace/entity')`
2. Bind means, the ON statement in your SQL. This was the hardest part and I will explain it in details later. **It is important to have your flat table BEFORE and your EAV table AFTER the equal sign.** Don't use `main_table.` before the attribute. Magento will do this for you. More on this later.
3. Fields is an **array**. If you use a string instead, you get this: `Warning: Invalid argument supplied for foreach()  in /var/www/magento-1.6.2.0/app/code/core/Mage/Eav/Model/Entity/Collection/Abstract.php on line 775`. You can use an array of the format `array('field1', 'field2', '...')` or `array('alias' => 'field1', '...')`
4. Condition is a ** <del>WHERE</del> ON condition** in the SQL.
5. joinType. I hope you know what it is. **But you have only the choice between LEFT and INNER**. `app/code/core/Mage/Eav/Model/Entity/Collection/Abstract.php:793`

## more details

The method can be found here:

	app/code/core/Mage/Eav/Model/Entity/Collection/Abstract.php:754

### check the tablename and alias

First, the array of the tablename is splitted into alias and tablename, the tablename is resolved and the alias is checked for existance.

    $tableAlias = null;
    if (is_array($table)) {
        list($tableAlias, $tableName) = each($table);
    } else {
        $tableName = $table;
    }

    // validate table
    if (strpos($tableName, '/') !== false) {
        $tableName = Mage::getSingleton('core/resource')->getTableName($tableName);
    }
    if (empty($tableAlias)) {
        $tableAlias = $tableName;
    }

### check the fields

Then the fields are checked. Are they already defined? If not, add them.

	// validate fields and aliases
    if (!$fields) {
        throw Mage::exception('Mage_Eav', Mage::helper('eav')->__('Invalid joint fields'));
    }
    foreach ($fields as $alias=>$field) {
        if (isset($this->_joinFields[$alias])) {
            throw Mage::exception(
                'Mage_Eav',
                Mage::helper('eav')->__('A joint field with this alias (%s) is already declared', $alias)
            );
        }
        $this->_joinFields[$alias] = array(
            'table' => $tableAlias,
            'field' => $field,
        );
    }
    
### the hard part, check the bind    

The bind is exploded at the `=`, and the foreign key is expected after the equality sign. It took me 25min to find this. I didn't think about this. I thought it will be took directly into the SQL, but no, magento processes it a lot. If the column of your flat table is the second "argument", magento can't find the attribute and throws an exception: `Invalid attribute name: product_id`

I started with `'main_table.entity_id=bonus.product_id'` and ended with ` 'product_id=entity_id'` and here is the code:

	// validate bind
    list($pk, $fk) = explode('=', $bind);
    $bindCond = $tableAlias . '.' . $pk . '=' . $this->_getAttributeFieldName($fk);

Then the join method is choosed and the conditions are added. Interessting to see here is, that the whole condition is put into the ON statement. To be honest, I don't know the difference between ON and WHERE, but this looks like ON is processed on the table and WHERE is processed on the result?

And the second gem, I found here is `str_replace('{{table}}', $tableAlias, $cond).`, so you can use `{{table}}` if your condition is a string instead of the alias.

    // process join type
    switch ($joinType) {
        case 'left':
            $joinMethod = 'joinLeft';
            break;

        default:
            $joinMethod = 'join';
    }
    $condArr = array($bindCond);

    // add where condition if needed
    if ($cond !== null) {
        if (is_array($cond)) {
            foreach ($cond as $k => $v) {
                $condArr[] = $this->_getConditionSql($tableAlias.'.'.$k, $v);
            }
        } else {
            $condArr[] = str_replace('{{table}}', $tableAlias, $cond);
        }
    }
    $cond = '('.implode(') AND (', $condArr).')';

	// join table
    $this->getSelect()->$joinMethod(array($tableAlias => $tableName), $cond, $fields);

    return $this;

# The end

And in the end, magento uses `getSelect->join()` wonderful :-) BUT magento makes a lot of checks for you and using this method feels better.