# PHP学习

[TOC]

## 数据类型

```php
<?php

$a_bool = TRUE;   // a boolean
$a_str  = "foo";  // a string
$a_str2 = 'foo';  // a string
$an_int = 12;     // an integer
echo gettype($a_bool); // prints out:  boolean
echo gettype($a_str);  // prints out:  string
// If this is an integer, increment it by four
if (is_int($an_int)) {
    $an_int += 4;
}
// If $bool is a string, print it out
// (does not print out anything)
if (is_string($a_bool)) {
    echo "String: $a_bool";
}
?>
```

| 函数          | 解释                         |
| ----------- | -------------------------- |
| var_dump()  | 查看某个表达式的值和类型               |
| gettype()   | 查看数据类型                     |
| is_int()    | 检查是否是integer，返回true或者flase |
| is-string() | 检查是否是string，返回true或者flase  |
| round()     | 四舍五入                       |
| int()       | 强制转换为integer               |
| floor()     | 地板除                        |
| ceil()      | 天花板除                       |

### 整形(integer)

```php
<?php
$a = 1234; // 十进制数
$a = -123; // 负数
$a = 0123; // 八进制数 (等于十进制 83)
$a = 0x1A; // 十六进制数 (等于十进制 26)
?>
```

### 布尔型(boolean)

```php
<?php
// == 是一个操作符，它检测两个变量是否相等，并返回一个布尔值
if ($action == "show_version") {
    echo "The version is 1.23";
}

// 这样做是不必要的...
if ($show_separators == TRUE) {
    echo "<hr>\n";
}

// ...因为可以使用下面这种简单的方式：
if ($show_separators) {
    echo "<hr>\n";
}
?>
```

### 浮点型(float)

### 字符型(string)

#### 单引号

```php
<?php
echo 'this is a simple string';

// 可以录入多行
echo 'You can also have embedded newlines in 
strings this way as it is
okay to do';

// 输出： Arnold once said: "I'll be back"
echo 'Arnold once said: "I\'ll be back"';

// 输出： You deleted C:\*.*?
echo 'You deleted C:\\*.*?';

// 输出： You deleted C:\*.*?
echo 'You deleted C:\*.*?';

// 输出： This will not expand: \n a newline
echo 'This will not expand: \n a newline';

// 输出： Variables do not $expand $either
echo 'Variables do not $expand $either';
?>
```



#### 双引号

如果字符串是包围在双引号（"）中， PHP 将对一些特殊的字符进行解析：

| 序列                   | 含义                        |
| -------------------- | ------------------------- |
| `\n`                 | 换行                        |
| `\r`                 | 回车                        |
| `\t`                 | 水平制表符                     |
| `\v`                 | 垂直制表符                     |
| `\e`                 | Escape                    |
| `\f`                 | 换页                        |
| `\\`                 | 反斜线                       |
| `\$`                 | 美元标记                      |
| `\"`                 | 双引号                       |
| `\[0-7]{1-3}`        | 符合该正则表达式序列的是一个以八进制来表达的字符  |
| `\x[0-9A-Fa-f]{1,2}` | 符合该正则表达式序列的是一个以十六进制来表达的字符 |

#### Heredoc

```php
<?php
$str = <<<EOD
Example of string
spanning multiple lines
using heredoc syntax.
EOD;

/* 含有变量的更复杂示例 */
class foo
{
    var $foo;
    var $bar;

    function foo()
    {
        $this->foo = 'Foo';
        $this->bar = array('Bar1', 'Bar2', 'Bar3');
    }
}

$foo = new foo();
$name = 'MyName';

echo <<<EOT
My name is "$name". I am printing some $foo->foo.
Now, I am printing some {$foo->bar[1]}.
This should print a capital 'A': \x41
EOT;
?>
```

以上例程会输出：

```php
My name is "MyName". I am printing some Foo.

Now, I am printing some Bar2.

This should print a capital 'A': A
```

也可以把 Heredoc 结构用在函数参数中来传递数据：

```php
<?php
var_dump(array(<<<EOD
foobar!
EOD
));
?>
```

使用 Heredoc 结构来初始化静态值：

```php
<?php
// 静态变量
function foo()
{
    static $bar = <<<LABEL
Nothing in here...
LABEL;
}

// 类的常量、属性
class foo
{
    const BAR = <<<FOOBAR
Constant example
FOOBAR;

    public $baz = <<<FOOBAR
Property example
FOOBAR;
}
?>
```

**在 heredoc 结构中使用双引号**

```php
<?php
echo <<<"FOOBAR"
Hello World!
FOOBAR;
?>
```

#### Nowdoc

```php
<?php
$str = <<<'EOD'
Example of string
spanning multiple lines
using nowdoc syntax.
EOD;

/* 含有变量的更复杂的示例 */
class foo
{
    public $foo;
    public $bar;

    function foo()
    {
        $this->foo = 'Foo';
        $this->bar = array('Bar1', 'Bar2', 'Bar3');
    }
}

$foo = new foo();
$name = 'MyName';
echo <<<'EOT'
My name is "$name". I am printing some $foo->foo.
Now, I am printing some {$foo->bar[1]}.
This should not print a capital 'A': \x41
EOT;
?>
```

以上例程会输出：

```php
My name is "$name". I am printing some $foo->foo.
Now, I am printing some {$foo->bar[1]}.
This should not print a capital 'A': \x41
```

不象` heredoc` 结构，`nowdoc `结构可以用在任意的静态数据环境中，最典型的示例是用来初始化类的属性或常量：

```php
<?php
class foo {
    public $bar = <<<'EOT'
bar
EOT;
}
?>
```

### Array数组

```php

<?php
$array = array(
    "foo" => "bar",
    "bar" => "foo",
);
// 自 PHP 5.4 起
$array = [
    "foo" => "bar",
    "bar" => "foo",
];
?>
```

```php
<?php
$array = array(
    1    => "a",
    "1"  => "b",
    1.5  => "c",
    true => "d",
);
var_dump($array);
?>
```

以上例程会输出：

```php
array(1) {
  [1]=>
  string(1) "d"
}
```

上例中所有的键名都被强制转换为 1，则每一个新单元都会覆盖前一个的值，最后剩下的只有一个 "d"。

```php
<?php
$array = array(
    "foo" => "bar",
    "bar" => "foo",
    100   => -100,
    -100  => 100,
);
var_dump($array);
?>
```

以上例程会输出：

```php
array(4) {
  ["foo"]=>
  string(3) "bar"
  ["bar"]=>
  string(3) "foo"
  [100]=>
  int(-100)
  [-100]=>
  int(100)
}
```

key 为可选项。如果未指定，PHP 将自动使用之前用过的最大 integer 键名加上 1 作为新的键名。

**Example 4 没有键名的索引数组**

```php
<?php
$array = array("foo", "bar", "hallo", "world");
var_dump($array);
?>
```

以上例程会输出：

```php
array(4) {
  [0]=>
  string(3) "foo"
  [1]=>
  string(3) "bar"
  [2]=>
  string(5) "hallo"
  [3]=>
  string(5) "world"
}
```

还可以只对某些单元指定键名而对其它的空置：

```php
<?php
$array = array(
         "a",
         "b",
    6 => "c",
         "d",
);
var_dump($array);
?>
```

以上例程会输出：

```php
array(4) {
  [0]=>
  string(1) "a"
  [1]=>
  string(1) "b"
  [6]=>
  string(1) "c"
  [7]=>
  string(1) "d"
}
```

可以看到最后一个值 "d" 被自动赋予了键名 7。这是由于之前最大的整数键名是 6。

**用方括号语法访问数组单元**

```php
<?php
$array = array(
    "foo" => "bar",
    42    => 24,
    "multi" => array(
         "dimensional" => array(
             "array" => "foo"
         )
    )
);

var_dump($array["foo"]);
var_dump($array[42]);
var_dump($array["multi"]["dimensional"]["array"]);
?>
```

以上例程会输出：

```php
string(3) "bar"
int(24)
string(3) "foo"
```

**Note:**

方括号和花括号可以互换使用来访问数组单元（例如 \$array[42] 和 \$array{42} 在上例中效果相同）。

要创建一个新的对象 object，使用 new 语句实例化一个类：

```php
<?php
class foo
{
    function do_foo()
    {
        echo "Doing foo."; 
    }
}

$bar = new foo;
$bar->do_foo();
?>
```

### 资源(resource)

### NULL	

### 类型转换

允许的强制转换有：

- (int), (integer) - 转换为整形 integer
- (bool), (boolean) - 转换为布尔类型 boolean
- (float), (double), (real) - 转换为浮点型 float
- (string) - 转换为字符串 string
- (array) - 转换为数组 array
- (object) - 转换为对象 object
- (unset) - 转换为 NULL (PHP 5)

## 变量

### 基础

一个有效的变量名由字母或者下划线开头，后面跟上任意数量的字母，数字，或者下划线。

```php
<?php
$var = 'Bob';
$Var = 'Joe';
echo "var, Var";      // 输出 "Bob, Joe"
$4site = 'not yet';     // 非法变量名；以数字开头
$_4site = 'not yet';    // 合法变量名；以下划线开头
$i站点is = 'mansikka';  // 合法变量名；可以用中文
?>
```

```php
<?php
$foo = 'Bob';              // 将 'Bob' 赋给 $foo
$bar = &$foo;              // 通过 $bar 引用 $foo
$bar = "My name is $bar";  // 修改 $bar 变量
echo $bar;
echo $foo;                 // $foo 的值也被修改
?>
```

有一点重要事项必须指出，那就是只有有名字的变量才可以引用赋值。

```php
<?php
$foo = 25;
$bar = &$foo;      // 合法的赋值
$bar = &(24 * 7);  // 非法; 引用没有名字的表达式

function test()
{
   return 25;
}

$bar = &test();    // 非法
?>
```

虽然在 PHP 中并不需要初始化变量，但对变量进行初始化是个好习惯。未初始化的变量具有其类型的默认值 - 布尔类型的变量默认值是 FALSE，整形和浮点型变量默认值是零，字符串型变量（例如用于 echo 中）默认值是空字符串以及数组变量的默认值是空数组。

### 预定义变量



### 变量范围

```php
<?php
$a = 1; /* global scope */
function Test()
{
    echo $a; /* reference to local scope variable */
}
Test();
?>
```

这个脚本不会有任何输出，因为 echo 语句引用了一个局部版本的变量 $a，而且在这个范围内，它并没有被赋值。

#### global关键字

```php
<?php
$a = 1;
$b = 2;
function Sum()
{
    global a, b;
    b = a + $b;
}
Sum();
echo $b;
?>
```

#### $GLOBALS 数组

```php
<?php
$a = 1;
$b = 2;

function Sum()
{
    $GLOBALS['b'] = $GLOBALS['a'] + $GLOBALS['b'];
}

Sum();
echo $b;
?>
```

\$GLOBALS 是一个关联数组，每一个变量为一个元素，键名对应变量名，值对应变量的内容。\$GLOBALS 之所以在全局范围内存在，是因为 $GLOBALS 是一个超全局变量。以下范例显示了超全局变量的用处：

```php
<?php
function test_global()
{
    // 大多数的预定义变量并不 "super"，它们需要用 'global' 关键字来使它们在函数的本地区域中有效。
    global $HTTP_POST_VARS;

    echo $HTTP_POST_VARS['name'];

    // Superglobals 在任何范围内都有效，它们并不需要 'global' 声明。Superglobals 是在 PHP 4.1.0 引入的。
    echo $_POST['name'];
}
?>
```

#### static关键字

```
<?php
function Test()
{
    $a = 0;
    echo $a;
    $a++;
}
?>

```

本函数没什么用处，因为每次调用时都会将 \$a 的值设为 0 并输出 0。将变量加一的 \$a++ 没有作用，因为一旦退出本函数则变量 \$a 就不存在了。要写一个不会丢失本次计数值的计数函数，要将变量 \$a 定义为静态的：

```php
<?php
function test()
{
    static $a = 0;
    echo $a;
    $a++;
}
?>
```

现在，变量 \$a 仅在第一次调用 test() 函数时被初始化，之后每次调用 test() 函数都会输出 $a 的值并加一

### 可变变量

```php


```

## 常量

合法的常量名以字母或下划线开始，后面跟着任何字母，数字或下划线。

### define()函数

```
<?php
define("CONSTANT", "Hello world.");
echo CONSTANT; // outputs "Hello world."
echo Constant; // 输出 "Constant" 并发出一个提示级别错误信息
?>
```

### const关键字（PHP 5.3.0 以后）

```php
<?php
// 以下代码在 PHP 5.3.0 后可以正常工作
const CONSTANT = 'Hello World';
echo CONSTANT;
?>
```

### 魔术常量

| 名称              | 说明          |
| --------------- | ----------- |
| `__LINE__`      | 文件中的当前行号    |
| `__FILE__`      | 文件的完整路径和文件名 |
| `__DIR__`       | 文件所在的目录     |
| `__FUNCTION__`  | 函数名称        |
| `__CLASS__`     | 类的名称        |
| `__TRAIT__`     | Trait的名字    |
| `__METHOD__`    | 类的方法名       |
| `__NAMESPACE__` | 当前命名空间的名称   |

## 运算符

## 控制结构

### if...else

```php
<?php
if (a > b) {
  echo "a is greater than b";
} else {
  echo "a is NOT greater than b";
}
?>
```

### elseif/else if

```php
<?php
if ($a > $b) {
    echo "a is bigger than b";
} elseif ($a == $b) {
    echo "a is equal to b";
} else {
    echo "a is smaller than b";
}
?>
```

```php
<?php

/* 不正确的使用方法： */
if($a > $b):
    echo $a." is greater than ".$b;
else if($a == $b): // 将无法编译
    echo "The above line causes a parse error.";
endif;

/* 正确的使用方法： */
if($a > $b):
    echo $a." is greater than ".$b;
elseif($a == $b): // 注意使用了一个单词的 elseif
    echo $a." equals ".$b;
else:
    echo $a." is neither greater than or equal to ".$b;
endif;

?>
```

### while

```php
while (expr)
    {statement}
```

```php
while (expr):
    statement
    ...
endwhile;
```

下面两个例子完全一样，都显示数字 1 到 10：

```php

<?php
/* example 1 */

$i = 1;
while ($i <= 10) {
    echo $i++;  /* the printed value would be
                    $i before the increment
                    (post-increment) */
}

/* example 2 */

$i = 1;
while ($i <= 10):
    print $i;
    $i++;
endwhile;
?>
```

### do-while

```php
<?php
$i = 0;
do {
   echo $i;
} while ($i > 0);
?>
```

### for

考虑以下的例子，它们都显示数字 1 到 10：

```php
<?php
/* example 1 */

for ($i = 1; $i <= 10; $i++) {
    echo $i;
}

/* example 2 */

for ($i = 1; ; $i++) {
    if ($i > 10) {
        break;
    }
    echo $i;
}

/* example 3 */

$i = 1;
for (;;) {
    if ($i > 10) {
        break;
    }
    echo $i;
    $i++;
}

/* example 4 */

for ($i = 1, $j = 0; $i <= 10; $j += $i, print $i, $i++);
?>
  
```

### foreach

foreach 语法结构提供了遍历数组的简单方式。foreach 仅能够应用于数组和对象

```php
foreach (array_expression as $value)
    statement
foreach (array_expression as $key => $value)
    statement
```

可以很容易地通过在 $value 之前加上 & 来修改数组的元素。此方法将以引用赋值而不是拷贝一个值。

```php
<?php
$arr = array(1, 2, 3, 4);
foreach ($arr as &$value) {
    $value = $value * 2;
}
// $arr is now array(2, 4, 6, 8)
unset($value); // 数组最后一个元素的 $value 引用在 foreach 循环之后仍会保留。建议使用 unset() 来将其销毁
?>
```

$value 的引用仅在被遍历的数组可以被引用时才可用（例如是个变量）。以下代码则无法运行：

```php
<?php
foreach (array(1, 2, 3, 4) as &$value) {
    $value = $value * 2;
}

?>
```

### break

break 结束当前 for，foreach，while，do-while 或者 switch 结构的执行。

break 可以接受一个可选的数字参数来决定跳出几重循环。

```php
<?php
$arr = array('one', 'two', 'three', 'four', 'stop', 'five');
while (list (, $val) = each($arr)) {
    if ($val == 'stop') {
        break;    /* You could also write 'break 1;' here. */
    }
    echo "$val<br />\n";
}

/* 使用可选参数 */

$i = 0;
while (++$i) {
    switch ($i) {
    case 5:
        echo "At 5<br />\n";
        break 1;  /* 只退出 switch. */
    case 10:
        echo "At 10; quitting<br />\n";
        break 2;  /* 退出 switch 和 while 循环 */
    default:
        break;
    }
}
?>
```

### continue

continue 在循环结构用来跳过本次循环中剩余的代码并在条件求值为真时开始执行下一次循环。

continue 接受一个可选的数字参数来决定跳过几重循环到循环结尾。默认值是 1，即跳到当前循环末尾。

```php
<?php
while (list ($key, $value) = each($arr)) {
    if (!($key % 2)) { // skip odd members
        continue;
    }
    do_something_odd($value);
}

$i = 0;
while ($i++ < 5) {
    echo "Outer<br />\n";
    while (1) {
        echo "Middle<br />\n";
        while (1) {
            echo "Inner<br />\n";
            continue 3;
        }
        echo "This never gets output.<br />\n";
    }
    echo "Neither does this.<br />\n";
}
?>
```

### switch

```php
<?php
if ($i == 0) {
    echo "i equals 0";
} elseif ($i == 1) {
    echo "i equals 1";
} elseif ($i == 2) {
    echo "i equals 2";
}

switch ($i) {
    case 0:
        echo "i equals 0";
        break;
    case 1:
        echo "i equals 1";
        break;
    case 2:
        echo "i equals 2";
        break;
}
?>
```

**switch 结构可以用字符串**

```php
<?php
switch ($i) {
case "apple":
    echo "i is apple";
    break;
case "bar":
    echo "i is bar";
    break;
case "cake":
    echo "i is cake";
    break;
}
?>
```

在一个 case 中的语句也可以为空，这样只不过将控制转移到了下一个 case 中的语句。

```php
<?php
switch ($i) {
    case 0:
    case 1:
    case 2:
        echo "i is less than 3 but not negative";
        break;
    case 3:
        echo "i is 3";
}
?>
```

一个 case 的特例是 default。它匹配了任何和其它 case 都不匹配的情况。例如：

```php
<?php
switch ($i) {
    case 0:
        echo "i equals 0";
        break;
    case 1:
        echo "i equals 1";
        break;
    case 2:
        echo "i equals 2";
        break;
    default:
        echo "i is not equal to 0, 1 or 2";
}
?>
```

switch 支持替代语法的流程控制。更多信息见控制结构(一)的替代语法一节。

```php
<?php
switch ($i):
    case 0:
        echo "i equals 0";
        break;
    case 1:
        echo "i equals 1";
        break;
    case 2:
        echo "i equals 2";
        break;
    default:
        echo "i is not equal to 0, 1 or 2";
endswitch;
?>
```

### declare

#### ticks

#### encoding

### return

### include

## 函数

```php
<?php
function foo($arg_1, $arg_2, ..., $arg_n)
{
    echo "Example function.\n";
    return $retval;
}
?>
```

Note: 函数名是大小写无关的，不过在调用函数的时候，通常使用其在定义时相同的形式。

### 函数的参数

#### 向函数传递数组：

```php
<?php
function takes_array($input)
{
    echo "$input[0] + $input[1] = ", $input[0]+$input[1];
}
?>
```

#### 通过引用传递参数

缺省情况下，函数参数通过值传递（因而即使在函数内部改变参数的值，它并不会改变函数外部的值）。如果希望允许函数修改它的参数值，必须通过引用传递参数。如果想要函数的一个参数总是通过引用传递，可以在函数定义中该参数的前面预先加上符号 &：

```php
<?php
function add_some_extra(&$string)
{
    $string .= 'and something extra.';
}
$str = 'This is a string, ';
add_some_extra($str);
echo $str;    // outputs 'This is a string, and something extra.'
?>
```

#### 默认参数的值

函数可以定义 C++ 风格的标量参数默认值，如下：

```php
<?php
function makecoffee($type = "cappuccino")
{
    return "Making a cup of $type.\n";
}
echo makecoffee();
echo makecoffee(null);
echo makecoffee("espresso");
?>
```

以上例程会输出：

```
Making a cup of cappuccino.
Making a cup of .
Making a cup of espresso.
```

### 函数的返回值

值通过使用可选的返回语句返回。可以返回包括数组和对象的任意类型。返回语句会立即中止函数的运行，并且将控制权交回调用该函数的代码行。

```php
<?php
function square($num)
{
    return $num * $num;
}
echo square(4);   // outputs '16'.
?>
```

#### 返回数组

函数不能返回多个值，但可以通过返回一个数组来得到类似的效果。

```php
<?php
function small_numbers()
{
    return array (0, 1, 2);
}
list ($zero, $one, $two) = small_numbers();
?>
```

#### 返回引用

从函数返回一个引用，必须在函数声明和指派返回值给一个变量时都使用引用操作符 & ：

```php
<?php
function &returns_reference()
{
    return $someref;
}

$newref =& returns_reference();
?>
```

### 可变函数

PHP 支持可变函数的概念。这意味着如果一个变量名后有圆括号，PHP 将寻找与变量的值同名的函数，并且尝试执行它。可变函数可以用来实现包括回调函数，函数表在内的一些用途。变量函数不能用于语言结构，例如 echo， print， unset()， isset()， empty()， include， require 以及类似的语句。需要使用自己的包装函数来将这些结构用作变量函数。

```php
<?php
function foo() {
    echo "In foo()<br />\n";
}

function bar($arg = '') {
    echo "In bar(); argument was '$arg'.<br />\n";
}

// 使用 echo 的包装函数
function echoit($string)
{
    echo $string;
}

$func = 'foo';
$func();        // This calls foo()

$func = 'bar';
$func('test');  // This calls bar()

$func = 'echoit';
$func('test');  // This calls echoit()
?>
```

还可以利用可变函数的特性来调用一个对象的方法。

```php
<?php
class Foo
{
    function Variable()
    {
        $name = 'Bar';
        $this->$name(); // This calls the Bar() method
    }

    function Bar()
    {
        echo "This is Bar";
    }
}

$foo = new Foo();
$funcname = "Variable";
$foo->$funcname();   // This calls $foo->Variable()

?>
```

### 匿名函数

```php
<?php
echo preg_replace_callback('~-([a-z])~', function ($match) {
    return strtoupper($match[1]);
}, 'hello-world');
// 输出 helloWorld
?>
```

闭包函数也可以作为变量的值来使用。PHP会自动把表达式转换成内置类Closure的 对象实例。把一个closure对象赋值给一个变量的方式与普通变量赋值的语法是一样的，最后也要加上分号。

```
<?php
$greet = function($name)
{
    printf("Hello %s\r\n", $name);
};

$greet('World');
$greet('PHP');
?>v
```

## 类与对象

每个类的定义都以关键字 class 开头，后面跟着类名，可以是任何非 PHP 保留字的名字。后面跟着一对花括号，里面包含有类成员和方法的定义。

```php
class SimpleClass
{
    // 成员声明
    public $var = 'a default value';

    // 方法声明
    public function displayVar() {
        echo $this->var;
    }
}
?>
```

### 基本概念

#### `$this`变量

```php
<?php
class A
{
    function foo()
    {
        if (isset($this)) {
            echo '$this is defined (';
            echo get_class($this);
            echo ")\n";
        } else {
            echo "\$this is not defined.\n";
        }
    }
}

class B
{
    function bar()
    {
        A::foo();
    }
}

$a = new A();
$a->foo();
A::foo();
$b = new B();
$b->bar();
B::bar();
?>
```

以上例程会输出：

```php
$this is defined (a)
$this is not defined.
$this is defined (b)
$this is not defined.
```

#### `new`关键字

要创建一个对象的实例，必须创建一个新对象并将其赋给一个变量。当创建新对象时该对象总是被赋值，除非该对象定义了构造函数并且在出错时抛出了一个异常。

#### `extends`关键字

一个类可以在声明中用 extends 关键字继承另一个类的方法和成员。PHP不支持多重继承，一个类只能继承一个基类。被继承的方法和成员可以通过用同样的名字重新声明被覆盖，除非父类定义方法时使用了 final 关键字。可以通过 parent:: 来访问被覆盖的方法或成员。

```php
<?php
class ExtendClass extends SimpleClass
{
    // Redefine the parent method
    function displayVar()
    {
        echo "Extending class\n";
        parent::displayVar();
    }
}

$extended = new ExtendClass();
$extended->displayVar();
?>
```

以上例程会输出：

```php
Extending class
a default value
```

#### `static`关键字

声明类成员或方法为static，就可以不实例化类而直接访问。不能通过一个对象来访问其中的静态成员（静态方法除外）。由于静态方法不需要通过对象即可调用，所以伪变量$this在静态方法中不可用。静态属性不可以由对象通过->操作符来访问。就像其它所有的PHP静态变量一样，静态属性只能被初始化为一个字符值或一个常量，不能使用表达式。 所以你可以把静态属性初始化为整型或数组，但不能指向另一个变量或函数返回值，也不能指向一个对象。

```php
<?php
class Foo
{
    public static $my_static = 'foo';

    public function staticValue() {
        return self::$my_static;
    }
}

class Bar extends Foo
{
    public function fooStatic() {
        return parent::$my_static;
    }
}


print Foo::$my_static . "\n";

$foo = new Foo();
print $foo->staticValue() . "\n";
print $foo->my_static . "\n";      // Undefined "Property" my_static 

print $foo::$my_static . "\n";
$classname = 'Foo';
print $classname::$my_static . "\n"; // PHP 5.3.0之后可以动态调用

print Bar::$my_static . "\n";
$bar = new Bar();
print $bar->fooStatic() . "\n";
?>
```

```php
<?php
class Foo {
    public static function aStaticMethod() {
        // ...
    }
}

Foo::aStaticMethod();
$classname = 'Foo';
$classname::aStaticMethod(); // As of PHP 5.3.0
?>
```

### 属性

类的变量成员叫做“属性”，或者叫“字段”、“特征”，在本文档统一称为“属性”。 属性声明是由关键字`public`或者`protected`或者`private`开头，然后跟一个变量来组成。 属性中的变量可以初始化，但是初始化的值必须是常数，这里的常数是指`php`脚本在编译阶段时就为常数，而不是在编译阶段之后在运行阶段运算出的常数。

在类的成员方法里面，可以通过`\$this->property(property`是属性名字)这种方式来访问类的属性、 方法，但是要访问类的静态属性或者在静态方法里面却不能使用，而是使用`self::$property`。

```php
<?php
class SimpleClass
{
   // 错误的属性声明
   public $var1 = 'hello ' . 'world';
   public $var2 = <<<EOD
hello world
EOD;
   public $var3 = 1+2;
   public $var4 = self::myStaticMethod();
   public $var5 = $myVar;

   // 正确的属性声明
   public $var6 = myConstant;
   public $var7 = array(true, false);

   //在php 5.3.0 及之后，下面的声明也正确
   public $var8 = <<<'EOD'
hello world
EOD;
}
?>
```

### 类常量

可以在类中定义常量。常量的值将始终保持不变。在定义和使用常量的时候不需要使用`$`符号。

```php
<?php
class MyClass
{
    const constant = 'constant value';

    function showConstant() {
        echo  self::constant . "\n";
    }
}

echo MyClass::constant . "\n";

$classname = "MyClass";
echo $classname::constant . "\n"; // PHP 5.3.0之后

$class = new MyClass();
$class->showConstant();

echo $class::constant."\n"; // PHP 5.3.0之后
?>
```

### 构造函数

```php
void __construct ([ mixed 、$args [, $... ]] )
```

PHP 5 允行开发者在一个类中定义一个方法作为构造函数。具有构造函数的类会在每次创建新对象时先调用此方法，所以非常适合在使用对象之前做一些初始化工作。如果子类中定义了构造函数则不会隐式调用其父类的构造函数。要执行父类的构造函数，需要在子类的构造函数中调用parent::__construct()。

```php
<?php
class BaseClass {
   function __construct() {
       print "In BaseClass constructor\n";
   }
}

class SubClass extends BaseClass {
   function __construct() {
       parent::__construct();
       print "In SubClass constructor\n";
   }
}

$obj = new BaseClass();
$obj = new SubClass();
?>
```

为了实现向后兼容性，如果 PHP 5 在类中找不到 __construct() 函数，它就会尝试寻找旧式的构造函数，也就是和类同名的函数。因此唯一会产生兼容性问题的情况是：类中已有一个名为__construct() 的方法，但它却又不是构造函数。

### 析构函数

```php
void __destruct ( void )
```

PHP 5 引入了析构函数的概念，这类似于其它面向对象的语言，如 C++。析构函数会在到某个对象的所有引用都被删除或者当对象被显式销毁时执行。

```php
<?php
class MyDestructableClass {
   function __construct() {
       print "In constructor\n";
       $this->name = "MyDestructableClass";
   }

   function __destruct() {
       print "Destroying " . $this->name . "\n";
   }
}

$obj = new MyDestructableClass();
?>
```

和构造函数一样，父类的析构函数不会被引擎暗中调用。要执行父类的析构函数，必须在子类的析构函数体中显式调用`parent::__destruct()`。析构函数即使在使用 exit()终止脚本运行时也会被调用。在析构函数中 调用 exit()将会中止其余关闭操作的运行。

### 访问控制

对属性或方法的访问控制，是通过在前面添加关键字 public、protected 或 private 来实现的。由 public 所定义的类成员可以在任何地方被访问；由 protected 所定义的类成员则可以被其所在类的子类和父类访问（当然，该成员所在的类也可以访问）；而由 private 定义的类成员则只能被其所在类访问。

#### 对类成员的访问控制

类成员都必须使用关键字`public`、`protected`或`private`进行定义，默认为`public`

```php
<?php
/**
 * Define MyClass
 */
class MyClass
{
    public $public = 'Public';
    protected $protected = 'Protected';
    private $private = 'Private';

    function printHello()
    {
        echo $this->public;
        echo $this->protected;
        echo $this->private;
    }
}

$obj = new MyClass();
echo $obj->public; // 这行能被正常执行
echo $obj->protected; // 这行会产生一个致命错误
echo $obj->private; // 这行也会产生一个致命错误
$obj->printHello(); // 输出 Public、Protected 和 Private


/**
 * Define MyClass2
 */
class MyClass2 extends MyClass
{
    // 可以对 public 和 protected 进行重定义，但 private 而不能
    protected $protected = 'Protected2';

    function printHello()
    {
        echo $this->public;
        echo $this->protected;
        echo $this->private;
    }
}

$obj2 = new MyClass2();
echo $obj->public; // 这行能被正常执行
echo $obj2->private; // 未定义 private
echo $obj2->protected; // 这行会产生一个致命错误
$obj2->printHello(); // 输出 Public、Protected2，但不会输出 Private

class Bar 
{
    public function test() {
        $this->testPrivate();
        $this->testPublic();
    }

    public function testPublic() {
        echo "Bar::testPublic\n";
    }

    private function testPrivate() {
        echo "Bar::testPrivate\n";
    }
}

class Foo extends Bar 
{
    public function testPublic() {
        echo "Foo::testPublic\n";
    }

    private function testPrivate() {
        echo "Foo::testPrivate\n";
    }
}

$myFoo = new foo();
$myFoo->test(); // Bar::testPrivate 
                // Foo::testPublic
?>
```

Note: 为了兼容性考虑，在 PHP 4 中使用 var 关键字对变量进行定义的方法在 PHP 5 中仍然有效（只是作为 public 关键字的一个别名）。在 PHP 5.1.3 之前的版本，该语法会产生一个 E_STRICT 警告。

#### 对方法的访问控制

类中的方法都必须使用关键字`public`、`protected`或` private` 进行定义。如果没有设置这些关键字，则该方法会被设置成默认的 `public`。

```php
<?php
/**
 * Define MyClass
 */
class MyClass
{
    // 构造函数必须是 public
    public function __construct() { }

    // 声明一个 public 的方法
    public function MyPublic() { }

    // 声明一个 protected 的方法
    protected function MyProtected() { }

    // 声明一个 private 的方法
    private function MyPrivate() { }

    // 这个方法也是 public 的
    function Foo()
    {
        $this->MyPublic();
        $this->MyProtected();
        $this->MyPrivate();
    }
}

$myclass = new MyClass;
$myclass->MyPublic(); // 这行能被正常执行
$myclass->MyProtected(); // 这行会产生一个致命错误
$myclass->MyPrivate(); // 这行会产生一个致命错误
$myclass->Foo(); // Public、Protected 和 Private 都被调用了


/**
 * Define MyClass2
 */
class MyClass2 extends MyClass
{
    // This is public
    function Foo2()
    {
        $this->MyPublic();
        $this->MyProtected();
        $this->MyPrivate(); // 这行会产生一个致命错误
    }
}

$myclass2 = new MyClass2;
$myclass2->MyPublic(); // 这行能被正常执行
$myclass2->Foo2(); // Public 和 Protected 都被调用了，但 Private 不会被调用
?>
```

### 对象继承

当扩展一个类，子类就会继承父类的所有公有和保护方法。但是子类的方法会覆盖父类的方法。

```php
<?php

class foo
{
    public function printItem($string) 
    {
        echo 'Foo: ' . $string . PHP_EOL;
    }

    public function printPHP()
    {
        echo 'PHP is great.' . PHP_EOL;
    }
}

class bar extends foo
{
    public function printItem($string)
    {
        echo 'Bar: ' . $string . PHP_EOL;
    }
}

$foo = new foo();
$bar = new bar();
$foo->printItem('baz'); // Output: 'Foo: baz'
$foo->printPHP();       // Output: 'PHP is great' 
$bar->printItem('baz'); // Output: 'Bar: baz'
$bar->printPHP();       // Output: 'PHP is great'

?>
```

### 范围解析操作符（::）

范围解析操作符（也可称作 Paamayim Nekudotayim）或者更简单地说是一对冒号，可以用于访问静态成员、方法和常量，还可以用于覆盖类中的成员和方法。当在类的外部访问这些静态成员、方法和常量时，必须使用类的名字。

```php
<?php
class MyClass {
    const CONST_VALUE = 'A constant value';
}

echo MyClass::CONST_VALUE;
?>  
```

self 和 parent 这两个特殊的关键字是用于在类的内部对成员或方法进行访问的。 

```php
class OtherClass extends MyClass

{

    public static $my_static = 'static var';

    public static function doubleColon() {
        echo parent::CONST_VALUE . "\n";
        echo self::$my_static . "\n";
    }

}
OtherClass::doubleColon();
?>
```

当一个子类覆盖其父类中的方法时，PHP 不会再执行父类中已被覆盖的方法，直到子类中调用这些方法为止。这种机制也作用于构造函数和析构函数、重载及魔术函数。

```php
<?php
class MyClass
{
    protected function myFunc() {
        echo "MyClass::myFunc()\n";
    }
}

class OtherClass extends MyClass
{
    // 覆盖父类中的方法
    public function myFunc()
    {
        // 但仍然可以调用已被覆盖的方法
        parent::myFunc();
        echo "OtherClass::myFunc()\n";
    }
}

$class = new OtherClass();
$class->myFunc();
?>
```

### 抽象类

PHP5 支持抽象类和抽象方法。定义为抽象的类可能无法直接被实例化，任何一个类， 如果它里面至少有一个方法是被声明为抽象的，那么这个类就必须被声明为抽象的。如果类方法被声明为抽象的， 那么其中就不能包括具体的功能实现。

```php
<?php
abstract class AbstractClass
{
 // 强制要求子类定义这些方法
    abstract protected function getValue();
    abstract protected function prefixValue($prefix);

    // 普通方法（非抽象方法）
    public function printOut() {
        print $this->getValue() . "\n";
    }
}

class ConcreteClass1 extends AbstractClass
{
    protected function getValue() {
        return "ConcreteClass1";
    }

    public function prefixValue($prefix) {
        return "{$prefix}ConcreteClass1";
    }
}

class ConcreteClass2 extends AbstractClass
{
    public function getValue() {
        return "ConcreteClass2";
    }

    public function prefixValue($prefix) {
        return "{$prefix}ConcreteClass2";
    }
}

$class1 = new ConcreteClass1;
$class1->printOut();
echo $class1->prefixValue('FOO_') ."\n";

$class2 = new ConcreteClass2;
$class2->printOut();
echo $class2->prefixValue('FOO_') ."\n";
?>
```

以上例程会输出：

```php
ConcreteClass1
FOO_ConcreteClass1
ConcreteClass2
FOO_ConcreteClass2
```

```php
<?php
abstract class AbstractClass
{
    // 我们的抽象方法仅需要定义需要的参数
    abstract protected function prefixName($name);

}

class ConcreteClass extends AbstractClass
{

    // 我们的子类可以定义父类签名中不存在的可选参数
    public function prefixName($name, $separator = ".") {
        if ($name == "Pacman") {
            $prefix = "Mr";
        } elseif ($name == "Pacwoman") {
            $prefix = "Mrs";
        } else {
            $prefix = "";
        }
        return "{$prefix}{$separator} {$name}";
    }
}

$class = new ConcreteClass;
echo $class->prefixName("Pacman"), "\n";
echo $class->prefixName("Pacwoman"), "\n";
?>
```

以上例程会输出：

```php
Mr. Pacman
Mrs. Pacwoman
```

### 接口

使用接口（interface），你可以指定某个类必须实现哪些方法，但不需要定义这些方法的具体内容。我们可以通过interface来定义一个接口，就像定义一个标准的类一样，但其中定义所有的方法都是空的。接口中定义的所有方法都必须是public，这是接口的特性。要实现一个接口，可以使用implements操作符。类中必须实现接口中定义的所有方法，否则会报一个fatal错误。如果要实现多个接口，可以用逗号来分隔多个接口的名称。实现多个接口时，接口中的方法不能有重名。接口也可以继承，通过使用extends操作符。

```php
<?php

// 声明一个'iTemplate'接口
interface iTemplate
{
    public function setVariable($name, $var);
    public function getHtml($template);
}


// 实现接口
// 下面的写法是正确的
class Template implements iTemplate
{
    private $vars = array();

    public function setVariable($name, $var)
    {
        $this->vars[$name] = $var;
    }

    public function getHtml($template)
    {
        foreach($this->vars as $name => $value) {
            $template = str_replace('{' . $name . '}', $value, $template);
        }

        return $template;
    }
}

// 下面的写法是错误的，会报错：
// Fatal error: Class BadTemplate contains 1 abstract methods
// and must therefore be declared abstract (iTemplate::getHtml)
class BadTemplate implements iTemplate
{
    private $vars = array();

    public function setVariable($name, $var)
    {
        $this->vars[$name] = $var;
    }
}
?>
```

Extendable Interfaces

```php
<?php
interface a
{
    public function foo();
}

interface b extends a
{
    public function baz(Baz $baz);
}

// 正确写法
class c implements b
{
    public function foo()
    {
    }

    public function baz(Baz $baz)
    {
    }
}

// 错误写法会导致一个fatal error
class d implements b
{
    public function foo()
    {
    }

    public function baz(Foo $foo)
    {
    }
}
?>
```

多个接口间的继承

```php
<?php
interface a
{
    public function foo();
}

interface b
{
    public function bar();
}

interface c extends a, b
{
    public function baz();
}

class d implements c
{
    public function foo()
    {
    }

    public function bar()
    {
    }

    public function baz()
    {
    }
}
?>
```

使用接口常量

```php
<?php
interface a
{
    const b = 'Interface constant';
}

// 输出接口常量
echo a::b;

// 错误写法，因为常量的值不能被修改。接口常量的概念和类常量是一样的。
class b implements a
{
    const b = 'Class constant';
}
?>
```

