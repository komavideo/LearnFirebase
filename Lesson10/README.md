Vue + Firebase 协作开发
=======================

## 知识点

* 前端框架：Vue(React, Angular均可)
* 后端框架：Firebase(Firestore, Functions, Hosting, ML...)

## 官网

### Vue CLI

https://cli.vuejs.org/

## 实战演习

~~~bash
#################################################
# 创建Vue应用部分
#################################################
# 安装Vue命令行工具
$ sudo npm install -g @vue/cli
$ vue -V
$ vue ui
# 建立一个web项目，并添加依赖
> vuex
> vue-router
> vuefire
> firebase
# 代码编写
$ code .
# 代码运行
$ npm run serve
$ npm run build

#################################################
# Firebase部分
# 
# 使用Firebase控制台建立一个项目
# 1. 建立一个托管Hosting主机
# 2. 建立一个Web项目，并托管在Hosting主机(可选)
#################################################
$ cd myweb
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
~~~

~~~bash
#################################################
# 编写Vue应用部分
#################################################
~~~

### main.js

~~~js
import { firestorePlugin } from 'vuefire'
Vue.use(firestorePlugin)
~~~

### ./firebase/db.js

~~~js
import firebase from 'firebase/app'
import 'firebase/firestore'

const firebaseConfig = {
    apiKey: "",
    authDomain: "",
    projectId: "",
    storageBucket: "",
    messagingSenderId: "",
    appId: "",
    measurementId: ""
}

// Get a Firestore instance
export const db = firebase
    .initializeApp(firebaseConfig)
    .firestore()

// Export types that exists in Firestore
// This is not always necessary, but it's used in other examples
const { Timestamp, GeoPoint } = firebase.firestore
export { Timestamp, GeoPoint }

// if using Firebase JS SDK < 5.8.0
db.settings({ timestampsInSnapshots: true })
~~~

### ./components/HelloWorld.vue

~~~html
...
<ul>
    <li v-for="doc in documents" :key="doc.id">
        {{ doc.title }} / {{ doc.content }}
    </li>
</ul>
...
~~~

~~~js
import { db } from '../firebase/db'
export default {
    name: 'HelloWorld',
    props: {
        msg: String
    },
    data() {
        return {
            documents: [],
        }
    },
    firestore: {
        documents: db.collection('todos'),
    },
}
~~~

## 课程文件

https://github.com/komavideo/LearnFirebase

## 小马视频频道

http://komavideo.com