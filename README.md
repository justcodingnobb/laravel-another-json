# laravel-anothor-json

Yet Another JSON Encoder For Laravel.  
用于修复 PHP7.1、7.2beta 中 json_encode() 处理 float/double 型数值时溢出的问题.
> 感谢博主提供的思路 [http://www.itread01.com/articles/1489774743.html](http://www.itread01.com/articles/1489774743.html)


## 示例

  ```shell
  >>> $a = 0.1 + 0.7
  => 0.8
  >>> printf('%.20f', $a)
  => 0.79999999999999993339
  >>> json_encode($a)
  => "0.7999999999999999"
  >>> \YaJson::encode($a)
  => "0.8"
  ```

## 用法
1. 修复精度并进行 `json_encode` ：
  ```php
  $data = [
      'a' => 0.1 + 0.7,
      'b' => ['string1', 'string2'],
  ];
  
 \YaJson::encode($data);    //"{"a":0.8,"b":["string1","string2"]}"
  ```
  
2. 只获取修复后的数据，不进行 `json_encode` ：
  ```php
  $data = [
      'a' => 0.1 + 0.7,
  ];
  
 \YaJson::prepare($data);   //['a'=>0.8]
  ```
  
## 安装

1. 安装包文件

  ```shell
  composer require "seekerliu/laravel-another-json:dev-master"
  ```

## 配置

### Laravel 5.5

>  `Laravel 5.5` 安装新包后会默认执行 `@php artisan package:discover` 命令，所以可以不进行下面的操作。

1. 注册 `ServiceProvider` 及 `Facade`:

  ```shell
  php artisan package:discover
  ```

2. 如需修改默认循环深度、精度位数，则创建配置文件：
 
  ```shell
  php artisan vendor:publish
  ```
  
### Laravel 5.4 及以下
1. 注册 `ServiceProvider` 及 `Facade`:

  ```php
  'providers' => [
      //...
      
      Seekerliu\YaJson\ServiceProvider::class,
  ],
  
  'aliases' => [
      //...
      
      'YaJson' => Seekerliu\YaJson\Facade::class,
  ],
  ```
 

2. 如需修改默认循环深度、精度位数，则创建配置文件：

  ```shell
  php artisan vendor:publish --provider="Seekerliu\YaJson\ServiceProvider"
  ```
  

## License

MIT
