# Thiết kế các ca sử dụng cho hệ thống "Payroll System":
## 1. Use Case : Login
### a. Tên : Login
### b. Mô tả ngắn gọn : Cho phép người dùng nhập thông tin tên đăng nhập và mật khẩu để truy cập vào hệ thống.
### c. Tác nhân chính: Any User (Bất kỳ người dùng nào muốn đăng nhập vào hệ thống)
### d. Luồng sự kiện (Flow of Events): 
- Luồng chính (Basic Flow):
  + Người dùng mở giao diện đăng nhập (LoginForm).
  + Hệ thống yêu cầu người dùng nhập tên đăng nhập và mật khẩu.
  + Người dùng nhập tên đăng nhập và mật khẩu vào form đăng nhập.
  + Hệ thống gửi thông tin tới chức năng xác thực (validate username and password).
  + Hệ thống kiểm tra thông tin đăng nhập.
    - Nếu thông tin hợp lệ:
      + Hệ thống cho phép người dùng truy cập vào hệ thống.
     
    - Nếu thông tin không hợp lệ:
      + Hệ thống hiển thị thông báo lỗi và yêu cầu người dùng nhập lại thông tin.
- Luồng phụ (Alternative Flows):
  + Luồng phụ 1: Thông tin không hợp lệ:
    - Nếu người dùng nhập sai tên đăng nhập hoặc mật khẩu, hệ thống sẽ hiển thị thông báo lỗi "Invalid username or password."
    - Người dùng có thể chọn nhập lại thông tin hoặc thoát khỏi giao diện đăng nhập.
### e. Điều kiện tiên quyết (Pre-Conditions):
- Người dùng cần phải có tài khoản hợp lệ trên hệ thống.
- Giao diện đăng nhập (LoginForm) phải được hiển thị.
### f. Điều kiện sau (Post-onditions):
- Nếu đăng nhập thành công, người dùng sẽ được chuyển đến màn hình chính của hệ thống.
- Nếu đăng nhập thất bại, hệ thống sẽ yêu cầu nhập lại thông tin hoặc hủy thao tác đăng nhập.
### g. Mối quan hệ giữa các lớp (Class Interactions):
- Any User: Tác nhân khởi tạo quy trình đăng nhập và nhập thông tin đăng nhập.
- LoginForm (Giao diện đăng nhập):
  + Nhận thông tin từ người dùng.
  + Hiển thị thông báo nếu thông tin đăng nhập không hợp lệ.
  + Gửi yêu cầu xác thực thông tin tới hệ thống.
 
- Authentication (Hệ thống xác thực):
  + Nhận thông tin đăng nhập từ giao diện LoginForm.
  + Kiểm tra tính hợp lệ của thông tin đăng nhập (username và password).
  + Trả về kết quả xác thực cho giao diện LoginForm.
## 2. Use Case : Maintain Timecard
### a. Tên : Maintain Timecard
### b. Mô tả ngắn gọn : 
- Ca sử dụng này cho phép Nhân viên duy trì (tạo mới, cập nhật và lưu) các bản ghi thời gian làm việc của họ cho mục đích quản lý dự án và tính toán chi phí. Hệ thống đảm bảo rằng mỗi mục nhập thẻ chấm công đều được liên kết với các mã chi phí hợp lệ và được lưu trữ để xử lý sau.
### c. Tác nhân (Actors):
- Nhân viên: Tác nhân chính, người tương tác với hệ thống để duy trì thẻ chấm công.
- Cơ sở dữ liệu Quản lý Dự án (Project Management Database): Hệ thống bên ngoài cung cấp mã chi phí để xác thực.
- Bộ điều khiển Thẻ chấm công (TimecardController): Quản lý tương tác giữa giao diện nhập liệu và hệ thống backend.
### d. Luồng sự kiện: 
- Luồng cơ bản:
  + Ca sử dụng bắt đầu khi Nhân viên chọn duy trì thẻ chấm công.
  + Hệ thống truy xuất thẻ chấm công hiện tại của Nhân viên: Nếu không tìm thấy thẻ chấm công, hệ thống sẽ tạo một thẻ mới.
  + Hệ thống hiển thị biểu mẫu thẻ chấm công, cho thấy các mục nhập hiện tại và mã chi phí.
  + Nhân viên nhập hoặc cập nhật số giờ làm việc và mã chi phí cho dự án tương ứng.
  + Hệ thống xác thực các mã chi phí đã nhập với Cơ sở dữ liệu Quản lý Dự á: Nếu mã chi phí không hợp lệ, hệ thống sẽ hiển thị thông báo lỗi và yêu cầu Nhân viên chỉnh sửa.
  + Sau khi xác thực thành công, Nhân viên lưu thẻ chấm công.
  + Hệ thống cập nhật và lưu trữ thẻ chấm công vào cơ sở dữ liệu.
 
- Luồng phụ:
  + Mã Chi Phí Không Hợp Lệ (Invalid Charge Code):
    - Nếu mã chi phí do Nhân viên nhập không hợp lệ, hệ thống sẽ hiển thị thông báo lỗi.
    - Nhân viên phải nhập lại mã chi phí hợp lệ hoặc chọn từ danh sách mã chi phí đã được cung cấp.
   
  + Không Tồn Tại Thẻ Chấm Công (No Timecard Exists):
    - Nếu không tồn tại thẻ chấm công cho Nhân viên, một thẻ mới sẽ được tạo tự động trong luồng sự kiện.
### e. Pre-Conditions:
- Nhân viên phải đăng nhập vào hệ thống trước khi duy trì thẻ chấm công.
### f. Post-Conditions:
- Nếu ca sử dụng thành công, thẻ chấm công của Nhân viên được cập nhật hoặc tạo mới trong hệ thống.
- Nếu ca sử dụng thất bại, trạng thái của hệ thống không thay đổi và Nhân viên có thể thử lại.
  








