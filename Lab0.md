*Tóm tắt một vài nội dung về PlantKet : 
1. Các loại đối tượng :
  - Actor : Đại diện cho người dùng hoặc hệ thống bên ngoài.
  - Use case: Mô tả một chức năng của hệ thống.
  - Class: Mô tả một lớp trong lập trình hướng đối tượng.
  - Component: Mô tả một thành phần phần mềm.
  - Node: Mô tả một nút trong một hệ thống phân tán.
2. Mối quan hệ :
  - Kế thừa: class A <|-- B (B kế thừa từ A)
  - Phụ thuộc: A --> B (A phụ thuộc vào B)
  - Kết hợp: A o-- B (A có một hoặc nhiều đối tượng B)
  - Tập hợp: A *-- B (A có một tập hợp các đối tượng B)
* Tùy chỉnh hình dạng và kiểu chữ :
    - Hình dạng: class MyClass << stereotype >> (<< stereotype >> cho phép bạn thêm các stereotype vào class)
    - Màu sắc: class MyClass {
                  color: blue
    } (Đặt màu cho class)
    - Font : fontname {fontname} (Thay đổi font chữ cho toàn bộ sơ đồ)
    - Tạo nhóm và gói : package "My Package" {
                          class A
                          class B
      }
    - Sơ Đồ Tuần Tự (Sequence Diagram) :
  
            @startuml
            participant Alice
            participant Bob
            Alice -> Bob: Hello
            Bob --> Alice: How are you?
            @enduml
 
    - Sơ Đồ Lớp (Class Diagram): 
-
  
        @startuml
        class Animal {
          - name: String
          + move()
        }

        class Dog {
          + bark()
        }

        Animal <|-- Dog
        @enduml
    - Sơ Đồ Use Case:
    -     @startuml
          actor User
          usecase "Login" as UC1
          usecase "Search" as UC2
          User -> UC1
          User -> UC2
          @enduml
    - Sơ Đồ Hoạt động (Activity Diagram):
- -- 
        @startuml
        start
        :Start;
        if (Condition) then (Yes)
          :Do something;
        else (No)
          :Do something else;
        endif
        stop
        @enduml
*Tóm tắt một vài nội dung về Markdown : 
- Tiêu đề :
  # Tiêu đề cấp 1
  ## Tiêu đề cấp 2
- Danh sách :
  + Danh sách không đánh số :
    - Mục 1
    - Mục 2
  + Danh sách đánh số :
  +   1.Mục 1
  +   2.Mục 2
- Đoạn văn : Viết bình thường, các đoạn cách nhau bằng một dòng trống
- Định dạng chữ :
  + In đậm: **text**
  + In nghiêng: *text*
  + ~~Gạch ngang:** ~~text~~
 
- Liên kết : [Tên liên kết](https://link.com)
- Hình ảnh : ![Mô tả hình ảnh](https://link-hinh-anh.jpg)
- Code :
  + \ : để thoát ký tự đặc biệt
  + Đoạn mã :
* Chèn hình ảnh :
  
![Diagram](http://www.plantuml.com/plantuml/png/encoded-diagram-text)

*Sơ đồ lớp:

![PlantText](https://www.planttext.com/api/plantuml/png/SoWkIImgAStDuU9ApaaiBbPmpClCJSofvb9Gq5N8IynDLR1I22ufoinB1ufeA-JcbwLgQ7BLGXKxPHQbL8Cbqd8gaSJTCeip8EB5vPcvO0c8kGesDRgwO6qe0Y3rN5mEgNafG9S00000)




*Sơ đồ Use Case: 

![PlantText](https://www.planttext.com/api/plantuml/png/SoWkIImgAStDuU9AJ2x9Br88BKujuYejJarEB4vLKFB9Jy_CKr98B5O8TJP420Ud9XObPq35ZRYuG9eKTEr0YXIi5790cf34Z81YnM0TN5mEgNafGDi0)
