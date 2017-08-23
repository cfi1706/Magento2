# **Dependency Injection**

Dependency Injection là một loại Design Pattern giúp ta giảm sự kết dính giữa các module, các class với nhau, giúp code dễ bảo trì và nâng cấp hơn.

Sự phụ thuộc của một đối tượng sẽ được chuyển ra môi trường bên ngoài thay vì tạo ra ở ngay trong bản thân đối tượng đó.

Constructor Injection: Các dependency sẽ được truyền vào \(inject vào\) 1 class thông qua constructor của class đó.

## Nguyên lý Dependency inversion

Các lớp cấp cao nên sử dụng interface của một lớp cấp thấp thay vì làm việc trực tiếp với nó.

File di.xml sẽ là file ánh xạ để xử lý interface nào đại diện cho class nào.

