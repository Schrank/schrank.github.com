---
published: true
layout: article
title: PHPUnit Best Pratice
abstract: Talk of Sebastian Bergmann about PHPUnit Best Practices
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
- IPC12
---

# PHPUnit Best Pratice
Sebastian Bergmann is talking about PHPUnit Best Pratices

> Nobody likes to install a software.

Install PHPUnit via PEAR or composer.

## Be descriptive about what you are testing

If you write tests for a class named `Money`, name the Test `MoneyTest`, give your test methods descriptive names.

> It (the descriptive name of the method) forces you to think about what the test code is supposed to do

##Be expressive what you are testing

In PHPUnit 3.7 there is a new @cover Annotation to only mark code inthis method in the code coverage report

    /**
      * @cover Money::negate
      */

This avoids false positives in the code coverage report, if the method only is a sidenote of a test.

## Create good error messages

	$this->assertEmpty(array()); # Error: asserted empty, got not empty
	# vs.
	$this->assertTrue(empty()) # Error: asserted true, got false <- bad.

## Use assertions

Obviously... Use them.

## Strict mode

The strict mode counts the assertions in a test. If there is no assertion, the test is marked as incomplete and there is no code coverage.

    phpunit --strict --verbose MoneyTest
    
**Use it!**
    
## Write real unit tests

Remove all dependencies, use mock objects or stubs.

    $stub = $this->getMock('MoneyInterface');

	$stub->expects($this->any())
    	 ->method('getAmount')
         ->will($this->returnValue(1));

## Decouple test code and data

Data providers solve the problem to duplicate the test code for different parameters.

	/**
     * @dataProvider provider
     */   
    public function testAdd($a, $b, $c) {
    	$this->assertEquals($c, $a + $b);
    }
    
    public function provider() {
    	return array(
        	'correct1' => array(1,2,3), 	# you can set names for the groups to pop up in error message
            'correct2' => array(5,6,11)
        );
    }
    
## Use a configuration file

### Bootstrap file, configuration settings

Bootstrap runs a bootstrap file before the tests are run.

* backupGlobals (backup global variables before tests and restore afterwards)
* backupStaticAttributes (same as above, but with static attributes)
* strict mode (see above)
* cacheTokens (static code analysis checks for die(), echo(), etc. and caches these tokens)

###It is possible to order the unit tests

1. (real) unit tests, run fast, are very valuable, because it shows directly the unit of code which fails
1. integration tests
1. edge-to-edge tests
1. end-to-end test

> The larger the test is, the less valuable the output is
    
### Define the type of logging
junit, coverage-clover, coverage-html and the targets of the export files

### Filters

Define filters, in which files should be looked for tests

> Use the most specific assertion!

> Write real unit tests