# Loại bỏ feild khi query mongoose

Giả sử có trường dữ liệu

```javascript
var userSchema = mongoose.Schema({
  email: {
    type: String,
    required: true,
    unique: true,
  },
  password: {
    type: String,
    required: true,
  },
});

var User = mongoose.model("User", userSchema);
```

Bạn không muốn show password khi người dùng findOne

Có 2 cách

### Individually

```
User.findOne({_id: userId}).select("-password")
```

### In the Schema

```
var userSchema = mongoose.Schema({
  email: {
    type: String,
    required: true,
    unique: true,
  },
  password: {
    type: String,
    required: true,
    select: false,
  },
});
```

