1 Phân tích kiến trúc : 
  - Đề xuất kiến trúc : kiến trúc Client-Server (máy khách-máy chủ) dạng 3 tầng (Three-Tier Architecture) là lựa chọn phù hợp nhất
  - Giả thích lí do :
    +> Khả năng mở rộng và bảo trì: Tầng xử lý nghiệp vụ và giao diện người dùng tách biệt, giúp cho việc bảo trì và mở rộng hệ thống dễ dàng hơn.
    +> Tích hợp hệ thống cũ: Kiến trúc này hỗ trợ việc tích hợp với cơ sở dữ liệu cũ của trường mà không làm gián đoạn các chức năng khác.
    +> Tăng cường bảo mật: Việc tách biệt giữa các tầng giúp bảo mật thông tin tốt hơn, đặc biệt là đối với thông tin nhạy cảm như điểm của sinh viên.
    +> Hiệu năng cải thiện: Tầng xử lý nghiệp vụ có thể được tối ưu hóa để giảm thiểu truy vấn không cần thiết đến cơ sở dữ liệu, giúp tăng tốc độ và hiệu năng của hệ thống.
     

Cơ chế phân tích :
Phân tích ca sử dụng Payment :
Phân tích ca sử dụng Maintain Timecard :
Hợp nhất ca sử dụng :
Sử dụng Makdown :
