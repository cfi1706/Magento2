Magento có cơ chế generate code để tạo ra các class không tồn tại. Các class được generate này sẽ nằm ở trong thư mục var/generation.

Có ba loại class được tự động sinh ra trong thư mục

**var/generation**

của Magento. Đó là:

**Factory, Proxy và Interceptor.**

#### Factory

Class Factory được dùng để khởi tạo ra các instances của class. Ví dụ sau đây là class AddressFactory được Magento generate ra .

#### Proxy

Class Proxy được sinh ra để chắc chắn rằng một instances của một class sẽ không được khởi tạo khi thực sự cần thiết.

Proxy sẽ được tham chiếu trực tiếp trong cấu hình DI.

Proxy kế thừa các class khác để trở thành một lazy-loaded của chúng.

#### Interceptor

Class Interceptor sẽ được tự động tạo ra để phục vụ cho cơ chế Plugin của Magento. Một class interceptor sẽ extend một class gốc và được trả về bởi Object Manager để cho phép các class có thể sử dụng nhiều plugin để thay đổi logic vào các method khác nhau.

Khi Magento gọi một class trong Magento, nó sẽ gọi vào class interceptor thay vì class gốc đó và gọi method tương ứng.

**Định nghĩa Proxy Pattern**

Proxy Pattern là mẫu thiết kế mà ở đó tất cả các truy cập trực tiếp đến một đối tượng nào đó sẽ được chuyển hướng vào một đối tượng trung gian \(Proxy Class\).  
 Đây là mô hình Proxy Pattern:

![](https://edenduong.com/wp-content/uploads/2016/10/400px-Proxy_pattern_diagram-300x167.png)

Khi gọi một class, việc xử lý sẽ được chuyển tiếp vào class Proxy. Proxy như một người đại diện, thay mặt để thực hiện các công việc thay cho chủ thể chính. Ở trong Magento, Proxy sẽ đại diện cho một class \(class gây tốn về hiệu năng\) để thực hiện việc tạo đối tượng cho class đó sau khi class đó bị loại bỏ ở hàm \_\_construct\(\) \(để tối ưu hiệu năng\).

**Implement trong Magento**

Proxy là code được sinh ra và do đó không cần phải được viết bằng tay. Chỉ cần refer tới một class có dạng Original\Class\Name\Proxy, việc generate code của Proxy class sẽ được Magento generate ra.

Class SlowLoading sẽ không được khởi tạo, do đó, các xử lí phức tạp gây tốn tài nguyên ở trong constructor sẽ không được thực hiện cho đến khi các đối tượng SlowLoading được sử dụng \(có nghĩa là, nếu phương thức getSlowValue được gọi\).

### Factory Pattern

Sử dụng constructor injection, nghĩa là khai báo class trong hàm construct. Đối tượng thu được theo cách này \(sử dụng các class injection\) là một mẫu singleton, nghĩa là cùng một instance luôn luôn được trả về bởi Object Manager khi class được yêu cầu.

Khi một class đã được khởi tạo đối tượng rồi, lần sau khi ta gọi lại, vẫn cùng một instance được trả về chứ sẽ không sinh ra một instance mới.

Khi sử dụng Factory, một instance mới của class đã được tạo ra.

**Mục đích của Factory**

Tạo ra một instance của một class non-injectable hoặc interfaces.

Factories được sử dụng để cô lập object manager từ logic code. Factories luôn được đặt tên giống hệt với class, với hậu tố Factory.



