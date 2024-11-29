# Thiết kế các ca sử dụng cho hệ thống "Payroll System":
## 1. Use Case : Login
### a. Tên : Login
### b. Mô tả ngắn gọn : Cho phép người dùng nhập thông tin tên đăng nhập và mật khẩu để truy cập vào hệ thống.
### c. Tác nhân chính: Any User (Bất kỳ người dùng nào muốn đăng nhập vào hệ thống)
### d. Dòng sự kiện (Flow of Events): 
- Dòng chính (Basic Flow):
  + Người dùng mở giao diện đăng nhập (LoginForm).
  + Hệ thống yêu cầu người dùng nhập tên đăng nhập và mật khẩu.
  + Người dùng nhập tên đăng nhập và mật khẩu vào form đăng nhập.
  + Hệ thống gửi thông tin tới chức năng xác thực (validate username and password).
  + Hệ thống kiểm tra thông tin đăng nhập.
    - Nếu thông tin hợp lệ:
      + Hệ thống cho phép người dùng truy cập vào hệ thống.
     
    - Nếu thông tin không hợp lệ:
      + Hệ thống hiển thị thông báo lỗi và yêu cầu người dùng nhập lại thông tin.
### e. Dòng phụ (Alternative Flows):
- Dòng phụ 1: Thông tin không hợp lệ:
  + Nếu người dùng nhập sai tên đăng nhập hoặc mật khẩu, hệ thống sẽ hiển thị thông báo lỗi "Invalid username or password."
  + Người dùng có thể chọn nhập lại thông tin hoặc thoát khỏi giao diện đăng nhập.
### f.Điều kiện tiên quyết (Preconditions):
- Người dùng cần phải có tài khoản hợp lệ trên hệ thống.
- Giao diện đăng nhập (LoginForm) phải được hiển thị.
### g. Điều kiện sau (Postconditions):
- Nếu đăng nhập thành công, người dùng sẽ được chuyển đến màn hình chính của hệ thống.
- Nếu đăng nhập thất bại, hệ thống sẽ yêu cầu nhập lại thông tin hoặc hủy thao tác đăng nhập.
### h. Mối quan hệ giữa các lớp (Class Interactions):
- Any User: Tác nhân khởi tạo quy trình đăng nhập và nhập thông tin đăng nhập.
- LoginForm (Giao diện đăng nhập):
  + Nhận thông tin từ người dùng.
  + Hiển thị thông báo nếu thông tin đăng nhập không hợp lệ.
  + Gửi yêu cầu xác thực thông tin tới hệ thống.
 
- Authentication (Hệ thống xác thực):
  + Nhận thông tin đăng nhập từ giao diện LoginForm.
  + Kiểm tra tính hợp lệ của thông tin đăng nhập (username và password).
  + Trả về kết quả xác thực cho giao diện LoginForm.
