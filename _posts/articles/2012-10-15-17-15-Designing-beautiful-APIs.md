---
published: true
layout: article
title: Designing beautiful APIs
abstract: Talk by Tobias Schlitt on the IPC12
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
- IPC12
---

#Desingnig Beautiful APIs
Talk by Tobias Schlitt (@tobySen)

> Cute little animals raise the concentration level

Know your audience. It depends on your developers and users, whether they understand a API or not.

## On the beauty of APIs

> A beautiful API enables you to realize even unforseen feautures with elegant code

### A good API...

* ... keeps you flexible, so you can easily add new features.
* ... is as much code as necassery.
* ... has a few code as possible.
* ... is easy to read and understand.
* ... is simple and testable.

## Where can APIs be found

* Web-APIs: REST, XML-RPC, SOAP, ...
* Libraries / frameworks
* Layer boundaries / components / modules
* Interfaces (and abstract calsses!)

## Levels of Beauty

* OOP/OOD
* Consistend, good looking code
* Tests

##Syntactic / semantical beauty

* Code structure
* Naming & meaning

## Documentation
* API docs
* Examples & Tutorials
* User generated docs (comments)

## Be descriptive, avoid being ambigious

find() is a lot better than fetch()

index() is better than add()

## Avoid dependencies and allow testability

    Service::getInstance() # IS BAD
    
## Make implementations replaceable

Use dependency injection to make classes replaceable, for example:

* search with Solr
* and put indexing jobs into a ZeroMQ to index it later

And if you want, change it later.   

> Writing strings in code sucks

No auto completion, you don't get errors shown in your IDE. So use classes and methods instead.

## Never use constants for processing instructions

Use a tree of classes instead and map the different criterions on differenct classes LogicalAnd, Equals, Like, etc.

Same for arrays, there is no autocompletion, nobody knows what to put into it. (e.g. Zend Framework Version 1 Zend_Db::__construct())

> Prefixing methods with `is` (e.g. `isAllowed()`) which returns a boolean value is common sense.

## Let your user create objects

No singletons, no static stuff, no static dependencies







