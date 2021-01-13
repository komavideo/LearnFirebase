使用云函数 - Cloud Functions
===========================

## 知识点

* 使用云函数完成自动化作业

## 官网

https://firebase.google.com/products/functions

★★★注意★★★

2020年12月开始只有【Blaze】方案才能使用。

## 官方样例

https://github.com/firebase/functions-samples

## 实战演习

### 提前准备

~~~bash
$ npm init -y
$ npm install firebase-functions@latest firebase-admin@latest --save
$ npm install uuid-v4 --save
$ firebase init functions
$ firebase init emulators
$ nano functions/package.json
...
    "node": "12"
...
# 编写云函数
$ nano functions/index.js
...
见下例
...
# 调试函数
$ firebase emulators:start --project=default
# 部署函数，Node.js 10以上需要Blaze方案
$ firebase deploy --only functions
~~~

## index.js

```javascript
const functions = require('firebase-functions');
const admin = require('firebase-admin');
admin.initializeApp();

exports.helo = functions.region('asia-northeast1').https.onRequest((request, response) => {
    response.json({
        result: 'ok'
    })
});

exports.users = functions.region('asia-northeast1').https.onRequest((request, response) => {
    var docList = []
    let usersRef = admin.firestore().collection('users')
    return usersRef.limit(10).get()
        .then(async queryResult => {
            queryResult.forEach((doc) => {
                var tmpDoc = doc.data()
                docList.push(tmpDoc)
            })    
            response.json({
                result: docList
            })
        })
        .catch(error => {
            console.error(error)
            response.json({
                result: 'fail'
            })
        })
});
```

## 课程文件

https://github.com/komavideo/LearnFirebase

## 小马视频频道

http://komavideo.com