---
title: PHP基础
date: 2020-02-28 21:34:36
categories:
- PHP
tags:
- PHP
keywords:
comments:
---

<center>
<img src="https://i.loli.net/2020/02/28/SWfE2B4qoaPFRKx.jpg
" style="zoom: 100%;"/>

PHP 自学笔记
</center>
<!-- more -->

# PHP基础语法

- PHP 脚本可以放在文档中的任何位置。以` <?php` 开始，以 `?>`结束。（如果代码段后面没有混编代码，可以不用加`?>`结尾。
- 声明变量：`$a=5;`变量名是区分大小写的。

>一般变量和函数都是建议采用 `snake_case`方式(小写字母下划线），都是小写。

## 导入文件

- 防止嵌套引入过程中的出错，可以使用物理路径而不是使用相对路径。

  >`require_once(dirname(\_FILE\_).'路径'）；`
  >
  >include引入方式也是一样
  >
  >HTML中的根目录是使用/路径

- `require 'file.php'`

>类似`css`中的`import`导入文件
>
>require在每一次调用时都会载入对应的文件
>
>文件错误报错后面的就不再执行

- `require_once 'file.php'`

>如果之前载入过就不在执行

- `include 'file.php'`

>文件错误报错后面的也能执行

- `include_once 'file.php'`

>只载入一次文件，不重复载入

## 作用域

- PHP有四种不同的变量作用域：local、global、static、parameter。
- 在所有函数外部定义的变量，拥有全局作用域。除了函数外，全局变量可以被脚本中的任何部分访问，要在一个函数中访问一个全局变量，需要使用 global 关键字==>`global $x,$y;`
  在 PHP 函数内部声明的变量是局部变量，仅能在函数内部访问.

## 输出方式

- PHP 中有两个基本的输出方式： `echo` 和 `print`。
- `echo <pre>;`可以使输出的内容更直观。

>```php
><?php
>$a = ['a','b','c','d'];
>echo "<pre>";
>print_r($a);
>?>
>//输出内容：
>    Array
>(
>    [0] => a
>    [1] => b
>    [2] => c
>    [3] => d
>)
>```

- `print`只能打印出简单类型变量的值（如`int`和`string`）。
- `print_r`可以打印出复杂类型变量的值（如数组、对象）。
-  `printf`和`sprintf`是函数

```php
printf('who am i? my name is %s. I am $d years old', 'zhangsan', '18');
//结果显示：who am i? my name is zhangsan. I am 18 years old
//结果是一个返回值，值与sprintf相同
$res = sprintf('who am i? my name is %s. I am $d years old', 'zhangsan', '18');
```



- `var_dump`打印出详细信息，显示关于一个或多个表达式的结构信息，包括表达式的类型与值。数组将递归展开值，通过缩进显示其结构。

  > echo 和 print 区别:
  >
  > 1. echo - 可以输出一个或多个字符串。echo 或 echo()。
  > 2. print - 只允许输出一个字符串，返回值总为 1。 print 或 print()。
  > 3. echo输出的速度比print快，echo没有返回值，print有返回值1。

## 常量

> 设置常量，使用define()函数。
>
> ```php
> define("GREETING", "欢迎访问 Runoob.com"); 
> echo GREETING;    // 输出 "欢迎访问 Runoob.com"
> ```
>
> - 该函数有三个参数:
>
> >name：必选参数，常量名称，即标志符。
> >		value：必选参数，常量的值。
> >		case_insensitive ：可选参数，如果设置为 TRUE，该常量则大小写不敏感。默认是大小写敏感的。（不建议使用）
>
> - 常量值被定义后，在脚本的其他任何地方都不能被改变,常量默认是全局变量，在整个脚本中都可以使用。
> - 一个常量由英文字母、下划线、和数字组成,但数字不能作为首字母出现。 (常量名不需要加 $ 修饰符)。
> - 一般程序的配置信息（不会在运行过程中被修改）都会在常量中定义。
> - 建议是`SNAKE_CASE`命名规则。一般写入一个单独的文件，便于维护。

## 定界符EOF

> `PHP EOF`是一种在命令行shell（如`sh`、`csh`、`ksh`、`bash`、`PowerShell`和`zsh`）和程序语言（像`Perl`、`PHP`、`Python和Ruby`）里定义一个字符串的方法。
> `PHP` 定界符 `EOF` 的作用就是按照原样，包括换行格式什么的，输出在其内部的东西； 
>
> ```php
> <?php
> $name="变量会被解析";
> $a=<<<EOF
> $name<br><a>html格式会被解析</a><br/>双引号和Html格式外的其他内容都不会被解析
> "双引号外所有被排列好的格式都会被保留"
> "但是双引号内会保留转义符的转义效果,比如table:\t和换行：\n下一行"
> EOF; // 结束需要独立一行且前后不能空格
> echo $a;
> ?>  
> ```

# 字符串

> 字符串使用`.`连接起来。

## 长度

- `strlen($string)`

> 函数返回字符串的长度（字节数）。中文字符一个占3个字符数，可以使用`strlen("中文字符",'utf-8');`输出中文数。空格也算长度。

## 查找
- `$int=strpos("asagaab","ab");`

> 函数用于在字符串内查找一个字符或一段指定的文本。匹配则返回字符位置，未找到则返回FALSE。

- `stripos($string, $search[,$offset])`

> 忽略大小写的去查找。

- `$int=strrpos("asagaabadfab","ab");`

> 在指定字符串中查找目标字符串最后一次出现的位置。

- `strripos($string, $search[, $offset])`

> 忽略大小写的去查找最后一次出现的位置。

- `$int=substr_count("abcdeabcdeablkabd","ab");`

> 返回第二个参数字符串在第一个字符串里出现的次数。

## 判断

- `isset()`

> 判断一个传入的数据是否被定义
>
> ```php
> if (isset($string['hello'])){
>     echo $string['hello'];
> }else{
>     echo '没有';
> }
> ```

- `empty()`

>判断传入的数据是否为空
>
>`empty($string['hello'])`相当于 `!isset($string['hello'])` ||  `$string['hello'] == false`(判断是否为空)
>
>```php
>if (empty($string['hello'])){
>   echo '没有';
>}else{
>    echo $string['hello'];
>}
>```

## 拼接

- `$str=implode("-",array("a","b","c"))`

> 用第一个参数里的字符串，把后面数组里的每个元素连接起来，返回一个字符串。

## 分割

- `$array=explode("d",'abcdefg')`

> 把字符串打散为数组。
>
> 字符串分割方法，返回一个数组，用第一个参数里的字符分割后面的字符串，指定字符的前后和之间都截取。
>
> 如果指定字符在开头或结尾则返回的数组开头或结尾的元素为空字符串。
>
> 最后一个数字限制返回数组长度（最后一次分割后余下的字符串不再分割，作为一个整体放在返回数组的最后一个元素中），可不限制，则一直分割下去。

```php
<?php 
	$str ="a,b,c";
	print_r(explode(",",$str));//结果是一个数组
?>
//输出：Array ( 
    [0] => a
    [1] => b
    [2] => c  )
```

## 删除

- `$str=ltrim("a asd ","a");`

> 剔除字符串左边开头的空格,并返回。如有第二个参数则是剔除左边开头的空格换成剔除第二个参数里的字符串。

- `$str=rtrim(" asd ");`

> 剔除字符串右边开头的空格

- `$str=trim(" sdsdfas ","a");`

> 把第一个字符串两边以第二个参数开头的字符串剔除。如没有第二个参数，默认剔除掉字符串两边开头的空格

## 截取

- `$str=substr("abcdefgh",0,4);`

> 从字符串第一个参数里的指定位置开始取多长（多少个）字符，字符串中第一个字符位置从0算。如果第二个参数为负则从字符串结尾倒数第几个开始取多长的字符串。结尾最后一个字符算-1，截取方向总是从左到右

- `$str=strstr("sdafsdgaababdsfgs","ab");`

> 截取返回参数一中从左至右第一个参数二至参数一最后一个字符的字符串

- `$str=strrchr("sdafsdgaababdsfgs","ab");`

> 截取返回参数一中从左至右最后一个参数二至参数一最后一个字符的字符串

## 替换

- `$str=str_replace("a","","abcabcAbca");`

- `$str=str_ireplace("a"," ","abcabcAbca");`不区分大小写

> 将第三个参数的第一个参数字符串用参数二字符串替换

## 转大小写

- `$str=strtoupper("sdaf");`

> 返回括号里字符串的字符全部大写的字符串。

- `$str=ucfirst("asdf");`

> 将括号里第一个字符串变成大写后返回。

- `ucwords($str);`

> 每一个单词的首字母转大写

- `strtolower($str);`

> 字母转小写

## 不转义字符

- `$str=htmlentities("<br/>");`

> 用echo等将括号里字符串打印在网页上时原汁原味打印出括号里的字符串，包括标签字符。

## 添加

- `$str=addcslashes("abcdefghijklmn","akd");`

> 将参数二中每一个字符在参数一中相同字符前加"\\"。

- `str_pad(string,length,pad_string,pad_type)`

>填充字符串到另一个字符串中
>
>*string*：必需。规定要填充的字符串。
>
>*length*：必需。规定新的字符串长度。如果该值小于字符串的原始长度，则不进行任何操作。
>
>*pad_string*：可选。规定供填充使用的字符串。默认是空白。
>
>*pad_type*：可选。规定填充字符串的哪边。
>
>- STR_PAD_BOTH - 填充字符串的两侧。如果不是偶数，则右侧获得额外的填充。
>- STR_PAD_LEFT - 填充字符串的左侧。
>- STR_PAD_RIGHT - 填充字符串的右侧。默认。
>
>```php
><?php
>$str = "Hello World";
>echo str_pad($str,30,".");
>?>
>//输出：Hello World................... 
>```

# 数组

## 索引数组

>带有数字索引的数组
>
>```php
><?php 
>    //自动分配索引值的声明方式1
>	$arr = ["a","b","c","d"];
>	print_r($arr);//Array ( [0] => a [1] => b [2] => c [3] => d )
>    //自动分配索引值的声明方式2
>	$arr2 = array('a','b','c');
>	print_r($arr2);//Array ( [0] => a [1] => b [2] => c )
>
>     //手动分配索引
>     $cars[0]="porsche";
>     $cars[1]="BMW";
>?>
>```
>
>

### 获取长度

> `count()`函数用于返回数组的长度（元素数）：
>
> ```php
> <?php
> $cars=array("porsche","BMW","Volvo");
> echo count($cars);  //3
> ?>
> ```

### 遍历数组

>```php
>//使用for循环遍历数组
><?php
>  $cars=array("porsche","BMW","Volvo");
>  $arrlength=count($cars);
>  for($i=0;$i<$arrlength;$i++){
>  echo $cars[$i];
>  echo "<br>";
>}
>?>// porsche BMW Volvo
>```

## 关联数组

>关联数组是自定义数组的健的数组  
>
>```php
>//创建数组方式
>$age = array("a"=>"1","b"=>"2","c"=>"3")
>//或
>$age['a'] = "1";
>$age['b'] = "2";
>```

### 遍历数组

>```php
><?php
>$age=array("Bill"=>"63","Steve"=>"56","Elon"=>"47");
>foreach($age as $i=>$i_value){
>    echo 'key='. $x .',Value='.$x_value;
>    echo '<br>';
>}
>?>
>```

## 查找/判断

- `$bool = is_array()`

>检测变量是否是数组。

- `array_search('键值','数组')`

>搜索数组中某个键值，并返回对应的键名（索引）。

- `$bool=in_array("b",$arr);`

>判断第二参数的数组元素中是否有第一个参数元素

- `$bool=array_key_exists("k1",$arr);`

>判断第二个参数的数组中是否有第一个参数的键值，返回真假。

- `$array=array_keys($arr);`

>返回括号中数组所有键值组成的新数组原数组不改变。

- `$array=array_values($arr);`

>返回原数组中所有元素值组成的新数组，键值从0开始自增，原数组不变。

- `$key=key($arr);`

>返回当前数组指针指向的键值。

- `$value=current($arr);`

>返回当前数组指针指向的元素值。

- `$value=array_pop($arr);`

>返回从数组尾部提取最后一个元素值，并把最后一个元素从原数组中剔除。

## 合并/增加

---

# 函数

## 语法

```php
<?php
function sayHi() {
  echo "Hello world!";
}
sayhi(); // 调用函数
?>
```

> - 函数名能够以字母或下划线开头（而非数字）。
> - 函数名对大小写不敏感。

## 时间

- `time();`

>time()得到的是以秒为单位的时间戳

- `date('Y-m-d H:i:s',time());`

>格式化时间
>
>第一个参数是一个时间格式，默认获取的是格林威治时间（比中国少8小时），获取中国时间需要在前面添加一行`date_default_timezone_set('PRC');`来**设置中国时区**。
>
>第二个参数是一个时间戳(默认可省略)。

- `strtotime($string)`

>将一个有格式的时间字符串转化成一个时间戳，可以用来修改一个时间的格式。
>

# 文件操作

- `basename()`：返回路径中的文件名部分。
- `copy()`：复制文件。
- `dirname()`：返回路径中的目录名部分。
- `disk_free_space()`：返回目录的可用空间。
- `disk_total_space()`：返回一个目录的磁盘总容量。
- `file()`：把文件读入一个数组中。
- `file_exists()`：检查文件或目录是否存在。
- `file_get_contents()`：将文件读入字符串。
- `file_put_contents()` ：将字符串写入文件。
- `filesize()`：返回文件大小。
- `is_dir()`：判断指定的文件名是一个目录。
- `id_file()`：判断指定文件是否为常规的文件。
- `mkdir()`：创建目录。
- `move_uploaded_file()`：将上传的文件移动到新位置。
- `pathinfo()`：返回关于文件路径的信息。
- `rename()`：重命名文件或目录。
- `rmdir()`：删除空的目录。
- `unlink()`：删除文件。

# 表单

## 表单语法

```html
<form action="<?php echo $_SERVER['PHP_SELF'] ?>" method="">
    //默认action不填写为当前页面，建议$_SERVER['PHP_SELF']动态获取当前页面路径
    //method默认为get方式
    //必须有一个提交的方法，submit、button、img等。
</form>
```

## 接收数据

PHP 超全局变量 `$_GET` 和 `$_POST` 用于收集表单数据（form-data）。

 >- `$_GET`：接受URL地址问号参数里的数据。不要使用GET来发送密码或其他敏感信息。
 >- `$_POST`：接受请求体中的数据。(推荐)
 >- `$_REQUEST`：相当于`$_GET`和`$_POST`的并集。
 >- `$_SERVER['REQUEST_METHOD']==='POST'`：判断请求的方式。
 >

## 文件上传/接收

```php
//客户端表单提交文件

 //enctype 必须设置文件格式
 //method 必须是post
<form action="<?php echo $_SERVER['PHP_SELF']; method="post" enctype="multipart/form-data" ?>">
   
    //accept="audio/*"是规定上传的文件种类为音频文件
    //multiple可以让一个文件域多选
    <input type="file" name="file1" accept="audio/*" multiple>
    
    <button>提交</botton>
</form>
    
 //服务端接收文件：$_FILES['表单的name']
 使用 $_FILES接收到的数据是一个数组：
    array (size=1)
    'file1' =>   //input里的name值
    array (size=5)
    'name' => string 'l.jpg' (length=5) //文件名称
    'type' => string 'image/jpeg' (length=10)  //文件格式
    'tmp_name' => string 'D:\wamp64\tmp\php99A5.tmp' (length=25)//临时存放路径，会删除
    'error' => int 0  //0代表是接收成功
    'size' => int 16699
```

## 移动文件

服务器端接收的文件存在一个临时文件夹中，会被删除，所以需要移动到一个固定文件夹中。

完整的文件上传、接收、移动的代码：

```php
<?php 
//使用函数嵌套代码
function upload () {
	//判断客户端的表单内容中有没有文本域（在浏览器端是可以删除文本域代码的）
	if ( !isset($_FILES['avatar']) ) {
		//提示信息
		$GLOBALS['message'] = '别玩我了';
		//结束函数
		return;
	}
    
	//接收文件（数组）
	$avatar = $_FILES['avatar'];

	//error是数组中的一个参数，专门用来判断上传成功与否。(常量)UPLOAD_ERR_OK=0; 0代表上传成功。
	if( $avatar['error'] != UPLOAD_ERR_OK ){
		$GLOBALS['message'] = '上传失败';
		return;
	}

	//将文件从临时目录移动到网站范围之内
	//源文件位置
	$source = $avatar['tmp_name'];
	//移动的位置
	$target = './php_dir/'.$avatar['name'];
	//返回的是一个布尔值
	$moved = move_uploaded_file($source,$target);
	//判断移动是否成功
	if(!$moved){
		$GLOBALS['message'] = '上传失败';
		return;
	}

	echo "上传成功";
}

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
	upload();
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>文件上传</title>
</head>
<body>
	<form action="<?php echo $_SERVER['PHP_SELF']; ?>" method = "post" enctype="multipart/form-data">
		<input type="file" name="avatar">
		<button>提交</button>
		<?php if ( isset($message) ): ?>
		<p> <?php echo $message; ?> </p>
		<?php endif ?>
	</form>
</body>
</html>
```

# JSON

- JSON是一种类似于js的字面量的表述数据的手段。是现如今使用最多的数据格式。

- JSON和JS字面量的区别。
  1. JSON中属性名称必须用双引号包裹。
  2. JSON中字符串必须用双引号包裹。
  3. JSON中不允许使用注释。

- `JSON.parse(str)`：js的方法解析JSON对象。
- `JSON.stringify(arr)`：js的方法转换成JSON对象。
- `JSON_decode()`：php的方法解码JSON对象。转换为php中stdClass类型的对象。如果想得到一个关联数组，可以传入第二个参数为true，得到的是一个关联数组。

# MySQL数据库

## 命令行语句

- `show databases;`：列出所有数据库。

- `create database demo;`：创建一个叫demo的数据库。
- `use demo;`：进入demo数据库。
- `show tables;`：打印当前数据库中的表。
- `create table users (id int,name char(5),age int,gender int);`：创建一个表。
- `desc 表名;`：查看指定表的结构。
- `drop table 表名/数据库名;`：删除表或者数据库。（不可逆的操作）
- `exit|quit;`：退出数据库终端。

## 数据库语句

常见的查询函数：

``` sql
-- 新增
insert into users values (内容);

-- 删除
delete from users where id = '' and title;

-- 修改
update users set title = '';

-- 查询
select * from users;

-- 列出总条目数
select count(1) as count from users;

-- 最大值、最小值、平均值
select max(id) from users;
select min(id) from users;
select avg(id) from users;

-- 限制取几条数据
select * from users limit 2;
-- 越过多少条数据取几条
select * from users limit 1,2;
```

## 操作数据库

### 连接数据库

```php
<?php 
//建立与数据库服务器之间的联系
//函数名前加上 @ 能忽略(不显示)错误信息
$connection = @mysqli_connect('127.0.0.1','root','123456','demo');
if (!$connection) {
	exit('连接数据库失败');
}

//关闭连接
mysqli_close($connection);
```

### 查询操作

```php
//基于刚刚创建的连接对象执行一次查询操作。得到的是一个查询对象（数据集）,暂存在数据库服务器上
// limit 1:在查询语句后面加上表示找到第一条后就不再继续查找，提高查询效率。
$query = mysqli_query($connection, 'select * from users;');
if (!$query) {
    exit('查询失败');
}

//取出一行数据
$row = mysqli_fetch_assoc($query);

//遍历查询对象，取出所有的数据
while($row = mysqli_fetch_assoc($query)) {
    var_dump($row);
}

//释放查询对象（数据集）
mysqli_free_result($query);
```

### 增删改操作

```php
$query = mysqli_query($connection, 'delect * from users where id = 2;');
if (!$query) {
    exit('查询失败');
}

//拿到受影响行，传入的是连接对象，得到的是距离上次连接所产生的影响
$rows = mysqli_affected_rows($connection); 
```

# cookie

```php
// setcookie 是专门用于设置 cookie 的函数
setcookie('key','value');

//只传一个参数是删除，原理：设置过期时间为一个过去时间
setcookie('key');

//传递第三个参数是设置过期时间，不传递就是会话级别的cookie（关闭浏览器会自动删除）
setcookie('key','value',time()+1*24*60*60);

//关联数组的方式访问客户端提交过来的 Cookie
$_COOKIE;
```

`path`是设置`cookie`的作用范围。

`domain`设置`cookie`的作用域名范围。

## session

为cookie加密。将值保存到服务器端

```php
//开启session
session_start();

//存
$_SESSION['name'] = $num;

//移除session
unset($_SESSION['num']);
```

