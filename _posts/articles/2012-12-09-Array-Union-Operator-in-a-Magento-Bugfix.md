---
published: true
layout: article
title: Array Union Operator
abstract: Use the Union Operator to fix a magento bug
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles

---

These days I found [a bug in magento](http://www.magentocommerce.com/bug-tracking/issue/?issue=7419).

# The bug
Magento has a method in `Mage_Core_Helper_Data` to `removeAccents`:
	
    public function removeAccents($string, $german=false)
    {
    	if (empty($replacements[$german])) {
            $subst = array(
                // single ISO-8859-1 letters
                192=>'A', 193=>'A', 194=>'A', 195=>'A', 196=>'A', 197=>'A', 199=>'C',
        		// [...] more characters
            );
			
            if ($german) {
				// umlauts
				$subst = array_merge($subst, array(
					196=>'Ae', 228=>'ae', 214=>'Oe', 246=>'oe', 220=>'Ue', 252=>'ue'
				));
			}

			// [...] replace the stuff and return it
    }
    
As you can see the code is easy to understand. Magento builds up an array with the charaters which should be replaced as the keys and the replacement as the value.

If you want to replace german characters with the german replacements, e.g. ä with ae and Ü with Ue you can pass a second parameter to the method. When you do it, a few keys will be overwritten with the german replacement.

I tried it and the result was a mess. Why? Because of the following little sentence in the [PHP doc on array_merge](http://php.net/manual/en/function.array-merge.php): 

>  Values in the input array with numeric keys will be renumbered with incrementing keys starting from zero in the result array. 

This error can't be unseen if anybody tried the code one time. But with Magento 2 and testing everything will hopefully be better.

# The [array union operator](http://php.net/manual/en/language.operators.array.php)

After this long introduction I'll come to the array union operator `+`. Did you know it? I program for eight years PHP and I can't remember ever seen a + between two arrays.

The usage is simple:

	$array1 = array('10' => 'test', '12' => 'foo');
    $array2 = array('12' => 'bar', '13' => 'magento');
    var_dump($array1 + $array2);
	var_dump($array1, $array2);
	// Result:
	array (size=3)
		10 => string 'test' (length=4)
		12 => string 'foo' (length=3)
		13 => string 'magento' (length=7)
        
	array (size=4)
		0 => string 'test' (length=4)
		1 => string 'foo' (length=3)
    	2 => string 'bar' (length=3)
    	3 => string 'magento' (length=7)        
        
This means that the array union operator merges the arrays considering keys and values. If the value exists in a following array it is ignored.

In comparison to array_merge the keys are ignored and the values are overwritten by later passed arrays.

# The fix for the bug

Use the array union operator to merge the arrays, but be careful with the order of the passed arrays, reverse them.

	if ($german) {
        // umlauts
        $subst = array(
            196=>'Ae', 228=>'ae', 214=>'Oe', 246=>'oe', 220=>'Ue', 252=>'ue'
        ) + $subst;
    }