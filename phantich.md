# TÀI LIỆU TỔNG HỢP KIẾN THỨC REST API

## 1. Thiết kế URL trong REST

**Đúng hay sai?** REST yêu cầu dùng danh từ (số nhiều) cho đường dẫn (URL), không dùng động từ.

**Trả lời:** ĐÚNG

**Giải thích:** REST tập trung vào quản lý các tài nguyên (Resources) được biểu diễn dưới dạng danh từ. Các hành động tác động lên tài nguyên đó sẽ do phương thức HTTP (GET, POST, PUT, DELETE) đảm nhận, tránh đưa động từ vào cấu trúc URL.

**Ví dụ đúng:**
- GET /api/v1/students (Lấy danh sách sinh viên)
- POST /api/v1/students (Tạo mới sinh viên)

**Ví dụ sai:**
- POST /api/v1/getAllStudents (Đưa động từ vào URL)
- GET /api/v1/createStudent (Dùng GET để tạo mới)

---

## 2. Bảng tổng hợp các phương thức HTTP

| Method | Mục đích chính | Có body không? |
|--------|----------------|----------------|
| GET | Truy xuất/Đọc thông tin của một hoặc một tập hợp tài nguyên | Không |
| POST | Tạo mới một tài nguyên cấp dưới nằm trong một tập hợp gốc | Có |
| PUT | Cập nhật ghi đè thay thế toàn bộ thông tin tài nguyên, hoặc tạo mới nếu chưa tồn tại | Có |
| PATCH | Cập nhật cục bộ (chỉ chỉnh sửa một vài trường dữ liệu được chỉ định của tài nguyên) | Có |
| DELETE | Gỡ bỏ/Xóa hoàn toàn một tài nguyên cụ thể ra khỏi hệ thống | Không |

---

## 3. Phân biệt PUT và PATCH qua ví dụ nhỏ

Giả sử ban đầu có một sản phẩm: {"id": 1, "name": "Bút bi", "price": 5000}

| Phương thức | Kết quả | Giải thích |
|-------------|---------|-------------|
| PUT /products/1 với body {"name": "Bút mực"} | {"id": 1, "name": "Bút mực", "price": null} | PUT thay thế toàn bộ tài nguyên cũ. Thuộc tính không được gửi lên sẽ bị xóa hoặc đưa về giá trị mặc định |
| PATCH /products/1 với body {"name": "Bút mực"} | {"id": 1, "name": "Bút mực", "price": 5000} | PATCH chỉ cập nhật từng phần. Các thuộc tính không được chỉ định sẽ giữ nguyên giá trị cũ |

---

## 4. Bảng mã trạng thái HTTP (Status Codes)

| Mã | Ý nghĩa | Tình huống ví dụ |
|----|---------|------------------|
| 200 | OK: Yêu cầu đã được xử lý thành công và kết quả được trả về trong phần Body của Response | Người dùng gọi API xem thông tin cá nhân của chính mình thành công |
| 201 | Created: Yêu cầu thành công và một tài nguyên mới đã được tạo dựng thành công trên hệ thống | Khách hàng điền đầy đủ thông tin vào form đăng ký để tạo một tài khoản mới |
| 204 | No Content: Yêu cầu thành công nhưng máy chủ không cần gửi dữ liệu gì về trong phần Body | Hệ thống thực hiện lệnh xóa thành công một bản ghi dữ liệu sản phẩm lỗi |
| 400 | Bad Request: Lỗi phía Client do cú pháp không hợp lệ, truyền thiếu trường bắt buộc hoặc sai định dạng | Client gửi chữ vào trường yêu cầu số lượng (ví dụ: quantity: "hai" thay vì quantity: 2) |
| 404 | Not Found: Máy chủ không tìm thấy tài nguyên được yêu cầu tại đường dẫn URL chỉ định | Hệ thống tìm kiếm thông tin của một học sinh dựa trên mã ID không tồn tại |
| 500 | Internal Server Error: Máy chủ gặp lỗi bất ngờ không thể kiểm soát trong quá trình xử lý logic Backend | Đoạn mã nguồn xử lý phép tính bị dính lỗi chia cho số 0 hoặc cơ sở dữ liệu bị sập kết nối giữa chừng |