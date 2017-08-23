# **Dependency Injection**

Dependency Injection là một loại Design Pattern giúp ta giảm sự kết dính giữa các module, các class với nhau, giúp code dễ bảo trì và nâng cấp hơn.

Sự phụ thuộc của một đối tượng sẽ được chuyển ra môi trường bên ngoài thay vì tạo ra ở ngay trong bản thân đối tượng đó.

Constructor Injection: Các dependency sẽ được truyền vào \(inject vào\) 1 class thông qua constructor của class đó.

## Nguyên lý Dependency inversion

Các lớp cấp cao nên sử dụng interface của một lớp cấp thấp thay vì làm việc trực tiếp với nó.

File di.xml sẽ là file ánh xạ để xử lý interface nào đại diện cho class nào.

## Di Container

Việc khởi tạo các module cấp thấp sẽ do DI Container thực hiện.

Di Container trong Magento 2 chính là ObjectManager. Object Manager có nhiệm vụ tạo ra các đối tượng trong Magento 2.

## Biên dịch dependencies

Một công cụ trình biên dịch code sẽ thu thập tất cả các thông tin về dependency trong một class và lưu trữ thông tin đó trong các files. Trong quá trình tạo class, ObjectManager sử dụng thông tin này để tạo các đối tượng trong Magento 2.

Nói cách khác, trình biên dịch sẽ giúp tạo ra tất cả các class dependency không tồn tại \(proxy, factory và interceptor\) được khai báo trong code. Ta có thể thấy các class đó trong thư mục **var/generation**.



