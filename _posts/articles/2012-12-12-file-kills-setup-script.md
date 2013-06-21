---
published: true
layout: article
title: $file kills setup script
abstract: It is possible to change important and used variables inside the setup model while installing
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

I implemented a data-setup script today.

It starts with defining a variable:
	
    $file = 'var/import/sample.csv';

# The error

When magento was called, I got this error:

	[message:protected] => Warning: Illegal string offset 'toVersion'  in app/code/core/Mage/Core/Model/Resource/Setup.php on line 641
	[string:Exception:private] => 
	[code:protected] => 0
	[file:protected] => app/code/core/Mage/Core/functions.php
    [line:protected] => 245
    [trace:Exception:private] => Array
		[...]
        
I opened the Setup model and found this code snippet:

	foreach ($files as $file) {
		[...]
        try {
            switch ($fileType) {
                case 'php':
                    $conn   = $this->getConnection();
                    $result = include $fileName;
                    break;
               [...]     
            }

            if ($result) {
                $this->_setResourceVersion($actionType, $file['toVersion']);
            }
        } catch (Exception $e) {
            [...]
        }
		[...]
    }

# Debugging

I debbuged and at the beginning of the foreach $file is an array with the keys toVersion 0.1.10 and fileName with the path to my setup script.

After the `$result` `$file` was 'var/import/sample.csv'. It took a while until I realized, that it is the value I write into the variable, because I debugged the import script for a while. But then I wondered. WHY!?

## Explanation

There is this small little line of code:

	$result = include $fileName;
    
it includes the data/install script and the variable `$file` is assigned with my value. Especially the loop variable `$file` is overwritten.

# Conclusion
Be careful with defining variables in setup scripts. I wanted to write a "bugfix" but thinking 10 minutes about the problem didn't develope a solution for the problem. There is no possibility in PHP to prevend the overwrite of this variable.

HAH! There is. I thought about changing the scope but didn't find a simple solution. but just implementing a method should do it!

Blog writing brings solutions. Thanks audience for help.

Hopefully you all know, what [Rubber ducking](http://en.wikipedia.org/wiki/Rubber_duck_debugging) is?