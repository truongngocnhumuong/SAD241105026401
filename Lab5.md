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
### e. Các bước thiết kế chi tiết:
- Phân tách giao diện: Xây dựng LoginForm với các trường username và password, cùng nút Login
- Xử lý logic đăng nhập : Triển khai LoginManager để quản lý xác thực và khóa tài khoản.
- Kết nối cở sở dữ liệu: Xây dựng các hàm tương tác cơ sở dữ liệu như getUser() và updateLoginAttempts().
## 2. Hệ thống con từ use-case Maintain Timecard:
### a. Mô hình class Diagram:
- Lớp 1: Employee
  + Thuộc tính:
    - employeeID: String
    - name: String
    - timecards: List<Timecard> (Danh sách các thẻ chấm công của nhân viên)
   
  + Phương thức:
    - getCurrentTimecard(): Timecard (Lấy thẻ chấm công hiện tại của nhân viên)
    - createNewTimecard(): Timecard (Tạo thẻ chấm công mới)
   
- Lớp 2: Timecard
  + Thuộc tính:
    - timecardID: String
    - date: Date
    - entries: List<TimeEntry> (Danh sách các mục ghi chép thời gian)
   
  + Phương thức:
    - addEntry(entry: TimeEntry): void (Thêm một mục mới vào thẻ chấm công)
    - validateEntries(): Boolean (Kiểm tra tính hợp lệ của các mục)
   
- Lớp 3: TimeEntry:
  + Thuộc tính:
    - projectCode: String (Mã chi phí dự án)
    - hoursWorked: Double (Số giờ làm việc)
   
  + Phươngg thức: isValid(projectDatabase: ProjectManagementDatabase): Boolean (Kiểm tra mã chi phí có hợp lệ hay không)
 
- Lớp 4: TimecardController
  + Thuộc tính: employee: Employee
  + Phương thức:
    - loadTimecard(employeeID: String): Timecard (Tải thẻ chấm công hiện tại hoặc tạo mới)
    - saveTimecard(timecard: Timecard): Boolean (Lưu thẻ chấm công)
    - validateChargeCode(code: String): Boolean (Kiểm tra mã chi phí)
   
- lớp 5: ProjectManagementDatabase
  + Phương thức: isChargeCodeValid(code: String): Boolean (Xác thực mã chi phí)
### b. Sequence Diagram:
- Nhân viên đăng nhập và truy cập giao diện thẻ chấm công.
- TimecardController kiểm tra xem thẻ chấm công có tồn tại không:
  + Nếu không, tạo mới.
  + Nếu có, tải dữ liệu từ cơ sở dữ liệu.
- Nhân viên nhập thông tin (hoursWorked và projectCode) vào thẻ chấm công.
- Timecard gọi TimeEntry để xác thực từng mục:
  + Dữ liệu được xác thực với ProjectManagementDatabase.
  + Nếu lỗi, hiển thị thông báo và yêu cầu sửa.
- Sau khi xác thực thành công, TimecardController lưu thẻ chấm công vào cơ sở dữ liệu.
### c. Activity Diagram:
- Hiển thị giao diện thẻ chấm công.
- Kiểm tra thẻ chấm công hiện tại: Nếu không tồn tại, tạo mới.
- Nhân viên thêm hoặc sửa thông tin.
- Xác thực dữ liệu:
  + Nếu hợp lệ, lưu thẻ chấm công.
  + Nếu không hợp lệ, hiển thị lỗi và yêu cầu chỉnh sửa.
- Lưu thẻ chấm công vào cơ sở dữ liệu.
### d. Mô tả hệ thống con:
- Module giao diện người dùng:
  + Biểu mẫu nhập liệu cho thẻ chấm công.
  + Hiển thị danh sách mã chi phí hợp lệ.
 
- Module xử lý logic: Quản lý thẻ chấm công và xác thực mã chi phí.
- Module cơ sở dữ liệu:
  + Lưu trữ và truy xuất thông tin thẻ chấm công.
  + Xác thực mã chi phí từ cơ sở dữ liệu dự án.
### e. Các bước thiết kế chi tiết:
- Tạo lớp dữ liệu: Lớp Timecard, TimeEntry, và Employee để quản lý dữ liệu.
- Xây dựng bộ điều khiển: TimecardController để xử lý các thao tác từ giao diện và logic backend.
- Kết nối cơ sở dữ liệu: Kết nối với ProjectManagementDatabase để xác thực mã chi phí.
- Phát triển giao diện người dùng: Giao diện nhập liệu thân thiện với người dùng và dễ dàng hiển thị lỗi.
## 3. Hệ thống con từ use-case Run Payroll:
### a. Mô hình class Diagram:
- Lớp 1: PayrollController
  + Thuộc tính: payrollDate: Date (Ngày trả lương hiện tại)
  + Phương thức:
    - runPayroll(): void (Khởi chạy quy trình bảng lương)
    - calculatePay(employee: Employee): double (Tính toán tiền lương cho nhân viên)
    - generatePaycheck(employee: Employee, amount: double): Paycheck (Tạo phiếu lương)
    - processPayment(employee: Employee, paycheck: Paycheck): void (Xử lý thanh toán)
- Lớp 2: Employee
  + Thuộc tính:
    - employeeID: String
    - name: String
    - paymentMethod: String (Phương thức thanh toán: "Bank" hoặc "Check")
    - bankAccount: String (Thông tin tài khoản ngân hàng, nếu nhận qua ngân hàng)
  + Phương thức:
    - getTimecard(): Timecard (Truy xuất thẻ chấm công)
    - getPurchaseOrder(): PurchaseOrder (Lấy đơn đặt hàng nếu có)
- Lớp 3: Timecard
  + Thuộc tính:
    - timecardID: String
    - totalHours: double (Tổng số giờ làm việc)
  + Phương thức: getTotalHours(): double (Lấy tổng giờ làm việc)
- Lớp 4: PurchaseOrder
  + Thuộc tính:
    - orderID: String
    - commissionRate: double (Tỷ lệ hoa hồng)
   
  + Phương thức: calculateCommission(): double (Tính hoa hồng từ đơn hàng)
- Lớp 5: Paycheck
  + Thuộc tính:
    - paycheckID: String
    - employeeID: String
    - amount: double (Tổng tiền lương)
   
  + Phương thức: print(): void (In phiếu lương)
### b. Sequence Diagram: Luồng xử lý tính toán và thanh toán lương
- System Clock kích hoạt PayrollController vào ngày trả lương.
- PayrollController lấy danh sách tất cả nhân viên cần thanh toán lương.
- Với từng nhân viên:
  + PayrollController gọi phương thức getTimecard() và getPurchaseOrder() để lấy dữ liệu.
  + Tính toán tiền lương bằng cách kết hợp:
    - Tổng giờ làm việc (Timecard).
    - Hoa hồng (PurchaseOrder).
  + Tạo đối tượng Paycheck lưu thông tin lương.
- Kiểm tra phương thức thanh toán của nhân viên:
  + Nếu qua ngân hàng: PayrollController gọi BankSystem để xử lý giao dịch.
  + Nếu qua phiếu lương: Gửi phiếu lương đến PrinterInterface để in.
- Kết thúc quy trình, ghi nhận thông báo kết quả.
### c. Activity Diagram:
- Khởi động quy trình:
  + System Clock kiểm tra ngày trả lương.
  + PayrollController nhận lệnh chạy bảng lương. 
- Xử lý lương từng nhân viên:
  + Truy xuất dữ liệu: Thẻ chấm công và đơn đặt hàng.
  + Tính toán tiền lương: Sử dụng giờ làm việc và hoa hồng.
  + Tạo phiếu lương.
  + Xử lý thanh toán.
- Kết thúc quy trình:
  + Ghi nhận giao dịch vào hệ thống.
  + Báo cáo lỗi (nếu có).
### d. Mô tả hệ thống con: 
- Module xử lý logic (Business Logic):
  + PayrollController: Điều phối toàn bộ quy trình xử lý lương.
  + Timecard và PurchaseOrder: Cung cấp dữ liệu đầu vào để tính toán lương.
  + Paycheck: Lưu trữ thông tin kết quả lương của từng nhân viên.
- Module kết nối bên ngoài:
  + BankSystem: Xử lý giao dịch chuyển khoản.
  + PrinterInterface: In phiếu lương.
- Module cơ sở dữ liệu: Lưu trữ và truy xuất dữ liệu thẻ chấm công, đơn đặt hàng, và thông tin lương.
### e. Các bước thiết kế chi tiết:
- Phát triển các lớp cơ bản: Xây dựng các lớp Employee, Timecard, PurchaseOrder, Paycheck.
- Triển khai bộ điều khiển: Tạo và tích hợp logic trong lớp PayrollController.
- Tích hợp hệ thống bên ngoài:
  + Kết nối với BankSystem để xử lý giao dịch.
  + Tích hợp PrinterInterface để in phiếu lương.
- Kiểm tra logic: Xác minh quy trình tính toán lương và xử lý thanh toán với dữ liệu mẫu.
## 4. Hệ thống con từ use-case Print Paycheck:
### a. Mô hình class Diagram:
- Lớp : PrintService
  + Thuộc tính: printerStatus: boolean (Trạng thái máy in: hoạt động hoặc không hoạt động)
  + Phương thức:
    - printPaycheck(paycheck: Paycheck): void (In phiếu lương)
    - checkPrinterStatus(): boolean (Kiểm tra trạng thái máy in)
    - retryPrint(paycheck: Paycheck): void (Thử lại nếu in thất bại)
- Lớp: Paycheck
  + Thuộc tính:
    - paycheckID: String
    - employeeID: String
    - amount: double
    - payDate: Date
  + Phương thức: getDetails(): String (Lấy chi tiết phiếu lương)
- Lớp : PayrollController
  + Thuộc tính: paychecks: List<Paycheck> (Danh sách phiếu lương cần in)
  + Phương thức: sendToPrint(paycheck: Paycheck): void (Gửi phiếu lương đến PrintService)
- Lớp: PrinterInterface
  + Phương thức: sendPrintCommand(data: String): boolean (Gửi lệnh in tới máy in)
- Lớp: AdminNotifier
  + Phương thức: notifyIssue(issue: String): void (Thông báo lỗi tới quản trị viên)
### b. Sequence Diagram:
- PayrollController gửi phiếu lương (Paycheck) đến PrintService thông qua phương thức sendToPrint().
- PrintService kiểm tra trạng thái máy in thông qua phương thức checkPrinterStatus():
  + Nếu máy in hoạt động:
    - Lấy thông tin phiếu lương bằng paycheck.getDetails().
    - Gửi lệnh in đến PrinterInterface bằng phương thức sendPrintCommand(data).
    - Nếu in thành công, kết thúc quy trình.  
  + Nếu máy in không hoạt động:
    - Gọi phương thức retryPrint() để thử lại (có giới hạn số lần).
    - Nếu vẫn thất bại, sử dụng AdminNotifier để thông báo lỗi.
### c. Activity Diagram: 
- Kiểm tra trạng thái máy in:
  + Nếu máy in hoạt động: Tiến hành in phiếu.
  + Nếu máy in không hoạt động: Báo lỗi.
- In phiếu lương:
  + Lấy thông tin phiếu lương từ đối tượng Paycheck.
  + Gửi lệnh in qua PrinterInterface.
- Xử lý lỗi:
  + Nếu in thất bại: Thử lại một số lần nhất định.
  + Nếu vẫn lỗi: Thông báo cho quản trị viên.
- Hoàn tất: Phiếu lương được in thành công hoặc ghi nhận lỗi.
### d. Mô tả hệ thống con:
- Module xử lý in ấn:
  + PrintService: Quản lý toàn bộ quy trình in phiếu lương, bao gồm kiểm tra trạng thái máy in và xử lý lỗi.
  + PrinterInterface: Gửi lệnh in tới phần cứng máy in.
- Module lưu trữ dữ liệu phiếu lương: Paycheck: Lưu trữ thông tin chi tiết phiếu lương.
- Module hỗ trợ xử lý lỗi: AdminNotifier: Gửi thông báo lỗi đến quản trị viên trong trường hợp cần can thiệp.
### e. Các bước thiết kế chi tiết: 
- Phát triển lớp cơ bản: Tạo các lớp PrintService, Paycheck, PrinterInterface, và AdminNotifier.
- Tích hợp quy trình in:
  + ích hợp phương thức sendToPrint() của PayrollController với PrintService.
  + Kết nối PrintService với PrinterInterface.
- Xử lý lỗi: Triển khai logic thử lại (retryPrint()) và thông báo lỗi.
- Kiểm tra hoạt động: Mô phỏng tình huống máy in hoạt động và không hoạt động để kiểm tra luồng xử lý.
## 5. Hệ thống con từ use-case Maintain Purchase Order:
### a. Mô hình class Diagram:
- Lớp : PurchaseOrder
  + Thuộc tính:
    - orderID: String
    - employeeID: String
    - productID: String
    - quantity: int
    - totalAmount: double
    - orderDate: Date
  + Phương thức:
    - validateOrder(): boolean (Xác thực thông tin đơn hàng)
    - calculateTotal(): double (Tính tổng số tiền)
- Lớp : PurchaseOrderController
  + Thuộc tính: purchaseOrders: List<PurchaseOrder> (Danh sách đơn hàng)
  + Phương thức:
    - createOrder(order: PurchaseOrder): void (Tạo đơn hàng mới)
    - updateOrder(orderID: String, updatedOrder: PurchaseOrder): void (Cập nhật đơn hàng)
    - deleteOrder(orderID: String): void (Xóa đơn hàng)
    - validateOrder(order: PurchaseOrder): boolean (Xác thực thông tin đơn hàng)
- Lớp : PurchaseOrderDatabase
  + Phương thức:
    - saveOrder(order: PurchaseOrder): void (Lưu đơn hàng)
    - updateOrder(orderID: String, updatedOrder: PurchaseOrder): void (Cập nhật đơn hàng trong cơ sở dữ liệu)
    - deleteOrder(orderID: String): void (Xóa đơn hàng khỏi cơ sở dữ liệu)
- Lớp: Employee
  + Thuộc tính:
    - employeeID: String
    - name: String
  + Phương thức: accessPurchaseOrder(): List<PurchaseOrder> (Xem danh sách đơn hàng của nhân viên)
- Lớp: ValidationService
  + Phương thức:
    - validateOrderID(orderID: String): boolean (Xác thực mã đơn hàng)
    - validateProductID(productID: String): boolean (Xác thực mã sản phẩm)
### b. Sequence Diagram:
- Luồng xử lý cơ bản:
  + Employee mở giao diện PurchaseOrderForm và nhập thông tin đơn hàng.
  + PurchaseOrderForm gửi thông tin đến PurchaseOrderController.
  + PurchaseOrderController:
    - Gọi ValidationService để xác thực thông tin đơn hàng (mã đơn hàng, mã sản phẩm, số lượng).
    - Nếu hợp lệ, gọi PurchaseOrderDatabase để lưu thông tin.
    - Trả về kết quả thành công hoặc thông báo lỗi.
- Luồng phụ: Mã đơn hàng không hợp lệ:
  + ValidationService trả về lỗi "Invalid Purchase Order".
  + PurchaseOrderController gửi thông báo lỗi tới PurchaseOrderForm.
  + Employee chỉnh sửa lại thông tin và gửi lại.
### c. Activity Diagram: 
- Nhập thông tin đơn hàng: Nhân viên nhập mã đơn hàng, mã sản phẩm, số lượng, và ngày đặt hàng.
- Xác thực đơn hàng:
  + Kiểm tra mã đơn hàng, mã sản phẩm, và số lượng:
    - Nếu hợp lệ, chuyển sang bước tiếp theo.
    - Nếu không hợp lệ, hiển thị thông báo lỗi.
- Lưu hoặc cập nhật đơn hàng: Lưu đơn hàng mới hoặc cập nhật đơn hàng hiện có.
- Hoàn tất: Thông báo thành công.
### d. Mô tả hệ thống con:
- Module xử lý chính:
  + PurchaseOrderController:
    - Điều phối luồng xử lý giữa giao diện người dùng và cơ sở dữ liệu.
    - Thực hiện xác thực và gọi các hành động liên quan (tạo, cập nhật, xóa đơn hàng).
  + ValidationService: Đảm bảo dữ liệu đầu vào hợp lệ (mã đơn hàng, mã sản phẩm).
  + PurchaseOrderDatabase: Lưu trữ và quản lý dữ liệu đơn hàng.
- Giao diện người dùng:
  + PurchaseOrderForm:
    - Cho phép nhân viên nhập thông tin đơn hàng.
    - Hiển thị thông báo lỗi hoặc thành công.
### e. Các bước thiết kế chi tiết:
- Phát triển các lớp cơ bản: Tạo các lớp PurchaseOrder, PurchaseOrderController, PurchaseOrderDatabase, và ValidationService.
- Kết nối giao diện người dùng: Tạo giao diện PurchaseOrderForm để nhập và hiển thị thông tin đơn hàng.
- Kiểm thử:
  + Mô phỏng việc tạo, cập nhật, và xóa đơn hàng để kiểm tra luồng xử lý.
  + Kiểm tra các tình huống lỗi như mã đơn hàng không hợp lệ hoặc lỗi kết nối cơ sở dữ liệu.

