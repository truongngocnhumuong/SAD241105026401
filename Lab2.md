# Phân tích tất cả các ca sử dụng còn lại trong hệ thống Payroll System.
## 1. Create Administrative Report: 
### a. Các lớp phân tích :
- **PayrollAdministrator**: Gửi yêu cầu tạo báo cáo và quyết định lưu hoặc hủy báo cáo.
- **ReportCriteria**: Lưu trữ tiêu chí báo cáo và xác thực tính hợp lệ của các tiêu chí.
- **ReportGenerator**: Thực hiện tạo báo cáo dựa trên tiêu chí được cung cấp.
- **Report**: Lưu trữ nội dung báo cáo và hỗ trợ hiển thị hoặc lưu báo cáo vào tệp.
- **ErrorHandler**: Quản lý và hiển thị các thông báo lỗi trong trường hợp thông tin không hợp lệ hoặc thiếu.
### b. Biểu đồ squence: 
![Diagram](https://www.planttext.com/api/plantuml/png/ZP712i8m38RlWxr3Zthm1NeOaodgJHIy1vf38UjccWtszjPs3WSJrqER_lnVagQb5s3fQiep5TOL1cw8zgQspdfXa8RLhYZK3Tk6fM8ho1Pqk3yxz9BapJRHSzCYzm2o1WG_ob_qX0vZ6rgD8IuLdMnVg5OLumz_j2szLgk3zIt1CAU0HDsXnn5Fueg9wKZDSo5vL1VNlqSHphPRa-x8tF0Pd24CFQOWQbDMP_Ai37lup1S0)

- Mô tả tương tác giữa các lớp:
    + PayrollAdministrator yêu cầu tạo báo cáo.
    + ReportCriteria xác thực tiêu chí báo cáo.
    + ReportGenerator tạo báo cáo dựa trên tiêu chí.
    + Báo cáo được trả về cho PayrollAdministrator.
    + PayrollAdministrator quyết định lưu báo cáo hoặc hủy bỏ.
    + Nếu lưu, báo cáo được lưu thông qua lớp Report.
### c. Các biểu đồ lớp mô tả lớp phân tích: 
![PlantText](https://www.planttext.com/api/plantuml/png/VPDDQiCm48Nt1jz1kxOKNy2BafAaFz2Ma8JkXsYQ3iYIAqq2flJkbINBhXEd6s4-lV6yDsFF78FbGwNoRAV0ER62nXgbxcL5cXnRO6F5Tvu9KOW0dnUb8CsHl465fV0oqlj0YlQy5MlyEg3ZDTR6ylLDX1iuua1-yYprZ71kYT4If6wHRfjwt45iMiSBO8_RCyAbbcUegfLf42zvV0T5qgjJtqbJZwXnD8CEe8ptPQVx--8a-IVhEEFSQ4RDuvWFfCwj1_fYTi1az5Ie1RbQGNC--ArfIq_CBAqrzWcqLDW73EmLdOFzvDYw3a7Ml-xA9r71bFkaskNPv6TK57Udk_OBmm_Iw4jERWRni8DIhAmvaaINP5kJ2WVLKEaBqZBw1k5wqbwxIpvOxT9ABuOOpQqKySa5savZXbg6N-eN)

- Giải thích:
    + PayrollAdministrator: Quản trị viên yêu cầu và lưu báo cáo.
    + ReportCriteria: Lớp chứa thông tin về loại báo cáo, ngày bắt đầu/kết thúc và tên nhân viên.
    + ReportGenerator: Tạo báo cáo dựa trên tiêu chí.
    + Report: Lớp biểu diễn báo cáo và có thể hiển thị hoặc lưu xuống file.
    + ErrorHandler: Xử lý các lỗi xảy ra trong quá trình nhập dữ liệu hoặc tạo báo cáo.
## 2. Create Employee Report:
### a. Các lớp phân tích :
- **Employee**: Đại diện cho người dùng hệ thống, cung cấp thông tin cần thiết để tạo báo cáo và lựa chọn các tùy chọn như loại báo cáo, thời gian, hoặc số dự án.
- **ReportController**: Điều phối và xử lý các yêu cầu tạo báo cáo từ nhân viên, thực hiện giao tiếp với hệ thống và các dịch vụ khác.
- **ProjectManagementDatabase**: Cung cấp thông tin về các dự án, bao gồm danh sách số dự án mà nhân viên có thể chọn khi tạo báo cáo "Total Hours Worked for a Project".
- **Report**: Đại diện cho một báo cáo được tạo ra theo yêu cầu của nhân viên.
- **FileSystem**: Quản lý việc lưu trữ và xử lý các tập tin báo cáo khi nhân viên yêu cầu lưu báo cáo.
### b. Biểu đồ squence: 
![Diagram](https://www.planttext.com/api/plantuml/png/ZLF1IiD04Bq7yWz3Jote3nIKGbMyA68B7iJ3D9dMrStkEZkfvE_TRPecRPDY3e7ip7lpvhtDp0kob8LE4yp4CjmNJjkAA4rSAAXCEJG2h-GiozmQOQiryN7rXUqNPVA41ZTKa94x55oXxoKvFdjGcXQL5ohI94sQuN1zUpPo2am_9Ncf2-D9cfosH5X3SMYVin9YXH5mcT-ntQgSzeKE37KZ7fQL8xY1qT8AQdYq9Njui_nDEQo3UzXuCKeJ24-Vma6tfh0XcNyYR-YvB5R4FWwFD8EG_aMoBiVxnx2KrgnSUQUnwfr-sJLFEaZh0YEEJDwVJtqMLpN4A7IQPg-ijgaEuw3eDzmX3sB1uvP2ulK5-uVeqBudDLZG5MYReIXh9iDcjLUrniVlSJto3D_s3YHapLfniGWqExTqYFAWE2oT8UV-Q9zBNku1hKixzsVXlVkn_m00)
- Mô tả tương tác giữa các lớp:
  + Employee khởi động ca sử dụng bằng cách yêu cầu tạo báo cáo.
  + ReportController yêu cầu nhân viên cung cấp thông tin về loại báo cáo và phạm vi thời gian.
  + Nếu báo cáo liên quan đến một dự án cụ thể, ReportController lấy danh sách dự án từ ProjectManagementDatabase và cho phép nhân viên chọn.
  + ReportController chuyển thông tin đến lớp Report để tạo báo cáo.
  + Sau khi báo cáo được tạo, nó sẽ được hiển thị cho nhân viên.
  + Nhân viên có thể chọn lưu báo cáo vào hệ thống tập tin thông qua FileSystem, hoặc hủy bỏ nếu không cần lưu.
### c. Các biểu đồ lớp mô tả lớp phân tích:
![PlantText](https://www.planttext.com/api/plantuml/png/TPBTIiH038Nl2ts7kUoozWMAB0khWg2BkBv0jWrrblcfcRHGn7Utq-beQzsRWNm9EIV9x1q3SQjLcfGAd1Ftkb6sHnIVQI94Bd2A7wj2d9YagGCte75EjeBmeqN7hzXOucmJO4EsanK6U239I19yyYjDekIKj8R9AeKKfMdaRts3I-dHyXtmWFqx-JJL4cr5ZGPfY9QEEb2o6kWLCozaBrZoCnYeKQFnGd06Dot4T-N3Er2DnrQVaLosASIJT7mRBEx-6MqvqF7FvdAXR0aihLdkivAkKT17tmwwsIGpZGUfyDGxHXqj-b9Fio1OJ3PkLaAnqS_HytotEaUQh0xaowukwafzW34veb_dQR8V3ZX-msy0)
- Giải thích:
  + Employee: Tương tác với hệ thống để yêu cầu và cung cấp thông tin báo cáo.
  + ReportController: Là lớp trung tâm, điều khiển luồng nghiệp vụ cho ca sử dụng "Create Employee Report", kết nối với các dịch vụ liên quan như ProjectManagementDatabase và Report.
  + ProjectManagementDatabase: Cung cấp dữ liệu liên quan đến các dự án khi cần thiết.
  + Report: Đại diện cho báo cáo được tạo ra. Báo cáo có thể được hiển thị cho nhân viên hoặc lưu trữ nếu nhân viên yêu cầu.
  + FileSystem: Quản lý việc lưu trữ báo cáo vào hệ thống tập tin.
## 3. Login:
### a. Các lớp phân tích :
- **User (Actor)**: Người dùng hệ thống, nhập tên đăng nhập và mật khẩu.
- **LoginController**: Điều khiển luồng tương tác trong quá trình đăng nhập.
- **AuthenticationService**: Thực hiện xác thực thông tin đăng nhập của người dùng.
- **UserSession**: Quản lý phiên đăng nhập của người dùng.
### b. Biểu đồ squence: 
![Diagram](https://www.planttext.com/api/plantuml/png/fL9DQyCm3BqR_1zqt63z0pcKZj91eJk5xYuSqHfSESXs-lSdDzsMXMmxp0U3_9xU1tYJCaekbs0DkXm5Zed4cbuVlVCzSeP3F7dUHiuIGvY3poMVYNN4x2Et98Dtz9rI5LjAIN5hhAaZhDPpsGPsd1Kf2ZDU290xw36bQvJEcXcx2YnQDp1Wy1rcsWfr5SQG7Zv4dpuL7xLloF1MoJ2XMWDw5gLXjPIwBSvfkN5l8UMaVGDEI9FTnrkgVKrILoUy7upkuAZH_MhOZC1NE0g9OC_3l-k-e0z5w0_tzXoli1FH__Ig_dZI1MBDlD7xzjdU0G00)
- Mô tả tương tác giữa các lớp:
  + User: Người dùng nhập tên đăng nhập và mật khẩu vào giao diện đăng nhập.
  + LoginController:
    - Nhận thông tin đăng nhập từ người dùng và gửi yêu cầu xác thực đến lớp AuthenticationService.
    - Nếu thông tin hợp lệ, tạo một phiên mới thông qua UserSession.
    - Nếu thông tin không hợp lệ, hiển thị thông báo lỗi cho người dùng.
   
  + AuthenticationService:
    - Kiểm tra thông tin đăng nhập trong cơ sở dữ liệu.
    - Phản hồi kết quả xác thực cho LoginController.
   
  + UserSession: Tạo và quản lý phiên đăng nhập cho người dùng nếu đăng nhập thành công.
### c. Các biểu đồ lớp mô tả lớp phân tích:
![PlantText](https://www.planttext.com/api/plantuml/png/ZLBBQiCm4BmR_0ywkhJ-0HzAsj13e3sPVi1YBOv0NeNTTK88_VTAVX3RfD2RD9hTsPdLJXHO-yxdMUD1n7mBihdbcJ7FVJmIT5YPMjbHEu2dIBe4jdVm9y_cui_GEje7KWxUptrAdz1QGNjPjJg3TnOKzumMIHruARQQBsOh-3JKMYSd3zT1i6uOaOhnGOxXyi4S-0j5eCK4BoPyw_MOj1fG5wX6Fhi69xzmVyF_35APzn0y0gqKKe1rr8xj9_yotWvswRvC0Xje8Zw8AZgCGqrjYtNfw5kHEqSBqknxM6XPlcwNKvde5LdoRBkrH7wOKsMYyXy52zkLwO1Yz96vGxB3v_e5)
- Giải thích:
  + User:
    - Nhiệm vụ: Lớp này đại diện cho người dùng của hệ thống. Người dùng sẽ cung cấp thông tin đăng nhập (tên đăng nhập và mật khẩu) để truy cập vào hệ thống.
    - Thuộc tính:
      + username: Tên đăng nhập của người dùng.
      + password: Mật khẩu của người dùng.
     
    - Quan hệ: Liên kết với lớp LoginController, nơi người dùng nhập thông tin đăng nhập.
   
  + LoginController:
    - Nhiệm vụ:
      + Điều khiển luồng nghiệp vụ của quá trình đăng nhập.
      + Nhận thông tin đăng nhập từ người dùng và xử lý xác thực thông qua dịch vụ xác thực.
      + Quản lý giao tiếp với các lớp khác và xử lý các hành động cần thiết dựa trên kết quả xác thực.
     
    - Thuộc tính: loginStatus: Trạng thái đăng nhập, có thể là Success hoặc Failure.
    - Phương thức:
      + validateCredentials(username, password): Xác thực thông tin đăng nhập.
      + displayLoginScreen(): Hiển thị màn hình đăng nhập.
      + showErrorMessage(): Hiển thị thông báo lỗi khi thông tin đăng nhập không hợp lệ.
     
    - Quan hệ:
      + Sử dụng dịch vụ xác thực thông qua lớp AuthenticationService.
      + Quản lý phiên đăng nhập thông qua lớp UserSession.
     
  + AuthenticationService:
    - Nhiệm vụ:
      + Xác thực thông tin đăng nhập của người dùng.
      + Kiểm tra thông tin đăng nhập dựa vào dữ liệu được lưu trong cơ sở dữ liệu (hoặc hệ thống bên dưới).
     
    - Phương thức: authenticate(username, password): Kiểm tra xem thông tin đăng nhập có hợp lệ hay không và trả về kết quả (true/false).
    - Quan hệ: Nhận yêu cầu xác thực từ lớp LoginController.
   
  + UserSession:
    - Nhiệm vụ:
      + Quản lý phiên làm việc của người dùng khi họ đăng nhập thành công.
      + Tạo và lưu trữ thông tin phiên để theo dõi trạng thái đăng nhập của người dùng.
    - Thuộc tính:
      + sessionId: ID của phiên làm việc.
      + userId: ID của người dùng hiện tại.
      + sessionStatus: Trạng thái của phiên đăng nhập (Active/Inactive).
    - Phương thức:
      + createSession(userId): Tạo một phiên làm việc mới sau khi xác thực thành công.
      + terminateSession(): Kết thúc phiên làm việc.
    - Quan hệ:
      + Liên kết với lớp LoginController, giúp tạo và quản lý phiên đăng nhập.
## 4. Maintain Employee Information:
### a. Các lớp phân tích :
- **PayrollAdministrator:** Là người sử dụng hệ thống để thêm, cập nhật, hoặc xóa thông tin nhân viên.
- **Employee:** Đại diện cho thông tin nhân viên trong hệ thống. Bao gồm tên, địa chỉ, số bảo hiểm xã hội.
- **EmployeeDatabase:** Quản lý và lưu trữ thông tin nhân viên trong cơ sở dữ liệu. Cung cấp các phương thức thêm, cập nhật, xóa nhân viên.
- **System:** Hệ thống giao tiếp với người quản trị, yêu cầu và xử lý các tác vụ thêm, sửa, xóa nhân viên.
- **EmployeeIDGenerator:** Cung cấp và quản lý việc tạo mã nhân viên duy nhất khi thêm nhân viên mới vào hệ thống.
### b. Biểu đồ squence: 
![Diagram](https://www.planttext.com/api/plantuml/png/vLKzJyCm4DqZvJzuX84_a06rKYXYG20X1aOJNv65lx2TIldtsB7TfAdLf64aIwBplNjtxrtaZR5OsvQpii2DbHgzuavBnhQ4Kq6DrTW5oqAv9DfGXOL5Rvsnm4zZ3rmnsG7KsE9FR21_-bG_We1OiYnoLEZkFX9KICDF2yRkMj5OAiNDRLc48v-K0rT8QNcW15wK1nYFS7CnYxQ47Bie2-IUkKgH_DYws4jVpaFd-evDvA03QqQJ2ds5pm5Q9s0c_LGgssfn3ZldImvL21EIWbEMb3IcQAJOKysTaZIviKJ724kL7Ho8nu8WoPntHTpCV_IdNklE8gsSlfh28Ulf9T4clbo_H44RSdc7XZxRFltQBgD7WMkbiR7HYRKrCFXtrYvKhjTcz2VDJJU1VO1PCXx7-Zj5Tr9FIHUiHO8ykqh1u1Nh4HPXl1uRz-xldLy0)
- Mô tả tương tác giữa các lớp:
  + Payroll Administrator yêu cầu hệ thống cung cấp các lựa chọn cho chức năng thêm, cập nhật, hoặc xóa nhân viên.
  + Trong trường hợp thêm nhân viên, hệ thống yêu cầu nhập thông tin nhân viên, tạo mã nhân viên duy nhất, sau đó thêm thông tin vào cơ sở dữ liệu và xác nhận việc thêm nhân viên.
  + Trong trường hợp cập nhật nhân viên, hệ thống yêu cầu nhập mã nhân viên, hiển thị thông tin hiện tại và yêu cầu cập nhật. Sau khi cập nhật, hệ thống cập nhật cơ sở dữ liệu và xác nhận việc cập nhật.
  + Trong trường hợp xóa nhân viên, hệ thống yêu cầu mã nhân viên, hiển thị thông tin nhân viên và yêu cầu xác nhận việc xóa. Sau khi xác nhận, nhân viên được đánh dấu xóa và hệ thống sẽ xử lý trong lần chạy bảng lương tiếp theo.
### c. Các biểu đồ lớp mô tả lớp phân tích:
![PlantText](https://www.planttext.com/api/plantuml/png/TP9D3e8m48NtJNe7bXhZ5Gmag75dOZp0I4VJs1-S3YR4U7S50GMXo_dwEZFlDGuCn8KrKcG6GeZsK98t9b5MEnsOW3r53ocYzraGtWeCl2bSnjgxsLoAfnIjz506HZkylBQvyINYpfrz9HXbQKSoxywQR4iIfL1DmMEkWATnYWOR_3DbHu7X106xUK6fbdKl5dM7YHMODDx7eGMwjc3ZgPxatx3l-bjqsBVwygbWtw9QF1hHShbg0f2Y2Q8g3RSTXJ_zfOZHgVe_l000)
- Giải thích:
  + **PayrollAdministrator:** Là lớp đại diện cho người quản trị, có nhiệm vụ yêu cầu hệ thống thực hiện các chức năng liên quan đến việc thêm, cập nhật, hoặc xóa nhân viên.
  + **System:** Lớp trung gian xử lý các yêu cầu từ người quản trị và điều phối các bước tiếp theo, bao gồm yêu cầu thông tin từ người quản trị và gọi các phương thức của các lớp khác như EmployeeDatabase và EmployeeIDGenerator.
  + **EmployeeDatabase:** Lớp này quản lý cơ sở dữ liệu nhân viên, thực hiện các hành động thêm, cập nhật và xóa thông tin nhân viên.
  + **EmployeeIDGenerator:** Cung cấp chức năng tạo mã nhân viên duy nhất khi thêm nhân viên vào hệ thống.
## 5. Maintain Purchase Order:
### a. Các lớp phân tích :
- CommissionedEmployee: Là người sử dụng hệ thống để thêm, cập nhật, hoặc xóa đơn đặt hàng. Người này cần ghi lại các đơn đặt hàng để nhận hoa hồng.
- PurchaseOrder: Đại diện cho thông tin đơn đặt hàng trong hệ thống. Bao gồm các thông tin như khách hàng, sản phẩm, ngày đặt hàng, v.v.
- PurchaseOrderDatabase: Quản lý và lưu trữ các đơn đặt hàng trong cơ sở dữ liệu. Cung cấp các phương thức thêm, cập nhật, xóa đơn đặt hàng.
- System: Hệ thống giao tiếp với nhân viên bán hàng, yêu cầu và xử lý các tác vụ thêm, sửa, xóa đơn đặt hàng.
- PurchaseOrderIDGenerator: Cung cấp và quản lý việc tạo mã đơn đặt hàng duy nhất khi thêm đơn đặt hàng vào hệ thống.
### b. Biểu đồ squence: 
![Diagram](https://www.planttext.com/api/plantuml/png/xLNBJiCm4Bn7yZ_u20T-80TKr03YL2J4WQF9Ri5IOXi_AkNlSHA79f53JCknlQIDTtPcToRfnbYchQihah7IIastigwvCLmAXFjQLR9199doHRpaYWbBNnfZiPxUUtQw_6G6TnfG5yooT__ZbvAduX45QkOPIKQo62czkGrKETNuvT3O1oTAwukkhadM7xL5CN1EbPO73hXJBS2q23zXPUbM8xFueuPsSaX6_MUjPL0n7KJiPTkynQzD4IGjue_yIxlAwKV_TTQa65ei0QVBj4wBXGOB6WPBSye09YTHvg5yJ5jAiUUwlWFWWuSfIm-mIVlUGsXRe831sLS5_-fiSPQlwHlrVcYE1pnjhJ4tevcAJmxSg8erKUx4kVkzGqAIZpEx3hEeEZLCFVKvKGhYPr4giC9BbFuOfR3URdUZ1tnjv1di3KtokD3PTDRhQAxsb0prQHbdQEEltN_gDm00)
- Mô tả tương tác giữa các lớp:
  + Commissioned Employee yêu cầu hệ thống cung cấp các lựa chọn cho chức năng tạo mới, cập nhật, hoặc xóa đơn đặt hàng.
  + Trong trường hợp tạo đơn hàng mới, hệ thống yêu cầu nhập thông tin đơn hàng, tạo mã đơn hàng duy nhất và thêm thông tin vào cơ sở dữ liệu.
  + Trong trường hợp cập nhật đơn hàng, hệ thống yêu cầu nhập mã đơn hàng cần cập nhật, kiểm tra và hiển thị thông tin đơn hàng hiện tại, sau đó yêu cầu nhập thông tin cập nhật.
  + Trong trường hợp xóa đơn hàng, hệ thống yêu cầu nhập mã đơn hàng, kiểm tra và yêu cầu xác nhận xóa đơn hàng.
### c. Các biểu đồ lớp mô tả lớp phân tích:
![PlantText](https://www.planttext.com/api/plantuml/png/XP912i8m44NtWToXIqMyWWYjYYi5yG2n-MgXINGo4OfuTskjnMghsMN-cyoVcKmzA-9WSYdIN7aVnSwOpFlCMUYPEUMk0AAh555vHeHpWETvi2cNn60enKsAL-gcy0pp2Qy3fKVbiI8DMjgzUsJr0qaZfyxkCp8jEIOeXlx9R4_wBvCWHysyDT165AjTUMdwKLgtWAP0g0h-wfCfmmNTsRgoygNrsLec2rYGOaUDiyCpWev9LizqxdGydjGRawBUt2FKEOD-uisE55DONNsbEm00)
- Giải thích:
  + CommissionedEmployee: Là lớp đại diện cho nhân viên bán hàng có hoa hồng, có nhiệm vụ yêu cầu hệ thống thực hiện các chức năng liên quan đến việc tạo, cập nhật hoặc xóa đơn đặt hàng.
  + System: Lớp trung gian xử lý các yêu cầu từ nhân viên bán hàng và điều phối các bước tiếp theo, bao gồm yêu cầu thông tin từ nhân viên và gọi các phương thức của các lớp khác như PurchaseOrderDatabase và PurchaseOrderIDGenerator.
  + PurchaseOrderDatabase: Lớp này quản lý cơ sở dữ liệu đơn đặt hàng, thực hiện các hành động thêm, cập nhật và xóa đơn đặt hàng.
  + PurchaseOrderIDGenerator: Cung cấp chức năng tạo mã đơn hàng duy nhất khi thêm đơn hàng vào hệ thống.
## 6. Run Payroll:
### a. Các lớp phân tích :
- **PayrollSystem**: Quản lý và điều phối quá trình chạy bảng lương.
- **Employee**: Đại diện cho nhân viên, cung cấp thông tin lương, thời gian làm việc và phương thức nhận lương.
- **PayrollCalculator**: Tính toán tiền lương dựa trên thông tin thời gian làm việc, đơn đặt hàng, các khoản khấu trừ.
- **PaymentProcessor**: Xử lý thanh toán và gửi thông tin thanh toán đến hệ thống ngân hàng.
- **BankSystem**: Hệ thống ngân hàng nhận và xử lý giao dịch thanh toán.
- **PaycheckPrinter**: In phiếu lương cho nhân viên trong trường hợp cần thiết.
### b. Biểu đồ squence: 
![Diagram](https://www.planttext.com/api/plantuml/png/VPF1ReCm38RlIBo3ZzjXBy1XQbSwgOT9LRiNS8FNHeG49MOJRxyaLQ0C1YShlxy_jcCsZj5orwWyGy76mX5xQvJQLetKW0vYa6Ujpv92jgWvfPnxnzHCfNtJAjCJBG8xLA9Jw6-PoGrfFbeZoBc_wXlgUkagJuaRYVfefMRoK9xTYtvvdLPOm45BbiW4fqudBSycIO5AnHTm8hQIlWdsIbxbHT6WkJnJnhJmxaT5A6uF7OF_PfwprWj8CGNnAV5G8kFpn6M45dho9NPMZsPLI0X320QeXgd2fOTTcDDT-Q_8nr4M48FX-4wISlHeMafBWg6arZZ9w-wJvmtsCLopc131PLo30iwagtW0dnQryuihZHxnCNNv-gsejVbHL5rfRk2jqnHN5kG3RPtqr0vvCD8pBkwbVtYZlwHj1cvdl1znu3OUZ3_XBm00)
- Mô tả tương tác giữa các lớp:
    + Admin (Payroll Administrator): Bắt đầu quy trình bằng cách gửi yêu cầu chạy bảng lương đến lớp PayrollSystem.
    + PayrollSystem:
       - Nhận yêu cầu từ Admin.
       - Truy xuất danh sách các nhân viên đủ điều kiện nhận lương thông qua lớp Employee.
       - Duyệt qua từng nhân viên để tính toán lương bằng cách gọi lớp PayrollCalculator.
    + PayrollCalculator: Nhận thông tin của nhân viên và tính toán tiền lương dựa trên thông tin thời gian làm việc, đơn đặt hàng, và các khoản khấu trừ.
    + PayrollSystem:
      - Nhận kết quả lương từ PayrollCalculator.
      - Dựa vào phương thức thanh toán của nhân viên, hệ thống lựa chọn:
        + Nếu là séc: Gửi yêu cầu in phiếu lương thông qua lớp PaycheckPrinter.
        + Nếu là chuyển khoản: Gửi yêu cầu xử lý thanh toán đến lớp PaymentProcessor.
       
    + PaymentProcessor: Gửi thông tin giao dịch đến BankSystem để thực hiện chuyển khoản.
    + BankSystem: Nhận thông tin giao dịch và phản hồi lại cho lớp PaymentProcessor về trạng thái giao dịch (thành công hoặc thất bại).
    + PayrollSystem:
      - Đánh dấu trạng thái bảng lương của nhân viên là đã xử lý.
      - Gửi xác nhận hoàn thành quy trình cho Admin.
### c. Các biểu đồ lớp mô tả lớp phân tích:
![PlantText](https://www.planttext.com/api/plantuml/png/dPF1Ri8m38RlbVeEkGsqzGLwcD1MD75WGi2qivTQ43LDKEmYLTFUVM5DW6phXLjZ__R_nKvdnE2uQtMUIGr4OWMzirflUc9inMUU2N4l5aQn0iPrPq9-CXqoQsIdy8XphNRgG-EyFMZR8r8KBC4reMRbh4GYh4-vhpoBbh5cS2lEvqLL2cLu2Bv2YwKWxsPsGsG36bnVYjfstdY8UQSM3I-HzxPEvCM0yuByRbrJ8OFIz0iaS3w3bfq6jYxUFqRGAoOOy2fWAC-mqmj8sl744sv-QHW2bN8ekSA39SKJQ6rdEFPv42D6YS4Jc2RTrHebgYDk7HW2oSgQcnfxShb7sQpy11clmFqnviP64HhTUHO_D4z0UtMWF4lVLb4yNbPVdb_Ilxg_cod56urg4_9IRD3KjBKZudH1gJhDdGgk1dubdVcFdv_e6m00)
- Giải thích:
  + **PayrollSystem**:
    - Nhiệm vụ: Điều phối toàn bộ quy trình chạy bảng lương, từ việc lấy danh sách nhân viên đủ điều kiện đến việc đánh dấu trạng thái hoàn tất.
    - Thuộc tính và quan hệ: Giao tiếp với tất cả các thành phần khác để xử lý bảng lương.
   
  + **Employee**:
    - Nhiệm vụ: Cung cấp thông tin cần thiết cho quá trình tính toán và xử lý thanh toán.
    - Thuộc tính:
      + EmployeeID: Mã số nhân viên.
      + Name: Tên nhân viên.
      + Salary: Lương của nhân viên.
      + PaymentMethod: Phương thức thanh toán.
     
  + **PayrollCalculator**: Nhiệm vụ: Tính toán tiền lương dựa trên thông tin của nhân viên và các yếu tố liên quan.
  + **PaymentProcessor**: Nhiệm vụ: Xử lý thanh toán, gửi giao dịch đến hệ thống ngân hàng.
  + **BankSystem**: Nhiệm vụ: Nhận và xử lý các giao dịch thanh toán từ hệ thống bảng lương.
  + **PaycheckPrinter**: Nhiệm vụ: In phiếu lương nếu phương thức thanh toán yêu cầu in séc.

