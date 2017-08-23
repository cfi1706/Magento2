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

#### Interceptor

Class Interceptor sẽ được tự động tạo ra để phục vụ cho cơ chế Plugin của Magento. Một class interceptor sẽ extend một class gốc và được trả về bởi Object Manager để cho phép các class có thể sử dụng nhiều plugin để thay đổi logic vào các method khác nhau.

