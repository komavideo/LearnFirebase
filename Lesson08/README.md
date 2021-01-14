操作数据的Web应用 - Cloud Firestore
=================================

## 知识点

* 建立一个Web应用，操作Firestore数据库(读写)
* 使用主机托管服务(Hosting)托管这个应用

## 官网

### Firestore

https://firebase.google.com/products/firestore

### Hosting

https://firebase.google.com/products/hosting

## 实战演习

~~~bash
#####################################
# 使用Firebase控制台建立一个项目
# 建立一个Web项目，并托管在Hosting主机
#####################################
# 本地安装firebase管理工具
$ sudo npm install -g firebase-tools
# 初始化npm工程
$ mkdir myweb
$ cd myweb
$ npm init
# 初始化firebase设置
$ firebase init
> 选择主机托管服务
$ nano public/index.html
~~~
~~~html
...
>>>index.html
...
~~~
~~~bash
# 本地部署测试
$ firebase serve --project=default
# 部署网站
$ firebase deploy --project=default
~~~

## 课程文件

https://github.com/komavideo/LearnFirebase

## 小马视频频道

http://komavideo.com