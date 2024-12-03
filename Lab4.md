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
## 3. Use-Case : Run Payroll
### a. Tên : Run Payroll
### b. Mô tả ngắn gọn : 
- Ca sử dụng Run Payroll được thực hiện để tính toán và xử lý bảng lương của nhân viên theo chu kỳ thanh toán định kỳ. Hệ thống thực hiện các bước để lấy thông tin bảng chấm công, tính toán lương, và tạo giao dịch thanh toán qua hệ thống ngân hàng hoặc in phiếu lương.
### c. Tác nhân :
- System Clock (Đồng hồ hệ thống): Kích hoạt việc chạy bảng lương đúng vào ngày trả lương.
- Payroll Controller (Bộ điều khiển bảng lương): Điều phối toàn bộ quy trình xử lý bảng lương.
- Employee (Nhân viên): Cung cấp thông tin chấm công và đơn đặt hàng nếu cần.
- Timecard (Thẻ chấm công): Chứa thông tin về giờ làm việc của nhân viên.
- Purchase Order (Đơn đặt hàng): Lưu trữ thông tin đơn hàng cho nhân viên làm việc theo hoa hồng.
- Paycheck (Phiếu lương): Lưu trữ thông tin phiếu lương đã được tạo.
- Printer Interface (Giao diện máy in): In phiếu lương cho nhân viên.
- Bank System (Hệ thống ngân hàng): Xử lý giao dịch chuyển khoản thanh toán lương.
### d. Luồng sự kiện :
- Luồng cơ bản:
  + System Clock khởi động ca sử dụng Run Payroll đúng ngày trả lương.
  + Payroll Controller bắt đầu chạy bảng lương:
    - Kiểm tra xem có phải ngày trả lương không.
    - Lấy thông tin lương của nhân viên từ Timecard và Purchase Order.
    - Tính toán số tiền lương phải trả.
    - Tạo đối tượng phiếu lương (Paycheck) với số tiền đã tính.
   
  + Payroll Controller kiểm tra phương thức thanh toán:
    - Nếu nhân viên nhận lương qua ngân hàng, hệ thống sẽ lấy thông tin ngân hàng và gửi giao dịch thanh toán đến Bank System.
    - Nếu nhân viên nhận lương qua phiếu lương, hệ thống sẽ gửi lệnh in phiếu lương qua Printer Interface để in phiếu.
   
- Luồng phụ :
  + Nếu ngày chạy bảng lương không phải ngày trả lương, hệ thống không thực hiện các bước tiếp theo.
  + Nếu không tìm thấy thông tin nhân viên hoặc thẻ chấm công, quá trình chạy bảng lương sẽ bị hủy và báo lỗi.
 
### e. Pre-Conditions:
- Hệ thống phải xác định đúng ngày trả lương theo lịch trình đã định trong hệ thống.
- Dữ liệu chấm công của tất cả nhân viên phải có sẵn trong cơ sở dữ liệu.
- Thông tin nhân viên đầy đủ bao gồm:
  + Thông tin thẻ chấm công (Timecard).
  + Thông tin đơn đặt hàng (Purchase Order) (đối với nhân viên hưởng hoa hồng).
  + Phương thức thanh toán (in phiếu lương hoặc chuyển khoản ngân hàng).
 
- Hệ thống ngân hàng phải sẵn sàng và kết nối để thực hiện giao dịch chuyển khoản nếu cần.
- Máy in hoạt động và kết nối với hệ thống để in phiếu lương cho nhân viên nhận phiếu giấy.
### f. Post-Conditions:
- Lương của tất cả nhân viên đã được tính toán và xử lý thành công.
- Phiếu lương (Paycheck) được tạo cho từng nhân viên với số tiền chính xác.
- Thanh toán lương được gửi thành công:
  + Giao dịch chuyển khoản được gửi đến hệ thống ngân hàng cho nhân viên nhận lương qua tài khoản ngân hàng.
  + Phiếu lương được in thông qua PrinterInterface cho nhân viên nhận lương bằng phiếu.
 
- Thông báo thành công hoặc lỗi được ghi nhận trong hệ thống, nếu xảy ra sự cố trong quá trình tính toán hoặc giao dịch.
- Dữ liệu bảng lương được cập nhật trong cơ sở dữ liệu để lưu lại các giao dịch đã thực hiện.
   

  








