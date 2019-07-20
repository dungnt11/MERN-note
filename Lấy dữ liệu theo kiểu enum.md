# Truy vấn enum *mongoose*

```javascript
var mongoose = require('./index')
  , TempSchema = new mongoose.Schema({
      salutation: {type: String, enum: ['Mr.', 'Mrs.', 'Ms.']}
    }); 

var Temp = mongoose.model('Temp', TempSchema);

console.log(Temp.schema.path('salutation').enumValues);
var temp = new Temp();
console.log(temp.schema.path('salutation').enumValues);
```

