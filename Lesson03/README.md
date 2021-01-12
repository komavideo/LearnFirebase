主机托管服务 - Hosting
=====================

## 知识点

* 使用主机托管服务托管一个网站

## 官网

https://firebase.google.com/products/hosting

## 控制台

https://console.firebase.google.com

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
$ npm init -y
# 初始化firebase设置
$ firebase init
> 选择主机托管服务
$ nano public/index.html
~~~
~~~html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Helo Firebase from Koma!</title>
</head>

<body>
    <h1>Helo Firebase from Koma!</h1>
    <!-- The core Firebase JS SDK is always required and must be listed first -->
    <script src="/__/firebase/8.2.2/firebase-app.js"></script>

    <!-- TODO: Add SDKs for Firebase products that you want to use
        https://firebase.google.com/docs/web/setup#available-libraries -->
    <script src="/__/firebase/8.2.2/firebase-analytics.js"></script>

    <!-- Initialize Firebase -->
    <script src="/__/firebase/init.js"></script>

    <script>
        let analytics = firebase.analytics();
        // 记载一个页面事件
        analytics.logEvent('homepage_content', {
            content_type: 'homepage',
            content_id: 'P1',
            items: [{ name: 'homepage/index' }]
        });
    </script>
</body>

</html>
~~~
~~~bash
# 本地部署测试
$ firebase serve --only hosting --project=default
# 部署网站
$ firebase deploy --project=default
~~~

## 课程文件

https://github.com/komavideo/LearnFirebase

## 小马视频频道

http://komavideo.com