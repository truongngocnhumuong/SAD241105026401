# Các hệ thống con trong hệ thống Payroll System
## 1. Hệ thống con từ use-case Login:
### a. Mô hình class Diagram:
- Lớp 1: User
  + Thuộc tính :
    - username: String
    - password: String
    - userRole: String (vai trò của người dùng, ví dụ: admin, user, etc.)
   
  + Phương thức:
    - validateCredentials(username, password): Boolean
   
- Lớp 2: LoginManager
  + Thuộc tính:
    - attempts: int (số lần đăng nhập sai)
   
  + Phương thức:
    - authenticate(username, password): Boolean (xác thực người dùng)
    - lockAccount(username): void (khóa tài khoản sau nhiều lần thất bại)
   
- Lớp 3: Database
  + Phương thức:
    - getUser(username): User (truy xuất thông tin tài khoản từ cơ sở dữ liệu)
    - updateLoginAttempts(username, attempts): void
   
- Lớp 4: LoginForm
  + Thuộc tính:
    - inputUsername: String
    - inputPassword: String
   
  + Phương thức:
    - submit(): void (gửi thông tin đăng nhập)
    - displayErrorMessage(message: String): void
### b. Sequence Diagram:
- Người dùng nhập username và password vào LoginForm.
- LoginForm gửi thông tin đến LoginManager qua phương thức authenticate(username, password).
- LoginManager gọi Database để lấy thông tin người dùng qua getUser(username).
- Database trả về thông tin người dùng (hoặc null nếu không tồn tại).
- LoginManager kiểm tra thông tin:
  + Nếu hợp lệ: Trả về kết quả success và chuyển người dùng đến màn hình chính.
  + Nếu không hợp lệ: Tăng số lần thất bại, cập nhật vào Database, và trả về lỗi.
### c. Activity Diagram: Biểu diễn quy trình đăng nhập
- Hiển thị giao diện đăng nhập.
- Người dùng nhập tên đăng nhập và mật khẩu.
- Kiểm tra:
  + Nếu thông tin hợp lệ, cho phép truy cập hệ thống.
  + Nếu không hợp lệ, hiển thị thông báo lỗi.
 
- Nếu quá số lần đăng nhập sai, khóa tài khoản.
### d. Mô tả hệ thống con: Hệ thống con sẽ bao gồm
- Module giao diện người dùng: Giao diện đăng nhập (LoginForm) và các thông báo lỗi.
- Module xử lý logic:
  + Kiểm tra thông tin đăng nhập.
  + Quản lý trạng thái tài khoản.
 
- Module cơ sở dữ liệu:
  + Lưu trữ thông tin người dùng.
  + Theo dõi số lần đăng nhập thất bại.
### e. Các bước thiết kế chi tiết
## 2. Hệ thống con từ use-case Login:
### a. Mô hình class Diagram:
### b. Sequence Diagram
### c. Activity Diagram
### d. Mô tả hệ thống con
### e. Các bước thiết kế chi tiết
## 3. Hệ thống con từ use-case Login:
### a. Mô hình class Diagram:
### b. Sequence Diagram
### c. Activity Diagram
### d. Mô tả hệ thống con
### e. Các bước thiết kế chi tiết
## 4. Hệ thống con từ use-case Login:
### a. Mô hình class Diagram:
### b. Sequence Diagram
### c. Activity Diagram
### d. Mô tả hệ thống con
### e. Các bước thiết kế chi tiết
## 5. Hệ thống con từ use-case Login:
### a. Mô hình class Diagram:
### b. Sequence Diagram
### c. Activity Diagram
### d. Mô tả hệ thống con
### e. Các bước thiết kế chi tiết

