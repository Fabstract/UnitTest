<p align="center"><img src="https://avatars3.githubusercontent.com/u/36798053?s=200&v=4"></p>

<p align="center">
    <a href="https://packagist.org/packages/fabstract/assert"><img src="https://poser.pugx.org/fabstract/unit-test/d/total.svg" alt="Total Downloads"></a>
    <a href="https://packagist.org/packages/fabstract/assert"><img src="https://poser.pugx.org/fabstract/unit-test/v/stable.svg" alt="Latest Stable Version"></a>
    <a href="https://packagist.org/packages/fabstract/assert"><img src="https://poser.pugx.org/fabstract/unit-test/license.svg" alt="License"></a>
</p>

## UnitTest

Unit test library on top of PHP Unit.

## Installation

**Note:** PHP 7.1 or higher is required.

1. Install [composer](https://getcomposer.org/download/).
2. Run `composer require fabstract/unit-test`.

## Usage

### MethodTestBase

This class is used for separating unit tests by which methods they were written for. Suppose you have the following class:

```php
    
    namespace MyPackage;
    
    class Calculator
    {
        public function add($a, $b) {
            return $a + $b;
        }
        
        public function multiply($a, $b) {
            return $a * $b;
        }
    }
```

Now in order to write tests for these two methods:

- Create a directory, preferably the same name with the class name.
- Inside that directory, create a class for each method you want to test.
- Name the class as `methodName` + `MethodTest`. For example `AddMethodTest`.
- Extend the class from `MethodTestBase`.

**Note:** Your method should be camelcase.

Here is what it looks like:

```php

    namespace MyPackage\Calculator;

    class AddMethodTest extends \Fabstract\Component\UnitTest\MethodTestBase
    {
        public function testOneAndOneEqualsTwo() {
            $arguments = [1, 1];
            
            $result = $this->call(new Calculator(), $arguments);
            
            $this->assertEquals(2, $result);
        }
        
        public function testOneAndZeroEqualsOne() {
            $arguments = [1, 0];
            
            $result = $this->call(new Calculator(), $arguments);
            
            $this->assertEquals(1, $result);
        }
    }
```

and 

```php

    namespace MyPackage\Calculator;

    class MultiplyMethodTest extends \Fabstract\Component\UnitTest\MethodTestBase
    {
        public function testOneAndOneEqualsOne() {
            $arguments = [1, 1];
            
            $result = $this->call(new Calculator(), $arguments);
            
            $this->assertEquals(1, $result);
        }
        
        public function testOneAndZeroEqualsZero() {
            $arguments = [1, 0];
            
            $result = $this->call(new Calculator(), $arguments);
            
            $this->assertEquals(0, $result);
        }
    }
```

You can add as many unit tests as you want, without worrying about a method's tests getting mixed up with other method\s tests.
