# TÌM HIỂU CÁC CHẾ ĐỘ CARD MẠNG TRONG KVM
Trong KVM/libvirt, cấu hình card mạng của máy ảo (Guest OS) quyết định cách nó giao tiếp với Hệ điều hành mẹ (Host OS) và mạng bên ngoài. Có 4 chế độ card mạng chính:

## NAT Mode (Network Address Translation) - Mặc định
![nat](./images/nm_1.png)
- Cơ chế: KVM tạo một interface mạng ảo (virbr0) và một DHCP Server nội bộ (thường qua dnsmasq). Máy ảo nằm trong một lớp mạng nội bộ riêng (ví dụ: 192.168.122.x) cách ly hoàn toàn với LAN vật lý. Khi máy ảo đi ra Internet, Host OS thực hiện NAT IP của máy ảo thành IP của Host.
- Đặc điểm:
    + Máy ảo có thể truy cập Internet và giao tiếp với Host OS.
    + Các máy tính khác trong mạng LAN vật lý không thể truy cập trực tiếp vào máy ảo (trừ khi cấu hình Port Forwarding trên Host).
- Trường hợp sử dụng: Môi trường Test/Dev, máy ảo cá nhân chỉ cần ra Internet mà không làm dịch vụ Server cho mạng ngoài.

## Bridged Mode
![bridge](./images/nm_3.png)
- Cơ chế: Tạo một cầu nối ảo (Network Bridge - ví dụ br0) gắn trực tiếp vào card mạng vật lý của Host OS (như eth0 hoặc eno1).
- Đặc điểm:
    + Máy ảo hoạt động như một thiết bị độc lập cắm chung switch với máy mẹ.
    + Máy ảo sẽ nhận IP từ DHCP Server của mạng LAN thật (cùng dải IP với Host, ví dụ: 192.168.1.x).
    + Các máy khác trong LAN thật có thể truy cập thẳng vào máy ảo bằng IP riêng.
- Trường hợp sử dụng: Cấu hình máy ảo làm Server cung cấp dịch vụ (Web Server, Database, DNS) trong mạng nội bộ hoặc Production.

## Isolated (Host-Only Mode)
![isolated](./images/nm_2.png)
- Cơ chế: Tương tự như NAT nhưng không bật tính năng NAT ra card mạng thật của Host.
- Đặc điểm:
    + Các máy ảo kết nối với nhau và giao tiếp được với Host OS.
    + Máy ảo hoàn toàn không thể kết nối ra Internet hoặc mạng LAN bên ngoài.
- Trường hợp sử dụng: Môi trường thử nghiệm malware, lab bảo mật, hoặc cụm máy ảo nội bộ chỉ giao tiếp với nhau mà không cho phép truy cập từ/ra bên ngoài.

## Direct / Macvtap / Passthrough Mode

- Cơ chế: Gắn card mạng ảo của VM trực tiếp vào card mạng vật lý của Host thông qua driver macvtap hoặc gán cứng PCI card mạng vật lý cho VM (SR-IOV / PCI Passthrough).
- Đặc điểm:
    + Bỏ qua hoàn toàn lớp Bridge phần mềm của Linux Kernel, giúp đạt tốc độ truyền tải cao nhất và độ trễ thấp nhất.
    + Lưu ý của Macvtap: Mặc định máy ảo và Host OS không thể giao tiếp trực tiếp với nhau (mặc dù máy ảo vẫn ra Internet và nhận IP LAN bình thường).
- Trường hợp sử dụng: Các hệ thống đòi hỏi băng thông mạng cực cao (High-performance Networking, NFV, Firewall VM).

## BẢNG SO SÁNH CÁC MODE
|        Tiêu chí        |           NAT Mode           |        Bridged Mode        | Isolated / Host-Only |      Direct / Macvtap      |
|:----------------------:|:----------------------------:|:--------------------------:|:--------------------:|:--------------------------:|
| Dải IP máy ảo          | Dải ảo riêng (192.168.122.x) | Dải LAN thật (192.168.1.x) | Dải ảo nội bộ riêng  | Dải LAN thật (192.168.1.x) |
| Truy cập Internet?     | Có                           | Có                         | Không                | Có                         |
| LAN ngoài vào được VM? | Không (Cần Port Forward)     | Có (Trực tiếp)             | Không                | Có (Trực tiếp)             |
| Giao tiếp VM <-> Host? | Có                           | Có                         | Có                   | Không (trừ khi chỉnh sửa)  |
| Hiệu năng I/O Mạng     | Trung bình                   | Tốt                        | Tốt                  | Cao nhất                   |



