“Hợp đồng dịch vụ” là một bộ PHP Interface được định nghĩa cho một module. Hợp đồng dịch vụ bao gồm các data interfaces dùng để bảo tồn tính toàn vẹn dữ liệu và service interfaces để cung cấp các xử lí. Chi tiết logic xử lí được ẩn đi với các phần sử dụng dịch vụ \(như controller, web services và các module khác\).

Nếu developer định nghĩa data và service interfaces theo một mẫu thiết kế, API của các modules khác và các extension bên thứ ba có thể implement nó thông qua Magento models và resource models.

![](/assets/import_2.png)

Controllers, Web Services, Other modules không thao tác trực tiếp với thành phần Model và Resource Model mà giao tiếp thông qua interface. Logic xử lí được ẩn đi, các thành phần sử dụng service chỉ quan tâm đến đầu ra và đầu vào chứ không cần quan tâm đến logic xử lí.

Việc model nào ứng với interface nào được cấu hình trong file **etc/di.xml** của magento 2.

&lt;preference for="Magento\Catalog\Api\ProductRepositoryInterface" type="Magento\Catalog\Model\ProductRepository" /&gt;

**Các loại Interface và nơi định nghĩa**

Có hai loại interface trong mô hình service contracts, đó là **Data Interfaces** và **Service Interfaces**.

**Data interfaces**

 được dùng để bảo tồn tính toàn vẹn dữ liệu. Data interfaces định nghĩa các hàm mà trả lại thông tin về các thực thể dữ liệu \(data entities\), kết quả tìm kiếm, và xác thực kết quả. Bạn phải định nghĩa các data interface cho một service contract trong thư mục **Api/Data.**

**Service interfaces** được dùng để ẩn logic xử lí từ các bên yêu cầu dịch vụ \(service requestors\). Bạn phải định nghĩa các service interfaces cho một service contract trong thư mục con **Api **của một module. Service interface bao gồm:

* Repository interfaces
* Management interfaces
* Metadata interfaces

Repository Interfaces cung cấp quyền truy cập vào một thực thể dữ liệu \(Data entity\). Chúng ta thường dùng Repository Interfaces trong trường hợp cần cung cấp các thao tác thêm, sửa, xóa, lấy dữ liệu.

**Management interfaces**

Management interfaces cung cấp chức năng quản lý mà không liên quan đến các Repository Interfaces.

**Metadata interfaces**

Metadata interface cung cấp thông tin về những gì thuộc tính \(attributes\) được định nghĩa cho một thực thể.



