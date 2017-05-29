# Laravel学习笔记

[TOC]
##安装
### 安装 Composer

```shell
php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"	#下载安装脚本composer-setup.php
php composer-setup.php		#执行安装过程
php -r "unlink('composer-setup.php');"		#删除安装脚本
```

### 配置镜像

```shell
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

### 安装Laravel

```shell
composer create-project laravel/laravel learnlaravel5 5.2.31
```

### 运行

```shell
cd learnlaravel5/public
php -S 0.0.0.0:1024
```

访问`http://127.0.0.1:1024`即可看到如下页面

![深度截图20170524230250](/home/alfred/Desktop/深度截图20170524230250.png)

## 框架目录

## 路由

### 基础路由

```php
Route::get('hello',function() {
  return 'getMehtod';
});
//浏览器访问locahost:8000/hello
```

```php
Route::post('hello',function () {
  return 'postMethod';
});
//浏览器访问locahost:8000/hello
```

### 多请求路由

```php
Route::any('hello',function () {
  return 'anyMethod';
});
//浏览器访问locahost:8000/hello
```

```php
Route::match(['get','post'], 'hello', function () {
  return 'matchMethod';
});
//浏览器访问locahost:8000/hello
```

### 路由参数

```php
Route::get(user/{id}, function($id) {
  return 'User-id' . $id;
});
//浏览器访问locahost:8000/user/5
```

```php
Route::get(user/{name?}, function($name = 'alfred') {
  return 'User-name' . $name;
});
//浏览器访问locahost:8000/user/alfred
```

```php
Route::get(user/{name}, function($name 'alfred') {
  return 'User-name' . $name;
})->where('name', '[A-Za-z]+');
//浏览器访问locahost:8000/user/alfred
```

```php
Route::get(user/{id}{name}, function($id, $name = 'alfred') {
  return 'User-id-' . $id . User-name' . $name;
})->where('id' => '[0-9]+', 'name' => '[A-Za-z]+');
//浏览器访问locahost:8000/id/5/alfred
```

### 路由别名

```php
Route::get('user/memeber-center', ['as' => 'center', function() {
  return 'center';
}])
//浏览器访问locahost:8000/user/center
```

### 路由群组

```php
Route::group(['prefix' => 'member'], function(){
  Route::get('user/center', ['as' => 'center', function() {
    return route('center');
  }]);
  Route::any('alfred', function() {
    return 'alfred';
  });
})
//浏览器访问locahost:8000/member/center
```

### 路由中输出视图

```php
Route::get('view', function() {
  return view('welcome');
});
//浏览器访问locahost:8000/view
```

## 控制器

### 新建控制器

右键`app`->`Http`->`Controllerss`文件夹，新建`php`文件，命名为`MemberController`:

```php
<?php
namespace App\Http\Controllers;		//命名空间
class MemberController extends Controller		//基于Controller类新建MemberController类
  {
    public function info()		//新建info方法
      {
        return 'member-info';
      }
  }
```

### 控制器和路由关联

```php
//routes.php
Route::get('member/info', 'MemberController@info');
//浏览器访问locahost:8000/member/info
```

或者

```php
Route::get('member/info', ['uses' => 'MemberController@info']);
```

```php
Route::get('member/info', [
  'uses' => 'MemberController@info',
  'as' => 'memberinfo'
]);
//给路由起别名
//在MemberController.php中添修改为
<?php
namespace App\Http\Controllers;		//命名空间
class MemberController extends Controller		//基于Controller类新建MemberController类
  {
    public function info()		//新建info方法
      {
        return route('memberinfo');
      }
  }
//浏览器访问locahost:8000/member/info
```

### 参数绑定

```php
//routes.php
Route::get('member/{id}', ['uses' => 'MemberController@info'])
  ->where('id', '[0-9]+');		//参数类型现限制
//在对应的方法中传入$id
//MemberController.php
public function info($id) 
{
  return 'member-info-id' . $id;
}
//浏览器访问locahost:8000/member/555
```

## 视图

### 新建视图

右键`resources`->`views`文件夹，新建php文件，命名为`member-info.php`，写入

```php
member-info php
```

### 输出视图

```php
//MemberController
<?php
namespace App\Http\Controllers;		//命名空间
class MemberController extends Controller		//基于Controller类新建MemberController类
  {
    public function info()		//新建info方法
      {
        return view('member-info');
      }
  }
//浏览器访问locahost:8000/member/555
```

### 新建默认模板

右键`resources`->`views`文件夹，新建文件，命名为`info.blade.php`，写入

```php
info blade
```

对应的控制器该为

```php
//MemberController
<?php
namespace App\Http\Controllers;		//命名空间
class MemberController extends Controller		//基于Controller类新建MemberController类
  {
    public function info()		//新建info方法
      {
        return view('info');
      }
  }
//浏览器访问locahost:8000/member/555
```

一般情况下，一个 控制器会对应一个目录

![深度截图20170529142503](/home/alfred/Desktop/深度截图20170529142503.png)
相应的`MemberController.php`中应该改为
```php
return view('member/info');
```

模板可以带变量

```php
//MemberController
<?php
namespace App\Http\Controllers;		//命名空间
class MemberController extends Controller		//基于Controller类新建MemberController类
  {
    public function info()		//新建info方法
      {
        return view('info', [
          'name' => 'alfred',
          'age' => 18
        ]);
      }
  }
//浏览器访问locahost:8000/member/555
```

相应的在`member.blade.php`中

```php
member/info blade
  {{$name}}  {{$age}}
```

## 模型

### 新建模型

右键`app`新建`php`文件，命名为`Member.php`

```php
<?php
namespace App;
use Illuminagte\Database\Eloquent\Model;
class Member extends Model
  {
    public static function getMember()
      {
        return 'member name is alfred';
      }
  }
```

### 调用模型

```php
//MemeberController.php
<?php
namespace App\Http\Controllers;		//命名空间
class MemberController extends Controller		//基于Controller类新建MemberController类
  {
    public function info()		//新建info方法
      {
		return Member::getMember();
      }
  }
//浏览器访问locahost:8000/member/555
```

## 数据库操作

### DB facade（原始查找）

#### 新建数据表

```mysql
CREATE TABLE IF NOT EXITS student(
	`id` INT AUTO_INCREMENT PRIMARY KEY,
  	`name` VARCHAR(255) NOT NULL DEFAULT '' COMMENT '姓名',
  	`age` TINYINT UNSIGNED NOT NULL DEFAULT 0  COMMENT '年龄',
  	`sex` TINYINT UNSIGNED NOT NULL DEFAULT 10 COMENT '性别',
  	`created_at` INT NOT NULL DEFAULT 0 COMMENT '新增时间',
  	`updated_at` INT NOT NULL DEFAULT 0 COMMENT 'XIUGAISHI修改时间'
)ENGINE=InnoDB DEFAULT CHARSET=utf8 AUTO_INCREMENT=1001 COMMENT='学生表';
```

#### 链接数据库

数据库配置文件在`config`目录下的`database`文件里，其中`env`是在根目录的`.env`文件里，修改相应的数据库配置信息即可。

#### 使用DB facade实现CURD

右键`app`->`Http`->`Controllers`文件夹，新建`php`文件，命名为`StudentController.php`

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton test1()
      {
        return 'test1';
      }
  }
```

添加路由

```php
//routes.php
Route::get('test1', ['uses' => 'StudentController@test1']);
//浏览器访问locahost:8000/test1
```

##### 查询

查询刚才创建的`student`数据表

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton test1()
      {
        $students = DB::select('select * from student');
      	dd($students);
      }
  }
```

##### 新增

```php
$bool = DB::insert('insert into student(name, age) values(?, ?)', ['alfred', 18]);
var_dump($bool);
```

##### 修改

```php
$num = DB::('update student set age = ? where name = ?', [20, 'alfred']);
var_dump($num);
```

##### 删除 

```php
$num = DB::('delete from student where id > ?', [1001]);
var_dump($num);
```

### 查询构造器

#### 使用查询构造器新增数据

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton query1()
      {
        $bool = DB::table('student')->insert(
        	['name' => 'sandy', 'age' => 18]
        );
      	var_dump($bool);
      }
  }
//新增数据并且返回id
$id = DB::table('student')->insertGetId(
	['name' => 'alfred', 'age' => 18]
);
var_dump($id);
```

新增路由：

```php
//routes.php
Route::get('query1', ['uses' => 'StudentController@query1']);
//浏览器访问locahost:8000/query1
```

#### 修改数据

```php
//StudentController.php
public function query2()
  {
    $num = DB::table('student')
      ->where('id', 12)
      ->update(['age' => 30]);
    var_dump($num);
  }
//自增
     $num = DB::table('student')
          ->where('id', 12)
          ->increment('age', 2);
     var_dump($num);
//自减
     $num = DB::table('student')
          ->where('id', 12)
          ->decrement('age', 2);
     var_dump($num);
//自增同时修改其他字段
     $num = DB::table('student')
          ->where('id', 12)
          ->increment('age', 3, ['name' => 'nancy']);
     var_dump($num);
//浏览器访问locahost:8000/query2
```

#### 删除数据

```php
//StudentController.php
public function query3()
  {
  //delete()
    $num = DB::table('student')
      ->where('id', 15)
    //->where('id', '>=', 13)
      ->delete();
    //truncate()		//清空数据表，不反回任何数据
    var_dump($num);
  }
```

新增一条路由

```php
//routes.php
Route::get('query3', 'StudentController@query3');
//浏览器访问locahost:8000/query3
```

#### 查询数据

```php
//StudentController.php
public function query4()
  {
  //get()
  $students = DB::table('student')->get();
  dd($students);
  //first
  $students = DB::table('student')
    ->orderBy('id','desc')
    ->first();
  dd($students);
  //where
  $students = DB::table('student')
   	->where('id', '>=', 1002)
    ->get();
  dd($students);
  //whereRaw多个条件
  $students = DB::table('student')
    ->whereRaw('id >= ? and age > ?', [1001, 18])
    ->get();
  dd($students);
  //pluck
  $names = DB::table('student')
    ->pluck('name');
  dd($names);
  //lists
  $names = DB::table('student')
    ->lists('name');
  dd($names);
  //lists指定某个键作为返回下标
  $names = DB::table('student')
    ->lists('name','id');	//指定id作为返回下标
  dd($names);
  //select
  $names = DB::table('student')
    ->select('id', 'name', 'age')
    ->get();
  dd($names);
  //chunk
  echo '<pre>';
  DB::table('student')->chunk(2, function($students) {
    var_dump($students);
    if (条件)
      {
        return false;		//停止
      }
    };
  }
```

添加一条路由

```php
//routes.php
Route::get('query4', 'StudentController@query4');
//浏览器访问locahost:8000/query4
```

#### 聚合函数

```php
//StudentController.php
public function query5()
  {
    //count
    $num = DB::table('student')->count();
    var_dump($num);
    //max()
    $max = DB::table('student')->max();
    var_dump($max);
    //min()
    $min = DB::table('student')->min();
    var_dump($min);
    //avg()
    $avg = DB::table('student')->avg();
    var_dump($avg);
    //sum()
    $sum = DB::table('student')->sum();
    var_dump($sum);
  }
```

添加一条路由

```php
//routes.php
Route::get('query5', 'StudentController@query5');
//浏览器访问locahost:8000/query5
```

### Eloquent ORM

#### 模型建立

右键`app`目录新建一个`php`文件，命名为`Student.php`

#### 查询数据库

```php
//StudnetController.php
<？php
namespace App;
use Illuminate\Database\Eloquent\Model;
class Student extends Model
  {
    //默认是使用模型名称的复数作为表来关联，在这里应该是studets表，如果没有这个表，就需要手动关联模型和表
  	protected $table = 'student';
  	//默认以id作为主键，如果不是需要手动指定
  	protected $primaryKey = 'id';
  	public function orm1()
      {
        //all()
      	$students = Student::all();
      	dd($students);
      	//find()
        $students = Student::find('1001');
      	dd($students);
      	//findOrFail()
      	$students = Student::findOrFail('1001');
      	dd($students);
      	//查询构造器在orm中的使用
      	//get()
      	$students = Student::get();
      	dd($students);
        //first()
      	$students = Student::where('id', '>', '1001')
          ->orderBy('age', 'desc')
          ->first();
      	dd($students);
      	//chunk()
      	echo '<pre>';
        Student::chunk(2, function($students) {
        	var_dump($students);
      	});
      	//聚合函数
      	//count()
      	$num = Student::count();
      	var_dump($num);
        //max()
      	$max = Student::max();
      	var_dump($max);
      }
  }
```

添加一条路由

```php
//routes.php
Route::get('orm1', 'StudentController@orm1');
//浏览器访问locahost:8000/orm1
```

#### 新增数据

##### 通过模型新增（涉及到自定义时间戳）

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton orm2()
      {
		$student = new Student();
      	$student->name  = 'alfred';
      	$student->age  = 18;
      	$bool = $student->save();
      	dd($bool);
      }
  }
```

新增一条路由

```php
//routes.php
Route::get('orm2', 'StudentController@orm2');
//浏览器访问locahost:8000/orm2
```

```php
//Student.php
protected $timestamps = true;	//自动维护时间戳
//返回unix格式的时间戳
protected function getDateFormat()
  {
    return time();
  }
//不使用自动的时间格式化
protected function asDateTime($val)
  {
    return $val;
  }
```

##### 使用`create`方法新增（涉及到批量赋值）

默认是不允许批量赋值字段的，所以需要在`Student.php`中设置允许批量赋值的字段：

```php
//Student.php
protected $fillable = ['name', 'age'];	//指定允许批量赋值的字段
protected $guarded - ['sex'];		//指定不允许批量赋值的字段
```

然后在`StudentController.php`中进行批量赋值：

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton orm2()
      {
		$student = Student::create(
        	['name' => 'alfred', 'age' => 18]
        );
      	dd($student);
      }
  }
```

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton orm2()
      {
		$student = Student::firstOrCreate(
        	['name' => 'alfred']
        );
      	dd($student);
      }
  }
```

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton orm2()
      {
		$student = Student::firstOrNew(
        	['name' => 'alfred']
        );
      	$bool = $student->save();
      	dd($bool);
      }
  }
```

#### 修改数据

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton orm3()
      {
		$student = Student::find(1021);
      	$student->name = 'kitty';
      	$bool = $student->save();
      	var_dump($bool);
      }
  }
```

添加一条路由

```php
//routes.php
Route::get('orm3', 'StudentController@orm3');
//浏览器访问locahost:8000/orm3
```

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton orm3()
      {
		$num = Student::where('id', '>', 1019)->update(
        	['age' => 41]
        );
      	var_dump($num);
      }
  }
```

#### 删除数据

##### 通过模型删除

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton orm4()
      {
		$student = Student::find(1021);
      	$bool = $student->delete();
      	var_dump($bool);
      }
  }
```

##### 通过主键删除

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton orm4()
      {
		$num = Student::destory(1020, 1021);
      //$num = Student::destory([1020, 1021]);
      	var_dump($num);
      }
  }
```

##### 根据指定条件删除	

```php
//StudentController.php
<?php
namespace App\Http\Controllers;
class StudentController extends Controller
  {
    public funciton orm4()
      {
		$num = Student::where('id', '>', 1004)->delete();
      	var_dump($num);
      }
  }
```

添加一条路由

```php
//routes.php
Route::get('orm4', 'StudentController@orm4');
//浏览器访问locahost:8000/orm4
```

## Blade模板引擎

### 模板继承

![深度截图20170529204201](/home/alfred/Desktop/深度截图20170529204201.png)

##### 



右键`resources`->`views`右键新建文件`layout.blade.php`：

```php
//layout.blade.php
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>轻松学会Laravel - 模板继承</title>
    <style type="text/css">
        .header {
            width: 1000px;
            height: 150px;
            margin: 0 auto;
            background: #f5f5f5;
            border: 1px solid #ddd;
        }

        .main {
            width: 1000px;
            height: 300px;
            margin: 0 auto;
            background: #f5f5f5;
            border: 1px solid;
        }

        .main .sidebar {
            float: left;
            width: 20%;
            height: inherit;
            background: #f5f5f5;
            border: 1px solid #ddd;
        }

        .footer {
            width: 1000px;
            height: 150px;
            margin:0 auto;
            margin-top: 15px;
            background: #f5f5f5;
            border: 1px solid #ddd;
        }
    </style>
</head>
<body>
<div class="header">
    @section('header')
    头部
    @show
</div>

<div class="main">
    <div class="sidebar">
        @section('sidebar')
        侧边栏
        @show
    </div>

    <div class="content">
        @yield('content', '主要内容区域')
    </div>
</div>

<div class="footer">
    @section('footer')
    底部
    @show
</div>
</body>
</html>
```

右键`resources`->`views`右键新建文件夹`member`，右键`member`文件夹新建`php`文件，命名为`section1.blade.php`

```php
//section1.blade.php
@extends('layout')

@section('header')
    @parent		//输出父模板视图
    header		//在父模板视图中添加header
@stop


@section('sidebar')
    @parent
    sidebar
@stop


@section('content')
    content
  
  <!--1. 模板中输出php变量 -->
  <p>{{$name}}</p>		//需要在控制器总先添加变量$name
  
  <!--2. 模板中调用php函数 -->
  <p>{{ time() }}</p>
  <p>{{ date('Y-m-d H:i:s'), time() }}</p>
  <p>{{ in_array($name, $arr) ? 'true' : 'false'}}</p>
  <p>{{ var_dump($arr) }}</p>
  <p>{{ isset(name) ? $name : 'defalut' }}</p>		//可以简写为： <p>{{ $name or 'default' }}</p>
  
  <!--3. 原样输出 -->
  <p>@{{ $name }}</p>
  
  <!--4. 模板中的注释 --> 
  {{-- 模板中的注释 --}}

  <!--5. 引入子视图 -->
    @include('member.common1')		//引入member文件夹下的common子视图
    @include('member.common1'， ['message' => '我是错误信息'])		//可以传值给common子视图中的变量$message
@stop
```

模板中输出变量需要在控制器`StudentController.php`中添加变量

```php
//StudentController.php
public function section1() 
{
  $name = 'alfred';
  $arr = ['alfred', 'sandy'];
  return view('member.section1', [
    'name' => $name,
    'arr' => $arr
  ]);
}
```

### 流程控制

```html
//section1.blade.php
@extends('layout')
@section('header')
    @parent		//输出父模板视图
    header		//在父模板视图中添加header
@stop
@section('sidebar')
    @parent
    sidebar
@stop
@section('content')
    content
<!-- if语句 -->
@if ($name = 'alfred')
  I'm alfred
@elseif ($name = 'sandy')
  I'm sandy
@else
  who am i?
@endif
  <br>
@if (in_array($name, $arr))
  true
@else
  false
@endif
  
<!-- unless语句 -->
@unless ($name != 'alfred')
  I'm alfred
@endunless

<!-- for语句 -->
@for ($i=0; $i < 1; $i++)
<p>{{ $i }}</p>
@endfor

<!-- foreach语句 -->
@foreach ($students as student)		//需要在控制器查询数据库并传入查询结果
	<p>{{ $student->name }}</p>
@endforeach

<!-- forelse语句 -->
@forelse ($students as student)		//需要在控制器查询数据库并传入查询结果
	<p>{{ $student->name }}</p>
@empty
	<p>null</p>
@endforelse
@stop
```

```php
//StudentController.php
public function section1() 
{
  $students = Student::get();
  $name = 'alfred';
  $arr = ['alfred', 'sandy'];
  return view('member.section1', [
    'name' => $name,
    'arr' => $arr,
    'students' => $students
  ]);
}
```

### 模板中的`url`

```php
//StudentController.php
public function urlTest() 
{
	return 'urlTest';
}
```

添加一条路由

```php
//routes.php
Route::get('url', ['as' => 'url‘, 'uses' => 'StudentController@urlTest']);
//浏览器访问locahost:8000/orm4
```

```php
//section1.blade.php
<a href="{{ url('url') }}">url()</a>		//ur()函数通过路由的名称生成url
<a href="{{ action('StudentController@urlTest') }}">action()</a>		//action()函数通过指定控制器及方法名生成url
<a href="{{ route('url') }}">route()</a>		//route()函数通过路由的别名生成url
```



