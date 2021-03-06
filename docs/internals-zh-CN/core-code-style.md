Yii2 Core framework code style
==============================

The following code style is used for Yii 2.x core and official extensions development. If you want to pull-request code
into the core, consider using it. We aren't forcing you to use this code style for your application. Feel free to choose
what suits you better.

You can get a config for CodeSniffer here: https://github.com/yiisoft/yii2-coding-standards

1. 概述
-----------

Overall we're using [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md)
compatible style so everything that applies to
[PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) is applied to our code
style as well.

- 文件必须使用 `<?php` 或 `<?=` 标签。
- 在文件的结尾应该有一个新行。
- 文件必须只使用UTF-8无BOM的PHP代码。
- 代码必须使用4个空格缩进，而不是 tabs。
- 类名必须在 `StudlyCaps` 中声明。
- Class constants MUST be declared in all upper case with underscore separators.
- 方法名称必须以 `camelCase` 声明。
- 属性名称必须以 `camelCase` 声明。
- Property names MUST start with an initial underscore if they are private.
- 始终使用 `elseif` 代替 `else if`。

2. 文件
--------

### 2.1. PHP 标签

- PHP code MUST use `<?php ?>` or `<?=` tags; it MUST NOT use the other tag variations such as `<?`.
- In case file contains PHP only it should not have trailing `?>`.
- Do not add trailing spaces to the end of the lines.
- Any file that contains PHP code should end with the extension `.php`.

### 2.2. 字符编码

PHP代码只能使用UTF-8编码无BOM。

3. 类名
--------------

Class names MUST be declared in `StudlyCaps`. For example, `Controller`, `Model`.

4. 类
----------

The term "class" refers to all classes and interfaces here.

- 类应该使用 `CamelCase` 命名。
- The brace should always be written on the line underneath the class name.
- Every class must have a documentation block that conforms to the PHPDoc.
- All code in a class must be indented with a single tab.
- 一个单一的 PHP 文件只能有一个类。
- 所有的类应该有命名空间。
- 类名应该匹配文件名。类的命名空间应该匹配目录结构。

```php
/**
 * Documentation
 */
class MyClass extends \yii\Object implements MyInterface
{
    // code
}
```

### 4.1. 常量

Class constants MUST be declared in all upper case with underscore separators.
例如：

```php
<?php
class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```
### 4.2. 属性

- When declaring public class members specify `public` keyword explicitly.
- Public and protected variables should be declared at the top of the class before any method declarations.
  Private variables should also be declared at the top of the class but may be added right before the methods
  that are dealing with them in cases where they are only related to a small subset of the class methods.
- The order of property declaration in a class should be ascending from public over protected to private.
- For better readability there should be no blank lines between property declarations and two blank lines
  between property and method declaration sections.
- Private variables should be named like `$_varName`.
- Public class members and standalone variables should be named using `$camelCase`
  with first letter lowercase.
- Use descriptive names. Variables such as `$i` and `$j` are better not to be used.

例如：

```php
<?php
class Foo
{
    public $publicProp;
    protected $protectedProp;
    private $_privateProp;
}
```

### 4.3. 方法

- Functions and methods should be named using `camelCase` with first letter lowercase.
- Name should be descriptive by itself indicating the purpose of the function.
- Class methods should always declare visibility using `private`, `protected` and
  `public` modifiers. `var` is not allowed.
- Opening brace of a function should be on the line after the function declaration.

~~~
/**
 * Documentation
 */
class Foo
{
    /**
     * Documentation
     */
    public function bar()
    {
        // code
        return $value;
    }
}
~~~

### 4.4 Doc blocks

`@param`, `@var`, `@property` and `@return` must declare types as `boolean`, `integer`, `string`, `array` or `null`. You can use a class names as well such as `Model` or `ActiveRecord`. For a typed arrays use `ClassName[]`.

### 4.5 Constructors

- `__construct` 应当被用来代替 PHP 4 风格的构造器。

## 5 PHP

### 5.1 Types

- All PHP types and values should be used lowercase. That includes `true`, `false`, `null` and `array`.

Use the following format for associative arrays:

```php
$config = [
    'name'  => 'Yii',
    'options' => ['usePHP' => true],
];
```

Changing type of an existing variable is considered as a bad practice. Try not to write such code unless it is really necessary.


```php
public function save(Transaction $transaction, $argument2 = 100)
{
    $transaction = new Connection; // bad
    $argument2 = 200; // good
}
```

### 5.2 字符串

- 如果字符串不包含变量或单引号，用单引号。

```php
$str = 'Like this.';
```

- 如果字符串中包含单引号，你可以使用双引号，以避免额外的转义。

#### 变量替换

```php
$str1 = "Hello $username!";
$str2 = "Hello {$username}!";
```

以下是不允许的：

```php
$str3 = "Hello ${username}!";
```

#### 连接

Add spaces around dot when concatenating strings:

```php
$name = 'Yii' . ' Framework';
```

When string is long format is the following:

```php
$sql = "SELECT *"
    . "FROM `post` "
    . "WHERE `id` = 121 ";
```

### 5.3 数组

对于数组我们使用 PHP 5.4 的短数组语法。

#### 数字索引

- 不要使用负数作为数组索引。

声明数组时，请使用以下格式：

```php
$arr = [3, 14, 15, 'Yii', 'Framework'];
```

如果有一个单行太多的元素：

```php
$arr = [
    3, 14, 15,
    92, 6, $test,
    'Yii', 'Framework',
];
```

#### Associative

Use the following format for associative arrays:

```php
$config = [
    'name'  => 'Yii',
    'options' => ['usePHP' => true],
];
```

### 5.4 控制语句

- Control statement condition must have single space before and after parenthesis.
- Operators inside of parenthesis should be separated by spaces.
- 左大括号是在同一行。
- 右大括号是在一个新行。
- Always use braces for single line statements.

```php
if ($event === null) {
    return new Event();
} elseif ($event instanceof CoolEvent) {
    return $event->instance();
} else {
    return null;
}

// the following is NOT allowed:
if (!$model && null === $event)
    throw new Exception('test');
```

#### switch

switch 语句使用以下格式：

```php
switch ($this->phpType) {
    case 'string':
        $a = (string) $value;
        break;
    case 'integer':
    case 'int':
        $a = (int) $value;
        break;
    case 'boolean':
        $a = (bool) $value;
        break;
    default:
        $a = null;
}
```

### 5.5 方法调用

```php
doIt(2, 3);

doIt(['a' => 'b']);

doIt('a', [
    'a' => 'b',
    'c' => 'd',
]);
```

### 5.6 匿名函数 (lambda) 的声明

Note space between `function`/`use` tokens and open parenthesis:

```php
// good
$n = 100;
$sum = array_reduce($numbers, function ($r, $x) use ($n) {
    $this->doMagic();
    $r += $x * $n;
    return $r;
});

// bad
$n = 100;
$mul = array_reduce($numbers, function($r, $x) use($n) {
    $this->doMagic();
    $r *= $x * $n;
    return $r;
});
```

文档
-------------

- Refer to [phpDoc](http://phpdoc.org/) for documentation syntax.
- 不含文档的代码是不允许的。
- All class files must contain a "file-level" docblock at the top of each file
  and a "class-level" docblock immediately above each class.
- 如果方法不返回任何结果没必要使用 `@return` 。
- All virtual properties in classes that extend from `yii\base\Object`
  are documented with an `@property` tag in the class doc block.
  These annotations are automatically generated from the `@return` or `@param`
  tag in the corresponding getter or setter by running `./build php-doc` in the build directory.
  You may add an `@property` tag
  to the getter or setter to explicitly give a documentation message for the property
  introduced by these methods when description differs from what is stated
  in `@return`. Here is an example:

  ```php
    <?php
    /**
     * Returns the errors for all attribute or a single attribute.
     * @param string $attribute attribute name. Use null to retrieve errors for all attributes.
     * @property array An array of errors for all attributes. Empty array is returned if no error.
     * The result is a two-dimensional array. See [[getErrors()]] for detailed description.
     * @return array errors for all attributes or the specified attribute. Empty array is returned if no error.
     * Note that when returning errors for all attributes, the result is a two-dimensional array, like the following:
     * ...
     */
    public function getErrors($attribute = null)
  ```

#### 文件

```php
<?php
/**
 * @link http://www.yiiframework.com/
 * @copyright Copyright (c) 2008 Yii Software LLC
 * @license http://www.yiiframework.com/license/
 */
```

#### 类

```php
/**
 * Component is the base class that provides the *property*, *event* and *behavior* features.
 *
 * @include @yii/docs/base-Component.md
 *
 * @author Qiang Xue <qiang.xue@gmail.com>
 * @since 2.0
 */
class Component extends \yii\base\Object
```


#### 函数 / 方法

```php
/**
 * Returns the list of attached event handlers for an event.
 * You may manipulate the returned [[Vector]] object by adding or removing handlers.
 * For example,
 *
 * ~~~
 * $component->getEventHandlers($eventName)->insertAt(0, $eventHandler);
 * ~~~
 *
 * @param string $name the event name
 * @return Vector list of attached event handlers for the event
 * @throws Exception if the event is not defined
 */
public function getEventHandlers($name)
{
    if (!isset($this->_e[$name])) {
        $this->_e[$name] = new Vector;
    }
    $this->ensureBehaviors();
    return $this->_e[$name];
}
```

#### Markdown

As you can see in the examples above we use markdown to format the phpDoc comments.

There is additional syntax for cross linking between classes, methods and properties in the documentation:

- `'[[canSetProperty]] ` will create a link to the `canSetProperty` method or property of the same class.
- `'[[Component::canSetProperty]]` will create a link to `canSetProperty` method of the class `Component` in the same namespace.
- `'[[yii\base\Component::canSetProperty]]` will create a link to `canSetProperty` method of the class `Component` in namespace `yii\base`.
- `'[[Component]]` will create a link to the `Component` class in the same namespace. Adding namespace to the class name is also possible here.

To give one of the above mentioned links another label than the class or method name you can use the syntax shown in the following example:

```
... as displayed in the [[header|header cell]].
```

The part before the | is the method, property or class reference while the part after | is the link label.

It is also possible to link to the Guide using the following syntax:

```markdown
[link to guide](guide:file-name.md)
[link to guide](guide:file-name.md#subsection)
```


#### Comments

- One-line comments should be started with `//` and not `#`.
- One-line comment should be on its own line.

附加规则
----------------

### `=== []` vs `empty()`

在可能的情况下使用 `empty()` 。

### multiple return points

Return early when conditions nesting starts to get cluttered. If the method is short it doesn't matter.

### `self` vs. `static`

始终使用 `static` 除下列情况：

- accessing constants MUST be done via `self`: `self::MY_CONSTANT`
- accessing private static properties MUST be done via `self`: `self::$_events`
- It is allowed to use `self` for recursion to call current implementation again instead of extending classes implementation.

### value for "don't do something"

Properties allowing to configure component not to do something should accept value of `false`. `null`, `''`, or `[]` should not be assumed as such.

### Directory/namespace names

- use lower case
- use plural form for nouns which represent objects (e.g. validators)
- use singular form for names representing relevant functionality/features (e.g. web)
