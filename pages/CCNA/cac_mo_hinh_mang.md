---
title: Các Mô Hình Mạng
summary: "Mô hình OSI và mô hình TCP/IP"
sidebar: mydoc_sidebar
permalink: cac_mo_hinh_mang.html
folder: CCNA
---

## MÔ HÌNH OSI

<p align="center">
  <img width="400px" src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/8d/OSI_Model_v1.svg/800px-OSI_Model_v1.svg.png" />
</p>

**Open Standard Interconnection (OSI)** Model là một sự chuẩn hóa cho những chức năng trong hệ thống mạng. Chức năng của mô hình là giúp cho tính phức tạp của mạng trở nên đơn giản hơn, cho phép các nhà phát triển module hóa việc thiết kế. Phương pháp này cho phép nhiều nhà phát triển làm việc độc lập nhau để tạo ra những chức năng riêng biệt mà vẫn có thể hòa hợp thành một thể thống nhất một cách dễ dàng (plug-and-play). Ngoài ra mô hình còn giúp cho những quản trị viên có thể hình tượng hóa quá trình trao đổi dữ liệu giữa các máy tính để hiểu được hoạt động của hệ thống mạng một cách tường minh hơn.

Mô hình **OSI** bao gồm 7 lớp:

|  |  |  |
| -------- | -------- | -------- |
| **7. Application** | Tầng ứng dụng cấp phương diện cho người dùng truy nhập các thông tin và dữ liệu trên mạng thông qua chương trình ứng dụng. Tầng này là giao diện chính để người dùng tương tác với chương trình ứng dụng, và qua đó với mạng. | Telnet, HTTP, FTP, SMTP, X.400 |
| **6. Presentation** | Tầng biên dịch có nhiệm vụ chuẩn hóa dữ liệu. Tầng này dịch dữ liệu được gửi từ tầng Application sang dạng Format chung. Và tại máy tính nhận, lớp này lại chuyển từ Format chung sang định dạng của tầng Application. | ASCII, JPEG, EBCDIC |
| **5. Session** | Tầng phiên kiểm soát các (phiên) hội thoại giữa các máy tính. | OS, Scheduling |
| **4. Transport** | Tầng vận chuyển cung cấp dịch vụ chuyển dữ liệu giữa các người dùng tại đầu cuối. Tầng giao vận kiểm soát độ tin cậy của một kết nối được cho trước. | TCP, UDP, SPX |
| **3. Network** | Tầng mạng thực hiện chức năng định tuyến. Tầng này cung cấp việc đánh địa chỉ luận lý (*IP Addressing*) - định tuyến các gói dữ liệu. | IP, IPX |
| **2. Datalink** | Tầng liên kết dữ liệu truyền dữ liệu giữa các thực thể mạng, phát hiện và có thể sửa chữa các lỗi trong tầng vật lý nếu có. Đánh địa chỉ vật lý (*MAC Address*) được mã hóa cứng vào trong các card mạng khi chúng được sản xuất. | 802.2, 802.3, HDLC |
| **1. Physical** | Tầng vật lý định nghĩa các đặc tả về điện và vật lý cho các thiết bị. Bao gồm bố trí các chân cắm (*pin*), hiệu điện thế (*volt*), và các cáp nối (*cable*); hay chuyển đổi giữa các loại tín hiệu điện như xung vuông trong thiết bị, sóng sin trong dây cáp đồng, ánh sáng trong cáp quang, sóng vô tuyến trong thiết bị không dây. | EIA/TIA, V.35 |

Dữ liệu trên máy tính có nhu cầu truyền sẽ chuyển từ tầng 7 xuống tầng 1. Khi đi qua mỗi tầng, dữ liệu sẽ được gắn thêm định dạng của tầng đó vào. Qua bên máy tính nhận thì dữ liệu sẽ được chuyển từ tầng 1 lên tầng 7. Khi đi qua mỗi tầng, dữ liệu sẽ được gỡ bỏ định dạng mà tầng tương ứng bên kia đã gắn vào.

<p align="center">
  <img src="https://vnpro.vn/upload/user/images/Tin%20T%E1%BB%A9c/1(2).jpg" />
</p>
