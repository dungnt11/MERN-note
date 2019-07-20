#  Sử dụng Jodit Editor và việc upload file

Khi làm việc với **WYSIWYG editor** có rất nhiều lựa chọn, ví dụ [github](<https://github.com/JefMari/awesome-wysiwyg#for-react>) . Sau khi nghiên cứu ta sẽ sử dụng thằng **[Jodit Editor 3](<https://xdsoft.net/jodit/doc/>)** 

## Tại sao lại sử dụng Jodit Editor

Ta đang cần một editor có thể chỉnh sửa dữ liệu && upload ảnh. Jodit Editor cung cấp cho chúng ta rất tốt về việc này. Về việc text thì ez rồi, còn upload ảnh có ta có 2 lựa chọn

- Upload lên trực tiếp server của mình, thông qua multer
- Upload lên server qua api thằng khác ( **POST** multipart/form-data )

## Cách sử dụng 

1. Install

   ```
   npm install jodit
   ```

2. Component ( React )

   ```javascript
   import React, { Component } from "react";
   
   import "jodit";
   import "jodit/build/jodit.min.css";
   import JoditEditor from "jodit-react";
   
   export default class EdittorComponent extends Component {
     constructor(props) {
       super(props);
       this.state = {
         content: ""
       };
     }
   
     updateContent = value => {
       this.setState({ content: value });
     };
   
     jodit;
     setRef = jodit => (this.jodit = jodit);
   
     config = {
       uploader: {
         url: "/upload",
         filesVariableName: "images", // ten file multer.eny('<-- ten file here -->')
         pathVariableName: "path",
         headers: {
           authorization: JSON.parse(localStorage.getItem("jwt")).token
         }
         prepareData: function(data) {
           return data;
         },
         isSuccess: function(resp) {
           return !resp.error;
         },
         process: function(resp) {
           /**
            * resp : response tra ve tu server 
            * {
               msg: "File was uploaded",
               error: 0,
               images: ["/url_image.png"]
             }
            */
           return {
             files: resp[this.options.filesVariableName] || [],
             baseurl: "http://localhost:8080/public/uploads/",
             error: resp.error,
             msg: resp.msg
           };
         },
         error: function(e) {
           console.log(e);
         }
       }
     };
     render() {
       return (
         <JoditEditor
           editorRef={this.setRef}
           value={this.state.content}
           config={this.config}
           onChange={this.updateContent}
         />
       );
     }
}
   
   ```
   
   



3. Cấu hình bên phía server

   ```javascript
   router.post("/upload", upload.any("images", 12), (req, res) => {
     console.log(req.files);
     res.json({
       msg: "File was uploaded",
       error: 0,
       images: ["/975fd98b-f4e5-4cd9-b085-1661ad7ce8f8.png"]
     });
   });
   ```

   

***

### Xem thêm

[DOC](<https://xdsoft.net/jodit/v.2/doc/tutorial-uploader-settings.html>)

