# Phân tích tất cả các ca sử dụng còn lại trong hệ thống Payroll System.
## 1. Create Administrative Report 
### a. Các lớp phân tích :
- PayrollAdministrator: Gửi yêu cầu tạo báo cáo và quyết định lưu hoặc hủy báo cáo.
- ReportCriteria: Lưu trữ tiêu chí báo cáo và xác thực tính hợp lệ của các tiêu chí.
- ReportGenerator: Thực hiện tạo báo cáo dựa trên tiêu chí được cung cấp.
- Report: Lưu trữ nội dung báo cáo và hỗ trợ hiển thị hoặc lưu báo cáo vào tệp.
- ErrorHandler: Quản lý và hiển thị các thông báo lỗi trong trường hợp thông tin không hợp lệ hoặc thiếu.
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
### b. Biểu đồ squence: 
- Mô tả tương tác giữa các lớp:
### c. Các biểu đồ lớp mô tả lớp phân tích:
- Giải thích:
## 3. Login  
## 4. Maintain Employee Information 
## 5. Maintain Purchase Order 
## 6. Run Payroll  
