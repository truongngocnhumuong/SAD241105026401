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
   
### b. Sequence Diagram
### c. Activity Diagram
### d. Mô tả hệ thống con
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

