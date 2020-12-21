### convention
 #### isset vs empty
   - isset()
     - return TRUE if a variable has a value ,  
       ```diff 
       + including (False, 0 or empty string)
       - not NULL
       ```
     - FALSE otherwise
   - empty()
     - return TRUE if a variable has 
       ```diff 
       + empty value, empty string, 0, NULL or False
       ```
     - FALSE otherwise
 
 #### API
   - URL: must be separate by dashes. Example: /pick-items/registration.json => controller: PickItemsController.php
   - Status code:
     ```diff
     + 200 => ‘Success’,
     - 400 => ‘Bad Request’,
     - 500 => ‘Internal Server Error’,
     ```
   - Phương thức HTTP(CRUD):
     - GET: được sử dụng để lấy thông tin từ server theo URI đã cung cấp.
     - HEAD: giống với GET nhưng response trả về không có body, chỉ có header.
     - POST: gửi thông tin tới sever thông qua các biểu mẫu http.
     - PUT: ghi đè tất cả thông tin của đối tượng với những gì được gửi lên.
     - PATCH: ghi đè các thông tin được thay đổi của đối tượng.
     - DELETE: xóa tài nguyên trên server.
     - CONNECT: thiết lập một kết nối tới server theo URI.
     - OPTIONS: mô tả các tùy chọn giao tiếp cho resource.
     - TRACE: thực hiện một bài test loop – back theo đường dẫn đến resource.
   - Authentication:
     - OAuth2: Open với Authentication hoặc Authorization
       - Authentication: xác thực người dùng
       - Authorization: người dùng ủy quyền cho ứng dụng truy cập tài nguyên của họ
       - Cách hoạt động
          - đăng nhập bằng Facebook hay Gmail -> website sẽ dẫn bạn đến Facebook hay Gmail -> yêu cầu đăng nhập -> Facebook sẽ phát cho website một cái token Token này chứa một số quyền hạn nhất định giúp cho website có thể xác minh bạn là ai cũng như giúp cho website có thể hoạt động được
         
     - JWT
