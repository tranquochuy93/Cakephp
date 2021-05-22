### convention
 #### isset vs empty vs is_null
 - isset: trả về true khi giá trị của biến KHÁC NULL
 - empty: kiểm tra biến có bị rỗng hay không, trả về true nếu giá trị là: NULL, '0', '0', [], false, ''
 - is_null: trả về true nếu giá trị của biến là NULL
 
| Value of variable ($var)	| isset($var)	| empty($var)	| is_null($var) |
|--------------|-------|--------------|--------------|
| “” (an empty string) | 	bool(true) | 	bool(true)	| |
| ” ” (space) |	bool(true) |	 	 
| FALSE	| bool(true)	| bool(true)	 
| TRUE	| bool(true)	 	 
| array() | (an empty array)	| bool(true)	 
| NULL	|	bool(true)	| bool(true)| bool(true)	
| “0″ (0 as a string)	| bool(true) |	bool(true)	 
| 0 (0 as an integer)	| bool(true)	| bool(true)	 
| 0.0 (0 as a float)	| bool(true)	| bool(true)	 
| var $var; (a variable declared, but without a value)	| bool(true)	| bool(true)
| NULL byte (“\ 0″)	 | bool(true)	 	 
 
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

### SSE(server side event) vs socket
| SSE	| Socket |
|--------------|-------|
| a one-way communication between the Server to Browser. SSE connections can only push data to the browser. | 	a two-way communication between the Server and Browser, Websockets connections can both send data to the browser and receive data from the browser |
|suffers from a limitation to the maximum number of open connections | |	 	 
|Use EventSource API Javascript||


### Regular HTTP
Người dùng gửi yêu cầu (request) 1 website từ một máy chủ.
Máy chủ (server) tính toán dữ liệu trả về ( response ).
Máy chủ gửi dữ liệu trả về (response) cho người dùng (client).

Client chủ động gửi request đến server thì sẽ có response trả về cho client, còn nếu ko có request từ client thì server sẽ không làm gì cả.

### AJAX Polling
Client yêu cầu 1 trang web từ server sử dụng “Regular http” (đã nói ở trên).
Trang web mà client vừa yêu cầu sẽ dùng javascript thực hiện request liên tục đến 1 file trên server trong một khoảng thời gian đều đặn (ví dụ: cứ mỗi 2 giây sẽ gửi 1 request đến server).
Server sẽ tính toán response ứng với mỗi request và gửi lại response cho client giống như giao thức http truyền thống.
~> Client không chủ động gửi request đến server nhưng javascript của website vẫn luân phiên gửi request đến server và client sẽ nhận response từ server 1 cách bị động.

### AJAX Long-Polling
Client yêu cầu 1 trang web từ server sử dụng “Regular http” (đã nói ở trên).
Trang web mà client vừa yêu cầu sẽ dùng javascript thực hiện request đến 1 file trên server.
Server sẽ không gửi response ngay cho client (ứng với request đã gửi) mà sẽ đợi cho đến khi có dữ liệu mới.
Khi có dữ liệu mới, server sẽ gửi dữ liệu mới đó (response) về cho client.
Client sau khi nhận dữ liệu mới từ server, ngay lập tức sẽ tiếp tục 1 request khác đến server để bắt đầu lại toàn bộ tiến trình này (bước 3 đến 5).
~> Client sẽ gửi request đến server, server tiến hành kiếm tra dữ liệu và đến khi nào có dữ liệu mới thì mới gửi response về cho client. Sau đó client lại tiếp tục tự động gửi 1 request mới và đợi dữ liệu mới trả về.

### HTML5 Server Sent Events (SSE) / Event Source
Client yêu cầu 1 trang web từ server sử dụng “Regular http” (đã nói ở trên).
Trang web mà client vừa yêu cầu sẽ dùng javascript mở 1 kết nối đến server.
Kể từ lúc này server sẽ gửi response trả về cho client mỗi khi có dữ liệu mới.
~> Tức là client luôn nhận dữ liệu mới theo thời gian thực từ server chỉ với 1 lần request (dữ liệu 1 chiều từ server đến client). Lúc này trên server sẽ thực hiện 1 vòng lặp (loop) sự kiện (bước 1 đến 3) để thực hiện lại nhiều lần quy trình này, tuy nhiên bạn không thể kết nối đến server từ 1 tên miền (domain) khác.

### Streaming
hình thức nó giống với kỹ thuật long-polling nhưng khác là ta chỉ khởi tạo kết nối đến server một lần và gửi nhận dữ liệu thông qua kết nối này chứ không tạo kết nối mới. ( kỹ thuật streaming trên thực tế có thể được ứng dụng để làm web xem phim trực truyến, tải tới đâu coi tới đó và chỉ request đến file phim đúng 1 lần).

### HTML5 Websockets:
Client yêu cầu 1 trang web từ server sử dụng “Regular http” (đã nói ở trên).
Trang web mà client vừa yêu cầu sẽ dùng javascript mở 1 kết nối đến server.
Bây giờ cả server và client có thể gửi nhận nhiều dữ liệu khác nhau với nhau khi có dữ liệu mới (giống như kiểu 2 bên đang chat với nhau chứ không phải tuân theo qui tắc nào).
~> Tức là client và server luôn nhận dữ liệu mới theo thời gian thực (2 chiều: server đến client hoặc client đến server). Lúc này trên server sẽ thực hiện 1 vòng lặp (loop) sự kiện (bước 1 đến 3) để thực hiện lại nhiều lần quy trình này và bạn có thể kết nối đến server từ 1 tên miền (domain) khác. Ngoài ra bạn cũng có thể sử dụng websocket server của bên thứ 3 cung cấp (ví dụ: http://pusher.com/) và việc còn lại là bạn chỉ việc code trên client ( dễ dàng hơn nhiều vì trước đó bạn phải code cả phía server và client).

