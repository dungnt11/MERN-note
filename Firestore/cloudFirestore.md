# Cloud Firestore [source](https://firebase.google.com/docs/firestore/quickstart?authuser=0)

Firebase cung cấp 2 gói trong database

- Cloud Firestore ( gói mới với nhiều tính năng hơn )
- Realtime Database ( gói cũ )

## Bắt đầu khởi tạo dự án

Cloud Firestore cung cấp cho chúng ta chế độ 

- **Test** **mode** : To get started with the web, iOS, or Android SDK, select test mode. Mọi người đều có thể read && write
- **Locked** **mode** :To get started with the C#, Go, Java, Node.js, PHP, Python, or Ruby server client library, select locked mode.

## Sử dụng cùng react

1. ```npm install fire-store``` rồi tạo file config

```js
import firebase from "firebase/app";
import "firebase/auth";
import "firebase/firestore";

let configFirebase = firebase.initializeApp({
  apiKey: "AIzaSyCdvHcI8LFIV89XwhuVQ5yae7gCoU6E-Us",
  authDomain: "ninja-learn.firebaseapp.com",
  databaseURL: "https://ninja-learn.firebaseio.com",
  projectId: "ninja-learn",
  storageBucket: "",
  messagingSenderId: "498944436996",
  appId: "1:498944436996:web:651d602c73657d24"
});

export default configFirebase;

```

2. Sử dụng

   ```js
   import configFirebase from "../../config/firebaseCf";
   const db = configFirebase.firestore();
   ```

### REST Full Api

1. GET

   ```js
   db.collection("tên").get().then((res) => {
       res.docs.map(e => e.data())
   }).catch(...)
   ```

2. POST

   ```js
   // Add a new document with a generated id.
   db.collection("cities").add({
       name: "Tokyo",
       country: "Japan"
   })
   .then(function(docRef) {
       console.log("Document written with ID: ", docRef.id);
   })
   .catch(function(error) {
       console.error("Error adding document: ", error);
   });
   ```

   Sử dụng add sẽ được id như sau

   ![1563596071577](C:\Users\Admin\OneDrive\img markdown\1563596071577.png)

   Còn nếu sử dụng ```set``` ta sẽ tạo id dựa vào tham số truyền lên

   ```js
   db
         .collection("users")
         .doc("LA") // tên id gửi lên
         .set({
           name: "Los Angeles",
           state: "CA",
           country: "USA"
         });
   ```

   **Chú ý** : nếu chưa có sẽ tạo, nếu có rồi sẽ thành update

   Phương thức ```set``` sẽ ghi đè, nếu muốn hợp nhất ta làm như sau

   ```js
   var cityRef = db.collection('cities').doc('BJ');
   
   var setWithMerge = cityRef.set({
       capital: true
   }, { merge: true }) // hợp nhất
   ```

   

3. Delete

   ```js
   const id = id cần xóa
   db.collection("cities").doc(id).delete().then(function() {
       console.log("Document successfully deleted!");
   }).catch(function(error) {
       console.error("Error removing document: ", error);
   });
   ```

4. Search && query

   ```js
   db.collection('cities').where('city', '==', 'manchester').get().then((res) => res.docs.map(e => e.data()))
   ```

5. [Order && limit](https://firebase.google.com/docs/firestore/query-data/order-limit-data?authuser=0) 

   ```js
   citiesRef.orderBy("name").limit(3)
   ```

   giảm dần ( default là tăng dần )

   ```js
   citiesRef.orderBy("name", "desc").limit(3)
   ```

   ```js
   citiesRef.orderBy("state").orderBy("population", "desc")
   // sắp xếp theo state, giảm dần trong mỗi đơn vị
   ```

6.  Update

   ```js
   yield db
         .collection("users")
         .doc("cl4VIzwYU2uAAocI7ya0")
         .update({
           name: "cc",
           age: 15
         });
   ```

   ```Update``` dữ liệu lồng nhau

   ```js
   // Create an initial document to update.
   var frankDocRef = db.collection("users").doc("frank");
   frankDocRef.set({
       name: "Frank",
       favorites: { food: "Pizza", color: "Blue", subject: "recess" },
       age: 12
   });
   
   // To update age and favorite color:
   db.collection("users").doc("frank").update({
       "age": 13,
       "favorites.color": "Red"
   })
   .then(function() {
       console.log("Document successfully updated!");
   });
   
   ```

   

   

## Xử lý thời gian

Lấy giờ hiện tại trên server

```js
var docRef = db.collection('objects').doc('some-id');

// Update the timestamp field with the value from the server
var updateTimestamp = docRef.update({
    timestamp: firebase.firestore.FieldValue.serverTimestamp()
});
```

Truyền giờ từ local vào

```js
 firebase.firestore.Timestamp.fromDate(new Date("December 10, 1815")),
```

