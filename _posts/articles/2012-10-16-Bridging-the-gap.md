---
published: true
layout: article
title: Bridging the gap
abstract: Talk on the IPC by Stefan Priebsch
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

# Bridging the gap

How to deal with legacy and how to modernize it.

> Architecture is recursive, you can design a nice class, component, application architecture...

> Recreating a component doesn't give you any business value.

> Prepared statements does't make anything secure.

## Not everything at the same time

Assumed you have a `global $db` variable and every code relies on this. Then the first step is to change the dependency from the `$db` to a new introduced Class `DB`. This class has an dependency on our global `$db`. Now you have no dependency on the `$db` anymore except from `DB` and you can remove `global $db`.

> Lazy initialization is a good idea. It is a detail of your implementation how to open the connection the database, because of this: `private function connect(){...}`
    
    
## Why factories?

When you move the instantiation to a factory, you can add dependency classes to the parameters.

## Switchable restful API

You habe an index.php every request comes in. so you can easily build something like:

    <?php
      	$new = array(
        	'customer/new-feauture',
            'admin/customer/new-feauture'
        );
        
        if(in_array($requestedUrl, $new) {
        	require 'new-index.php';
        }


## Transforming Data

> In the end the "old world" is a backend data container.


Up to date ORMs e.g. Doctrine 2 separates the Data model from the data mapper to write to the database. It looks like:

    <?php
		class User {} # No inheritance here!
        $user = new User();
        
        $orm->save($user);

> It is not necessary that the data model knows about the data mapper, nor the old format of the informations.

## Be careful with monolithic databases

Don't mix up all databases. One Service, one persistance-layer (whatever it looks like). Not one database and a lot of mixed tables which reference everything else.





    
    
    
    
    