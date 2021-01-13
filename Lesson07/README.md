iOS联合开发 - 数据读取
===================

## 知识点

* iOS + Firestore联合开发

## 实战演习

## pod工具安装

https://cocoapods.org/

## Firebase控制台

1. 注册应用
   com.komavideo.myapp  
2. 下载配置文件 - GoogleService-Info.plist
3. 添加 Firebase SDK

~~~bash
$ pod init
$ nano Podfile
...
# add the Firebase pod for Google Analytics
pod 'Firebase/Analytics'
pod 'Firebase/Core'
pod 'Firebase/Firestore'
# Optionally, include the Swift extensions if you're using Swift.
pod 'FirebaseFirestoreSwift'
# add pods for any other desired Firebase products
# https://firebase.google.com/docs/ios/setup#available-pods
...
$ pod install
~~~

## Xcode 工程编辑

### AppDelegate.swift

```swift
import Firebase
...
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    FirebaseApp.configure()
    return true
}
```

### NewsHomeViewModel.swift

```swift
import FirebaseFirestore
struct News: Identifiable {
    var id: String
    var title: String
}
class NewsHomeViewModel: ObservableObject {
    @Published var newsList = [News]()
    private var db = Firestore.firestore()
    func fetchNews() {
        db.collection("news").limit(to: 5).addSnapshotListener { (query, error) in
            guard let documents = query?.documents else {
                print("没有找到数据")
                return
            }
            self.newsList = documents.map { (doc) -> News in
                let data = doc.data()
                let id = doc.documentID
                let title = data["title"] as? String ?? ""
                return News(id: id, title: title)
            }
        }
    }
}
```

### ContentView.swift

```swift
import SwiftUI
struct ContentView: View {
    @ObservedObject private var viewModel = NewsHomeViewModel()
    var body: some View {
        Group {
            VStack {
                ForEach(viewModel.newsList) { news in
                    Text(news.title)
                }
            }
            .onAppear() {
                self.viewModel.fetchNews()
            }
        }
    }
}
```

## 改良 NewsHomeViewModel.swift - Codable

```swift
import FirebaseFirestore
import FirebaseFirestoreSwift

struct News: Identifiable, Codable {
    // 属性包装器，自动映射文档ID
    @DocumentID
    var id: String? = UUID().uuidString
    var title: String
    // 编码字段
    enum CodingKeys: String, CodingKey {
        case title
    }
}

class NewsHomeViewModel: ObservableObject {
    @Published var newsList = [News]()
    private var db = Firestore.firestore()
    func fetchNews() {
        db.collection("news").limit(to: 5).addSnapshotListener { (query, error) in
            guard let documents = query?.documents else {
                print("没有找到数据")
                return
            }
            // 使用compactMap，过滤nil数据
            self.newsList = documents.compactMap { (doc) -> News? in
                return try? doc.data(as: News.self)
            }
        }
    }
}
```

## 课程文件

https://github.com/komavideo/LearnFirebase

## 小马视频频道

http://komavideo.com