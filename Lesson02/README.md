服务器SDK安装 - Firebase Admin SDK
=================================

## 知识点

* 服务器端全功能管理SDK安装 - Firebase Admin SDK

## 官网

https://firebase.google.com/docs/admin/setup

## 官方样例

https://github.com/firebase/firebase-admin-node

## 控制台

https://console.firebase.google.com

## 实战演习

~~~bash
$ mkdir myfirebase
$ cd myfirebase
$ npm init -y
$ npm install firebase-admin --save
$ nano main.js
...
var admin = require('firebase-admin');
...
$ node main.js
~~~

## 生成新的工程项目-LearnFirebase

## 生成(Firebase控制台-项目设置-服务账号)

*生成新的私钥*

`myapp-00000-firebase-adminsdk-00000-0000000000.json`

## main.js

```js
var admin = require("firebase-admin");
var serviceAccount = require("./myapp-00000-firebase-adminsdk-00000-0000000000.json");
admin.initializeApp({
    credential: admin.credential.cert(serviceAccount),
});
// var defaultProjectManagement = admin.projectManagement();
// console.log(defaultProjectManagement)

let db = admin.firestore();
db.collection('users').get()
    .then((snapshot) => {
        snapshot.forEach((doc) => {
            console.log(doc.id, '=>', doc.data());
        });
    })
    .catch((err) => {
        console.log('Error getting documents', err);
    });
```

## 课程文件

https://github.com/komavideo/LearnFirebase

## 小马视频频道

http://komavideo.com