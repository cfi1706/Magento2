**Plugin** hoặc **Interceptor** là một class mà thay đổi hành vi của một public function bằng cách chặn khi function được gọi. Điều này cho phép bạn thay thế hoặc mở rộng hành vi cho các function của bất kì class hoặc interface nào.

Plugins không thể được sử dụng trong các trường hợp sau đây:

**– Đối tượng được khởi tạo trước Magento\Framework\Interception**  
**– Final methods**  
**– Final classes**  
**– Bất kì class nào có chứa ít nhất một final public method.**  
**– Method không phải public**  
**– Class methods \(ví dụ static methods\)**  
**\_\_construct**  
**– Virtual types**



