“Hợp đồng dịch vụ” là một bộ PHP Interface được định nghĩa cho một module. Hợp đồng dịch vụ bao gồm các data interfaces dùng để bảo tồn tính toàn vẹn dữ liệu và service interfaces để cung cấp các xử lí. Chi tiết logic xử lí được ẩn đi với các phần sử dụng dịch vụ \(như controller, web services và các module khác\).

Nếu developer định nghĩa data và service interfaces theo một mẫu thiết kế, API của các modules khác và các extension bên thứ ba có thể implement nó thông qua Magento models và resource models.

![](/assets/import_2.png)

Controllers, Web Services, Other modules không thao tác trực tiếp với thành phần Model và Resource Model mà giao tiếp thông qua interface. Logic xử lí được ẩn đi, các thành phần sử dụng service chỉ quan tâm đến đầu ra và đầu vào chứ không cần quan tâm đến logic xử lí.

Việc model nào ứng với interface nào được cấu hình trong file **etc/di.xml** của magento 2.

&lt;preference for="Magento\Catalog\Api\ProductRepositoryInterface" type="Magento\Catalog\Model\ProductRepository" /&gt;

