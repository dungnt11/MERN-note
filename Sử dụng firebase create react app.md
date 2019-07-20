# Sử dụng firebase create react app

Các bước sử dụng firebase

1. Vào trang firebase tạo project, tiếp đến vào app react, ```npm install --save firebase```

2. Tạo file config ```/config/fbConfig.js```

   ```js
   // must be listed before other Firebase SDKs
   import * as firebase from "firebase/app";
   
   // Add the Firebase services that you want to use
   import "firebase/auth";
   import "firebase/firestore";
   
   const firebaseConfig = {
     apiKey: "AIzaSyDl4SiOGTkvf1Fq64ZrsBMJ5gvswrm2vp4",
     authDomain: "ninja-learn.firebaseapp.com",
     databaseURL: "https://ninja-learn.firebaseio.com",
     projectId: "ninja-learn",
     storageBucket: "",
     messagingSenderId: "498944436996",
     appId: "1:498944436996:web:651d602c73657d24"
   };
   
   firebase.initializeApp(firebaseConfig);
   firebase.firestore().settings({ timestampsInSnapshots: true });
   
   export default firebase;
   
   ```

   [Setup link](https://firebase.google.com/docs/web/setup?authuser=0)

   

Kết nối redux với firebase

```npm install react-redux-firebase redux-firestore```

