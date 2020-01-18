# Setup
Có 2 cái mà ta cần quan tâm là ```connect``` và ```createConnection```, hiểu nôm na thì ```connect``` cho phép ta kết nối tới 1 database còn ```createConnection``` cho phép ta kết nối tới nhiều DB 1 lúc
1. ```mongoose.connect(url, { useNewUrlParser: true });```
> Xem chi tiết các model ```mongoose.modelNames()```
2. ```const test = await mongoose.createConnection(urlTest, { useNewUrlParser: true })```
> Để truy vấn tới model 1 là cần file model -> bắt buộc phải require vào
> 2 là tạo tên model mới như sau ```mongoose.model('TênModel', new mongoose.Schema())```
> Khi đó: truy vấn như sau ```const test = await conn1.model('TênModel', 'orders').find();```
> model([Tên model], [Tên Collection])