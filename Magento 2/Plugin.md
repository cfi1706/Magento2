**Plugin** hoặc **Interceptor** là một class mà thay đổi hành vi của một public function bằng cách chặn khi function được gọi. Điều này cho phép bạn thay thế hoặc mở rộng hành vi cho các function của bất kì class hoặc interface nào.

Plugins không thể được sử dụng trong các trường hợp sau đây:

* Đối tượng được khởi tạo trước Magento\Framework\Interception
* Final methods
* Final classes
* Bất kì class nào có chứa ít nhất một final public method.
* Method không phải public
* Class methods \(ví dụ static methods\)
* \_\_construct
* Virtual types

**Cách khai báo một Plugin**

Một plugin cho một class sẽ được khai báo trong file di.xml:

&lt;config&gt;

```
&lt;type name="{ObservedType}"&gt;

    &lt;plugin name="{pluginName}" type="{PluginClassName}" sortOrder="1" disabled="false"/&gt;

&lt;/type&gt;
```

&lt;/config&gt;

type: Một class hoặc interface mà các plugin quan sát.  
Tên plugin: Tên cho plugin dùng để nhận dạng. Cũng được sử dụng để hợp nhất các file configuration cho các plugin.  
Loại plugin. Tên class của một plugin hoặc virtual type của nó. Sử dụng quy ước đặt tên sau khi bạn xác định yếu tố này: \Vendor\Module\Plugin\Plugin.

Các thành phần sau đây là tùy chọn:  
sortOrder: Thứ tự mà các plugin  
Disabled: Dùng để disable plugin. Giá trị mặc định là false

### **Định nghĩa một plugin**

Một plugin được sử dụng để mở rộng hoặc thay đổi hành vi của một function nào bằng cách áp dụng mã trước \(before\), sau \(after\) hoặc xung quanh \(around\):

Đối số đầu tiên của plugin là một đối tượng cung cấp quyền truy cập vào tất cả các public function của class mà plugin quan sát.

**Before methods**

Bạn có thể sử dụng “Before” để thay đổi các tham số của một function được quan sát bằng cách trả lại một đối số đã được sửa đổi. Nếu có nhiều tham số, phương pháp này sẽ trả về một mảng các đối số. Return null sẽ chỉ ra rằng các đối số cho phương pháp quan sát không được sửa đổi.

Phải có tiền tố “before”.

**After methods**

Những phương pháp này có thể được sử dụng để sửa đổi các kết quả của một function được quan sát và bắt buộc phải có một giá trị trả về.

Phải có tiền tố “a

**Around methods**

Around methods được định nghĩa là code có thể chạy cả trước và cả sau của function được quan sát. Điều này cho phép bạn ghi đè hoàn toàn lên fuction đó.

Phải có tiền tố là “around”.fter”.



