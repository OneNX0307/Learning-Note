# Laravel 5.2安装笔记

[TOC]

## 安装 Composer

```shell
php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"	#下载安装脚本composer-setup.php
php composer-setup.php		#执行安装过程
php -r "unlink('composer-setup.php');"		#删除安装脚本
```

## 配置镜像

```shell
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

## 安装Laravel

```shell
composer create-project laravel/laravel learnlaravel5 5.2.31
```

## 运行

```shell
cd learnlaravel5/public
php -S 0.0.0.0:1024
```

访问`http://127.0.0.1:1024`即可看到如下页面

![深度截图20170524230250](/home/alfred/Desktop/深度截图20170524230250.png)