# Phân Tích Kiến Trúc và Ca Sử Dụng Hệ Thống "Payroll System"
## 1. Phân tích yêu cầu :
  - Yêu cầu chức năng:
    + Nhập liệu và xử lý:
      Nhân viên ghi lại thẻ chấm công hoặc lệnh mua.
      Lưu trữ và tính toán bảng lương dựa trên số giờ làm việc, mức lương, hoa hồng (nếu có).
      Chỉ định phương thức thanh toán: gửi séc qua bưu điện, nhận tại văn phòng, hoặc chuyển khoản ngân hàng.
    + Tự động hóa:
      Hệ thống tự động tính toán bảng lương vào mỗi thứ Sáu và ngày làm việc cuối tháng.
    + Quản lý và báo cáo:
      Báo cáo chi tiết cho nhân viên: số giờ làm việc, số giờ được tính cho một dự án, tổng lương, thời gian nghỉ phép còn lại.
      Quản trị viên duy trì thông tin nhân viên: thêm, xóa, sửa thông tin, phân loại nhân viên.
  - Yêu cầu phi chức năng:
    + Tích hợp với cơ sở dữ liệu cũ:
      Hệ thống cần truy cập dữ liệu từ cơ sở dữ liệu DB2 (IBM) hiện có mà không thay đổi dữ liệu này.
    + Bảo mật:
      Đảm bảo chỉ nhân viên được truy cập và chỉnh sửa thông tin của mình.
      Quản trị viên có quyền quản lý toàn bộ hệ thống.
    + Hiệu năng:
      Hỗ trợ khoảng 5.000 nhân viên trên toàn cầu với tính năng tự động hóa và báo cáo theo thời gian thực.
## 2. Phân tích kiến trúc : 
  Hệ thống Payroll sẽ sử dụng kiến trúc **Client-Server** với ba lớp chính: **Client**, **Application Server**, và **Database Server**.
- **Client**: Đây là giao diện người dùng (Windows-based desktop interface) cho phép nhân viên nhập liệu, xem báo cáo và thay đổi các thông tin cá nhân. Các yêu cầu từ client sẽ được gửi đến application server để xử lý.
  
- **Application Server**: Lớp này sẽ xử lý các nghiệp vụ như tính toán lương, lưu trữ thông tin nhân viên, báo cáo, và các tính toán liên quan đến thời gian làm việc và hoa hồng. Hệ thống này sẽ giao tiếp với cơ sở dữ liệu và gửi các yêu cầu thanh toán đến các phương thức thanh toán.
- **Database Server**: Chứa các thông tin về nhân viên, lịch sử thanh toán, thông tin thời gian làm việc và các dữ liệu khác. Hệ thống sẽ truy vấn dữ liệu từ cơ sở dữ liệu **Project Management Database** (DB2), nhưng không thực hiện bất kỳ thao tác cập nhật nào.

### Lý do lựa chọn kiến trúc

Kiến trúc Client-Server giúp tách biệt các vai trò, dễ dàng bảo trì và mở rộng. Dữ liệu nhạy cảm về nhân viên được bảo vệ trong lớp riêng biệt, giúp giảm thiểu rủi ro bảo mật. Hệ thống có thể hoạt động trên nhiều máy tính cá nhân trong công ty mà không cần thay đổi cơ sở hạ tầng.
  ### Biểu đồ Package
![Diagram](https://www.planttext.com/api/plantuml/png/V5ExJWCn4Epz5QjKKAJX0r0WIO44KXJeeYiMtt8o-2NRLvmGNqR19_4B-7Ava8ljkFJCpixEsh_VFmiVq8LMIMQHVs13CDjWvuoKyDpvG6e6dmpYES9BAKW7UCIEt0ZsPxTMLfgE21vq8FU6dAf_S4lMk925NeGYZgwEe6qJoXURjh-pLWgEGHYTyJ1wNwBahTopSfsUK4Sn5UUe9hNz3MoSuUIzq4tYFzx1MZT25yojCE0hUhgKpiZ9-UgnAfrcIzousfyYphmJ3oU3x6lXQdL_SprwY-voIu7v_BQGLBgcWPnENzxQK96DccMx3WMPVB8YP_93OhdTJSSyHfZEKkvVe2QQR9UyoWDr-Y2YvDd5GV3oDXUaw_w7_W400F__0m00)
  

## 3. Cơ chế phân tích :
- Xác thực và phân quyền :
    + Nhân viên chỉ được truy cập và chỉnh sửa thông tin cá nhân (thẻ chấm công, lệnh mua).
    + Quản trị viên có quyền quản lý toàn bộ dữ liệu.
    + Lý do: Đảm bảo bảo mật và phân quyền rõ ràng, tránh truy cập trái phép.
- Tính toán bảng lương :
    + Tính lương dựa trên:
      - Giờ làm việc và giờ làm thêm (với nhân viên làm việc theo giờ).
      - Lương cố định và hoa hồng (với nhân viên hưởng lương và hoa hồng).
    + Tự động hóa việc tính toán và xử lý vào các ngày định sẵn.
    + Lý do: Đáp ứng yêu cầu tự động hóa và chính xác cao.
- Tích hợp cơ sở dữ liệu:
    + Truy vấn thông tin dự án và số phí từ cơ sở dữ liệu DB2.
    + Lý do: Sử dụng dữ liệu cũ mà không làm gián đoạn hoặc thay đổi hệ thống hiện tại.
- Quản lý báo cáo :
    + Cung cấp báo cáo về giờ làm việc, tổng số tiền lương, thời gian nghỉ phép.
    + Báo cáo hành chính cho quản trị viên.
    + Lý do: Hỗ trợ nhân viên và quản trị viên theo dõi thông tin dễ dàng.
- Lập lịch tự động :
    + Chạy tự động tính lương vào mỗi thứ Sáu và ngày làm việc cuối tháng.
    + Lý do: Giảm thiểu sự can thiệp thủ công.
## 4. Phân tích ca sử dụng Payment :
#### Các lớp phân tích

- **Employee**: Nhân viên yêu cầu thanh toán và cung cấp thông tin về phương thức thanh toán và ngày thanh toán.
- **PayrollSystem**: Hệ thống tính toán số tiền lương và gửi thông tin thanh toán đến **PaymentMethod**.
- **PaymentMethod**: Lớp này xác định phương thức thanh toán cho nhân viên, bao gồm chuyển khoản ngân hàng, gửi qua bưu điện, hoặc nhận trực tiếp tại văn phòng.

#### Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/T94zZi8m48Lxds94lnUWG4W9I2aYMOWB3Cu0blmJx4d1sIZsI7k5dH28287EUjydlsVvx_Qxpeo9E-yK6eu9DhvryKgaMecjiIq6XiKpXIemfICQMW1cs5HJJUCrHUUWG6SwXsnZk7kwc7cUvA1JD9Ip3QT1qv-rclWScq6flmmhaV60-R6hL6eaFolP2KlOqQMZBAN3hKf2GRgOelVzIeJ-XbAqBR4vmwHoZlVMay7Kl6Aj1LV1iaKccBzUYT1hjMYFT9mfOL_mB5r24SFH9ZyAQmfD_t__0000__y30000)

### Phân Tích Biểu Đồ Sequence "Select Payment"

##### 1. Các Lớp và Nhiệm Vụ

###### **Employee (Actor)**
- **Nhiệm vụ**: Gửi yêu cầu thanh toán.
- **Quan hệ**: Gửi yêu cầu tới `Employee Interface`.

###### **Employee Interface (EI)**
- **Nhiệm vụ**: Cung cấp giao diện yêu cầu thanh toán và thông báo kết quả.
- **Quan hệ**: Nhận yêu cầu từ `Employee`, gửi tới `Payroll Calculation`.

###### **Payroll Calculation (PC)**
- **Nhiệm vụ**: Tính toán lương nhân viên (lương cơ bản, giờ làm thêm, hoa hồng).
- **Quan hệ**: Truy vấn `Employee Database` và `Timecard Data`, gửi yêu cầu tới `Payment Processing`.

###### **Employee Database (ED)**
- **Nhiệm vụ**: Cung cấp thông tin nhân viên.
- **Quan hệ**: Cung cấp dữ liệu cho `Payroll Calculation`.

###### **Payment Processing (PP)**
- **Nhiệm vụ**: Xử lý thanh toán.
- **Quan hệ**: Gửi yêu cầu thanh toán tới `Payment Method`.

###### **Payment Method (PM)**
- **Nhiệm vụ**: Thực hiện thanh toán cho nhân viên.
- **Quan hệ**: Thực hiện thanh toán và thông báo kết quả cho `Employee Interface`.

##### 2. Quy Trình Thanh Toán

1. **Nhân viên yêu cầu thanh toán**: Nhân viên gửi yêu cầu thanh toán qua `Employee Interface`.
2. **Tính toán thanh toán**: `Employee Interface` gửi yêu cầu tính toán thanh toán tới `Payroll Calculation`.
3. **Truy vấn dữ liệu**: `Payroll Calculation` truy vấn `Employee Database` và `Timecard Data` để tính toán lương.
4. **Xử lý thanh toán**: `Payroll Calculation` gửi yêu cầu thanh toán tới `Payment Processing`.
5. **Thực hiện thanh toán**: `Payment Processing` gửi yêu cầu thanh toán tới `Payment Method`.
6. **Xác nhận thanh toán**: Sau khi thanh toán, `Payment Method` gửi xác nhận thanh toán về lại `Employee Interface`.
## 5. Phân tích ca sử dụng Maintain Timecard :
#### Các lớp phân tích

- **Employee**: Nhân viên cung cấp thông tin về thời gian làm việc của họ và các dự án liên quan, nhập số giờ đã làm cho mỗi ngày và mỗi charge number (mã dự án).
- **Timecard**: Lớp này lưu trữ các bản ghi thời gian làm việc của nhân viên. Mỗi bản ghi bao gồm thông tin về ngày làm việc, số giờ làm việc, và charge number (mã dự án).
- **PayrollSystem**: Xử lý và lưu trữ thông tin thời gian làm việc vào hệ thống. Sau khi nhân viên nhập thời gian làm việc, hệ thống sẽ tính toán tổng số giờ, xác định việc trả lương theo kiểu gì (theo giờ, lương cố định), và lưu trữ thông tin này để thanh toán vào các ngày thanh toán quy định.

### Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/T90z3e9048NxFSM4tjXJ61B0X896yG3ZCYW9kwoxG-7PB3oILt1NVX9YQAQOzxqtB_DvlHF7Q7bGdK39lOLScQv_4WdZrwri3Mg6g6eLIRGr5DeCx2UJRL1I1EYWIeiDkaIDDrAaUGBBDJWVWmmPh-Z6l3pRY0lK59G9iPXtXr01OZZHOo37i1WkfaOc4TGVL7heJBg6LQG8WjVppCj7Odc7LR5PzrU3tt-9zcFoHiviZY7jTTDQzTSeyIN2pxy0003__mC0)

### Phân Tích Biểu Đồ Sequence "Maintain Timecard"

### 1. Các Lớp và Nhiệm Vụ

- **Employee**: Nhân viên nhập thời gian làm việc qua giao diện.
- **Timecard Input Interface**: Cung cấp giao diện cho nhân viên nhập liệu.
- **Timecard Management**: Quản lý và lưu trữ thông tin thời gian làm việc.
- **Employee Database**: Lưu trữ thông tin nhân viên.
- **Timecard Data**: Lưu trữ bản ghi thời gian làm việc.

### 2. Quan Hệ Giữa Các Lớp
- **Employee**: Nhân viên nhập thông tin thời gian làm việc qua giao diện.
  - Thuộc tính: `EmployeeID`, `Name`, `Role`
  - Quan hệ: Gửi yêu cầu tới `Timecard Input Interface` để nhập thời gian làm việc.

- **Timecard Input Interface**: Cung cấp giao diện cho nhân viên nhập liệu.
  - Thuộc tính: `InputFields`, `ErrorMessages`
  - Quan hệ: Nhận yêu cầu từ nhân viên, chuyển tiếp tới `Timecard Management` để xử lý.

- **Timecard Management**: Quản lý thông tin về thời gian làm việc của nhân viên.
  - Thuộc tính: `TimecardID`, `EmployeeID`, `WorkedHours`, `Date`
  - Quan hệ: Gửi yêu cầu tới `Employee Database` để xác minh thông tin nhân viên, lưu trữ vào `Timecard Data`.

- **Employee Database**: Lưu trữ thông tin về nhân viên.
  - Thuộc tính: `EmployeeID`, `EmployeeName`, `EmployeeRole`
  - Quan hệ: Cung cấp thông tin nhân viên cho `Timecard Management` khi cần xác minh.

- **Timecard Data**: Lưu trữ thông tin thời gian làm việc của nhân viên.
  - Thuộc tính: `TimecardID`, `WorkedHours`, `Date`
  - Quan hệ: Lưu trữ dữ liệu từ `Timecard Management`.
## 6. Hợp nhất ca sử dụng :
### Tổng quan về các ca sử dụng

Hệ thống "Payroll System" được phân tích thông qua hai ca sử dụng chính: **Select Payment** và **Maintain Timecard**. Mỗi ca sử dụng có mục đích và hành vi riêng biệt, nhưng đều liên quan mật thiết đến các hoạt động xử lý lương cho nhân viên.

1. **Ca sử dụng "Select Payment"**:
   - Mục đích: Xử lý yêu cầu thanh toán của nhân viên và xác định phương thức thanh toán (chuyển khoản ngân hàng, gửi qua bưu điện, hoặc nhận trực tiếp tại văn phòng).
   - Các lớp phân tích liên quan: **Employee**, **PayrollSystem**, **PaymentMethod**.
   - Hành vi chính: Nhân viên yêu cầu thanh toán, hệ thống tính toán và gửi yêu cầu thanh toán tới phương thức thanh toán đã chọn.

2. **Ca sử dụng "Maintain Timecard"**:
   - Mục đích: Xử lý và lưu trữ thông tin về thời gian làm việc của nhân viên và các dự án họ tham gia. Hệ thống tính toán số tiền lương dựa trên thời gian làm việc và phương thức thanh toán.
   - Các lớp phân tích liên quan: **Employee**, **Timecard**, **PayrollSystem**.
   - Hành vi chính: Nhân viên nhập thời gian làm việc, hệ thống lưu trữ thời gian và tính toán lương theo giờ hoặc lương cố định.

### Hợp nhất các kết quả phân tích

Hai ca sử dụng trên đều nhằm mục đích xử lý các yếu tố liên quan đến việc thanh toán lương cho nhân viên, nhưng với các chức năng riêng biệt:
- **Ca "Select Payment"** tập trung vào việc xử lý yêu cầu thanh toán của nhân viên, với các phương thức thanh toán khác nhau (chuyển khoản, bưu điện, nhận trực tiếp).
- **Ca "Maintain Timecard"** giúp hệ thống quản lý và tính toán thời gian làm việc, từ đó xác định số tiền lương phải trả cho nhân viên, dựa trên thời gian và phương thức thanh toán.
Cả hai ca sử dụng này đều có sự liên kết chặt chẽ với các lớp phân tích như **PayrollSystem**, **PaymentMethod**, **Employee**, và **Timecard**, và đều ảnh hưởng trực tiếp đến việc tính toán và thực hiện thanh toán cho nhân viên.

#### Các lớp phân tích chung

- **Employee**: Là người yêu cầu thanh toán và cung cấp thông tin về thời gian làm việc và các dự án tham gia.
- **PayrollSystem**: Lớp trung gian xử lý các yêu cầu thanh toán và tính toán lương cho nhân viên. Đối với "Maintain Timecard", hệ thống tính toán lương từ số giờ làm việc và lưu trữ thông tin. Đối với "Select Payment", hệ thống gửi yêu cầu thanh toán tới phương thức thanh toán đã được nhân viên chọn.
- **PaymentMethod**: Xác định phương thức thanh toán cho nhân viên, thực hiện việc thanh toán dựa trên yêu cầu từ PayrollSystem.

#### Biểu đồ Sequence hợp nhất
![Diagram](https://www.planttext.com/api/plantuml/png/T9FFIiD04CRl-nI35qyMr5iFKaWgzX09seFNCTac2yacRgP2dy2p3o1OZq91hmRn4EXxv0by1MURDfZ-kSxtsvdlcs5_ovz1GMXecYO20yeC3DCyoMPIYfpBAb0vQeAZJHL6cgIPO22F00iOZhhOMAKoG1Cobazf2nuxXsWFDKOobPeQqEjoFivCbYJWO19C4oILwHNdEpkSxG6-oG9P54f73URlnpn9SHOsY7SWhek4zrYiqxe7_5jg7T4LuXXEUt0TLsyQ7bNrha77zTSY1uhhyaL1f513KhschDRbKo3QOISNl53emurycCg2eEq_r6HcWZKcU8kCDFlj611MiO37-YsVKcxfREoi1rSySsNbMKT0rKB7G5arPqlBZ-MSQs5TVYAGiSuFMUOPFCbt_fdTSoJ1WCtaCdOfAOYXizUrp3jhzQxXHlVzLLv52ad2xerjhlCUtDNbWZr-isVSP1ByrdQm6ra_s3GG_Yf2QwWFJgOdogGjC90wjD_Y3m00__y30000)
