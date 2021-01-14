Vite(Vue 3)托管Firebase主机服务
==============================

## 知识点

* Vue 3 (Vite方式)
* Firebase Hosting

## 官网

### Vite

https://github.com/vitejs/vite

## 实战演习

~~~bash
#################################################
# Vue3(Vite)应用开发
#################################################
# 项目初始化
$ npm init @vitejs/app
>myapp
# 安装项目必要文件
$ cd myapp
$ npm install
# 开发调试
$ npm run dev
# 代码调试
$ code .
# 文件打包
$ npm run build
# 本地运行打包文件
$ python3 -m http.server 8000 --directory dist

#################################################
# Firebase部分
# 
# 使用Firebase控制台建立一个项目
# 1. 建立一个托管Hosting主机
# 2. 建立一个Web项目，并托管在Hosting主机(可选)
#################################################
$ cd myapp
$ firebase init
>主机服务+单页设置
>本地模拟器设置
# 设置部署目标
$ nano firebase.json
...
{
  "hosting": {
    "site": "[hosting_name]",
    "public": "dist",
...
# 本地调试，动作确认
$ firebase serve --only hosting --project=default
# 部署到Firebase Hosting
$ firebase deploy --project=default

Done.
~~~

## 课程文件

https://github.com/komavideo/LearnFirebase

## 小马视频频道

http://komavideo.com