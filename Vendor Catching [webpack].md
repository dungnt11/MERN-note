# Vendor Catching

Để cache những thư viện không muốn load cùng khi chuyển trang ta sẽ sử dụng kĩ thuật này

1. Trước hết tạo mảng chứa các thư viện muốn catching

   ```js
   const LIBS = ["react", "react-dom"];
   ```

   

2. Sử dụng webpack bundle thành 2 khối: **bundle** & **vendor** 

   Xử lý **entry** 

   ```js
     entry: {
       bundle: "./src/index.js",
       vendor: LIBS
     },
       output: {
       path: path.resolve(__dirname, "./dist"),
       filename: "[name].js", // đổi tên out put để tạo thành 2 file linh động
       publicPath: "/"
     },
   ```

   