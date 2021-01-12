使用数据库服务 - Cloud Firestore
==============================

## 知识点

* 建立NoSql数据库服务
* 通过Node.js接口访问数据库

## Firebase Admin Node.js SDK Reference

https://firebase.google.com/docs/reference/admin/node

## 控制台

https://console.firebase.google.com

## 实战演习

### 提前准备

~~~bash
$ npm init -y
$ npm install firebase-admin --save
~~~

### main.js

~~~js
const admin = require('firebase-admin');
// 取得Key认证文件
var serviceAccount = require("./myfirebase-483d9-firebase-adminsdk-hthhq-c8397c40c8.json");
admin.initializeApp({
    credential: admin.credential.cert(serviceAccount),
});
// 数据库对象
let db = admin.firestore();
// 服务器时间戳
const FieldValue = admin.firestore.FieldValue;

// addData()
// 添加数据
async function addData() {
    for (i = 1; i <= 5; i++) {
        const res = await db.collection('users').add({
            name: '用户' + i,
            sex: i % 2 == 0 ? '男' : '女',
            regdate: FieldValue.serverTimestamp()
        });
        console.log('Added document with ID: ', res.id);
    }
}

// getData()
// 读取数据
async function getData() {
    await db.collection('users').get()
        .then((snapshot) => {
            snapshot.forEach((doc) => {
                console.log(doc.id, '=>', doc.data());
            });
        })
        .catch((err) => {
            console.log('Error getting documents', err);
        });
}

// updData()
// 更新数据
async function updData() {
    const userRef = db.collection('users').doc('RNd4RyaDsHE8fsQr6DV1');
    const res = await userRef.update({
        age: 25,
        upddate: FieldValue.serverTimestamp()
    });
}

// delData()
// 删除数据
async function delData() {
    let deleteDoc = await db.collection('users').doc('RNd4RyaDsHE8fsQr6DV1').delete();
    console.log(deleteDoc)
}
~~~

## 课程文件

https://github.com/komavideo/LearnFirebase

## 小马视频频道

http://komavideo.com