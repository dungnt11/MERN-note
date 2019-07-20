# URL Friendly 

Xử lý URL theo dạng tit-le-id

## Vấn đề

Bình thường khi tạo end point ta hay dùng kiểu

```javascript
route.get("/all/:id", controller.handle);
```

> Có thể lấy id thông qua req.params.id

Giờ ta lại muốn lấy id theo kiểu tieu-de-id thì phải dùng **regex** 

## Cách làm

```javascript
route.get(/^\/(.*?)-(\w{24})/, controller.handle);
```

```\w{24}``` chính là id được mongodb lưu vào db ( Dài 24 kí tự )

Lấy ra **id** 	```req.params[1]``` còn ```req.params[0]``` là title truyền vào

## Xử lý ở client

Nhận route giống với server

```javascript
<Route
    path={/^\/(.*?)-(\w{24})/}
    component={() => <div>xin chao</div>}
    />
```



## Tạo slug tự động

Tham khảo [freetut](https://freetuts.net/tao-slug-tu-dong-bang-javascript-va-php-199.html) 

```javascript
function ChangeToSlug(title)
{
 
    //Đổi chữ hoa thành chữ thường
    slug = title.toLowerCase();
 
    //Đổi ký tự có dấu thành không dấu
    slug = slug.replace(/á|à|ả|ạ|ã|ă|ắ|ằ|ẳ|ẵ|ặ|â|ấ|ầ|ẩ|ẫ|ậ/gi, 'a');
    slug = slug.replace(/é|è|ẻ|ẽ|ẹ|ê|ế|ề|ể|ễ|ệ/gi, 'e');
    slug = slug.replace(/i|í|ì|ỉ|ĩ|ị/gi, 'i');
    slug = slug.replace(/ó|ò|ỏ|õ|ọ|ô|ố|ồ|ổ|ỗ|ộ|ơ|ớ|ờ|ở|ỡ|ợ/gi, 'o');
    slug = slug.replace(/ú|ù|ủ|ũ|ụ|ư|ứ|ừ|ử|ữ|ự/gi, 'u');
    slug = slug.replace(/ý|ỳ|ỷ|ỹ|ỵ/gi, 'y');
    slug = slug.replace(/đ/gi, 'd');
    //Xóa các ký tự đặt biệt
    slug = slug.replace(/\`|\~|\!|\@|\#|\||\$|\%|\^|\&|\*|\(|\)|\+|\=|\,|\.|\/|\?|\>|\<|\'|\"|\:|\;|_/gi, '');
    //Đổi khoảng trắng thành ký tự gạch ngang
    slug = slug.replace(/ /gi, "-");
    //Đổi nhiều ký tự gạch ngang liên tiếp thành 1 ký tự gạch ngang
    //Phòng trường hợp người nhập vào quá nhiều ký tự trắng
    slug = slug.replace(/\-\-\-\-\-/gi, '-');
    slug = slug.replace(/\-\-\-\-/gi, '-');
    slug = slug.replace(/\-\-\-/gi, '-');
    slug = slug.replace(/\-\-/gi, '-');
    //Xóa các ký tự gạch ngang ở đầu và cuối
    slug = '@' + slug + '@';
    slug = slug.replace(/\@\-|\-\@|\@/gi, '');
    
    return slug;
}
```

> Nếu bị cảnh cáo lỗi 

```javascript
createURLFriendly = title => {
    let slug = "";
    //Đổi chữ hoa thành chữ thường
    slug = title.toLowerCase(); //Đổi ký tự có dấu thành không dấu
    slug = slug.replace(/á|à|ả|ạ|ã|ă|ắ|ằ|ẳ|ẵ|ặ|â|ấ|ầ|ẩ|ẫ|ậ/gi, "a");
    slug = slug.replace(/é|è|ẻ|ẽ|ẹ|ê|ế|ề|ể|ễ|ệ/gi, "e");
    slug = slug.replace(/i|í|ì|ỉ|ĩ|ị/gi, "i");
    slug = slug.replace(/ó|ò|ỏ|õ|ọ|ô|ố|ồ|ổ|ỗ|ộ|ơ|ớ|ờ|ở|ỡ|ợ/gi, "o");
    slug = slug.replace(/ú|ù|ủ|ũ|ụ|ư|ứ|ừ|ử|ữ|ự/gi, "u");
    slug = slug.replace(/ý|ỳ|ỷ|ỹ|ỵ/gi, "y");
    slug = slug.replace(/đ/gi, "d"); //Xóa các ký tự đặt biệt
    slug = slug.replace(
      /`|~|!|@|#|\||\$|%|\^|&|\*|\(|\)|\+|=|,|\.|\/|\?|>|<|'|"|:|;|_/gi,
      ""
    ); //Đổi khoảng trắng thành ký tự gạch ngang
    slug = slug.replace(/ /gi, "-"); //Đổi nhiều ký tự gạch ngang liên tiếp thành 1 ký tự gạch ngang //Phòng trường hợp người nhập vào quá nhiều ký tự trắng
    slug = slug.replace(/-----/gi, "-");
    slug = slug.replace(/----/gi, "-");
    slug = slug.replace(/---/gi, "-");
    slug = slug.replace(/--/gi, "-"); //Xóa các ký tự gạch ngang ở đầu và cuối
    slug = "@" + slug + "@";
    slug = slug.replace(/@-|-@|@/gi, "");
    return slug + "-";
  };
```

