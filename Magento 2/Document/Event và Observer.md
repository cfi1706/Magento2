**Event và Observer**

Dựa theo design pattern: Publish–subscribe pattern.

Về nguyên tắc hoạt động, khi chúng ta tương tác với Magento, sẽ phát ra một số sự kiện gọi là event. Module của chúng ta sẽ khai báo và sử dụng Observer để bắt và xử lý event đó.

**Event**

Event được phát ra khi một hành động cụ thể nào đó trong Magento được kích hoạt.

Khi một sự kiện được phát ra, bạn có thể truyền data cho sự kiện đó và các observer có thể bắt được và xử lý data đó.

Phát sự kiện \(Dispatching events\) : Sự kiện trong Magento được phát ra \(dispatch\) bằng cách sử dụng class Magento\Framework\Event\Manager.

Vị trí của các file khai báo quan sát event sẽ nằm trong thư mục/etc và tên là events.xml.

**-etc/events.xml**: phạm vi global  
**-etc/frontend/events.xml**: chỉ ở ngoài frontend  
**-etc/adminhtml/events.xml**: chỉ ở trong backend

**Observer và subscribe event**

Observer là thành phần dùng để bắt event và xử lý chúng.

Để quan sát một events, chúng ta sẽ viết trong file events.xml:

File đó gồm những thuộc tính sau:

* Name \(bắt buộc\) – Tên của observer
* instance \(bắt buộc\) – tên đầy đủ của class observer
* disabled – Xác định xem observer này có được kích hoạt hay không. Mặc định sẽ là false.
* shared – Có shared hay không, mặc định là false.



